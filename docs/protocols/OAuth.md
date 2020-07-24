# OAuth 2.0

OAuth 2.0 is a security standard where you give one application permission to access your data in another application. The steps to grant permission, or **consent**, are often referred to as **authorization** or even **delegated authorization**. You authorize one application to access your data, or use features in another application on your behalf, without giving them your password.

If **Authorization Server** supports [Open ID Connect](/protocols/OpenID) it is sometimes called "Identity Provider".

There are scenarions when Authorization Server allows

## Terminolagy

- **Resource Owner**: person who owns data (i.e. web-app user who has google acoount with data)
- **Client**: Application which gets access to user's data (i.e. webapp which user is using)
- **Authorization Server**: System which user can use to agree to grant access to **Client** (i.e. iframe with google account)
- **Resource Server**: System which stores user's data
- **Authorization grant**: It is a thing that proves that user agreed to give data to **Client**
- **Redirect URI**
- **Authorization Code**: It is given after **Consent** and can be exchanged by client to get **Access Token**. Exchange happens with **Back Channel** and requires secret key only backend knows
- **Access Token**: it is a way for a **Client** to get data from **Resource Server**
- **Scope**: **Authorization Server** has list of scopes which permissions can be granted
- **Consent**: screen which **Authorization Server** shows to ask for consent. It consists of scopes which have been required by **Client**
- **Back Channel**: highly secure channel
- **Front Channel**: less secure channel

## Flow

---

# References

- [OAuth 2.0 Habr](https://habr.com/ru/company/mailru/blog/115163/)
- [OAuth & Open ID explanation](https://speakerdeck.com/nbarbettini/oauth-and-openid-connect-in-plain-english)
- [OUath 2.0 Autho0](https://auth0.com/docs/protocols/oauth2)
- [Okta Blog](https://developer.okta.com/blog/2019/10/21/illustrated-guide-to-oauth-and-oidc)
