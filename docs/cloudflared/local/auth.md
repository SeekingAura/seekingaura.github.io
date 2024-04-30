---
title: Cloudflared-Auth
---
<!-- omit from toc -->
# Cloudflared Authentication
To Expose connection, port or most usages of Cloudflared requires stablish connection to your cloudflare account, authentication is managed via **cert.pem** file from cloudflared auth system

<!-- omit from toc -->
## Pre-requisites
To run this requires:
* cloudflared installed locally if do not have yet follow this [guide](/docs/cloudflared/local/install)

<!-- omit from toc -->
# TOC
- [Authenticate](#authenticate)
  - [Login command](#login-command)
  - [Redirect to expected browser](#redirect-to-expected-browser)
- [Cert.pem file](#certpem-file)


<!-- omit from toc -->
# TL;DR

# Authenticate
## Login command
Run the next command

```shell
cloudflared tunnel login
```

will output something like this
```txt
https://dash.cloudflare.com/argotunnel?aud=&callback=https%3A%2F%2Flogin.cloudflareaccess.org%2XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX%3D
If the browser failed to open, please visit the URL above directly in your browser.
2024-03-25T18:01:19Z INF Waiting for login...
```

automatically will open on default browser that url, should go that website on browser where you have you cloudflare session if you have that session on another browser you can close, copy the url from **Terminal** and go to the expected browser.

If you perform login on cloudflare is possible you do not be redirected to expected site for tunnel configuration (specially if you have Two factor auth), the website for tunnel config is something like this:

![Cloudflared auth Select domain](/assets/img/screenshots/docs/cloudflared/cloudflared-auth-select_domain.png)

## Redirect to expected browser
If website is not that try to access again to the url that are on the **Terminal**, remember exist a timeout so if Terminal output something like this

```txt
Failed to write the certificate due to the following error:
Failed to fetch resource

Your browser will download the certificate instead. You will have to manually
copy it to the following path:

%USERPROFILE%\.cloudflared\cert.pem
Failed to fetch resource
```

Start again with `cloudflared tunnel login` command [follow this](#login-command)

# Cert.pem file
**Cert.pem** are stored at default [cloudflare location](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/get-started/tunnel-useful-terms/#default-cloudflared-directory) (%USERPROFILE%\.cloudflared\cert.pem for windows)
This file file is used for auth on cloudflared tunnel operationsBEWARE this file actually if for some reason being **compromised** could be perform cloudflared operations with that file, so it is recommended to generate authentication with external member cloudflare account (cloudflare account super admin can add multiple accounts).

**I do not tested yet** but it is possible the **cert.pem** value vary for each authenticated userIn any case, handle cert.pem file carefully

If already have cert.pem file and requires to auth again just delete file and Start again with `cloudflared tunnel login` command [follow this](#login-command)

---

[Next topic](/docs/cloudflared/local/create_tunnel)

<!-- omit from toc -->
# Navigation
* [Cloudflared local index](/docs/cloudflared/local)
* [Cloudflared index](/docs/cloudflared)
* [Docs index](/docs)