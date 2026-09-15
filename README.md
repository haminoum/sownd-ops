# sownd-db-backup

Weekly `pg_dump` of the SOWND production database to Cloudflare R2.

This repository is public on purpose: GitHub Actions minutes are free and
unlimited for public repositories, so the backup can never be skipped because
private-repo CI used up the monthly quota. Nothing in here is sensitive. The
credentials live in repository secrets and the dumps go straight from the
runner to R2.

- Schedule: Sundays 05:00 UTC, plus manual runs from the Actions tab.
- Output: `<YYYY-MM-DD>/backup-full-*.sql.gz` and `backup-schema-*.sql.gz`,
  and a `latest.txt` marker at the bucket root. `LAST_RUN` in this repo is a
  heartbeat commit that keeps the cron schedule from being auto-disabled.
- Retention: objects older than 30 days are deleted at the end of each run.
- Scope: the `public` schema. Supabase-managed schemas (`auth`, `storage`,
  `vault`, ...) are excluded.

Secrets required: `PRODUCTION_DATABASE_URL`, `R2_ACCESS_KEY_ID`,
`R2_SECRET_ACCESS_KEY`, `R2_ACCOUNT_ID`, `R2_BUCKET_NAME`.

Restore instructions live in the private migrations repository
(`scripts/restore-database.sh`).
