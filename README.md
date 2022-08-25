# **_VivifyIdeas React Native boilerplate_**

## **Built in functions**

- React query
- Formik & Yup
- Sign in
- Sign up
- Facebook sign in
- Google sign in
- Forgot & reset password
- Internationalization
- Deeplinking
- Global Error Modal ( Something went wrong )
- Edit profile
- Change password
- Push and inapp notifications

## **TBD**

- Sockets
- Chat

## **Code structure and technologies**

For our forms we use [Formik](https://github.com/jaredpalmer/formik), and for validation we use [Yup](https://github.com/jquense/yup).

In components folder there are some examples of our forms, they all use custom text inputs which are located in `FormFields.js`, and in validation folder you will find some `Yup` validation examples.

    ├── components
    ├──── auth
    ├──── shared
    ├─────── FormFields.js
    └── validation

For localization we have `$t` wrapper around [I18n-js](https://github.com/fnando/i18n-js) library.

To use it all you need to do is:

```
import $t from 'i18n';

$t('common.ok');
```

For notifications we use expo notifications. Their setup is located in `NetworkInterceptor.js`. Since the **_iOS_** doesnt support inapp notifications, we use [React Native In App Notifications](https://github.com/AlexSensei/react-native-in-app-notification).

All handling of notifications is done in `NotificationHandleService.js`. It has two main methods, `showInApp` which will trigger the `In App Notification` to be shown, and `handleOnClick` which handles the logic when you click on notification.

The whole application is wrapped in `InAppNotificationProvider` which, as props takes styles for `In APp notifications` you can see them all [here](https://github.com/AlexSensei/react-native-in-app-notification).

## **Going to production**

...

# Fastlane

First create application on iTunes and choose some identifier for it.

In order to store certificates for building app, you need to run inside ios folder:

```
APP_IDENTIFIER= APPLE_ID= DEVELOPER_TEAM_ID= CI_KEYCHAIN_NAME= CI_KEYCHAIN_PASSWORD= GIT_REPO_URL= fastlane match appstore
```

On github you need to define secrets, they can be defined in repository settings:

```
GIT_REPO_URL - https://{your_account_token}@github.com/vivifyideas-internal/{repo_with_certs}
CI_KEYCHAIN_NAME - Name of your keychain
CI_KEYCHAIN_PASSWORD - Password of your keychain
APPLE_ID - email for your Apple Account
APP_STORE_TEAM_ID - teamID on Apple Account
DEVELOPER_TEAM_ID - Developer Team ID On Apple Account
APP_IDENTIFIER - Example: com.vivifyideas.{some_name}
FASTLANE_APPLE_APPLICATION_SPECIFIC_PASSWORD - Password for Fastlane to login to Apple Account
APPLICATION_ID - unique app id (Apple ID in App Information)
MATCH_PASSWORD - Password for fastlane match, which persist encypted certificates
APP_PROVISIONING_PROFILE_NAME - Specify same name that's on https://developer.apple.com/account/resources/certificates/list if you don't have your provisioning profile then create it and choose certificates
PROJECT_NAME - Example: myprojectname - same project name as file for xcode (take a look at .xcodeproj and copy name of that one without extension)
```

If you are using same certificates for multiple projects then you can create provisioning profile and running, you would be able to import existing certificates to new repository:

```
fastlane match import \
    --username {EMAIL_FOR_ITUNES} \
    --git_url {GITHUB_URL_TO_STORE_CERTS} \
    --app_identifier {APP_IDENTIFIER} \
    --team_name {TEAM_NAME_FROM_ITUNES} \
    --type appstore
```
