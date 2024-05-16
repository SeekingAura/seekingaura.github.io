---
title: Cloudflared Local | Create Tunnel
permalink: /docs/dev_notes/cloudflared_local/create_tunnel/
toc: true
---
# Cloudflared Expose service from Port
Expose port via cloudflared tunnel is commonly used for projects that are in development or a cheap way to deploy a service from your local (I have not yet tested the stability of the connection)

## Pre-requisites
To run this requires:
* cloudflared installed if do not have yet follow this [guide](/docs/cloudflared/install)
* Already authenticated for cloudflared system with cert.pem file, if do not have yet follow this [guide](/docs/cloudflared/auth)


# TL;DR
To create tunel with name **example** run 
```shell
cloudflared tunnel create example
```

# Create tunnel from CLI
according to [official guide](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/get-started/create-local-tunnel/#3-create-a-tunnel-and-give-it-a-name) on machine that want the tunnel with the next command can create tunnel

```shell
cloudflared tunnel create <NAME>
```

for example create a tunnel with name *example*
```shell
cloudflared tunnel create example
```

If auth is ok and name has valid chars the command should output something like this

Tunnel credentials written to C:\Users\user\.cloudflared\fedb123-fa123-1234-b123-1234567bd.json. cloudflared chose this file based on where your origin certificate was found. Keep this file secret. To revoke these credentials, delete the tunnel.
<br>
<br>
Created tunnel example with id fedb123-fa123-1234-b123-1234567bd
{: .notice}

**NOTE**: if for some reason output something like this.
<br>
<br>
---
failed to create tunnel: Create Tunnel API call failed: Failed to create tunnel: code: 10000, reason: Authentication error
<br>
<br>
Try to perform [auth](/docs/cloudflared/auth) again and retry
{: .notice--danger}
