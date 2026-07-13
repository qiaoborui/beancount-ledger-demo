# Beancount Ledger Demo

Public synthetic ledger data for the preview deployments of
[Beancount Ledger Web](https://github.com/qiaoborui/beancount-ledger-web).

This repository contains no real personal financial data. The accounts,
transactions, balances, prices, merchants, and import configuration are all
sanitized demo fixtures copied from the application's public
`examples/preview-ledger` dataset.

## Contents

- Seven months of 2026 transactions covering income, daily spending,
  transfers, credit cards, reimbursements, investments, and multi-currency
  balances.
- 391 postings across CNY, HKD, USD, and three synthetic securities.
- Example Alipay, WeChat Pay, and bank import configuration.
- A GitHub Actions indexer that publishes `main` into the dedicated Ledger Web
  Preview Postgres read model after every push.

## Branch

`main` is both the public demo snapshot and the branch used by Vercel Preview
deployments and app-created GitHub API writes. Preview uses its own Supabase
database, so the demo read model is isolated from production.

## Validation

Install Beancount 3 and run:

```bash
bean-check main.bean
```

The index workflow additionally validates and indexes the complete ledger with
the current `ledger-indexer` command from Beancount Ledger Web.

## Required Repository Configuration

The `Index Ledger Web` workflow requires:

- Actions secret `DATABASE_URL`.
- Optional Actions variable `LEDGER_WEB_APP_REF` (defaults to `main`).
- Optional Postgres pool variables used by the workflow defaults.

Never commit database credentials, GitHub tokens, imported bills, or private
ledger exports to this repository.
