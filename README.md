# openipsl.github.io — redirect for openipsl.org

This repository exists only to make **https://openipsl.org** (and `www.openipsl.org`) redirect to the OpenIPSL library repository:
**https://github.com/OpenIPSL/OpenIPSL**

## Why this exists

The domain `openipsl.org` is registered at **Hover**. It used Hover's built-in URL forwarding, which points the domain to Hover's forwarding server (`216.40.34.41`). That server only answers plain HTTP (port 80) and does **not** serve HTTPS (port 443).

Modern browsers (Chrome first) try `https://` by default, so `openipsl.org` timed out (`ERR_TIMED_OUT`), while `http://openipsl.org` still worked.

GitHub Pages serves custom domains over HTTPS with a free, auto-renewed certificate. Hosting a one-page redirect here gives a working `https://openipsl.org` at no cost.

## Contents

| File | Purpose |
|---|---|
| `index.html` | Redirects to https://github.com/OpenIPSL/OpenIPSL (meta refresh + JavaScript, with a fallback link). |
| `404.html` | Same redirect, so any path (e.g. `openipsl.org/foo`) also lands on the repository. |
| `CNAME` | Tells GitHub Pages the custom domain is `openipsl.org`. |
| `.nojekyll` | Disables Jekyll processing; files are served as-is. |

## DNS configuration (Hover → DNS tab for openipsl.org)

URL forwarding must be **removed**, and these records set:

| Type | Host | Value |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | openipsl.github.io |

Nameservers stay at Hover (`ns1.hover.com`, `ns2.hover.com`).

## GitHub Pages settings (Settings → Pages)

1. Source: *Deploy from a branch* → `main` / `(root)`.
2. Custom domain: `openipsl.org`.
3. *Enforce HTTPS*: ticked (available once GitHub has issued the certificate, typically 15–60 min after DNS propagates).

## Changing the redirect target

Edit the URL in `index.html` and `404.html` (three occurrences each: meta refresh, canonical link, JavaScript) and commit. No DNS change is needed.

## Verifying

```bash
dig +short openipsl.org          # should list the four 185.199.x.153 addresses
curl -sI https://openipsl.org    # should return 200 from GitHub Pages
```

Maintained by ALSETLab / the OpenIPSL maintainers.
