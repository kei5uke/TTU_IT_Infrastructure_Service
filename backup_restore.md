# Backup Restore Manual

Run Ansible playbook to install all the necessary configurations, run this command from the ica0002 on your machine.  
```ansible-playbook```

To restore **MySQL** database you will have to run commands on the second virtual machine where our MySQL configuration is made. 

Firstly, In order to restore the backup from the server, run this command as **backup** user:  
```sudo su - backup```    
``` rm -r /home/backup/mysql/restore/* ```  
```duplicity --no-encryption restore rsync://kei5uke@backup.noobmaster69.net//home/kei5uke/mysql/ /home/backup/mysql/restore```

Secondly, In order to upload the restore backup onto the machine, run this command as **root** user:  
```mysql agama < /home/backup/mysql/restore/agama.sql```

To restore **InfluxDB** database you will have to run commands as root on the first virtual machine where our InfluxDB configuration is made.

Firstly, In order to restore the backup from the server, run this command as **backup** user:  
```sudo su - backup```   
```rm -r /home/backup/influxdb/restore/*```  
```duplicity --no-encryption restore rsync://kei5uke@backup.noobmaster69.net//home/kei5uke/influxdb/ /home/backup/influxdb/restore```

To restore the backup you will need to delete existing telegraf database first. It also makes sense to stop the Telegraf service so that it doesn't recreate the database before you could restore it, run these commands from **root** user:  
```service telegraf stop```  
```influx -execute 'DROP DATABASE telegraf'```  
```influxd restore -portable -database telegraf /home/backup/influxdb/restore```

After you have verified that backup was restored successfully, run this command from the ica0002 on your machine,
it will start the telegraf service again:  
```ansible-playbook infra.yaml```  