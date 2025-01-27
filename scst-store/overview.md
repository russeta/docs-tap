# Supply Chain Security Tools for Tanzu – Store

Supply Chain Security Tools - Store saves software bills of materials (SBoMs) to a database and allows you to query for image, source, package, and vulnerability relationships.  It integrates with [Supply Chain Security Tools - Scan](../scst-scan/overview.md) to automatically store the resulting source and image vulnerability reports. It accepts any CycloneDX input and outputs in both human-readable and machine-readable formats, including JSON, text, and CycloneDX.


The following is a four-minute demo of scanning an image for CVEs and querying the database for CVEs and dependencies.

<iframe width="480" height="270"
src="https://www.youtube.com/embed/UoWSsJBjFgc"
frameborder="0" allow="autoplay; encrypted-media" allowfullscreen
alt="A demonstration of the features. First ingesting a bill of materials file. Then investigating vulnerabilities of different images."></iframe>

Supply Chain Security Tools - Store has three components:

* [API details](api.md)
* [CLI installation](cli_installation.md) (Insight)
* Postgres database

## Install

Supply Chain Security Tools - Store is released as an individual Tanzu Application Platform component.

To install, see [Install Supply Chain Security Tools - Store](../install-components.md#install-scst-store).  It will install the Postgres database and an [API](api.md) backend.

> **Note:** The Insight CLI requires a [separate installation](cli_installation.md).

For more information, see [Deployment Details and Configuration](deployment_details.md).

## <a id='usage'></a>Querying the database

### <a id='required-set-up'></a>Set up

The following steps are required to use the API or CLI:

* [Creating service accounts and access tokens](create_service_account_access_token.md)
* [Using encryption to connect to the database](using_encryption_and_connection.md)

The Insight CLI is the recommended means to query the database.

> **Note:** The Insight CLI is in beta and is separate from the Tanzu CLI. It still works with the final 1.0.0 version of Supply Chain Security Tools - Store.

* [CLI installation](cli_installation.md)
* [CLI configuration](cli_configuration.md)
* [CLI details](cli_docs/insight.md)

### Adding & querying data

See [Add data](add_data.md) to post CycloneDX scan reports to the Supply Chain Security Tools - Store.

See [Query data](query_data.md) to understand vulnerability, image, and dependency relationships.

## Auditing

The API server outputs logs when an endpoint is accessed, which can be used for auditing purposes. For information about the logs generated, see [Log configuration and usage](logs.md).

## Known issues

See [Troubleshooting and Known Issues](known_issues.md).

## Security

See [Security](security.md).
