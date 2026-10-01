# The assertion says which application it is for. What would happen if an application accepted an assertion that named a different application?

***If an application accepted an assertion intended for a different application, it could incorrectly authenticate the user. An attacker could potentially take a valid assertion issued for one application and reuse it against another application that fails to check the Audience, gaining access as that user.***

