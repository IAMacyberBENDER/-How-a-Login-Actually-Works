#  Identity and Federation Vocabulary

***Identity Provider (IdP)***

- The identity provider is the system that verifies who you are and handles your login credentials. It then tells another application that you have been authenticated.

***Service Provider (SP) / Relying Party (RP)***

- The service provider is the application you are trying to access. It trusts the identity provider to verify your identity instead of checking your password itself.

***Token***

- A token is a package of information issued by the identity provider after authentication. The application uses the token to determine who you are and what information or access applies to you.

***Claim***

- A claim is an individual piece of information about the authenticated user contained in a token or assertion. For example, your email address, department, or the fact that you completed multifactor authentication can be a claim.

***Assertion***

- An assertion is SAML's term for a signed package of information about a user. The identity provider sends the assertion to the application so the application can verify who the user is.

***Federation***

- Federation is an arrangement where two systems agree to trust each other's identity information. This allows one system to authenticate the user while another system accepts that authentication without needing the user's password.
