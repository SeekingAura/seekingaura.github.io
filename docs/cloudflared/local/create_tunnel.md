---
title: Cloudflared-Port
---
<!-- omit from toc -->
# Cloudflared Expose service from Port
Expose port via cloudflared tunnel is commonly used for projects that are in development or a cheap way to deploy a service from your local (I have not yet tested the stability of the connection)

<!-- omit from toc -->
## Pre-requisites
To run this requires:
* cloudflared installed if do not have yet follow this [guide](/docs/cloudflared/install)
* Already authenticated for cloudflared system with cert.pem file, if do not have yet follow this [guide](/docs/cloudflared/auth)

<!-- omit from toc -->
# TOC
- [Create tunnel from CLI](#create-tunnel-from-cli)


<!-- omit from toc -->
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

```txt
Tunnel credentials written to C:\Users\user\.cloudflared\fedb123-fa123-1234-b123-1234567bd.json. cloudflared chose this file based on where your origin certificate was found. Keep this file secret. To revoke these credentials, delete the tunnel.

Created tunnel example with id fedb123-fa123-1234-b123-1234567bd
```

**NOTE**: if for some reason output something like this
```
failed to create tunnel: Create Tunnel API call failed: Failed to create tunnel: code: 10000, reason: Authentication error
```

Try to perform [auth](/docs/cloudflared/auth) again and retry

---

[Next topic](/docs/cloudflared/local/create_tunnel)

<!-- omit from toc -->
# Navigation
* [Cloudflared local index](/docs/cloudflared/local)
* [Cloudflared index](/docs/cloudflared)
* [Docs index](/docs)