# Send A Hug

## Version

Version 1 (currently in development).

## Desciption

People suffering from depression and other mental illnesses often feel like nobody sees or cares about them. This often creates a vicious cycle, in which the people fighting depression pull away from those they love (as they don't want to be a burden, or they feel like they're already invisible), which makes it difficult for people to see they're struggling, and that only 'confirms' to those suffering that they're invisible. That cycle is difficult to break out of.

That's why I've started developing this app. As someone who's intimately familiar with depression and its destructive power, I know how difficult it can be to convince oneself that people do care about you. I also know how much even the tiniest bit of kindness means when you're struggling. Even a virtual hug or a 'you are not alone' message can be the things to give you strength for a day, or convince you to try to reach out again. Every little gesture can be the difference between life and death.

So this is the idea of this project. If a person is struggling, if they need to let something off their chest, all they need to do is write it. The app allows users to send virtual hugs, as well as support messages (messages are not encrypted, but they can only be viewed by the users). The suggested posts are sorted by the number of hugs, which means posts with fewer hugs are pushed higher up the list. This helps ensuring that as many users as possible will have at least one person showing them they care and they're not alone.

## Requirements

- Node.js (Frontend)

- Python 3 (Backend)

## Installation and Usage

- Backend installation and usage instructions - [`Backend README`](https://github.com/sendahug/send-hug-backend/blob/Dev/README.md)
- Frontend installation and usage instructions - [`Frontend README`](https://github.com/sendahug/send-hug-frontend/blob/Dev/README.md)

## Authentication

The project uses Auth0 as a third-party authentication provider. Authentication is done by Auth0, which in turn returns a JSON Web Token containing the user's data and permissions.

The backend handles decoding and verifying the given token, as well as checking the authenticated user's permissions. For full information about the backend authentication checks, read the [`backend README`](https://github.com/sendahug/send-hug-backend/blob/Dev/README.md).

The frontend also decodes the token in order to get the user's permissions and Auth0 ID (the JWT payload 'sub'), but doesn't verify that the token is authentic. This is done by the backend upon fetching the user's data from the database. For full information about the frontend authentication process, read the [`frontend README`](https://github.com/sendahug/send-hug-frontend/blob/Dev/README.md).

This project uses Role-based Authentication. There are currently three roles defined in the app:

  - User
  - Moderator
  - Admin

### User

The base role. Given to each user upon registration using an Auth0 rule. Includes the following permissions:

  - read:user - Read their own user data.
  - read:messages - Read messages sent to them.
  - post:post - Create a new post.
  - post:message - Create a new message.
  - post:report - Create a new report.
  - patch:user - Update their own user data.
  - patch:my-post - Update their own post.
  - delete:my-post - Delete their own post.
  - delete:messages - Delete a message sent them.

### Moderator

This role is meant for app moderating, in order to ensure posts' texts are appropriate. Includes the following permissions:

  - read:user - Read their own user data.
  - read:messages - Read messages sent to them.
  - post:post - Create a new post.
  - post:message - Create a new message.
  - post:report - Create a new report.
  - patch:user - Update their own user data.
  - patch:any-post - Update any user's post.
  - delete:my-post - Delete their own post.
  - delete:messages - Delete a message sent them.

### Admin

This role is meant for app admins and thus contains full access to the app. App admins can edit and delete any post (if necessary). Includes the following permissions:

  - read:user - Read their own user data.
  - read:messages - Read messages sent to them.
  - post:post - Create a new post.
  - post:message - Create a new message.
  - post:report - Create a new report.
  - patch:any-user - Update any user's data.
  - patch:any-post - Update any user's post.
  - delete:any-post - Delete any user's post.
  - delete:messages - Delete a message sent them.
  - read:admin-board - Use the admin dashboard.

### Auth0 Configuration

The default Auth0 configuration (meaning, the domain, audience, client ID, etc) can be altered to reflect your own Auth0 account. Auth0 configuration variables are stated in four places:

1. [`./backend/auth.py`](https://github.com/sendahug/send-hug-backend/blob/master/auth.py) - Contains the backend's authentication logic, as well as the Auth0 domain and the audience (both coming from an environment variable), and the used algorithm. These three variables can be found at the top of the file (lines 8-10).
2. [`./backend/setup.sh`](https://github.com/sendahug/send-hug-backend/blob/master/setup.sh) - Contains setup variables, which include: the database URL, the Auth0 domain, the audience, the used algorithm and the client ID.
3. [`frontend environment config`](https://github.com/sendahug/send-hug-frontend/blob/Dev/src/environments/environment.ts) - Contains the development environment configuration required by Angular. Within that JSON configuration is the Auth0 variable, containing: the Auth0 domain, the app's client ID, the audience, the URL to which the user is redirected after login, and the URL to which the user is redirected after logging out.
4. [`frontend production environment config`](https://github.com/sendahug/send-hug-frontend/blob/Dev/src/environments/environment.prod.ts) - Contains the production environment configuration required by Angular. Within that JSON configuration is the Auth0 variable, containing: the Auth0 domain, the app's client ID, the audience, the URL to which the user is redirected after login, and the URL to which the user is redirected after logging out.

## Hosting

- Backend hosting instructions - [`./backend/`](https://github.com/sendahug/send-hug-backend/blob/Dev/README.md#hosting)
- Frontend hosting instructions - [`./frontend/`](https://github.com/sendahug/send-hug-frontend/blob/Dev/README.md#hosting)

## Live Version

A live version of the app is hosted on Heroku.

- The backend: [Backend live version](https://send-hug-server.herokuapp.com/).
- The frontend: [Frontend live version](https://send-hug.herokuapp.com/).

**Note: The frontend live version is not yet ready for users!**

## Known Issues

There are no current issues at the time.
