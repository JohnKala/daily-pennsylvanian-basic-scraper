# Schedule Explanation

The `schedule` section of the GitHub Actions workflow uses cron syntax to define when the scraper should run.

## Cron Expressions Used
0 3 * * * → runs every day at 3:00 AM UTC
0 15 * * * → runs every day at 3:00 PM UTC

## Cron Format

The format is:  
`minute hour day-of-month month day-of-week`

So:
- `0 3 * * *` means at 03:00 UTC every day.
- `0 15 * * *` means at 15:00 UTC (i.e. 3:00 PM UTC) every day.

These times ensure the scraper checks for updates **twice daily**, improving its ability to catch new headlines throughout the day.

