# Contributing

Thanks for taking the time to contribute.

## What to change

This repo is intentionally small. Typical contributions are:

- Updating `.well-known/mta-sts.txt` when MX hosts change
- Updating documentation in `README.md`

## Policy changes

If you change the policy:

- Update the DNS TXT record at `_mta-sts.toppymicros.com` by bumping the `id=` value
- Prefer `mode: testing` first, then switch to `enforce` once validated

## Quick checks

- `curl -i https://mta-sts.toppymicros.com/.well-known/mta-sts.txt`
- `dig TXT _mta-sts.toppymicros.com +short`
