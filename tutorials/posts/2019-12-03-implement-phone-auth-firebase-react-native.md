---
date: 2019-12-03
title: 'Implement Firebase Phone Authentication in React Native Apps'
template: post
thumbnail: '../thumbnails/react.png'
slug: implement-phone-auth-firebase-react-native
categories:
  - React Native
  - Firebase
tags:
  - react-native
  - firebase
---

Phone authentication allows the user to sign in using their phone number. This could be done traditionally by associating a password and storing it when the user first registers with the app. However, another common pattern to log in a user using their phone number is by sending a verification code in their registered mobile number. This verification code is a unique number and the user is only allowed to sign in when it matches.

In this tutorial, let us try creating a small login screen using a Phone authentication. To quickly and efficiently establish a backend service, let us use good old Firebase with a React Native app.

## Table of Contents

- Requirements
- Generate a new project
- Enable Phone Authentication
- Create PhoneAuthScreen component
- Add a method to send an OTP
- Add OTP confirmation view
- Running the app
- Conclusion

## Requirements/Stack

- Node.js >= `10.x.x` version installed
- watchman
- react-native-cli
- Active Firebase project
- react-native-firebase

Do note that, I am going to use an iOS simulator. So any library (such as react-native-firebase) that needs configuration set up to be platform-specific, please refer to their official docs.

If you are not familiar with how to set up a new Firebase project, please follow the instructions under [**Create a Firebase Project**](https://heartbeat.fritz.ai/how-to-build-an-email-authentication-app-with-firebase-firestore-and-react-native-a18a8ba78574#87a3) from a previous post.

## Generate a new project

Create a new React Native app by executing the following command in a terminal window.

```shell
react-native init rnPhoneAuthDemo

# install following dependencies
yarn add react-native-firebase
```

## Enable Phone Authentication

To use Firebase SDK in React Native apps, you have to add the config file to your app. From Firebase console, click on **Settings icon** and go to **Project settings**.

![ss2](https://miro.medium.com/max/241/1*oLL2EY57s8AoyUaIky3Q9Q.png)

At this web page, click on the button **Add app** select the platform and follow the instructions that are mentioned.

![ss3](https://miro.medium.com/max/698/1*tFpadx7Si90JEG-N0sLvJg.png)

Download the file **GoogleService-info.plist** if you selected platform in the previous step is iOS. Then, open XCode add this file to the project.

![ss4](https://miro.medium.com/max/851/1*WOpo20-9K_iRCYA0ftc3aA.png)

For android users, you will download `google-services.json` and save it at the location `android/app/`.

After adding the config file, you will have to follow the instructions at `react-native-firebase` documentation **[here](https://rnfirebase.io/docs/v5.x.x/installation/initial-setup)**. Do not forget to configure `Firebase/Auth` dependency from the docs **[here](https://rnfirebase.io/docs/v5.x.x/auth/ios)**.

To use phone authentication as a sign-in method, you have to enable it in the Firebase project. From Firebase console, go to **Authentication** > **Sign-in method** tab. There, enable the **Phone** authentication method.

![ss5](https://miro.medium.com/max/1027/1*4Tzd_jUTBkX1iHRVWaFOYw.png)

![ss6](https://miro.medium.com/max/973/1*7pTqSKFAfKzrPgyTf5vAUA.png)

The React Native app is going to use reCAPTCHA verification to verify a user. To set up this, open the file `[PROJECT_NAME]/ios/[PROJECT_NAME].xworkspace` in Xcode. Double-click the project name in the left tree view and select the app from the **TARGETS** section. Then select the **Info** tab, and expand the **URL Types** section.

Click the **+** button, and add a URL scheme for your reversed client ID. To find this value, open the **GoogleService-Info.plist** configuration file, and look for the **REVERSED_CLIENT_ID** key. Copy the value of that key, and paste it into the URL Schemes box on the configuration page. Leave the other fields blank.

![ss7](https://miro.medium.com/max/1145/1*YfyS1GCF1K2xSMTFSu01cw.png)

That's it for all configuration and setups.

## Create PhoneAuthScreen component

Phone authentication follows a particular flow to sign-in the user. It starts by a user entering their number and requests an OTP from the Firebase. The Firebase uses reCAPTCHA first, to verify the user's authenticity. Then, once that is confirmed, it sends the OTP to the mobile number ad user can enter that value to sign in successfully, if the OTP entered matches.

To start this process, first, let us import all the necessary statements for the `PhoneAuthScreen` component.

```js
import React, { Component } from 'react';
import {
  StyleSheet,
  SafeAreaView,
  TouchableOpacity,
  View,
  Text,
  TextInput
} from 'react-native';
import firebase from 'react-native-firebase';
```

Create a class component with an initial state object. When the user enters the detail following variables have to be tracked.

- `phone`: user's phone number.
- `verificationCode`: OTP code sends by Firebase via SMS (by default).
- `confirmResult`: when the verification code is received, Firebase provides a parameter `confirmResult` that you can manually save to confirm the code and proceed further.
- `userId`: The unique identifier creates by Firebase on when a new user registers with the app.

```js
class PhoneAuthScreen extends Component {
  state = {
    phone: '',
    confirmResult: null,
    verificationCode: '',
    userId: ''
  };

  // ...
}

export default PhoneAuthScreen;
```

## Method to send an OTP

Using a RegExp pattern, you can match the phone number against a pattern manually. If the phone number entered by the user in the input field matches the RegExp pattern, return a boolean `true` from this method. JavaScript's `.test()` the method is to match a string and it returns true if the phone number entered is valid.

Add the utility method `validatePhoneNumber`.

```js
validatePhoneNumber = () => {
  var regexp = /^\+[0-9]?()[0-9](\s|\S)(\d[0-9]{8,16})$/;
  return regexp.test(this.state.phone);
};
```

This method is used inside the handler method that contains logic to send the OTP to the user on the phone number entered. Create a handler method `handleSendCode`. Inside this method, using `firebase.auth().signInWithPhoneNumber()` is used. At this step, Firebase uses reCAPTCHA for the user to be verified as a "human". If the reCAPTCHA verification process is a success, this Firebase method has a promise attached to it that gets resolved.

```js
handleSendCode = () => {
  // Request to send OTP
  if (this.validatePhoneNumber()) {
    firebase
      .auth()
      .signInWithPhoneNumber(this.state.phone)
      .then(confirmResult => {
        this.setState({ confirmResult });
      })
      .catch(error => {
        alert(error.message);

        console.log(error);
      });
  } else {
    alert('Invalid Phone Number');
  }
};
```

When the promise resolves, it saves updates the state variable `confirmResult`.

## Add OTP confirmation view

In this section, you are going to add the view when the user has received the verification code. The app at this point will display two input fields. One, for the user to change their phone number if there has been a mistake. Otherwise, the phone number is displayed from the initial screen and the user has to enter the OTP.

The method `changePhoneNumber` is going to take care of incorrect phone numbers and the handler method `handleVerifyCode` is going to send the request back to the Firebase to verify the OTP entered by the user. If the OTP verification approves, for now, you can display the user's `uid` in an alert message.

```js
 this.setState({ confirmResult: null, verificationCode: '' })
 }

 handleVerifyCode = () => {
 // Request for OTP verification
 const { confirmResult, verificationCode } = this.state
 if (verificationCode.length == 6) {
 confirmResult
 .confirm(verificationCode)
 .then(user => {
 this.setState({ userId: user.uid })
 alert(`Verified! ${user.uid}`)
 })
 .catch(error => {
 alert(error.message)
 console.log(error)
 })
 } else {
 alert('Please enter a 6 digit OTP code.')
 }
 }
 renderConfirmationCodeView = () => {
 return (
 <View style={styles.verificationView}>
 <TextInput
 style={styles.textInput}
 placeholder='Verification code'
 placeholderTextColor='#eee'
 value={this.state.verificationCode}
 keyboardType='numeric'
 onChangeText={verificationCode => {
 this.setState({ verificationCode })
 }}
 maxLength={6}
 />
 <TouchableOpacity
 style={[styles.themeButton, { marginTop: 20 }]}
 onPress={this.handleVerifyCode}>
 <Text style={styles.themeButtonTitle}>Verify Code</Text>
 </TouchableOpacity>
 </View>
 )
 }
```

Lastly, add the render method with the following JSX snippet:

```js
render() {
 return (
 <SafeAreaView style={[styles.container, { backgroundColor: '#333' }]}>
 <View style={styles.page}>
 <TextInput
 style={styles.textInput}
 placeholder='Phone Number with country code'
 placeholderTextColor='#eee'
 keyboardType='phone-pad'
 value={this.state.phone}
 onChangeText={phone => {
 this.setState({ phone })
 }}
 maxLength={15}
 editable={this.state.confirmResult ? false : true}
 />

 <TouchableOpacity
 style={[styles.themeButton, { marginTop: 20 }]}
 onPress={
 this.state.confirmResult
 ? this.changePhoneNumber
 : this.handleSendCode
 }>
 <Text style={styles.themeButtonTitle}>
 {this.state.confirmResult ? 'Change Phone Number' : 'Send Code'}
 </Text>
 </TouchableOpacity>

 {this.state.confirmResult ? this.renderConfirmationCodeView() : null}
 </View>
 </SafeAreaView>
 )
 }
```

Also, do not forget to add some styling to the above components.

```js
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#aaa'
  },
  page: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center'
  },
  textInput: {
    marginTop: 20,
    width: '90%',
    height: 40,
    borderColor: '#555',
    borderWidth: 2,
    borderRadius: 5,
    paddingLeft: 10,
    color: '#fff',
    fontSize: 16
  },
  themeButton: {
    width: '90%',
    height: 50,
    alignItems: 'center',
    justifyContent: 'center',
    backgroundColor: '#888',
    borderColor: '#555',
    borderWidth: 2,
    borderRadius: 5
  },
  themeButtonTitle: {
    fontSize: 24,
    fontWeight: 'bold',
    color: '#fff'
  },
  verificationView: {
    width: '100%',
    alignItems: 'center',
    marginTop: 50
  }
});
```

## Running the app

Open the app in a simulator. Initially, the user will be welcomed by the following screen. Enter the phone number.

![ss8](https://miro.medium.com/max/350/1*JNjXwQ2BVnYNj615Vil3TA.png)

On clicking the button `Send code`, reCAPTCHA process is going to trigger if the user is signing-in for the first time.

![ss9](https://miro.medium.com/max/350/1*UgP02HjKR85v0uqwF-h2uA.png)

After that, the user receives the verification code via SMS.

![ss10](https://miro.medium.com/max/350/1*a8SWGwBtXhrRB2ZBAMhLlQ.jpeg)

Enter the verification code.

![ss11](https://miro.medium.com/max/350/1*kS2_cGIGsHYFuFD0CaxoVw.png)

On success, it responds with a `uid` in an alert message that you can verify in the Firebase console.

![ss12](https://miro.medium.com/max/350/1*mxPx3gOy8yR_ZUtyYiCY4A.png)

![ss13](https://miro.medium.com/max/941/1*SJ8EgtsJDKlmnDoGrHtXDg.png)

## Conclusion

_Congratulations!_ You have learned how to integrate the Phone auth process using Firebase SDK in a React Native application.

You can find the complete source code at **[this Github repo](https://github.com/amandeepmittal/rnPhoneAuthDemo)**.

---

Originally published at [Heartbeat.Fritz.AI](https://heartbeat.fritz.ai/implement-firebase-phone-authentication-in-react-native-apps-237959027611)
