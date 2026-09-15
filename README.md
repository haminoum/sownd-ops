# sownd-ops

Scheduled monitors for SOWND that must keep running even when the private
repos' Actions minutes are used up.

## Database backup

Weekly `pg_dump` of the SOWND production database, Sundays 05:00 UTC.

- Retention: objects older than 30 days are deleted at the end of each run.
- Scope: the `public` schema. Supabase-managed schemas (`auth`, `storage`,
  `vault`, ...) are excluded.

## Certificate expiry

Weekly check, Mondays 09:00 UTC, that the certificate serving the press kit
subdomains has more than 21 days left. Run it manually with
`threshold_days=9999` to force the alert and verify the wiring.

Both workflows alert Telegram on failure.
