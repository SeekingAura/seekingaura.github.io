---
title: Cloudflared Local
permalink: /docs/dev_notes/cloudflared_local/
---

A tunnel is a secure, outbound-only pathway you can establish between your origin to global network without **publicly routable IP address**, on this case Cloudflare have `Cloudflared tunnels` these connect to global Cloudflare's global network [followed by](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/get-started/tunnel-useful-terms/#tunnel). Tunnels are managed on cloudflare and use *Authentication* of your cloudflare account to work

These notes are based on [Cloudflared Official](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/)

A simple way to use for dev environments is to manage tunnel from local machine, can create tunnels, and connect tunnels with CLI from machine that you want to redirect traffic by cloudflare DNS configuration.
