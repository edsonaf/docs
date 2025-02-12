---
description: The User object contains the user's account information.
---

# User

## Overview

The `User` object holds all the information for a user of your application and provides a set of methods to manage their account.

Users have a unique authentication identifier which might be their email address, phone number or a username.

Users can be contacted at their primary email address or primary phone number. They can have more than one registered email addresses, but only one of them will be their primary email address. Same thing with phone numbers; they can have more than one, but only one will be their primary.

Finally, `User` objects hold profile data like their name, a profile image and a set of metadata that can be used internally to store arbitrary information. The metadata are split into public and private. Both types are set from the [Backend API](../backend-api-reference/), but public metadata can be accessed from the [Frontend API](../frontend-api-reference/) and [Backend API](../backend-api-reference/).

The ClerkJS SDK provides some helper [methods](user.md#methods) on the `User` object to help retrieve and update user information and authentication status.

## Attributes

| Name                      | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **id**                    | <p><em>string</em></p><p>A unique identifier for the user.</p>                                                                                                                                                                                                                                                                                                                                                                                                                    |
| **firstName**             | <p><em>string | null</em></p><p>The user's first name.</p>                                                                                                                                                                                                                                                                                                                                                                                                                        |
| **lastName**              | <p><em>string | null</em></p><p>The user's last name.</p>                                                                                                                                                                                                                                                                                                                                                                                                                         |
| **fullName**              | <p><em>string | null</em></p><p>The user's full name, a combination of their first and last name.</p>                                                                                                                                                                                                                                                                                                                                                                             |
| **username**              | <p><em>string | null</em></p><p>The user's username.</p>                                                                                                                                                                                                                                                                                                                                                                                                                          |
| **profileImageUrl**       | <p><em>string | null</em></p><p>The URL for the user's profile image.</p>                                                                                                                                                                                                                                                                                                                                                                                                         |
| **primaryEmailAddress**   | <p><em></em><a href="emailaddress.md"><em>EmailAddress</em></a> <em>| null</em></p><p>Information about the user's primary email address.</p>                                                                                                                                                                                                                                                                                                                                     |
| **primaryEmailAddressId** | <p><em>string | null</em></p><p>The unique identifier for the <a href="emailaddress.md">EmailAddress</a> that the user has set as primary.</p>                                                                                                                                                                                                                                                                                                                                    |
| **emailAddresses**        | <p><em></em><a href="emailaddress.md"><em>EmailAddress</em></a><em>[]</em></p><p>Any array of all the <a href="emailaddress.md">EmailAddress</a> objects associated with the user. Includes the primary.</p>                                                                                                                                                                                                                                                                      |
| **primaryPhoneNumber**    | <p><em></em><a href="phonenumber.md"><em>PhoneNumber</em> </a><em>| null</em></p><p>Information about the user's primary phone number.</p>                                                                                                                                                                                                                                                                                                                                        |
| **primaryPhoneNumberId**  | <p><em>string | null</em></p><p>The unique identifier for the <a href="phonenumber.md">PhoneNumber</a> that the user has set as primary.</p>                                                                                                                                                                                                                                                                                                                                      |
| **phoneNumbers**          | <p><em></em><a href="phonenumber.md"><em>PhoneNumber</em></a><em>[]</em></p><p>Any array of all the <a href="phonenumber.md">PhoneNumber</a> objects associated with the user. Includes the primary.</p>                                                                                                                                                                                                                                                                          |
| **primaryWeb3WalletId**   | <p><em>string | null</em></p><p>The unique identifier for the <a href="web3wallet.md">Web3Wallet</a> that the user signed up with.</p>                                                                                                                                                                                                                                                                                                                                            |
| **web3Wallets**           | <p><em></em><a href="web3wallet.md"><em>Web3Wallet</em></a><em>[]</em></p><p>Any array of all the <a href="web3wallet.md">Web3Wallet</a> objects associated with the user. Includes the primary.</p>                                                                                                                                                                                                                                                                              |
| **externalAccounts**      | <p><em></em><a href="user.md#externalaccount"><em>ExternalAccount</em></a><em>[]</em></p><p> Any array of all the <a href="user.md#externalaccount">ExternalAccount</a> objects associated with the user with OAuth.</p>                                                                                                                                                                                                                                                          |
| **passwordEnabled**       | <p><em>boolean</em></p><p> A boolean indicating whether the user has a password on their account.</p>                                                                                                                                                                                                                                                                                                                                                                             |
| **publicMetadata**        | <p><em>{[string]: any} | null</em></p><p>Metadata that can be read from the <a href="../frontend-api-reference/">Frontend API</a> and <a href="../backend-api-reference/">Backend API</a> and can be set only from the Backend API .</p>                                                                                                                                                                                                                                          |
| **privateMetadata**       | <p><em>{[string]: any} | null</em></p><p>Metadata that can be read and set only from the <a href="../backend-api-reference/">Backend API</a>.</p>                                                                                                                                                                                                                                                                                                                                 |
| **unsafeMetadata**        | <p><em>{[string]: any} | null</em></p><p>Metadata that can be read and set from the frontend. <br><em></em>One common use case for this attribute is to use it to implement custom fields that will be attached to the User object.<br>Please note that there is also an <code>unsafeMetadata</code> attribute in the <a href="signup.md">SignUp</a> object. The value of that field will be automatically copied to the user's unsafe metadata once the sign up is complete.</p> |
| **createdAt**             | <p><em>Date</em></p><p>Date when the user was first created.</p>                                                                                                                                                                                                                                                                                                                                                                                                                  |
| **updatedAt**             | <p><em>Date</em></p><p>Date of the last time the user was updated.</p>                                                                                                                                                                                                                                                                                                                                                                                                            |

## Methods

### createEmailAddress(email)

`createEmailAddress(email: string) => Promise<EmailAddressResource>`

Adds an email address for the user. A new [EmailAddress](emailaddress.md) will be created and associated with the user.

{% tabs %}
{% tab title="Parameters" %}
| Name      | Description                                                                |
| --------- | -------------------------------------------------------------------------- |
| **email** | <p><em>string</em></p><p>The email address to associate with the user.</p> |
{% endtab %}

{% tab title="Returns" %}
_Promise<_[_EmailAddressResource_](emailaddress.md)_>_

This method returns a `Promise` which resolves with an `EmailAddress` object.
{% endtab %}
{% endtabs %}

### createPhoneNumber(phoneNumber)

`createPhoneNumber(phoneNumber: string) => Promise<PhoneNumberResource>`

Adds a phone number for the user. A new [PhoneNumber](phonenumber.md) will be created and associated with the user.

{% tabs %}
{% tab title="Parameters" %}
| Name            | Description                                                               |
| --------------- | ------------------------------------------------------------------------- |
| **phoneNumber** | <p><em>string</em></p><p>The phone number to associate with the user.</p> |
{% endtab %}

{% tab title="Returns" %}
_Promise<_[_PhoneNumberResource_](phonenumber.md)_>_

This method returns a `Promise` which resolves with a `PhoneNumber` object
{% endtab %}
{% endtabs %}

### getSessions()

`getSessions() => Promise<SessionWithActivities[]>`

Retrieves all **active** sessions for this user. This method uses a cache so a network request will only be triggered only once.

{% tabs %}
{% tab title="Parameters" %}
This method accepts no parameters.
{% endtab %}

{% tab title="Returns" %}
_Promise<_[_SessionWithActivities_](sessionwithactivities.md)_\[]>_

This method returns a `Promise` which resolves to an array of `SessionWithActivities` objects.
{% endtab %}
{% endtabs %}

### getToken(service, options?)

`getToken(service: JWTService, options?: GetUserTokenOptions) => Promise<string>`

Retrieves the user's token for the given integration service. This method uses a cache so a network request will only be made if the token in memory has expired. The TTL for each token is one minute.

{% tabs %}
{% tab title="Parameters" %}
| Name         | Description                                                                                                                                                                                                                               |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **service**  | <p><em></em><a href="user.md#jwtservice"><em>JWTService</em></a><em></em></p><p>The name of the service that you've integrated with. </p>                                                                                                 |
| **options?** | <p><em></em><a href="user.md#usergettokenoptions"><em>GetUserTokenOptions</em></a><em></em></p><p>Optionally pass the leeway for expiring the cache. Default leeway is 10 seconds and cannot exceed the token TTL, which is 1 minute.</p> |
{% endtab %}

{% tab title="Returns" %}
_Promise\<string>_\
Returns a `Promise` that resolves to a `string`. The string is the user's token for the provided integration service.
{% endtab %}
{% endtabs %}

### setProfileImage(file)

`setProfileImage(file: Blob | File) => Promise<ImageResource>`

Add the user's profile image or replace it if one already exists. This method will upload an image and associate it with the user.

{% tabs %}
{% tab title="Parameters" %}
| Name     | Description                                                                                  |
| -------- | -------------------------------------------------------------------------------------------- |
| **file** | <p><em>Blob | File</em></p><p>A file or file-like object (raw data). Should be an image.</p> |
{% endtab %}

{% tab title="Returns" %}
_Promise<_[_ImageResource_](user.md#imageresource)_>_

This method
{% endtab %}
{% endtabs %}

### twoFactorEnabled()

`twoFactorEnabled() => boolean`

Checks if the user has enabled 2-step verification (2FA) for their account.

{% tabs %}
{% tab title="Parameters" %}
This method accepts no parameters.
{% endtab %}

{% tab title="Returns" %}
_boolean_

This method returns `true` when the user has enabled 2-factor authentication, `false` otherwise.
{% endtab %}
{% endtabs %}

### update(params)

`update(params: UpdateUserParams) => Promise<UserResource>`

Updates the user's attributes. Use this method to save information you collected about the user.&#x20;

{% tabs %}
{% tab title="Parameters" %}
| Name       | Description                                                                                                                      |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------- |
| **params** | <p><em></em><a href="user.md#updateuserparams"><em>UpdateUserParams</em></a><em></em></p><p>User profile related attributes.</p> |
{% endtab %}

{% tab title="Returns" %}
_Promise<_[_UserResource_](user.md)_>_

This method returns a `Promise` which resolves to a `User` object.
{% endtab %}
{% endtabs %}

## Interfaces

### ExternalAccount

| Property           | Description                                                                                                                     |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------- |
| **id**             | <p><em>string</em></p><p>A unique identifier for this external account.</p>                                                     |
| **provider**       | <p><em></em><a href="user.md#oauthprovider"><em>OAuthProvider</em></a><em></em></p><p>The name of the OAuth provider. </p>      |
| **externalId**     | <p><em>string</em></p><p>The user's unique identifier at the OAuth provider.</p>                                                |
| **emailAddress**   | <p><em>string</em></p><p>The user's email address registered with the OAuth provider.</p>                                       |
| **approvedScopes** | <p><em>string</em></p><p>A list of <a href="https://oauth.net/2/scope/">OAuth scopes</a> as returned by the OAuth provider.</p> |
| **firstName**      | <p><em>string</em></p><p>The user's first name as registered with the OAuth provider.</p>                                       |
| **lastName**       | <p><em>string</em></p><p>The user's first name as registered with the OAuth provider.</p>                                       |
| **picture**        | <p><em>string</em></p><p>URL for the user's profile picture (avatar) that's registered with the OAuth provider.</p>             |

### ImageResource

| Property      | Description                                                                  |
| ------------- | ---------------------------------------------------------------------------- |
| **id**        | <p><em>string</em></p><p>A unique identifier for this image.</p>             |
| **name**      | <p><em>string</em></p><p>A name for this image. The image title.</p>         |
| **publicUrl** | <p><em>string</em></p><p>The URL which can be used to access this image.</p> |

### UpdateUserParams

| Property                  | Description                                                                                                                                                                                                                             |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **username**              | <p><em>string</em></p><p>The username for the user.</p>                                                                                                                                                                                 |
| **firstName**             | <p><em>string</em></p><p>The user's first name.</p>                                                                                                                                                                                     |
| **lastName**              | <p><em>string</em></p><p>The user's last name.</p>                                                                                                                                                                                      |
| **primaryEmailAddressId** | <p><em>string</em></p><p>Use this attribute to reference an <a href="emailaddress.md">EmailAddress</a> object by ID and associate it with the user.</p>                                                                                 |
| **primaryPhoneNumberId**  | <p><em>string</em></p><p>Use this attribute to reference a <a href="phonenumber.md">PhoneNumber</a> object by ID and associate it with the user.</p>                                                                                    |
| **password**              | <p><em>string</em></p><p>The user's password.</p>                                                                                                                                                                                       |
| **unsafeMetadata**        | <p><em>{[string]: any} | null</em></p><p>Metadata that can be read and set from the frontend. <br><em></em>One common use case for this attribute is to use it to implement custom fields that will be attached to the User object.</p> |

### GetUserTokenOptions

| Property             | Description                                                                              |
| -------------------- | ---------------------------------------------------------------------------------------- |
| **leewayInSeconds?** | <p><em>number</em></p><p>The number of seconds that we allow the token to be cached.</p> |

## Types

### JWTService

`clerk | firebase | hasura`

| Value        | Description                                                  |
| ------------ | ------------------------------------------------------------ |
| **clerk**    | Get a short-lived Clerk JWT.                                 |
| **firebase** | Integration with [Firebase](../../integrations/firebase.md). |
| **hasura**   | Integration with [Hasura](../../integrations/hasura.md).     |

### OAuthProvider

`facebook | github | google | hubspot | tiktok | gitlab | discord | twitter | twitch | linkedin | dropbox`

| Value        | Description              |
| ------------ | ------------------------ |
| **facebook** | Facebook OAuth provider. |
| **github**   | Github OAuth provider.   |
| **google**   | Google OAuth provider.   |
| **hubspot**  | Hubspot OAuth provider.  |
| **tiktok**   | TikTok OAuth provider.   |
| **gitlab**   | GitLab OAuth provider.   |
| **discord**  | Discord OAuth provider.  |
| **twitter**  | Twitter OAuth provider.  |
| **twitch**   | Twitch OAuth provider.   |
| **linkedin** | LinkedIn OAuth provider. |
| **dropbox**  | Dropbox OAuth provider.  |
