# GCP Secret To File Buildkite Plugin

This repository is inspired by [avaly/gcp-secret-manager-buildkite-plugin](https://github.com/avaly/gcp-secret-manager-buildkite-plugin).

Other preinstalled requirements:

- [`gcloud`](https://cloud.google.com/sdk/)
- [`jq`](https://stedolan.github.io/jq/)

## Example

Add the following to your `pipeline.yml`:

```yml
steps:
  - command: 'echo \$SECRET_VAR'
    plugins:
      - thilinaperera/gcp-secret-to-file#v1.0.0:
          credentials_file: /etc/gcloud-credentials.json
          env:
            FILE_NAME: ".servicerc"
            SECRET_NAME: secret-name
```

## Configuration

### `credentials_file` (Required, string)

The file path of a Google Cloud credentials file, which is used to access the secrets. The account of the credentials file needs to have the Secret Manager Secret Accessor role (`roles/secretmanager.secretAccessor`).

### `env` (object)

An object defining the export file name and the secret name which will populate the data.

## Developing

To run the tests:

```shell
docker-compose run --rm shellcheck
docker-compose run --rm tests
```