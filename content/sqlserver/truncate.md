# Turning trace flags on when string or binary data truncate error occurs

This is used to investigate, on some instances turning on in prod can be risky.

## Sql Server 2019 or later

Simply run:

```sql
ALTER DATABASE SCOPED CONFIGURATION 
  SET VERBOSE_TRUNCATION_WARNINGS = ON;
```

## Sql Server 2017

You can turn the trace flag on:

```sql
DBCC TRACEON(460, -1);
GO
```

Then turn it off, once used:

```sql
DBCC TRACEOFF(460, -1);
GO
```

For more information check [Brent Ozar site](https://www.brentozar.com/archive/2019/03/how-to-fix-the-error-string-or-binary-data-would-be-truncated/)
