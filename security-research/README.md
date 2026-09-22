# Security Research Evidence

This directory organizes evidence generated during controlled testing.

## Layout

- `baseline/` — pre-test state
- `network/` — network observations
- `processes/` — process observations
- `filesystem/` — filesystem observations
- `hashes/` — file hashes
- `reports/` — sanitized reports

## Sensitive evidence

Raw logs may contain credentials, tokens, cookies, personal data, or unrelated system information. Keep sensitive material outside Git or under ignored local paths.

Only sanitized evidence suitable for repository publication should be committed.
