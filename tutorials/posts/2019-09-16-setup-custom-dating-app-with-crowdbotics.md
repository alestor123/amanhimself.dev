---
date: 2019-09-16
title: 'How to Manually Setup and Deploy The Crowdbotics Dating App Blueprint'
template: post
thumbnail: '../thumbnails/react.png'
slug: setup-custom-dating-app-with-crowdbotics
categories:
  - React Native
tags:
  - react-native
---

![cover_image](https://blog.crowdbotics.com/content/images/2019/08/5cd460c263a1fe60b5694b05_dating.png)

The [Crowdbotics Dating App Blueprint](https://marketplace.crowdbotics.com/product/dating-app) is a match-making app built in the style of Tinder or Bumble. Users can create profiles, find matches, communicate in real-time, and more.

[Crowdbotics Blueprints](https://marketplace.crowdbotics.com/product/dating-app) are 'batteries-included' application builds: UI/UX, hosting, security, updates, expert developer support – everything you need to launch and grow your application from the ground up. Crowdbotics blueprints each contain a fixed set of 'minimum viable' features that can be used as a springboard for further development. Blueprints are available for purchase in combination with a Crowdbotics subscription.

[Crowdbotics](http://app.crowdbotics.com/) is a full-stack app-building platform that enables anyone with an idea to go from 'zero to one' (idea to MVP) faster than ever before. With your minimum viable product deployed, you can then tweak, iterate, test, and scale to millions of users -- no need to switch platforms as you grow.

When you purchase a Crowdbotics blueprint, a Crowdbotics PM coordinate application set up with the help of an expert developer. However, some Crowdbotics users still choose to set up blueprints on their own. As with all Crowdbotics applications, you have direct access to the underlying code powering your full-stack application.

The following walkthrough shows technical users how to set up deploy the Crowdbotics Dating App Blueprint from the ground up.

## Requirements

- Node.js (>=8.x.x) with npm/yarn installed.
- expo-cli (>=3.0.4), previously known as create-react-native-app.
- Crowdbotics App builder Platform account (preferably log in with your valid Github ID)
- Firebase and Firestore account

_Dating App Blueprint Technology Stack:_ Redux, NativeBase, React Navigation, Expo, iOS and Android

## Setup Your Custom Dating App On GitHub

![1](https://blog.crowdbotics.com/content/images/2019/09/5d681b415eedc61867765755_dating-app-5-1.png)

Once you have purchased your Custom Dating App Blueprint, login to your Crowdbotics account. Connect your Crowdbotics account to GitHub if you have not already.

Click the Dating App Blueprint on your Crowdbotics Dashboard. On the App Details page for your Dating App Blueprint, click the GitHub button and you will be directed to your applications repository.

The structure of the repository will look something like this:

![2](https://blog.crowdbotics.com/content/images/2019/08/css5.png)

The development team at Crowdbotics actively maintains and manages blueprints to keep them user-friendly and with up to date dependencies. You can connect with the team Crowdbotics development team and ask questions specific to the Dating App Blueprint at discuss.crowdbotics.com.

The Custom Dating App is based on the latest versions React Native and Expo.

Some of the common features and functionalities you will find in this blueprint are:

- Login
- Favorite, Like, Dislike
- Swipe UX
- Search
- Matches
- Chat
- Profile with photos
- Settings
- Bio
- And More

The Blueprint also comes with a backend API written in Django that can be used in web versions of the application. Here is a wireframe of how it looks in the web browser.

![3](https://blog.crowdbotics.com/content/images/2019/08/css6.png)

To continue with the process of setting up this app on your local development environment, make sure you have installed the latest edition of `expo-cli`.

After that, open a terminal window and navigate to the project directory that you have just cloned. All you have to do, to run this application initially is to execute the following command to install dependencies. You can choose either package manager, `yarn` or `npm`.

```shell
# navigate to project directory
cd dating-app

# install dependencies
yarn add
```

After all, dependencies have installed, you can take a look at the `package.json` file to find out the complete list of modules that are being used in this template.

```json
"dependencies": {
    "axios": "^0.19.0",
    "babel-preset-expo": "5.0.0",
    "color": "3.1.0",
    "expo": "^33.0.0",
    "firebase": "^6.2.2",
    "jest-cli": "23.5.0",
    "lodash": "4.17.11",
    "moment": "2.22.2",
    "native-base": "2.8.1",
    "react": "16.8.3",
    "react-native": "https://github.com/expo/react-native/archive/sdk-33.0.0.tar.gz",
    "react-native-camera-roll-picker": "1.2.3",
    "react-native-gifted-chat": "0.5.0",
    "react-native-multi-slider": "0.3.6",
    "react-native-scrollable-tab-view": "0.10.0",
    "react-native-swiper": "1.5.14",
    "react-navigation": "2.17.0",
    "react-redux": "5.1.1",
    "redux": "4.0.1",
    "redux-form": "7.4.2",
    "redux-persist": "5.10.0",
    "redux-promise": "^0.6.0",
    "redux-thunk": "2.3.0",
    "remote-redux-devtools": "0.5.13",
    "remote-redux-devtools-on-debugger": "^0.8.0",
    "superagent": "^5.1.0",
    "whatwg-fetch": "2.0.4"
}
```

From the above snippet, you can notice that this custom template heavily depends on Redux to manage the application state. When it comes to larger applications in React or React Native, it is hard to keep track of which component is acting as the top-level state provider and which component is only written for presentational use. Redux is still the most popular choice among the developer community. The Dating template provides integration of Redux as state management library with pre-defined actions and reducers.

To help you create or modify existing presentational UI components, Dating App template uses [Native-base](https://docs.nativebase.io/). Again, Nativebase is well-maintained and one of the most popular libraries that provides a huge set of pre-defined components to build a cross-platform and pleasing user interface for mobile applications that use React Native. We will take a look at some of them later.

## Running the Custom Dating App

For now, let us run and see how this application works on its default mode. Run the following command from the terminal window and make sure you have either simulator or device with Expo client installed connected to see this demonstration.

```shell
yarn start
```

Follow the instructions on the expo command-line interface as to what are the next steps to open this application on a simulator or a real device using Expo client. On running the app, you will be welcomed by a splash screen until all the assets are loaded.

![css7](https://blog.crowdbotics.com/content/images/2019/08/css7-2.png)

Then it moves on to the first set of screens which gives an onboarding experience along with a login button. The login button is built of actually a social login provider using Facebook.

![css8](https://blog.crowdbotics.com/content/images/2019/08/css8.png)

If using the application for the first time, the App asks for permission to access a Facebook account using an alert box message.

![css9](https://blog.crowdbotics.com/content/images/2019/08/css9.png)

Once successfully logged in, the user of the application will be welcomed by the HomeScreen with a tab navigator at the bottom. To edit the strategy of how the user logs in to your application or add another social provider or change the onboarding screens, you can always visit the file that contains the business logic behind them at `src/screens/Login`.

## Enable Facebook Auth and add Firebase Config

The Crowdbotics dating app currently relies on Firebase to saving users to the application from their Facebook account. To make sure the user logs in successfully, you will first have to enable Firebase service. To sign-up or log-in for one, visit [console.firebase.com](https://console.firebase.google.com/). Once you are logged in, you will be welcomed by a screen below.

![cs11](https://blog.crowdbotics.com/content/images/2019/08/css11.png)

Click on the button **Add Project**. This leads to another screen which contains a form to be fulfilled in order to create a new Firebase project.

![css12](https://blog.crowdbotics.com/content/images/2019/08/css12.png)

Fill the name of the project, check both the boxes for now and click on the button Create project. This will take some moments. Once the Firebase project is created, you will be welcomed by the home screen like below.

![cs13](https://blog.crowdbotics.com/content/images/2019/08/css13.png)

Take a look at the side menu bar on the left. This is the main navigation in any Firebase project. To connect Firebase with React Native app, you need API key and store in the client-side app inside the file `src/constants/database.js`. All the configuration to enable and run the instance of your Firebase application is already written, as shown below. All you have to do is change the values of `config` object. You have to add yours for it to work.

```js
import firebase from 'firebase';
import '@firebase/firestore';
import { Constants } from 'expo';
// Initialize Firebase
var config = {
  apiKey: 'XXXX',
  authDomain: 'XXXX',
  databaseURL: 'XXXX',
  projectId: 'XXXX',
  storageBucket: 'XXXX',
  messagingSenderId: 'XXXX',
  appId: 'XXXX'
};

firebase.initializeApp(config);

const store = firebase.firestore();
const auth = firebase.auth();

export { store, auth, firebase };
```

Click on the settings ⚙️ in the sidebar menu and go to **Project settings**. There you will see under Your apps section all the platforms available such as iOS, and web. Click on the **Web** as shown below. Next, copy only the config variable in a new file called `database.js` as shown above.

From the above snippet, you can notice that the initialization of Firebase SDK in the expo app has already be done by using `firebase` npm module.

![css14](https://blog.crowdbotics.com/content/images/2019/08/css14.png)

Firebase also uses Firestore cloud storage to store login credentials and user details when the user logs into the dating for the first time. In the Database section from the sidebar, choose the cloud Firestore and go to the second tab called Rules. If you are enabling Firestore for the first time, chances are you need to set the database security rules to test mode. This is where the firebase SDK will allow anyone (one who has access to the config keys) to read and write to the database. That said, this section should look like below.

```js
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write;
    }
  }
}
```

Again the configuration to use Firestore instance inside the source code of our application is already written.

To use Facebook login, you will have to create an app and generate an `appId` using `https://developers.facebook.com/apps/`. This piece of information has to be added to two files: one is `app.json` and another is `src/constants/config.js`.

```js
export default {
  facebook: {
    appId: 'XXXX'
  }
};
```

You can find the appID and app secret tokes in **Settings > Basic** section from the sidebar.

![css15](https://blog.crowdbotics.com/content/images/2019/08/css15.png)

Lastly, you are required to enable these tokens inside the Firebase console and enable the Facebook **sign-in** method, as shown below.

![css16](https://blog.crowdbotics.com/content/images/2019/08/css16.png)

Now if you try logging into the application as a new user, the user details will be reflected back in the firebase console.

![css17](https://blog.crowdbotics.com/content/images/2019/08/css17.png)

Using the same user UID is as shown in the above image, you can find the complete details about the user inside the Firestore database collection `users`. The user UID is used as the identifier for each individual document that contains data fields as shown below.

![css18](https://blog.crowdbotics.com/content/images/2019/08/css18.png)

## Tab Navigation

Once the user is logged in, they are welcomed by the initial screen rendered via a custom component called `PhotoCard`.

![css20](https://blog.crowdbotics.com/content/images/2019/08/css20.png)

The dating app uses tab navigation component that is created using `react-navigation` library. This bottom tab navigation is made of three screens, the `PhotoCard` which is the initial route of the app, the `Profile` screen, and the `Chat` screen. Here is the snippet of creating tab navigation with the navigation library.

```js
const HomeTabNavigation = createBottomTabNavigator(
    {
        Profile: { screen: Profile },
        PhotoCard: { screen: PhotoCard },
        Chat: { screen: ChatList }
    },
    {
        initialRouteName: 'PhotoCard',
    lazy: true,

    // rest of the code
  }
```

The configuration object of the `HomeTabNavigation` describes two properties. The first one, `intialRouteName` indicates which route or the screen to be rendered first when the application loads. The second property described here is `lazy`. This is often defined in the case when you want to load the particular tab only when they are made active for the first time.

You can find the complete code to either modify or add more tabs to your application inside `src/screens/Home/tabNavigation.js.` file. For example, _what if you want to change the color of the bottom tab navigator from the current white color to a gray color?_

The `tab bar component` is another configuration property that overrides the default look and feels of a tab navigator that comes with `react-navigation` library. Currently, the custom dating app is using one to create a bottom tab navigator with external elements from `native-base` and custom icons.

```js
tabBarComponent: props => {
  return (
    <Header>
      <FooterTab>
        <Button onPress={() => props.navigation.navigate('Profile')}>
          <Icon
            name='md-person'
            size={20}
            style={
              props.navigation.state.index === 0
                ? styles.activeIcon
                : styles.inActiveIcon
            }
          />
        </Button>

        <Button onPress={() => props.navigation.navigate('PhotoCard')}>
          <Thumbnail
            small
            source={
              props.navigation.state.index === 1
                ? require('../../../assets/logo.png')
                : require('../../../assets/logo1.png')
            }
          />
        </Button>

        <Button onPress={() => props.navigation.navigate('Chat')}>
          <Icon
            name='md-chatboxes'
            style={
              props.navigation.state.index === 2
                ? styles.activeIcon
                : styles.inActiveIcon
            }
          />
        </Button>
      </FooterTab>
    </Header>
  );
};
```

Now, back to the original question, how to change the color of the current tab navigator? Just modify the following line by providing an inline style value to the native base element `FooterTab`.

```js
<FooterTab style={{ backgroundColor: 'gray' }}>
```

You will get the following result.

![css21](https://blog.crowdbotics.com/content/images/2019/08/css21.png)

For more information on how to configure a tab navigator, we recommend you to go through the official documentation of `react-navigation` library [here](https://reactnavigation.org/docs/en/bottom-tab-navigator.html).

## Profile Screen

The next screen that is available with the template is the `Profile` screen. This screen, by default, has two clickable actions that will further navigate you to different screens. First, have a look at how it is being displayed on the device.

![css19](https://blog.crowdbotics.com/content/images/2019/08/css19-1.png)

As you can see from the above image, it displays a placeholder for the user avatar image and underneath that placeholder displays the username. Along with the username is the value of `0`. This value is the age of the user displayed by default. Also, there is a settings column related to in-app settings. If you click on the user thumbnail, it will open the profile page that contains user profile details.

![css22](https://blog.crowdbotics.com/content/images/2019/08/css22.png)

To edit the user profile, you can either add a profile image and some details about the user. Look at the screen below.

![css23](https://blog.crowdbotics.com/content/images/2019/08/css23.png)

Do not forget the save any details enter here as the user. Again, the application is using Firebase Firestore to store the image as well as profile details of the app user. This updates the same user document in the Firestore that we took a look in the previous section. On clicking the save button, there is an alert message, and by going back to the Profile screen, you will notice that the user avatar being shown instead of the placeholder image and the correct age of the user.

![css25](https://blog.crowdbotics.com/content/images/2019/08/css25.png)

Here is how an individual user object looks in the Firestore database.

![css26](https://blog.crowdbotics.com/content/images/2019/08/css26.png)

## Settings Screen

The next screen is about the settings available in the application. By default, this blueprint comes up with the following settings screen. It uses native base elements to create toggle buttons and range elements that you are looking at the screen below.

![css27](https://blog.crowdbotics.com/content/images/2019/08/css27.png)

Again, all of the settings modified are saved in the same user document in the Firestore. Keeping all the data related to an individual user inside one document is beneficial to manage and scale.

The settings component comes with a whole of settings that is written inside the file `src/screens/Settings/index.js`. For example, if you decide to add notifications support to the app you are building using this template, you just to visit the `Settings` component file location and you can uncomment the following code.

```js
<Card style={{ borderRadius: 5 }}>
  <CardItem style={{ borderRadius: 5 }}>
    <Text style={styles.redText}>Notifications</Text>
  </CardItem>
  <CardItem>
    <Left>
      <Text style={styles.cardItemText}>New Matches</Text>
    </Left>
    <Right>
      <Switch
        onValueChange={value => this.setState({ notSwitch1: value })}
        onTintColor={commonColor.brandPrimary}
        thumbTintColor={Platform.OS === 'android' ? '#ededed' : undefined}
        value={this.state.notSwitch1}
      />
    </Right>
  </CardItem>
  <CardItem>
    <Left>
      <Text style={styles.cardItemText}>Messages</Text>
    </Left>
    <Right>
      <Switch
        onValueChange={value => this.setState({ notSwitch2: value })}
        onTintColor={commonColor.brandPrimary}
        thumbTintColor={Platform.OS === 'android' ? '#ededed' : undefined}
        value={this.state.notSwitch2}
      />
    </Right>
  </CardItem>
  <CardItem>
    <Left>
      <Text style={styles.cardItemText}>Message Likes</Text>
    </Left>
    <Right>
      <Switch
        onValueChange={value => this.setState({ notSwitch3: value })}
        onTintColor={commonColor.brandPrimary}
        thumbTintColor={Platform.OS === 'android' ? '#ededed' : undefined}
        value={this.state.notSwitch3}
      />
    </Right>
  </CardItem>
  <CardItem>
    <Left>
      <Text style={styles.cardItemText}>Super Likes</Text>
    </Left>
    <Right>
      <Switch
        onValueChange={value => this.setState({ notSwitch4: value })}
        onTintColor={commonColor.brandPrimary}
        thumbTintColor={Platform.OS === 'android' ? '#ededed' : undefined}
        value={this.state.notSwitch4}
      />
    </Right>
  </CardItem>
</Card>
```

This will output the following result on the Settings screen.

![css28](https://blog.crowdbotics.com/content/images/2019/08/css28.png)

## Conclusion

Using a template like this has its benefits. It saves a lot of time and effort to write components from scratch rather than modify the built-in ones. Templates like that are built with commonly used modules like `react-navigation`, `redux`, `native-base` and so on, do save a ton of time when you are building an application for your own business.

This article was to give you an overview how at Crowdbotics we are trying to provide common app solutions in the form of templates and integrations such that you as the app developer can focus on writing advance features, fulfilling your client requests and building businesses.

---

[Originally published at Crowdbotics](https://blog.crowdbotics.com/how-to-use-crowdbotics-template-to-build-a-custom-dating-react-native-app/)
