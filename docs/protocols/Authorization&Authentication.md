# Authentication and Authorization

| Authentication                                                           | Authorization                                                                                |
| ------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------- |
| Authentication confirms your identity to grant access to the system.     | Authorization determines whether you are authorized to access the resources.                 |
| It is the process of validating user credentials to gain user access.    | It is the process of verifying whether access is allowed or not.                             |
| It determines whether user is what he claims to be.                      | It determines what user can and cannot access.                                               |
| Authentication usually requires a username and a password.               | Authentication factors required for authorization may vary, depending on the security level. |
| Authentication is the first step of authorization so always comes first. | Authorization is done after successful authentication.                                       |

> Example: Employees in a company are required to authenticate through the network before accessing their company email Example: After an employee successfully authenticates, the system determines what information the employees are allowed to access

## Authentication

Authentication is about validating your credentials such as Username/User ID and password to verify your identity. The system then checks whether you are what you say you are using your credentials. Whether in public or private networks, the system authenticates the user identity through login passwords. Usually authentication is done by a username and password, although there are other various ways to be authenticated.

- **Single-Factor Authentication**: This is the simplest form of authentication method which requires a password to grant user access to a particular system such as a website or a network. The person can request access to the system using only one of the credentials to verify one’s identity. For example, only requiring a password against a username would be a way to verify a login credential using single-factor authentication.

- **Two-Factor Authentication**: This authentication requires a two-step verification process which not only requires a username and password, but also a piece of information only the user knows. Using a username and password along with a confidential information makes it that much harder for hackers to steal valuable and personal data.

- **Multi-Factor Authentication**: This is the most advanced method of authentication which requires two or more levels of security from independent categories of authentication to grant user access to the system. This form of authentication utilizes factors that are independent of each other in order to eliminate any data exposure. It is common for financial organizations, banks, and law enforcement agencies to use multiple-factor authentication.

## Authorization

Authorization, on the other hand, occurs after your identity is successfully authenticated by the system, which ultimately gives you full permission to access the resources such as information, files, databases, funds, locations, almost anything. In simple terms, authorization determines your ability to access the system and up to what extent. Once your identity is verified by the system after successful authentication, you are then authorized to access the resources of the system.

Authorization is the process to determine whether the authenticated user has access to the particular resources. It verifies your rights to grant you access to resources such as information, databases, files, etc. Authorization usually comes after authentication which confirms your privileges to perform. In simple terms, it’s like giving someone official permission to do something or anything.

## Identification

Identity - basic information about resource owner who is logged in which allows to establish a login session(profile data). For example, OIDC - gives basic information about user on authentication = ID Token = JSON Web Token (JWT).

JWT - data inside token is called "claims".

## OAuth

---

# References

- [Authentication](https://auth0.com/docs/application-auth/current)
- [Authorization](https://auth0.com/docs/authorization)
- [Authorization vs Authentication](https://auth0.com/docs/authorization/concepts/authz-and-authn)
- [Auth in Frontend Apps overview](https://www.telerik.com/blogs/authentication-in-frontend-applications)
- [Difference Between Authentication & Authorization](http://www.differencebetween.net/technology/difference-between-authentication-and-authorization/)
- [OAuth 2.0 overview by auth0](https://auth0.com/docs/protocols/oauth2)
- [how the open authorization framework works](https://www.csoonline.com/article/3216404/what-is-oauth-how-the-open-authorization-framework-works.html)
