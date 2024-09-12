
# SQL DATABASE BACKUP THROUGH QUERY

How we can create any sql datababse backup using query.

## BACKUP

#### Query

```bash
  BACKUP DATABASE Taskmangement_syss
  TO DISK = 'D:\backups\Taskmangement_syss.bak';
```
- **Taskmangement_syss** is datababse name
- **Taskmangement_syss.bak** database backup file name
- before backup you need to create backup folder in    drive that not automatic create folder


## RESTORE

#### Query

```bash
RESTORE DATABASE Taskmangement_syss
FROM DISK = 'D:\db_backup\Taskmangement_syss.bak'
WITH MOVE 'Taskmangement_syss' TO 'C:\Program Files\Microsoft SQL Server\MSSQL15.SQLEXPRESS\MSSQL\DATA\Taskmangement_syss.mdf',
MOVE 'Taskmangement_syss_log' TO 'C:\Program Files\Microsoft SQL Server\MSSQL15.SQLEXPRESS\MSSQL\DATA\Taskmangement_syss_log.ldf',
REPLACE;
```
- **Taskmangement_syss** is datababse name
- **Taskmangement_syss.bak** database backup file name
- before restore you need to put that bak file in that location
- mdf and ldf file name is same as db name

**If face error on mdf and ldf file:**
```bash
RESTORE FILELISTONLY 
    FROM DISK = 'D:\db_backup\Intercompany_Reconciliation_Dev.bak'
```

- this query display actual ldf or mdf file
- **Intercompany_Reconciliation_Dev.bak** is backup file
- that return log and mdf original name that issue face on when db name renamed.
- after this query you need to run restore query

```bash
RESTORE DATABASE Intercompany_Reconciliation_Dev
FROM DISK = 'D:\db_backup\Intercompany_Reconciliation_Dev.bak'
WITH MOVE 'Intercompany Reconciliation' TO 'C:\Program Files\Microsoft SQL Server\MSSQL15.SQLEXPRESS\MSSQL\DATA\Intercompany Reconciliation.mdf',
MOVE 'Intercompany Reconciliation_log' TO 'C:\Program Files\Microsoft SQL Server\MSSQL15.SQLEXPRESS\MSSQL\DATA\Intercompany Reconciliation_log.ldf',
REPLACE;
```
