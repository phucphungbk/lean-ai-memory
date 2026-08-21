## Date 2026-08-22

- **File:** src/AuthService.cs | **Action:** Fixed JWT expiration validation | **Reason:** Prevent expired tokens from reaching application logic.

- **File:** tests/AuthServiceTests.cs | **Action:** Added regression test | **Reason:** Ensure the authentication fix remains protected.