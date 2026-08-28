# Ordo documentation

Plain-language product help for **Ordo** — insurance payment posting for dental practices.

Published at **https://docs.perfect.ventures/ordo/** (after DNS for `docs.perfect.ventures` points at GitHub Pages).

The Ordo application itself lives in a separate repo. In-app **Docs** stay short; this site is the longer guide, written so office managers and billing staff can use it without a technical background.

Other products can be added later as sibling paths on the same domain, for example `https://docs.perfect.ventures/another-product/`. GitHub Pages allows only one custom domain per site, so those paths should live in this same published tree.

## Local preview

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve
```

Open [http://127.0.0.1:8000](http://127.0.0.1:8000).

## Publishing

Pushes to `main` build Ordo into `/ordo/` and deploy GitHub Pages via `.github/workflows/deploy-docs.yml`.

## Custom domain (`docs.perfect.ventures`)

In GoDaddy DNS for `perfect.ventures`:

| Field | Value |
| --- | --- |
| Type | CNAME |
| Name | `docs` |
| Value | `tools772.github.io` |
| TTL | 1 Hour |

That creates `docs.perfect.ventures` → GitHub Pages. Ordo help is then at `/ordo/`. After DNS propagates, GitHub issues a certificate.
