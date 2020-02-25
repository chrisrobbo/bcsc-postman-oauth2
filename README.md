# BCSC-Postman OAuth 2.0
A Postman collection for authenticating to the BCSC API. 

## Steps to get up and running
Follow these steps to quickly test out your access to the BC Services Card OIDC environment

### 1. Get an OAuth2 (OIDC)  key and secrect for your application from the BC Services Card Self Service site
Lets assume that these are called "Client key" and "Client secret". Remember your redirect URL "Redirect URL"

### 2. Import the BCSC OAuth 2.0 collection and BCSC environment into Postman
Click the button below and select the Desktop version of Postman (Chrome extension doesn't support environment variables). This will also install the Collection and Environment we'll be using.

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/fill-this-in

Alternatively, you can download the BCSC OAuth2.0.postman_collection and BCSC 2.0.postman_environment JSON files above and import them via the Import button in the top left of the Postman Workplace sceen.

### 3. Add your first set of environment variables in Postman
Copy your  Client id, Client secret and OAuth 2.0 redirect URI from your request to the test system into the environment variables in Postman. To add these details to the Environment, make sure you have the OAuth 2.0 Environment selected, click the eye button, then edit.

![Environment with some details](images/3_1_addedToEnvironment.PNG)

### 4. Add the scopes for the endpoints you will be accessing.
Our Developer Center lists the available scopes [here](https://developer.xero.com/documentation/oauth2/scopes). For getting started you will need at least:

`offline_access accounting.transactions`

In addition, to make further test calls we would also suggest adding:

`openid profile email accounting.contacts accounting.settings`

Add the scopes required to the `scopes` environment variable.

![Add some Scopes to your Environment](images/4_1_addScopesToEnvironment.PNG)

### 5. Generate your access token
1. Double-click on the GET Get Started request under the Xero OAuth 2.0 Collection
1. Select the Authorization tab
1. Click Get New Access Token

![Click the Get new Access Token Button](images/5_1_generateAccessToken.png)

1. Add the Variable names surronded by {{}} from your Environment into the fields, as shown in the screenshot below
1. Add https://login.xero.com/identity/connect/authorize to the Auth URL field
1. Add https://identity.xero.com/connect/token to the Access Token Field
1. Click Request Token

![Request your Access Token](images/5_2_addTheVariablesAndURLs.PNG)

At this stage you will be prompted to log in to Xero. 

![Login to Xero](images/5_3_askedToLogin.PNG)

If you've included the `openid profile email` scopes, you'll be asked to access your basic profile information.

![Allow Basic Profile Information](images/5_4_basicProfile.PNG)

You'll then be taken through to the Organisation Select window. Select the Organisation you want to connect to. If you want to connect to more than one Organisation, you can repeat the steps above and select another Organisation. 

![Select your Organisation](images/5_5_selectOrganisation.PNG)

Once complete you'll be passed back to Postman.

### 6. Set your Access and Refresh Tokens
We now have the last remaining tokens needed to access the Xero API. These need to be set to the Environment Variables, to do this:
1. Highlight the Access Token
1. Right-click on it
1. Select Set: OAuth 2.0 > access_token

Follow the same process for the Refresh Token.

![Set your Access and Refresh Tokens](images/6_1_setTheAccessAndRefreshTokens.png)

Congrats! You're now authenticated and can start making API calls. Your access token will last for 12mins, after which time you'll need to refresh the token. 

### 8. Make your first API call!
1. Double-click to load the GET Invoices request
1. Ensure No Auth is set on the Authorization tab
1. Click Send

### 9. Refreshing the token
1. Double-click to load the POST Refresh token request
1. Ensure No Auth is set on the Authorization tab
1. Click Send

### Notes:
* We use the built in OAuth 2.0 support to get the token, however we then set this as an environment variable. So we don't need to use this support when making the normal API calls.
