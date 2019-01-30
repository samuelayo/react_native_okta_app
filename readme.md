# Handling Authentication using Stormpath in React Native

While building applications, authentication is usually a very important aspect because this is how you identify every user and it can sometimes be tedious. This problem is what Authentication Service Providers solve. They provide authentication and user management services for applications and sometimes easily configurable functionalities such as the login, log out, social media integration, etc. and they support authentication protocols such as `OpenID Connect` and `SMAL`.


[View tutorial](https://pusher.com/tutorials/authentication-react-native-okta)

## Getting Started
Clone the project repository by running the command below if you use SSH

```
git clone git@github.com:samuelayo/react_native_okta_app.git
```

If you use https, use this instead

```
git clone https://github.com/samuelayo/react_native_okta_app.git
```

Change directory into the newly cloned project and install dependencies

```
cd react_native_okta
npm install
```

### Prerequisites

#### Setup Okta

To get started with using Okta, create an account on the [registration page](https://developer.okta.com/signup/) and if you’ve already got an account, [log in](https://login.okta.com/). 


After login is successful, we need to add an application and then configure the app. To add an application, from the **Shortcut > Add Application > Create new app**. Then select “Native apps” from the drop-down and click “create”
This will take you to a “Create OpenID Connect Integration” page. Replace "developer" in the redirect URI with your Okta account company name and then save.

Copy out the `ClientID` and the `redirect_uri` when setting up our React Native app.

- Open the `App.js` file and look for line 16 where you have something like this:

```
const config = {
  issuer: 'https://<oktausername>.okta.com',
  clientId: '<your okta application client ID>',
  redirectUrl: 'com.okta.<oktausername>:/callback',
  serviceConfiguration: {
    authorizationEndpoint: 'https://<oktausername>.okta.com/oauth2/v1/authorize',
    tokenEndpoint: 'https://<oktausername>.okta.com/oauth2/v1/token',
    registrationEndpoint: 'https://<oktausername>.okta.com/oauth2/v1/clients'
  },
  additionalParameters: {
    prompt: 'login'
  },
  scopes: ['openid', 'profile', 'email', 'offline_access']
};
```

- Replace the `<oktausername>` placeholder with your username.  
- Replace the `clientId` value with the `clientID` you copied out.
- Ensure that the `redirectUrl` matches with the one you copied.



And finally, build the application:


To build for Android

```
$ react-native run-android
```

To build for iOS

- Navigate to the iOS folder

- install cocoapods 

```
sudo gem install cocoapods
```

- Create a `Podfile` and paste

```
platform :ios, '11.0'
    
target 'react_native_okta_app' do
    pod 'AppAuth', '>= 0.95'
end
```
    

Run `pod install`. If you encounter any error, run `pod repo update`. 
If there are no errors, open the `react_native_okta_app.xcworkspace` and edit the `AppDelegate.h` file.

```
#import <UIKit/UIKit.h>
#import "RNAppAuthAuthorizationFlowManager.h"
    
@interface AppDelegate : UIResponder <UIApplicationDelegate, RNAppAuthAuthorizationFlowManager>
    
@property (nonatomic, weak) id<RNAppAuthAuthorizationFlowManagerDelegate>authorizationFlowManagerDelegate;
    
@property (nonatomic, strong) UIWindow *window;
    
@end

```


```
$ react-native run-ios
```


## Built With

* [React Native](https://facebook.github.io/react-native/) - Build native mobile apps using JavaScript and React
* [Okta](https://www.okta.com/) - OKTA IS THE IDENTITY STANDARD 

