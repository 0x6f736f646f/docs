---
title: Security
---


## Server Configuration

### Users

If either the cert or key is not set, the server will use insecure transport.

`SMQ_USERS_SERVER_CERT` the path to server certificate in pem format.

`SMQ_USERS_SERVER_KEY` the path to the server key in pem format.

### Things

If either the cert or key is not set, the server will use insecure transport.

`SMQ_THINGS_SERVER_CERT` the path to server certificate in pem format.

`SMQ_THINGS_SERVER_KEY` the path to the server key in pem format.

### Standalone mode

Sometimes it makes sense to run Things as a standalone service to reduce network traffic or simplify deployment. This means that Things service operates only using a single user and is able to authorize it without gRPC communication with Auth service. When running Things in the standalone mode, `Auth` and `Users` services can be omitted from the deployment.
To run service in a standalone mode, set `SMQ_THINGS_STANDALONE_EMAIL` and `SMQ_THINGS_STANDALONE_TOKEN`.

## Client Configuration

If you wish to secure the gRPC connection to `Things` and `Users` services you must define the CAs that you trust. This does not support mutual certificate authentication.

### Adapter Configuration

`SMQ_HTTP_ADAPTER_CA_CERTS`, `SMQ_MQTT_ADAPTER_CA_CERTS`, `SMQ_WS_ADAPTER_CA_CERTS`, `SMQ_COAP_ADAPTER_CA_CERTS` - the path to a file that contains the CAs in PEM format. If not set, the default connection will be insecure. If it fails to read the file, the adapter will fail to start up.

### Things Configuration

`SMQ_THINGS_CA_CERTS` - the path to a file that contains the CAs in PEM format. If not set, the default connection will be insecure. If it fails to read the file, the service will fail to start up.

## Securing PostgreSQL Connections

By default, SuperMQ will connect to Postgres using insecure transport.
If a secured connection is required, you can select the SSL mode and set paths to any extra certificates and keys needed.

`SMQ_USERS_DB_SSL_MODE` the SSL connection mode for Users.
`SMQ_USERS_DB_SSL_CERT` the path to the certificate file for Users.
`SMQ_USERS_DB_SSL_KEY` the path to the key file for Users.
`SMQ_USERS_DB_SSL_ROOT_CERT` the path to the root certificate file for Users.

`SMQ_THINGS_DB_SSL_MODE` the SSL connection mode for Things.
`SMQ_THINGS_DB_SSL_CERT` the path to the certificate file for Things.
`SMQ_THINGS_DB_SSL_KEY` the path to the key file for Things.
`SMQ_THINGS_DB_SSL_ROOT_CERT` the path to the root certificate file for Things.

Supported database connection modes are: `disabled` (default), `required`, `verify-ca` and `verify-full`.

## Securing gRPC

By default gRPC communication is not secure as SuperMQ system is most often run in a private network behind the reverse proxy.

However, TLS can be activated and configured.
