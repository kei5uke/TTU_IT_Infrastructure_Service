# Backup manually  
## SQL   
``` sudo su backup ```  
``` mysqldump agama > /home/backup/mysql/agama.sql ```  
``` duplicity --no-encryption full /home/backup/mysql/  rsync://keisuke-jpn@backup.noobmaster69.kk//home/keisuke-jpn/```  
  
## Influx  
``` rm -rf /home/backup/influxdb/*; influxd backup -portable -database telegraf /home/backup/influxdb ```   
``` sudo su backup ```  
``` duplicity --no-encryption full /home/backup/influxdb/ rsync://keisuke-jpn@backup.noobmaster69.kk//home/keisuke-jpn/ ```