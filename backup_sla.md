# Backup Service Level Agreement (SLA)

## Backup Coverage  
Folloing services will be backed up using ansible playbook  
- Web Service with Nginx - covered by ansible repository  
- App Service (Agama) - covered by ansible repository  
- Database services (InfluxDB, MySQL) - Daily back up 
- DNS services (Bind9) - covered by ansible repository 
- Logging services (Grafana, exporters) - covered by ansible repository 

## RPO  
The backup will be updated to the point where the database is no more than one day in the past.  

## Versioning and retention 
Local backup is made once a day at 1:00 AM(EET), includeing Influnxdb, MySQL   
Old back up will be deleted after the new one is made.  

Full backup is made every Sunday at 1:30 AM(EET), including Influxdb, MySQL.  
The backup will be kept for one month.  

Incremental backup is made at 1:30 AM(EET) on weekdays(Mon - Fri), including Influxdb, MySQL. 
The back up will be kept for one week.  

All the backup will be retained for 4 weeks/28 days.
Only 2 versions can be stored at the same time.
The oldest backup will be deleted at 2:00 AM(EET) on 28th day of every month.  

## Usability checks  
Usability of backups must be checked before implemented on the reaul production infrastacture. The test will be simulated on virtual environment every Monday.  

## Restoratoin criteria  
Backup will be restored in any case of data loss or down in monitorloing service.  

## RTO  
Our infrastructure is still small, therefore restoring of backup should take no longer than 2 hours.