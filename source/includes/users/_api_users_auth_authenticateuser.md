##AuthenticateUser

**Category:** Authentication<br />
**Permissions:** Public<br />
**CallType:** Synchronous

###Request
>Use this request call

```json
{
  "UserName": "",
  "Password": ""
}
```
> Or you can use this request call

```json
{
  "APIKey": "28c68ac3fcfafc3d4e8d653fe57e5baf",
  "Signature": "29c15c42e4fabcc9e229421e148e647903927c503ab4578ada55bb13a63a9636",
  "UserId": "96",
  "Nonce": "2247733562"
}
```

Authenticates a user for the current websocket session.


| Key       | Value                                                        |
| --------- | ------------------------------------------------------------ |
| Username  | **string.** The user's assigned user name.                   |
| Password  | **string.** The user's assigned password.                    |

or

| Key       | Value                                                        |
| --------- | ------------------------------------------------------------ |
| APIKey    | **string.**  This is an AlphaPoint-generated key used in user-identification. |
| Signature  | **string.** A long, alphanumeric string generated by AlphaPoint by using the APIKey and Nonce. |
| UserId    | **string.** The ID of the user, stated as a string.                             |
| Nonce     | **string.** Any arbitrary number or random string used with the APIKey to generate a signature.                                             |

###Response
>Authenticated response

```json
{
  "authenticated": true,
  "user":
  { "userId": 0,
    "userName": "",
    "email": "",
    "emailVerified": false,
    "accountId": 0,
    "omsId": 0,
    "use2FA": false
  },
  "locked": false,
  "requires2FA": false,
  "twoFAType": "",
  "twoFAToken": "",
  "errormsg": ""
}

```
>False authenticated response

```json
{
  "authenticated": false,
  "locked": false,
  "errormsg": "Invalid username or password"
}

```

| Key           | Value                                                        |
| ------------- | ------------------------------------------------------------ |
| authenticated | **Boolean.** *True* if the user is authenticated; *false* otherwise. |
| user          | JSON user object (below)                                     | 
| locked        | **Boolean.** *True* if this affiliated user is currently locked; *false* otherwise. A user may be locked by trying to log in too many times in rapid succession. He must be *unlocked* by an admin.     |
| requires2FA   | **Boolean.** *True* if the user must use two-factor authentication; *false* otherwise.                                               |
| twoFAType     | **string.** Returns the type of 2FA this user requires. For example, "Google." |
| twoFAToken    | **string.** Returns an appropriate token. In the case of Google, this is a QR code. |
| errormsg      | **string.** A successful receipt of the call returns *null*. |

JSON user object:

| Key           | Value                                                        |
| ------------- | ------------------------------------------------------------ |
| userId        | **integer.** The ID of the user being authenticated on the exchange. |
| userName      | **string.** The name of the user.                            |
| email         | **string.** The email address of the user.                   |
| emailVerified | **Boolean.** Whether the email address has been verified by the registration process or directly by an Admin. |
| accountId     | **integer.** The ID of the account with which the user is associated (each user has a default account). |
| omsId         | **integer.** The ID of the Order Management System with which the user and account are associated. |
| use2FA        | **Boolean.** *True* if the user must use 2FA to log in; *false* otherwise. |


