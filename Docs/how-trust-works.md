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

This is why certificate expiration must be monitored and signing-key rotation planned in advance. Administrators should update the trust configuration, make sure applications can validate signatures with the new key, and test the change before the old certificate expires.

