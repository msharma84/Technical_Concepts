# OAUTH 2.0 and OpenID Connect

OpenID Connect - a protocol built on top of OAuth 2.0 to enable using the same identity for authentication across multiple applications.

There are several key actors in the OAuth protocol flows:
* Resource owner : Typically the user of an application, the resource owner has the ability to grant access to their own data hosted on the resource server.
* Device (Agent) : Generally you interacting device through which you connect to Resource server.
* Application : On which app/application you required permission. An application making API requests to perform actions on protected resources on behalf of the resource owner and with its authorization.
* Authorization server : The authorization server gets consent from the resource owner and issues access tokens to clients for accessing protected resources hosted by a resource server. Smaller API providers may use the same application and URL space for both the authorization server and resource server.
* Resource server : The server hosting user-owned resources that are protected by OAuth. This is typically an API provider that holds and protects data such as photos, videos, calendars, or contacts.

![oauth1](https://github.com/msharma84/Technical_Concepts/assets/19761136/4ea4cd2b-beea-4cb9-b1fa-2d311265cd6b)
