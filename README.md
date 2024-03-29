# OAuth2

This is my journey on the OAuth2 Spec. I intend to follow Aaron Parecki's book called [OAuth2 Simplified](https://aaronparecki.com/oauth-2-simplified) which is an amazing book to help describe the terminology in a simplified format.

## Motivation

This GIT repo is my collection of notes as I have worked through the tutorials in this book. In my day job as an *Integration and API Specialist* we are currently designing our consumer facing APIs around the **OAuth2** and **OpenID** specification and this book has been instrumental in learning the OAuth2 spec.

## Resources

Some really useful resources can be found here;

[OAuth 2.0 and OpenID Connect (in plain English)
](https://youtu.be/996OiexHze0)

## OAuth 2.0 Clients

In part 1 of this book, we'll walk through the things you need to know when you're building an app that talks to an existing OAuth 2.0 API.

### Create an Application

Before we can begin, we'll need to create an *application* on GitHub in order to get a **client ID** and **client secret**.

The *client ID* is considered public information, and is used to build login URLs, or can be included in the Javascript source code of a web page. The *client secret* must be kept **confidential**. Don't commit this to your git repository!

The application will look similar to this:

[FileSafe:c8578613-72c0-4c6e-9e30-ff483eac4315:github-OAuth-application-settings am.png]

## Setting Up the Environment

We are going to build a simple PHP website with no external pacakges and no frameworks needed. 

From the command line, run `php -S localhost:8000` from inside that folder, and you'll be able to visit http://localhost:8000 in your browser to run your code. All the code is located in the [index.php](https://raw.githubusercontent.com/wvella/OAuth2-Simplified-Client/master/sample-app/index.php) file.

It's important to generate a "state" parameter to use to protect the client. This is a random string that the client generates and stores in the session. We use the state parameter as an extra security check so that when Github sends the user back here with the state in the query string, we can verify that we did actually initiate this request and it's not an attacker making that request.

We build up the authorization URL and then send the user [there](https://github.com/login/oauth/authorize). The URL contains our *public client ID*, the *redirect URL* which we previously registered with Github, the *scope* we're requesting, and the *state* parameter.

At this point, the user will see Github's OAuth authorization prompt.

When the user approves the request, they will be redirected back to our page with `code` and `state` parameters in the request. The next step is to exchange the *authorization code* for an *access token*.
