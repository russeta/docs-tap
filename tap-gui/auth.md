## Setting up a Tanzu Application Platform GUI authentication provider

<<<<<<< Updated upstream
Tanzu Application Platform GUI extends the current [Backstage's auth plug-in](https://backstage.io/docs/auth/) so that you can see a login page based on the authentication providers configured at install time. This feature is a work in progress, and, at the moment, should support the following authentication providers out-of-the-box:
=======
The Tanzu Application Platform GUI extends the current [Backstage's auth plug-in](https://backstage.io/docs/auth/) so that you can see a login page based on the authentication providers configured at install time. This feature is a work in progress, and, at the moment, should support the following auth providers out-of-the-box:
>>>>>>> Stashed changes

- [Auth0](https://backstage.io/docs/auth/auth0/provider)
- [Azure](https://backstage.io/docs/auth/microsoft/provider)
- [Bitbucket](https://backstage.io/docs/auth/bitbucket/provider)
- [GitHub](https://backstage.io/docs/auth/github/provider)
- [GitLab](https://backstage.io/docs/auth/gitlab/provider)
- [Google](https://backstage.io/docs/auth/google/provider)
- [Okta](https://backstage.io/docs/auth/okta/provider)
- [OneLogin](https://backstage.io/docs/auth/onelogin/provider)

Follow the [Backstage auth docs](https://backstage.io/docs/auth/) to configure a supported authentication provider.

We also support a custom OIDC provider shown here:

- Edit your tap-gui-values.yaml or your custom configuration file to include an OIDC authentication provider. Configure the OIDC authentication provider with your OAuth App values. Example:

    ```
    auth:
      environment: development
      session:
        secret: custom session secret
      providers:
        oidc:
          development:
            metadataUrl: ${AUTH_OIDC_METADATA_URL}
            clientId: ${AUTH_OIDC_CLIENT_ID}
            clientSecret: ${AUTH_OIDC_CLIENT_SECRET}
            tokenSignedResponseAlg: ${AUTH_OIDC_TOKEN_SIGNED_RESPONSE_ALG} # default='RS256'
            scope: ${AUTH_OIDC_SCOPE} # default='openid profile email'
            prompt: auto # default=none (allowed values: auto, none, consent, login)
    ```

    `metadataUrl` is a JSON file with generic OIDC provider config. It contains the `authorizationUrl` and `tokenUrl`. The Tanzu Application Platform GUI reads these values from the `metadataUrl` file, and you do not need to specify them explicitly in your authorization configuration.
    
    For more information, check out [this example](https://github.com/backstage/backstage/blob/e4ab91cf571277c636e3e112cd82069cdd6fca1f/app-config.yaml#L333-L347).

### Allowing guest access

If you want to enable guest access along other providers, you do this by providing the following flag under your authentication configuration:

  ```
  auth:
    allowGuestAccess: true
  ```

## Customizing the Login page

You can change the card's title and/or description for a specific provider with the following authentication configuration:

  ```
  auth:
    environment: development
    providers:
      ... # auth providers config
    loginPage:
      github:
        title: Github Login
        message: Enter with your GitHub account
  ```

To show an authentication provider in the login page, you must keep properly configure it under the `auth.providers` section of your values file.
