# Known Issues

## Persistent Volume Retains Data
If the Metadata Store is deployed, deleted and redeployed, the `metadata-store-db` pod may fail to start up if the database password changed during redeployment. This is due to
the persistent volume used by postgres retaining old data, even though the retention policy is set to `DELETE`.

In the meantime, to prevent this issue, if the app needs to be redeployed, either use the same database password, or follow these steps to erase the data on the volume:
1. deploy metadata-store app (via kapp)
2. watch the `metadata-store-db-*` pod fail
3. `kubectl exec -it metadata-store-db-<some id> -n metadata-store /bin/bash`
4. `rm -rf /var/lib/postgresql/data/*` (path found in postgres-db-deployment.yaml) - This should delete all database data
5. delete the metadata-store app via kapp
6. deploy metadata-store app (via kapp)

where:
* `some id`: is the id generated by k8s that is appended to the pod name

## Querying local path source reports
If a source report has a local path as the name (ex: `/path/to/code`), the leading `/` on the resulting repository name will cause the querying (packages & vulnerabilities) to return an error from the client lib and the CLI. The error message is `{ "message": "Not found" }`.

The URL of the resulting HTTP request is properly escaped (ex: `/api/sources/%2Fpath%2Fto%2Fdir/vulnerabilities`), but the rbac-proxy used for authentication, handles this URL in a way that the response is a redirect (ex: `HTTP 301\nLocation: /api/sources/path/to/dir/vulnerabilities`). The Client Lib follows the redirect, making a request to the new URL which does not exist in the Metadata Store API, thus resulting in the mentioned error message.

## No support for installing in custom namespaces
All of our testing uses the `metadata-store` namespace. Using a different namespace could break authentication and certificate validation for the metadata-store api.

# Deploying for Internal/External customers

Using `imgpkg copy` command copies the image bundle along with all images it references to a target repository. This is very useful as it ensures the images used in the bundle are always
available, even if the images in where they originally came from are no longer available (since there is now a copy in the target repo.)

To deploy the bundle, run the following command:

`imgpkg copy -b <bundle image registry>:<bundle version tag> --to-repo <target image registry repo>/`

where:
* `bundle image registry` is the registry where the image bundle currently will be copied from
* `bundle version tag` is the image bundle version tag to copy
* `target image registry repo` is where the image bundle and all associated images will be copied to