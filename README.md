# duplicity2mega
Since [mega.py](https://github.com/richardasaurus/mega.py) is broken here is docker based replacement


##How to use:
1. create free [mega account[(https://mega.nz)
1. start container
  * `git clone https://github.com/bitswarming/duplicity2mega.git`
  * `cd duplicity2mega`
  * edit `.env` file. set PASSPHRASE (pass for encrypted backups), USERNAME (mega login),PASSWORD (mega password), optionally change HOSTNAME,VOLSIZE (backup volume size),OLDERTHAN (full backup if older),TZ (timezone), RESTOREDPATH (path for restored files)
  * `sudo docker-compose  -f docker-compose.yml up -d` after build docker container named megafuse launched and mega already connected 
1. backup and restore
set list of folders to backup at configs/include.txt 
  * backup with `sudo docker exec -it megafuse bash -c /root/configs/backup.sh`
  * verify backup `sudo docker exec -it megafuse bash -c /root/configs/verify.sh [filepath/filename]`
  * list backups with dates `sudo docker exec -it megafuse bash -c /root/configs/list.sh`
  * restore `sudo docker exec -it megafuse /root/configs/restore.sh "Sat Feb  4 16:53:38 2017" [filepath/filename]`
  * attach container and view megafuse communication logs `sudo docker logs  -f  megafuse`
1. after finish. stop container `sudo docker stop megafuse` and delete it `sudo docker rm megafuse`.
