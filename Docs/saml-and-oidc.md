***The assertion says which application it is for. What would happen if an application accepted an assertion that named a different application?***

- If an application accepted an assertion intended for a different application, it could incorrectly authenticate the user. An attacker could potentially take a valid assertion issued for one application and reuse it against another application that fails to check the Audience, gaining access as that user.***


***The assertion is valid for a limited window, on the order of an hour. Why not forever?***

- Because a SAML assertion is a temporary proof of authentication, not a permanent credential. If it were valid forever, someone who obtained a copy of the assertion could potentially reuse it indefinitely. By giving it a limited validity window, the risk is reduced because the assertion eventually expires and can no longer be used.

