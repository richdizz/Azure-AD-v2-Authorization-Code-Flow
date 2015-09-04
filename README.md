# Performing OAuth2 Authorization Code Flow with Azure AD v2 App Model

{paste your client id}
{paste your client secret}
{paste your reply url}

## STEP 1: Redirect to login and acquire authorization code ##
*Method*: GET (just paste into browser address bar)

*End-Point*:
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
?client_id={paste your client id}
&scope=openid+https://outlook.office.com/contacts.read+offline_access
&redirect_uri={paste your reply url}
&response_type=code

## Step 2: Post authorization code to get access token ##
*Method*: POST

*End-Point*: 
https://login.microsoftonline.com/common/oauth2/v2.0/token

*Headers*:
Content-Type: application/x-www-form-urlencoded

*Body*:
grant_type=authorization_code
&redirect_uri={paste your reply url}
&client_id={paste your client id}
&client_secret={paste your client secret}
&code={paste authorization code from previous step}
&scope=openid+https://outlook.office.com/contacts.read+offline_access

## Step 3: Get data with access token in header ##
*Method*: GET

*End-Point*: 
https://outlook.office.com/api/v1.0/me/contacts

*Headers*:
Accept:application/json
Content-Type:application/json
Authorization: Bearer {access_token from previous step}
