---
description: >-
  The SignUp object contains the state of the current sign-up that the user has
  initiated.
---

# SignUp

## Overview

The SignUp object holds the state of the current sign up and provides helper methods to navigate and complete the [sign up flow](../../main-concepts/sign-up-flow.md). Once a sign up is complete, a new user is created.

There are two important steps that need to be done in order for a sign up to be completed:

* Supply all the required fields. The required fields depend on your [instance settings](../../popular-guides/setup-your-application.md#user-management).
* Verify contact information. Some of the supplied fields need extra verification. These are the email address and phone number.

The above steps can be split into smaller actions (e.g. you don't have to supply all the required fields at once) and can done in any order. This provides great flexibility and supports even the most complicated sign up flows. The SignUp object provides a number of helper methods to achieve the above.

Also, the attributes of the SignUp object can basically be grouped into three categories:

* Those that contain information regarding the sign-up flow and what is missing in order for the sign-up to complete. For more information on these, check our [detailed sign-up flow guide](../../main-concepts/sign-up-flow.md).
* Those that hold the different values that we supply to the sign-up. Examples of these are **username**, **emailAddress**, **firstName**, etc.
* Those that contain references to the created resources once the sign-up is complete, i.e. **createdSessionId** and **createdUserId**.

## Attributes

| Name                          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **status**                    | <p><em>string</em></p><p>The status of the current sign-up. It can take the following values:</p><ul><li><strong>missing_requirements</strong><em>:</em> There are required fields that are either missing or they are unverified. </li><li><strong>complete</strong><em>:</em> All the required fields have been supplied and verified, so the sign-up is complete and a new user and a session have been created.</li><li><strong>abandoned</strong><em>:</em> The sign-up has been inactive for a long period of time, thus it's considered as abandoned and need to start over.</li></ul> |
| **requiredFields**            | <p><em>string[]</em></p><p>An array of all the required fields that need to be supplied and verified in order for this sign-up to be marked as complete and converted into a user.</p>                                                                                                                                                                                                                                                                                                                                                                                                        |
| **optionalFields**            | <p><em>string[]</em></p><p>An array of all the fields that can be supplied to the sign-up, but their absence does not prevent the sign-up from being marked as complete.</p>                                                                                                                                                                                                                                                                                                                                                                                                                  |
| **missingFields**             | <p><em>string[]</em></p><p>An array of all the fields whose values are not supplied yet but they are mandatory in order for a sign-up to be marked as complete.</p>                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **unverifiedFields**          | <p><em>string[]</em></p><p>An array of all the fields whose values have been supplied, but they need additional verification in order for them to be accepted.</p><p>Examples of such fields are <code>emailAddress</code> and <code>phoneNumber</code>.</p>                                                                                                                                                                                                                                                                                                                                  |
| **supportedExternalAccounts** | <p><em>string[]</em></p><p>An array of all the external accounts that are supported in the current sign-up, e.g. <code>oauth_google</code>, <code>oauth_facebook</code>, etc.</p>                                                                                                                                                                                                                                                                                                                                                                                                             |
| **verifications**             | <p><em></em><a href="signup.md#signupverificationresource"><em>SignUpVerificationsResource</em></a><em></em></p><p>An object that contains information about all the verifications that are in-flight.</p>                                                                                                                                                                                                                                                                                                                                                                                    |
| **username**                  | <p><em>string | null</em></p><p>The username supplied to the current sign-up. <br>This attribute is available only <em>if usernames are enabled</em>. Check the available <a href="../../popular-guides/setup-your-application.md#user-management">instance settings</a> for more information.</p>                                                                                                                                                                                                                                                                                            |
| **emailAddress**              | <p><em>string | null</em></p><p>The email address supplied to the current sign-up.</p><p>This attribute is available only <em>if the selected contact information includes email address</em>. Check the available <a href="../../popular-guides/setup-your-application.md#user-management">instance settings</a> for more information.</p>                                                                                                                                                                                                                                                   |
| **phoneNumber**               | <p><em>string | null</em></p><p>The phone number supplied to the current sign-up.<br>This attribute is available only <em>if the selected contact information includes phone number</em>. Check the available <a href="../../popular-guides/setup-your-application.md#user-management">instance settings</a> for more information.</p>                                                                                                                                                                                                                                                        |
| **passwordEnabled**           | <p><em>boolean</em></p><p>The value of this attribute is true if a password was supplied to the current sign-up.</p><p>This attribute is available only <em>if password-based authentication is enabled</em>. Check the available <a href="../../popular-guides/setup-your-application.md#user-management">instance settings</a> for more information.</p>                                                                                                                                                                                                                                    |
| **firstName**                 | <p><em>string | null</em></p><p>The first name supplied to the current sign-up.<br>This attribute is available only <em>if  name is enabled in personal information</em>. Check the available <a href="../../popular-guides/setup-your-application.md#user-management">instance settings</a> for more information.</p>                                                                                                                                                                                                                                                                        |
| **lastName**                  | <p><em>string | null</em></p><p>The last name supplied to the current sign-up.<br>This attribute is available only <em>if  name is enabled in personal information</em>. Check the available <a href="../../popular-guides/setup-your-application.md#user-management">instance settings</a> for more information.</p>                                                                                                                                                                                                                                                                         |
| **unsafeMetadata**            | <p><em>{[string]: any} | null</em></p><p>Metadata that can be read and set from the frontend. <br><em></em>Once the sign up is complete, the value of this field will be automatically copied to the newly created user's unsafe metadata.<br>One common use case for this attribute is to use it to implement custom fields that can be collected during sign up and will automatically be attached to the created <a href="user.md">User object</a>.</p>                                                                                                                                    |
| **createdSessionId**          | <p><em>string | null</em></p><p>The<em> </em>identifier of the newly-created session. This attribute is populated only when the sign-up is complete.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| **createdUserId**             | <p><em>string | null</em></p><p>The<em> </em>identifier of the newly-created user. This attribute is populated only when the sign-up is complete.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                         |

## Methods

### create(params)

`create(params: SignUpParams) => Promise<SignUpResource>`

This method initiates a new [sign up flow](../../main-concepts/sign-up-flow.md). It creates a new SignUp object and de-activates any existing SignUp that the client might already had in progress.

The form of the given `params` depends on the [configuration of the instance](../../popular-guides/setup-your-application.md#user-management). Choices on the instance settings affect which options are available to use.

The `create` method will return a promise of the new SignUp object. This sign up might be complete if you supply the required fields in one go. However, this is not mandatory. Our sign up process provides great flexibility and allows users to easily create multi-step sign up flows.

{% tabs %}
{% tab title="Parameters" %}
| Name       | Description                                  |
| ---------- | -------------------------------------------- |
| **params** | __[_SignUpParams_](signup.md#signupparams)__ |
{% endtab %}

{% tab title="Returns" %}
_Promise<_[_SignUpResource_](signup.md#attributes)_>_

This method returns a `Promise` which resolves with a `SignUp` object. Check the `status` attribute to see if the `SignUp` has been completed or a hint on what needs to happen next.
{% endtab %}
{% endtabs %}

### update(params)

`update(params: SignUpParams) => Promise<SignUpResource>`

This method is used to update the current sign up.

As with `create`, the form of the given `params` depends on the [configuration of the instance](../../popular-guides/setup-your-application.md#user-management).

{% tabs %}
{% tab title="Parameters" %}
| Name       | Description                                  |
| ---------- | -------------------------------------------- |
| **params** | __[_SignUpParams_](signup.md#signupparams)__ |
{% endtab %}

{% tab title="Returns" %}
_Promise<_[_SignUpResource_](signup.md#attributes)_>_

This method returns a `Promise` which resolves with a `SignUp` object. Check the `status` attribute to see if the `SignUp` has been completed or a hint on what needs to happen next.
{% endtab %}
{% endtabs %}

### prepareVerification(strategy)

`prepareVerification(strategy: SignUpVerificationStrategy) => Promise<SignUpResource>`

The `prepareVerification` is used to initiate the verification process for a field that requires it. As mentioned above, there are two fields that need to be verified:&#x20;

* emailAddress: The email address can be verified via an email code. This is a one-time code that is sent to the email already provided to the SignUp object. The `prepareVerification` sends this email.
* phoneNumber: The phone number can be verified via a phone code. This is a one-time code that is sent via an SMS to the phone already provided to the SignUp object. The `prepareVerification` sends this SMS.

{% tabs %}
{% tab title="Parameters" %}
| Name         | Description                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **strategy** | <p><em></em><a href="signup.md#signupverificationstrategy"><em>SignUpVerificationStrategy</em></a><em></em></p><p>The strategy you want to use for the verification process.</p><p>Each strategy applies to a different identification type, e.g. <code>email_code</code> can only be used to verify email addresses whereas <code>phone_code</code> can be used only for phone numbers.<br>Select the one that makes for your use case.</p> |
{% endtab %}

{% tab title="Returns" %}
_Promise<_[_SignUpResource_](signup.md#attributes)_>_

This method returns a `Promise` which resolves with a `SignUp` object.
{% endtab %}
{% endtabs %}

### attemptVerification(params)

`attemptVerification(params: SignUpVerificationAttemptParams) => Promise<SignUpResource>`

Attempts to complete the in-flight verification process that corresponds to the given strategy. In order to use this method, you should first initiate a verification process by calling [SignUp.prepareVerification](signup.md#prepareverification-strategy).

Depending on the strategy, the method parameters could differ.

{% tabs %}
{% tab title="Parameters" %}
| Name       | Description                                                                        |
| ---------- | ---------------------------------------------------------------------------------- |
| **params** | __[_SignUpVerificationAttemptParams_](signup.md#signupverificationattemptparams)__ |
{% endtab %}

{% tab title="Returns" %}
_Promise<_[_SignUpResource_](signup.md#attributes)_>_

This method returns a `Promise` which resolves with a `SignUp` object. Check the `status` attribute to see if the `SignUp` has been completed or a hint on what needs to happen next.
{% endtab %}
{% endtabs %}

### prepareEmailAddressVerification()

`prepareEmailAddressVerification() => Promise<SignUpResource>`

Helper method that allows you to initiate a verification process for an email address. It basically sends a one-time code to the email address already supplied to the current sign up.

This is equivalent to calling `SignUp.prepareVerification("email_code")`.

{% tabs %}
{% tab title="Returns" %}
_Promise<_[_SignUpResource_](signup.md#attributes)_>_

This method returns a `Promise` which resolves with a `SignUp` object.
{% endtab %}
{% endtabs %}

### attemptEmailAddressVerification(params)

`attemptEmailAddressVerification(params: VerificationAttemptParams) => Promise<SignUpResource>`

Helper method that attempts to complete the verification process for an email address. It basically verifies that the supplied code is the same as the one-time code that was sent to the email address during the prepare verification phase.

This is equivalent to calling `SignUp.attemptVerification({strategy: "email_code", ...params})`.

{% tabs %}
{% tab title="Parameters" %}
| Name       | Description                                                            |
| ---------- | ---------------------------------------------------------------------- |
| **params** | __[_VerificationAttemptParams_](signup.md#verificationattemptparams)__ |
{% endtab %}

{% tab title="Returns" %}
_Promise<_[_SignUpResource_](signup.md#attributes)_>_

This method returns a `Promise` which resolves with a `SignUp` object. Check the `status` attribute to see if the `SignUp` has been completed or a hint on what needs to happen next.
{% endtab %}
{% endtabs %}

### preparePhoneNumberVerification()

`preparePhoneNumberVerification() => Promise<SignUpResource>`

Helper method that allows you to initiate a verification process for a phone number. It basically sends a one-time code to the phone number already supplied to the current sign up.

This is equivalent to calling `SignUp.prepareVerification("phone_code")`.

{% tabs %}
{% tab title="Returns" %}
_Promise<_[_SignUpResource_](signup.md#attributes)_>_

This method returns a `Promise` which resolves with a `SignUp` object.
{% endtab %}
{% endtabs %}

### attemptPhoneNumberVerification(params)

`attemptPhoneNumberVerification(params: VerificationAttemptParams) => Promise<SignUpResource>`

Helper method that attempts to complete the verification process for a phone number. It basically verifies that the supplied code is the same as the one-time code that was sent to the phone number during the prepare verification phase..

This is equivalent to calling `SignUp.attemptVerification({strategy: "phone_code", ...params})`.

{% tabs %}
{% tab title="Parameters" %}
| Name       | Description                                                            |
| ---------- | ---------------------------------------------------------------------- |
| **params** | __[_VerificationAttemptParams_](signup.md#verificationattemptparams)__ |
{% endtab %}

{% tab title="Returns" %}
_Promise<_[_SignUpResource_](signup.md#attributes)_>_

This method returns a `Promise` which resolves with a `SignUp` object. Check the `status` attribute to see if the `SignUp` has been completed or a hint on what needs to happen next.
{% endtab %}
{% endtabs %}

### authenticateWithRedirect(params) <a href="signinwithoauth" id="signinwithoauth"></a>

`authenticateWithRedirect(params: AuthenticateWithRedirectParams) => Promise<void>`

Signs up users via OAuth,  where an external account provider is used to verify the user's identity and provide certain information about the user.

{% tabs %}
{% tab title="Parameters" %}
| Name       | Description                                                                                                                                                                                                                                                                                                                                                        |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **params** | <p><em></em><a href="signup.md#authenticatewithredirectparams"><em>AuthenticateWithRedirectParams</em></a><em></em></p><p>An object that specifies the verification strategy (one of the supported OAuth providers), the callback URL the OAuth provider should redirect to, as well as the URL that the user should be redirected to upon successful sign in.</p> |
{% endtab %}

{% tab title="Returns" %}
_Promise\<void>_

This method returns a `Promise` which doesn't resolve to any value.
{% endtab %}
{% endtabs %}

## Interfaces

### SignUpParams

| Name               | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **firstName**      | <p><em>string | null</em></p><p>The user's first name.</p><p>This option is available only if name is selected in personal information.</p><p>Please check the <a href="../../popular-guides/setup-your-application.md#user-management">instance settings</a> for more information.</p>                                                                                                                                                                    |
| **lastName**       | <p><em>string | null</em></p><p>The user's last name.</p><p>This option is available only if name is selected in personal information.</p><p>Please check the <a href="../../popular-guides/setup-your-application.md#user-management">instance settings</a> for more information.</p>                                                                                                                                                                     |
| **password**       | <p><em>string | null</em></p><p>The user's password.</p><p>This option is available only if password-based authentication is selected.</p><p>Please check the <a href="../../popular-guides/setup-your-application.md#user-management">instance settings</a> for more information.</p>                                                                                                                                                                     |
| **emailAddress**   | <p><em>string | null</em></p><p>The user's email address.</p><p>This option is available only if email address is selected in contact information. <br>Keep in mind that the email address requires an extra verification process.</p><p>Please check the <a href="../../popular-guides/setup-your-application.md#user-management">instance settings</a> for more information.</p>                                                                         |
| **phoneNumber**    | <p><em>string | null</em></p><p>The user's phone number.</p><p>This option is available only if phone number is selected in contact information.<br>Keep in mind that the phone number requires an extra verification process.</p><p>Please check the <a href="../../popular-guides/setup-your-application.md#user-management">instance settings</a> for more information.</p>                                                                             |
| **username**       | <p><em>string | null</em></p><p>The user's username.</p><p>This option is available only if usernames are enabled.</p><p>Please check the <a href="../../popular-guides/setup-your-application.md#user-management">instance settings</a> for more information.</p>                                                                                                                                                                                         |
| **unsafeMetadata** | <p><em>{[string]: any} | null</em></p><p>Metadata that can be read and set from the frontend. <br><em></em>Once the sign up is complete, the value of this field will be automatically copied to the newly created user's unsafe metadata.<br>One common use case for this attribute is to use it to implement custom fields that can be collected during sign up and will automatically be attached to the created <a href="user.md">User object</a>.</p> |

### SignUpVerificationsResource

| Name             | Description                                                                   |
| ---------------- | ----------------------------------------------------------------------------- |
| **emailAddress** | __[_SignUpVerificationResource_](signup.md#signupverificationattemptparams)__ |
| **phoneNumber**  | [_SignUpVerificationResource_](signup.md#signupverificationattemptparams)__   |

### SignUpVerificationResource

| Name                    | Description                                                                                                                                                                                                                                                                                                                        |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **status**              | <p><em>string | null</em></p><p>The verification status.</p>                                                                                                                                                                                                                                                                       |
| **nextAction**          | <p><em>string</em></p><p>Specifies the action that you could do next in order to complete this verification.</p>                                                                                                                                                                                                                   |
| **supportedStrategies** | <p><em>string[]</em></p><p>An array of all strategies supported for this resource.</p>                                                                                                                                                                                                                                             |
| **strategy**            | <p><em>string | null</em></p><p>The verification strategy. Possible <code>strategy</code> values are:</p><ul><li><strong>email_code</strong>: User will receive a one-time authentication code via email.</li><li><strong>phone_code</strong>: User will receive a one-time authentication code in their phone, via SMS.</li></ul> |
| **attempts**            | <p><em>number | null</em></p><p>The number of attempts to complete the verification so far. Usually, a verification allows for maximum 3 attempts to be completed.</p>                                                                                                                                                             |
| **expireAt**            | <p><em>Date | null</em></p><p>The timestamp when the verification will expire and cease to be valid.</p>                                                                                                                                                                                                                           |
| **error**               | <p><a href="broken-reference"><em>ClerkAPIError</em></a><em> | null</em></p><p>Any error that occurred during the verification process from the <a href="../frontend-api-reference/">Clerk API</a>.</p>                                                                                                                            |

### SignUpVerificationAttemptParams

| Name         | Description                                                                                                                                                                                                                                                                                                                         |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **strategy** | __[_SignUpVerificationStrategy_](signup.md#signupverificationstrategy)__                                                                                                                                                                                                                                                            |
| **code**     | <p><em>string</em></p><p>This property is applicable for strategies <code>email_code</code> and <code>phone_code</code>.</p><p>This represents the one-time code that was sent to either the email address or the phone number during the <a href="signup.md#prepareverification-strategy">SignUp.prepareVerification</a> step.</p> |

### VerificationAttemptParams

| Name     | Description                                                                                                                                                                                                                                                                                                                         |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **code** | <p><em>string</em></p><p>This property is applicable for strategies <code>email_code</code> and <code>phone_code</code>.</p><p>This represents the one-time code that was sent to either the email address or the phone number during the <a href="signup.md#prepareverification-strategy">SignUp.prepareVerification</a> step.</p> |

### AuthenticateWithRedirectParams

| Property                | Description                                                                                                                                                                |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **strategy**            | <p><em>string</em></p><p>The OAuth provider that will be used for singing in. Must be one of the supported <a href="signup.md#oauthstrategy">OAuthStrategy</a> values.</p> |
| **callbackUrl**         | <p><em>string</em></p><p>The URL that the OAuth provider should redirect to, on successful authorization on their part.</p>                                                |
| **callbackUrlComplete** | <p><em>string</em></p><p>The URL that the user will be redirected to, after successful authorization from the OAuth provider and Clerk sign in</p>                         |

## Types

### SignUpVerificationStrategy

`email_code | phone_code`

| Value           | Description                                                                                                                                               |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **email\_code** | <p>Specify email code as the verification strategy.</p><p>This applies only to email addresses and is a one-time code sent to that email address.</p>     |
| **phone\_code** | <p>Specify phone code as the verification strategy.</p><p>This applies only to phone number and is a one-time code sent to that phone number via SMS.</p> |

### OAuthStrategy

`oauth_facebook | oauth_github | oauth_google | oauth_hubspot | oauth_tiktok`

| Value               | Description                                          |
| ------------------- | ---------------------------------------------------- |
| **oauth\_facebook** | Specify Facebook as the verification OAuth provider. |
| **oauth\_github**   | Specify Github as the verification OAuth provider.   |
| **oauth\_google**   | Specify Google as the verification OAuth provider.   |
| **oauth\_hubspot**  | Specify Hubspot as the verification OAuth provider.  |
| **oauth\_tiktok**   | Specify TikTok as the verification OAuth provider.   |