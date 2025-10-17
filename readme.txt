# run dev (default docker-compose.yml) ใน path 
docker compose up -d

#path
docker compose -f /path/to/docker-production.yml up -d

#FullLocal Dev
docker compose -f dev.yml up -d
docker compose -f dev.yml down




#Production
docker compose -f production.yml up -d
docker compose -f production.yml down



#new add
docker run --rm -v apache_project:/data -v /c/Users/tow/Desktop/apache/project:/source busybox cp -r /source/. /data 
docker run --rm -v apache_project:/data -v "$(pwd)/project:/source busybox cp -r /source/. /data"  # is production 
#เปลี่ยนเจ้าของ
docker run --rm -v apache_project:/data busybox chown -R 33:33 /data

docker exec -it apache bash
docker exec -it apache ls -l /var/www/html


#clean - copy 
docker run --rm -v apache_project:/data -v /c/Users/tow/Desktop/apache/project:/source busybox sh -c "rm -rf /data/* && cp -r /source/. /data 
#owner set
docker run --rm -v apache_project:/data busybox chown -R 33:33 /data

#backup
docker run --rm -v apache_project:/data -v ./:/backup busybox sh -c "cd /data && tar -czf /backup/apache_project_backup.tar.gz ."
docker run --rm -v apache_project:/data -v /c/Users/tow/Desktop/backup:/backup busybox sh -c "cd /data && tar -czf /backup/apache_project_backup.tar.gz ."
#restore
docker run --rm -v apache_project:/data -v /c/Users/tow/Desktop/backup:/backup busybox sh -c "tar -xzf /backup/apache_project_backup.tar.gz -C /data"
docker run --rm -v apache_project:/data -v ./:/backup busybox sh -c "tar -xzf /backup/apache_project_backup.tar.gz -C /data"



#restore linux 
docker run --rm -v apache_project:/data -v "$(pwd)/backup:/backup" busybox sh -c "tar -xzf /backup/apache_project_backup.tar.gz -C /data"



#cron job (optional)
chmod +x backup-mysql.sh
./backup-mysql.sh

crontab -e

0 2 * * * /path/to/project/backup-mysql.sh >> /path/to/project/backup.log 2>&1



#ย่อชือให้ terminal จะได้พิ่มสั้นลง
alias artisan="docker exec -it apache php artisan"
alias composer="docker exec -it apache composer"

ab -n 1000 -c 50 http://localhost:8000/benchmark.php

