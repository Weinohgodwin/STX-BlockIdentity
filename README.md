### STX-BlockIdentity : Decentralized Social Login Contract

This decentralized social login contract enables users to register, manage their profiles, and interact with the system while ensuring various validation checks for usernames, emails, and profile images. The contract is designed for use with blockchain platforms that support Clarity, such as Stacks.

#### Table of Contents
- [Contract Overview](#contract-overview)
- [Error Messages](#error-messages)
- [Data Structures](#data-structures)
- [Functions](#functions)
  - [Register User](#register-user)
  - [Update Profile](#update-profile)
  - [Set Profile Image](#set-profile-image)
  - [Clear Profile Image](#clear-profile-image)
  - [Delete Profile](#delete-profile)
  - [Get User Information](#get-user-information)
  - [Get User Count](#get-user-count)
  - [Check User Registration](#check-user-registration)
  - [Is Username Available](#is-username-available)
  - [Check Username Match](#check-username-match)
- [Contract Operations](#contract-operations)
  - [User Registration](#user-registration)
  - [Profile Update](#profile-update)
  - [Profile Management](#profile-management)
- [Error Handling](#error-handling)
- [Future Enhancements](#future-enhancements)

---

### Contract Overview
This contract provides functionality for user registration, profile management, and username validation. It allows users to set and clear their profile image, update their username and email, and delete their profile. Additionally, it ensures that usernames are unique, emails are valid, and that users can be validated before changes are made.

### Error Messages
The contract uses the following error messages to ensure the integrity of operations:
- `ERR-USER-EXISTS`: Raised when a user attempts to register again with an existing account.
- `ERR-USER-NOT-FOUND`: Raised when an operation references a non-existing user.
- `ERR-INVALID-USERNAME`: Raised when a username doesn't meet the required character length (between 3 and 50 characters).
- `ERR-INVALID-EMAIL`: Raised when the email does not meet the required length (between 5 and 100 characters) and is missing an "@" or "." character.
- `ERR-INVALID-IMAGE-URL`: Raised when the provided image URL is invalid.
- `ERR-USERNAME-TAKEN`: Raised when a username is already in use by another user.

### Data Structures
1. **Users Map**: Stores user data indexed by `principal`.
   - `username`: User's chosen username (up to 50 characters).
   - `email`: User's email address (up to 100 characters).
   - `profile-image`: An optional profile image URL (up to 256 characters).

2. **Taken Usernames Map**: Stores usernames already taken by registered users.

3. **User Count Variable**: Tracks the total number of registered users.

### Functions

#### Register User
- **register-user**: Registers a new user by providing a username and email.
  - Validates the username, email, and checks if the user already exists.
  - Checks if the username is unique before registration.
  - Increments the user count and stores the user's data.

#### Update Profile
- **update-profile**: Allows users to update their username and email.
  - Validates the new username and email.
  - Ensures the new username is unique and updates the taken username map accordingly.
  - Modifies the user's profile with the new username and email.

#### Set Profile Image
- **set-profile-image**: Allows users to set a profile image.
  - Ensures the provided image URL is valid and updates the user's profile with the new image.

#### Clear Profile Image
- **clear-profile-image**: Clears the user's profile image.
  - Updates the user's profile to remove the profile image.

#### Delete Profile
- **delete-profile**: Allows users to delete their profile.
  - Removes the user from the `users` map and decrements the user count.
  - Deletes the user's taken username from the `taken-usernames` map.

#### Get User Information
- **get-user-info**: A read-only function to fetch a user's information based on their principal address.

#### Get User Count
- **get-user-count**: A read-only function to retrieve the total number of registered users.

#### Check User Registration
- **is-user-registered**: Checks if a user is registered by verifying their existence in the `users` map.

#### Is Username Available
- **is-username-available**: Checks if a username is available by ensuring it meets the required validation and is not already taken.

#### Check Username Match
- **check-username-match**: Verifies if the provided username matches the one stored in the user's profile.

---

### Contract Operations

#### User Registration
1. A user must call `register-user` with a valid username and email.
2. If the username and email pass validation checks, the user is successfully registered, and their profile is created.
3. The system prevents duplicate registrations and ensures usernames are unique.

#### Profile Update
1. To update their profile, users call `update-profile` with a new username and email.
2. The contract checks that the username is unique before allowing the update.
3. The user's old username is removed from the taken list, and the new one is added.

#### Profile Management
1. Users can set or clear their profile image using the `set-profile-image` and `clear-profile-image` functions.
2. If a user wishes to delete their profile, they can use the `delete-profile` function, which removes all associated data.

---

### Error Handling
The contract uses assertions to validate input and ensure consistency. The main error cases include:
- Duplicate user registration (`ERR-USER-EXISTS`).
- Invalid username or email format.
- Trying to set an image with an invalid URL.
- Attempting operations on non-existing users.

These errors ensure that only valid operations are executed and that the system remains in a consistent state.

---

### Future Enhancements
- **Password Recovery**: Implement functionality for password recovery and authentication.
- **Social Media Integration**: Allow users to link their social media accounts for login and profile management.
- **Security Enhancements**: Add encryption and other security features to protect user data.

---
