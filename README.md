# mta-sts.toppymicros.com

MTA-STS policy hosting repo for `toppymicros.com`.

This repository is intended to be published via GitHub Pages on the domain `mta-sts.toppymicros.com` and serve the policy file at:

- `https://mta-sts.toppymicros.com/.well-known/mta-sts.txt`

## GitHub Pages setup

- GitHub Pages: serve from the default branch (commonly `main`) at the repository root
- Custom domain: `mta-sts.toppymicros.com` (see `CNAME`)
- HTTPS must be enabled

## Customize for your domain

If you reuse this repo for your company (e.g., your company website is hosted on GitHub Pages), swap `toppymicros.com` to your domain everywhere:

- Update `CNAME` to `mta-sts.<your-domain>`
- Update the policy URL to `https://mta-sts.<your-domain>/.well-known/mta-sts.txt`
- Update `.well-known/mta-sts.txt`:
	- Set `mx:` lines to match your domain’s actual MX hosts (check with `dig MX <your-domain>`)
	- Choose `mode: testing` first, then move to `enforce`
- Create the DNS TXT record at `_mta-sts.<your-domain>` with `v=STSv1; id=<some-id>`

## Served policy

Path: `https://mta-sts.toppymicros.com/.well-known/mta-sts.txt`

```
version: STSv1
mode: testing
mx: mail.protonmail.ch
mx: mailsec.protonmail.ch
max_age: 86400
```

## DNS TXT record

Create a TXT record:

- Name/Host: `_mta-sts.toppymicros.com` (or `_mta-sts` if your DNS provider appends the zone)
- Type: `TXT`
- Value:

```
v=STSv1; id=20260106T000000Z
```

After publishing, verify:

```sh
dig TXT _mta-sts.toppymicros.com +short
```

Also verify the policy is reachable over HTTPS:

```sh
curl -i https://mta-sts.toppymicros.com/.well-known/mta-sts.txt
```

## Notes

- `mode: testing` is a safe rollout; switch to `enforce` once confident.
- `max_age` is 1 day; increase (e.g., 604800) after validating delivery.
- Update `id` when the policy changes to force re-fetching by senders.

## Customize for your domain

If you want to reuse this repo for your company domain, replace `toppymicros.com` with your domain and update:

- `CNAME` to `mta-sts.<your-domain>`
- `.well-known/mta-sts.txt` `mx:` lines to match `dig MX <your-domain>`
- DNS TXT `_mta-sts.<your-domain>` to `v=STSv1; id=<some-id>` (bump `id` whenever the policy changes)

## Work log

- Added `.well-known/mta-sts.txt` with Proton Mail MX hosts, `mode: testing`, and `max_age: 86400`.
- Added `.nojekyll` so GitHub Pages serves the `.well-known` path.
- Documented the required TXT at `_mta-sts.toppymicros.com` and policy details above.

## License

MIT: see `LICENSE`.
