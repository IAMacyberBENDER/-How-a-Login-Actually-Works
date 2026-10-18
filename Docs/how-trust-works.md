# Where the trust actually comes from

Before any user signs in, an administrator configures the trust relationship between the application (Service Provider or SP) and the Identity Provider (IdP). This setup is called federation. It establishes how the two sides recognize and trust each other. Every authentication that follows relies on this configuration.

***The following information is exchanged or configured in advance:***

- Application identifier: Identifies the application to the IdP. It helps the IdP recognize which application is requesting authentication and allows the application to validate that the returned assertion or token is intended for it.

- Reply address: Specifies where the IdP should send the authentication response. This address must be registered in advance so the IdP can validate the destination instead of allowing responses to be sent to arbitrary URLs. This is a security control, not just an administrative requirement.

- Signing certificate or public key: The IdP uses its private key to sign authentication information. The application uses the corresponding public key, often provided through a signing certificate, to verify the signature. The private key is never shared with the application; only public verification information is distributed.

- Claims and attributes: The configuration determines which user information the IdP sends to the application, such as a user identifier, email address, or group membership, depending on the protocol and setup. This helps the application receive the information it needs without receiving the user's password.

# What Happens When a Signing Certificate Expires?

If the IdP's signing certificate expires and nobody plans for it, applications that rely on that certificate may no longer be able to validate new authentication responses or tokens. Users could be unable to sign in to multiple applications across the organization, potentially disrupting business operations and user productivity.

The problem occurs when applications no longer accept the signatures they receive, not because the user's password has changed. If the applications have not been configured with a valid replacement signing certificate or public key, authentication can fail until the trust configuration is updated.

This is why certificate expiration must be monitored and signing-key rotation planned in advance. Administrators should update the trust configuration, make sure applications can validate signatures with the new key, and test the change 
before the old certificate expires.



# What Can Go Wrong When Trust Fails?

- ***Both SAML and OpenID Connect (OIDC)*** issue bearer credentials, meaning whoever possesses a valid token may be able to use it. The application does not automatically know whether the person presenting the token is the person it was originally issued to. If a token is stolen, an attacker may be able to use it until it expires or is otherwise invalidated.

- ***TLS protects communication:*** Every connection between the browser, application, and Identity Provider (IdP) must use HTTPS/TLS to protect sensitive information in transit. Without it, a malicious actor may be able to intercept or modify authentication messages, authorization codes, or tokens. TLS helps protect the communication channel, while signatures provide a separate way to verify the authenticity and integrity of authentication information.

- ***Tokens should be short-lived:*** Tokens should expire after a limited time to reduce the window in which a stolen token can be used. A permanent token would give an attacker much longer to exploit it. Short expiration times reduce risk but do not prevent token theft.

- ***Applications must validate the intended audience:*** A token or assertion issued for one application should not be accepted by another. If an application skips the audience check, an attacker may be able to present a valid token intended for a different application and gain unauthorized access.

- ***Signatures must be validated:*** The application must verify the token or assertion's signature using the trusted IdP's public key. Without signature validation, an attacker could create a fake token containing claims such as a victim's identity and attempt to impersonate that user. The application must also validate other required fields, including the issuer and expiration.

- ***MFA has limits:*** Multifactor authentication makes it harder for an attacker to complete the initial authentication using only a stolen password. However, MFA does not automatically protect a token after it has been issued. If an attacker steals a usable token, they may be able to reuse it without completing MFA again.
