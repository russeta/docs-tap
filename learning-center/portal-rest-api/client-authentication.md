# Client authentication

The training portal web interface is a quick way of providing access to a set of workshops when running a supervised training workshop. For integrating access to workshops into an existing website or for creating a custom web interface for accessing workshops hosted across one or more training portals, you can use can use the portal REST API.

The REST API gives you access to the list of workshops hosted by a training portal instance and allow you to request and access workshop sessions. This bypasses the training portal's own user registration and log in so you can implement whatever access controls you need. This could include anonymous access or access integrated into an organization's single sign-on system.

## Querying the credentials

To provide access to the REST API a robot account is automatically provisioned. The login credentials and details of the OAuth client endpoint used for authentication can be obtained by querying the resource definition for the training portal after it has been created and the deployment completed. If using ``kubectl describe``, you would use:

```
kubectl describe trainingportal.learningcenter.tanzu.vmware.com/<training-portal-name>
```

In the status section of the output you will see:

```
Status:
  learningcenter:
    Clients:
      Robot:
        Id:      ACZpcaLIT3qr725YWmXu8et9REl4HBg1
        Secret:  t5IfXbGZQThAKR43apoc9usOFVDv2BLE
    Credentials:
      Admin:
        Password:  0kGmMlYw46BZT2vCntyrRuFf1gQq5ohi
        Username:  learningcenter
      Robot:
        Password:  QrnY67ME9yGasNhq2OTbgWA4RzipUvo5
        Username:  robot@learningcenter
```

The admin login credentials are what you would use when you log into the training portal web interface to access admin pages.

The robot login credentials is what you would use if you wish to access the REST API.

## Requesting an access token

Before you can make requests against the REST API to query details on workshops or request a workshop session, you need to login via the REST API to get an access token.

This is done from any front end web application or provisioning system, but the step is equivalent to making a REST API call using ``curl`` of:

```
curl -v -X POST -H \
"Content-Type: application/x-www-form-urlencoded" \
-d "grant_type=password&username=robot@learningcenter&password=<robot-password>" \
-u "<robot-client-id>:<robot-client-secret>" \ 
<training-portal-url>/oauth2/token/
```

The URL sub path is ``/oauth2/token/``.

Upon success, the output will be a JSON response consisting of:

```
{
    "access_token": "tg31ied56fOo4axuhuZLHj5JpUYCEL",
    "expires_in": 36000,
    "token_type": "Bearer",
    "scope": "user:info",
    "refresh_token": "1ryXhXbNA9RsTRuCE8fDAyZToJmp30"
}
```

## Refreshing the access token

The access token which is provided will expire: it needs to be refreshed before it expires if in use by a long-running application.

To refresh the access token you would use the equivalent of:

```
curl -v -X POST -H \
"Content-Type: application/x-www-form-urlencoded" \
-d "grant_type=refresh_token&refresh_token=<refresh-token>& \client_id=<robot-client-id>&client_secret=<robot-client-secret>" \
https://lab-markdown-sample-ui.test/oauth2/token/
```

As with requesting the initial access token, the URL sub path is ``/oauth2/token/``.

The JSON response will be of the same format as if a new token had been requested.
