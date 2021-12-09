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
Local backup is made once a day at 2:00 AM, includeing Influnxdb, MySQL   
Old back up will be deleted after the new one is made.  

Full back is made every Sunday at 2:30 AM, including Influxdb, MySQL.  
The backup will be kept for one month.  

Incremental backup is made 2:30 AM on weekdays(Mon - Fri), including Influxdb, MySQL. 
The back up will be kept for one week.  

## Usability checks  
Backup recovery will be verified by administration tools, which compare database dump to live database.  

## Restoratoin criteria  
Backup will be restored in any case of data loss or down in monitorloing service.  

## RTO  
Our infrastructure is still small, therefore restoring of backup should take no longer than 2 hours.