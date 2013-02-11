mongodb-server
============

Blueprint to deploy mongodb on a Cloud Server.

## Quick Start

Use the `pawn` command-line tool to fetch the mongodb-server blueprint and deploy it using https://checkmate.rackspace.com.

    pawn clone mongodb-server
    pawn use credentials --username myusername --apikey ABC123
    pawn deploy

## Manual Deployment using Checkmate API

These instructions assume you are running Checkmate with Vagrant using the following resources:

* [https://github.rackspace.com/checkmate/checkmate](https://github.rackspace.com/checkmate/checkmate)
* [https://github.rackspace.com/checkmate/checkmate/blob/master/vagrant/README.md](https://github.rackspace.com/checkmate/checkmate/blob/master/vagrant/README.md)

In addition, it is highly recommend that you use [HTTPie](https://github.com/jkbr/) instead of cURL for issuing API requests. This document assumes its usage.

### Fetch an Auth Token

Obtain an Auth token for your account to auth with Checkmate:

```bash
$ echo '{"auth": {"RAX-KSKEY:apiKeyCredentials": {"username": "<username>", "apiKey":"<apiKey>"}}}'|http POST https://identity.api.rackspacecloud.com/v2.0/tokens content-type:application/json accept:application/json 
```

### Deploy Blueprint

POST the deployment to /\<tenantId>/deployments to run the deployment:

```bash
$ http POST http://localhost:8080/<tenantId>/deployments X-Auth-Token:<authToken> accept:application/json content-type:application/x-yaml @mongodb-server.yaml
```

Once the deployment finishes, you will have a working mongodb Server install. 
