# SAML

***The assertion says which application it is for. What would happen if an application accepted an assertion that named a different application?***

- If an application accepted an assertion intended for a different application, it could incorrectly authenticate the user. An attacker could potentially take a valid assertion issued for one application and reuse it against another application that fails to check the Audience, gaining access as that user.***


***The assertion is valid for a limited window, on the order of an hour. Why not forever?***

- Because a SAML assertion is a temporary proof of authentication, not a permanent credential. If it were valid forever, someone who obtained a copy of the assertion could potentially reuse it indefinitely. By giving it a limited validity window, the risk is reduced because the assertion eventually expires and can no longer be used.


***The application knows the assertion is genuine because it is signed. What does the application need to have been given, ahead of time, to check that signature?***

- The application needs the Identity Provider's public key ahead of time. It uses that public key to verify the digital signature created with the IdP's private key.


# OIDC 

***ID token vs. access token***

- ID token = tells the application who you are.

It is meant for the application (client). It contains identity information about the authenticated user, such as their subject identifier and possibly name/email.

- Access token = allows access to an API.

It is meant to be presented to a resource server/API to access resources on the user's behalf.

ID token: “This is Christopher, and the IdP authenticated him.”

Access token: “Christopher authorized this application to access this API.”

- You don't use one in place of the other because they have different purposes and audiences. An ID token is not an API authorization credential, and an access token is not the application's proof of the user's identity.
