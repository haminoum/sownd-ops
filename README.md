# sownd-db-backup

Weekly `pg_dump` of the SOWND production database.


- Retention: objects older than 30 days are deleted at the end of each run.
- Scope: the `public` schema. Supabase-managed schemas (`auth`, `storage`,
  `vault`, ...) are excluded.
