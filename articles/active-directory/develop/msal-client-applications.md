---
title: Public and confidential client apps (MSAL) | Azure
titleSuffix: Microsoft identity platform
description: Learn about public client and confidential client applications in the Microsoft Authentication Library (MSAL).
services: active-directory
author: mmacy
manager: CelesteDG

ms.service: active-directory
ms.subservice: develop
ms.topic: conceptual
ms.workload: identity
ms.date: 10/26/2021
ms.author: marsma
ms.reviewer: saeeda
ms.custom: aaddev, has-adal-ref
#Customer intent: As an application developer, I want to learn about the types of client apps so I can decide if this platform meets my app development requirements.
---

# Public client and confidential client applications

The Microsoft Authentication Library (MSAL) defines two types of clients: public clients and confidential clients. The two client types are distinguished by their ability to authenticate securely with the authorization server and maintain the confidentiality of their client credentials. In contrast, Azure Active Directory Authentication Library (ADAL) uses what's called _authentication context_ (which is a connection to Azure Active Directory).

- **Confidential client applications** are apps that run on servers (web apps, web API apps, or even service/daemon apps). They're considered difficult to access, and for that reason can keep an application secret. Confidential clients can hold configuration-time secrets. Each instance of the client has a distinct configuration (including client ID and client secret). These values are difficult for end users to extract. A web app is the most common confidential client. The client ID is exposed through the web browser, but the secret is passed only in the back channel and never directly exposed.

  Confidential client apps: 

  ![Web app](media/msal-client-applications/web-app.png) ![Web API](media/msal-client-applications/web-api.png) ![Daemon/service](media/msal-client-applications/daemon-service.png)

- **Public client applications** are apps that run on devices or desktop computers or in a web browser. They're not trusted to safely keep application secrets, so they only access web APIs on behalf of the user. (They support only public client flows.) Public clients can't hold configuration-time secrets, so they don't have client secrets.

  Public client apps: 

  ![Desktop app](media/msal-client-applications/desktop-app.png) ![Browserless API](media/msal-client-applications/browserless-app.png) ![Mobile app](media/msal-client-applications/mobile-app.png)

In MSAL.js, there's no separation of public and confidential client apps. MSAL.js represents client apps as user agent-based apps, public clients in which the client code is executed in a user agent like a web browser. These clients don't store secrets because the browser context is openly accessible.

## Comparing the client types

Here are some similarities and differences between public and confidential client apps:

- Both kinds of app maintain a user token cache and can acquire a token silently (when the token is already in the token cache). Confidential client apps also have an app token cache for tokens that are for the app itself.
- Both types of app manage user accounts and can get an account from the user token cache, get an account from its identifier, or remove an account.
- Public client apps have four ways to acquire a token (four authentication flows). Confidential client apps have three ways to acquire a token (and one way to compute the URL of the identity provider authorize endpoint). For more information, see [Acquiring tokens](msal-acquire-cache-tokens.md).

In MSAL, the client ID (also called the _application ID_ or _app ID_) is passed once at the construction of the application. It doesn't need to be passed again when the app acquires a token. This is true for both public and confidential client apps. Constructors of confidential client apps are also passed client credentials: the secret they share with the identity provider.

## Next steps

For more information about application configuration and instantiating, see:

- [Client application configuration options](msal-client-application-configuration.md)
- [Instantiating client applications by using MSAL.NET](msal-net-initializing-client-applications.md)
- [Instantiating client applications by using MSAL.js](msal-js-initializing-client-applications.md)
