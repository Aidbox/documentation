# Optional environment variables

### Optional environment variables

#### AIDBOX\_BASE\_URL

```
AIDBOX_BASE_URL=<url>
```

URL to use in links between resources.

Default is

```
http://localhost:[AIDBOX_PORT]
```

#### AIDBOX\_DB\_PARAM\_\*

```
AIDBOX_DB_PARAM_<parameter name>=<parameter value>
```

Parameters prefixed with `AIDBOX_DB_PARAM_` will be passed to [JDBC PostgreSQL connection string](https://jdbc.postgresql.org/documentation/80/connect.html).

#### AIDBOX\_ES\_URL

If provided, enables mode to push logs to ElasticSearch



| Env variable name                                                    | Meaning                                                                                                                                                                                                                                                    |
| -------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `AIDBOX_ES_AUTH`                                                     | Basic auth credentials for ElasticSearch in `user:password` format                                                                                                                                                                                         |
| `AIDBOX_ES_BATCH_SIZE`                                               | Log batch size used to optimize log shipping performance. The default value is 200                                                                                                                                                                         |
| `AIDBOX_ES_BATCH_TIMEOUT`                                            | Timeout to post a batch to ElasticSearch. If there is not enough records to reach full batch size                                                                                                                                                          |
| `AIDBOX_ES_INDEX_PAT`                                                | Custom index format string. The default value is 'aidbox-logs'-yyyy-MM-dd.                                                                                                                                                                                 |
| `AIDBOX_LOGS`                                                        | If provided, enables mode to pipe logs as json into the file by specified path. If ElasticSearch URL is provided then the file is used as a fallback in case if ElasticSearch is not available                                                             |
| `AIDBOX_LOGS_MAX_LINES`                                              | Sets the limit of log records to push into the file. When the limit is reached, the current log file is renamed with ".old" postfix and a new log file is created. The default value is "10000"                                                            |
| `AIDBOX_STDOUT_JSON`                                                 | If provided, enables mode to write logs as json into stdout                                                                                                                                                                                                |
| `AIDBOX_STDOUT_PRETTY`                                               | If provided, enables mode to write logs in prettified format into stdout                                                                                                                                                                                   |
| `AIDBOX_DEVLOGS`                                                     | If provided, pushes logs into \_logs table of aidboxdb. Can be useful for testing and debugging                                                                                                                                                            |
| `AIDBOX_DD_API_KEY`                                                  | If provided, enables mode to push logs to DataDog                                                                                                                                                                                                          |
| `AIDBOX_DD_BATCH_SIZE`                                               | Size of log batch, used to optimize performance of log shipping. The default value is 200                                                                                                                                                                  |
| `AIDBOX_DD_BATCH_TIMEOUT`                                            | Timeout (in ms) to post a batch to DataDog if there are not enough records to reach full batch size. Default value: 3600000 (1 hour)                                                                                                                       |
| `AIDBOX_DD_LOGS`                                                     | Fallback file to write logs in if uploading to DataDog fails                                                                                                                                                                                               |
| `AIDBOX_CREATED_AT_URL`                                              | Overrides createdAt extension url, default is `ex:createdAt`                                                                                                                                                                                               |
| `AIDBOX_CORRECT_AIDBOX_FORMAT`                                       | <p>If provided, activates transforming unknown polymorphic extensions to the correct Aidbox format avoiding keeping them at FHIR-format.</p><p>For example,</p><p><code>extension.*.valueString</code> stored as <code>extension.0.value.string</code></p> |
| `AIDBOX_DEV_MODE`                                                    | Enables `_debug=policy` for [access policy debugging](https://docs.aidbox.app/security-and-access-control-1/security/access-policy#policy-debugging)                                                                                                       |
| `AIDBOX_ZEN_ENTRYPOINT`                                              | Specifies entry point for loading Aidbox configuration                                                                                                                                                                                                     |
| `AIDBOX_ZEN_PATHS`                                                   | Specifies how Aidbox loads project                                                                                                                                                                                                                         |
| `AIDBOX_EXTENSION_SCHEMA`                                            | Schema for PostgreSQL extensions. Default is current schema. See [use different PostgreSQL schema section](optional-environment-variables.md#use-different-postgresql-schema).                                                                             |
| `BOX_SEARCH_DEFAULT__PARAMS_COUNT`                                   | Overrides the default count search parameter value. 100 is the default value. The provided value should be <= 1000                                                                                                                                         |
| `BOX_COMPATIBILITY_VALIDATION_JSON__SCHEMA_REGEX="#{:fhir-datetime}` | Enables strict date time validation in JSON schema validation engine per [FHIR spec](https://www.hl7.org/fhir/datatypes.html#dateTime).                                                                                                                    |
| `BOX_COMPATIBILITY_AUTH_PKCE_CODE__CHALLENGE_S256_CONFORMANT`        | Use conformant S256 code challenge validation scheme.                                                                                                                                                                                                      |
| `BOX_DEBUG_SU_ENABLE`                                                | Enables `su` request header [functionalty](https://docs.aidbox.app/security-and-access-control-1/security/debug#su-request-header)                                                                                                                         |
| `BOX_FEATURES_VALIDATION_SKIP_REFERENCE`                             | Enables skip resource reference validation [functionality](../../../profiling-and-validation/profiling.md#aidbox-validation-skip-request-header)                                                                                                           |
| `BOX_WEB_MAX__BODY`                                                  | Maximum size of request body in bytes. Default is 8388608 (8 MiB).                                                                                                                                                                                         |
| `BOX_FEATURES_TERMINOLOGY_IMPORT_SYNC`                               | Enables synchronous terminology bundle import                                                                                                                                                                                                              |

### Enable Aidbox compliance mode

`AIDBOX_COMPLIANCE=enabled`:

\- Adds various attributes and endpoints info to CapabilityStatement

\- Adds CapabilityStatement sanitizing (i.e. removes attributes containing `null` values and empty arrays)

\- Adds AIDBOX\_BASE\_URL in `Bundle.link.url`

\- Adds FHIR date search parameter validation on `lastUpdated` search parameter

\- Adds "alg": "RS256" entry for JWKS

\- Changes validation error status to 422 (instead of 400)

\- Changes `cache-control` header to `no-store` on authorization code auth flow (instead of `no-cache, no-store, max-age=0, must-revalidate`)

\- Removes `Bundle.entry` if empty

### Configuring SSL connection with PostgreSQL

Parameters prefixed with AIDBOX\_DB\_PARAM is passed to JDBC PostgreSQL connection string.

For an instance:

`AIDBOX_DB_PARAM_SSL=true`\
`AIDBOX_DB_PARAM_SSLMODE=verify-ca`

will add `ssl=true&sslmode=verify-ca` params to connection string.

These parameters will enable SSL connection from Aidbox to postgresql Docs on JDBC PostgreSQL connection string are here: [https://jdbc.postgresql.org/documentation/80/connect.html](https://jdbc.postgresql.org/documentation/80/connect.html) [https://jdbc.postgresql.org/documentation/head/ssl-client.html](https://jdbc.postgresql.org/documentation/head/ssl-client.html)

The next step is to configure your database to accept SSL connections. You can do that by passing your own postgresql.conf with argument -c config\_file passed into the db containter and probably you want to set up postgres to receive only SSL connections, you can do that by passing your own pg\_hba.conf file with -c hba\_file

### Use different PostgreSQL schema

By default Aidbox uses `public` schema. If you want Aidbox to use different schema, set [JDBC parameter `currentSchema`](https://jdbc.postgresql.org/documentation/head/connect.html#connection-parameters) using environment variable `AIDBOX_DB_PARAM_CURRENT_SCHEMA`:

```
AIDBOX_DB_PARAM_CURRENT_SCHEMA=myschema
```

PostgreSQL extensions can create objects. By default PostgreSQL sets up extension to use current schema. If you are going to share database between multiple applications, we recommend to create a dedicated schema for the extensions.

Use `AIDBOX_EXTENSION_SCHEMA` environment variable to set up Aidbox to use dedicated extension schema:

```
AIDBOX_EXTENSION_SCHEMA=myextensionschema
```

Note: if your database already has extensions installed and you change extension schema (or current schema if extension schema is not configured), then you need to drop extensions from previous schema:

```
DROP EXTENSION IF EXISTS fuzzystrmatch
                       , jsonknife
                       , jsquery
                       , pg_stat_statements
                       , pg_trgm
                       , pgcrypto
                       , unaccent;
```

Then change `AIDBOX_EXTENSION_SCHEMA` and restart Aidbox.



### Set up RSA private/public keys and secret

Aidbox generates JWT tokens for different purposes:

* As part of Oauth 2.0 authorization it generates authorization\_code in JWT format
* If you specify auth token format as JWT, then your access\_token and refresh\_token will be in JWT format.

Aidbox supports two signing algorithms: RS256 and HS256. RS256 expects providing private key for signing JWT and public key for verifing it. As far as HS256 needs only having secret for both operations.

By default Aidbox generates both keypair and secret on every startup. This means that on every start all previously generated JWT will be invalid.

In order to avoid such undesirable situation, you may pass RSA keypair and secret as Aidbox parameters.

#### Generate RSA keypair

Generate private key with `openssl genrsa -out key.pem 2048` in your terminal. Private key will be saved in file `key.pem`. To generate public key run `openssl rsa -in key.pem -outform PEM -pubout -out public.pem`. You will find public key in `public.pem` file.

Use next env vars to pass RSA keypair:

```
BOX_AUTH_KEYS_PRIVATE=-----BEGIN RSA PRIVATE KEY-----\n...\n-----END RSA PRIVATE KEY-----
BOX_AUTH_KEYS_PUBLIC=-----BEGIN PUBLIC KEY-----\n...\n-----END PUBLIC KEY-----
```

#### Generate secret

To generate random string for HS256 algorith you can run `openssl rand -base64 36` command. The lenght of the random string must be more than 256 bits (32 bytes).

use next env var to pass secret param:

```
BOX_AUTH_KEYS_SECRET=<rand_string>
```