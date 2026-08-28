# Ordo documentation

Plain-language product help for **Ordo** — insurance payment posting for dental practices.

This repository is only documentation. It is published as GitHub Pages at **https://docs.ordo/** (after DNS is pointed at GitHub Pages).

The Ordo application itself lives in a separate repo. In-app **Docs** stay short; this site is the longer guide, written so office managers and billing staff can use it without a technical background.

## Local preview

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve
```

Open [http://127.0.0.1:8000](http://127.0.0.1:8000).

## Publishing

Pushes to `main` build the site with MkDocs Material and deploy GitHub Pages via `.github/workflows/deploy-docs.yml`.

## Custom domain (`docs.ordo`)

GitHub Pages is set to serve this site at `https://docs.ordo/`. In the DNS for the `ordo` zone (the same place `test.ordo` is defined), add:

```
docs.ordo.   CNAME   tools772.github.io.
```

After DNS propagates, GitHub issues a certificate. The github.io URL keeps working as a fallback until then.
