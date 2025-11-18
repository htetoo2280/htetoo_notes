---
id: e87zdfj9mki2wmnc4ze3qe3
title: Rclone_in_a_docker
desc: ''
updated: 1762510843309
created: 1762510835953
---


```bash
## checking image
sudo docker images

## checking container
sudo docker ps -a 
```
----------------

## Old exited containers တွေကို cleanup လုပ်ချင်ရင်:
```bash

sudo docker rm $(sudo docker ps -a -q)

```
## running rclone in a docker with rclone script

## server list
```bush

- sudo docker run -it -v ~/.config/rclone:/root/.config/rclone rclone/rclone listremotes
```

## testing connection
```bush

- sudo docker run -it -v ~/.config/rclone:/root/.config/rclone rclone/rclone lsd myserver:

```

✅ Stage 1: rclone scripts ထားမယ့် folder create

Home directory ထဲမှာ folder တစ်ခု သတ်မှတ်ထားမယ်။

mkdir -p ~/rclone/scripts
-----------

✅ Stage 2: Script file တစ်ခု create

nano ~/rclone/scripts/upload_to_s3.sh

-------------------------------------------

```bush
#!/bin/bash
set -euo pipefail

# Variables - update these
SFTP_REMOTE="1st_rclone"
SFTP_PATH="/DEStaging/KBZPay/ABVC/KBZPay_Center/Center_Mapping_Format_2025-11-07.csv"

S3_REMOTE="s3"
S3_BUCKET_PATH="testmty/ho_test/rclone_testing/Center_Mapping_Format_2025-11-07.csv"

LOGDIR="/home/ubuntu/rclone/logs"
mkdir -p "$LOGDIR"
LOGFILE="$LOGDIR/copy_one_file_$(date +%F_%H%M%S).log"

echo "=== START $(date) ===" >> "$LOGFILE"

sudo docker run --rm \
  -v ~/.config/rclone:/root/.config/rclone \
  rclone/rclone copyto \
    "${SFTP_REMOTE}:${SFTP_PATH}" \
    "${S3_REMOTE}:${S3_BUCKET_PATH}" \
    --progress -vv >> "$LOGFILE" 2>&1

RET=$?
echo "=== END $(date) exit=$RET ===" >> "$LOGFILE"
exit $RET
```

## build script to executable 
- chmod +x ~/rclone/scripts/copy_one_file.sh

## run manual ?
- bash -x ~/rclone/scripts/upload_to_s3.sh


# ပြီးရင် log ကြည့်ပါ
- ls -lh ~/rclone/logs
- tail -n 200 ~/rclone/logs/upload_to_s3_*.log

## log folder permission check ရန်

- ls -ld /home/ubuntu/rclone/logs (root user ဆို ပြောင်းဖို့လို)
- sudo chown -R ubuntu:ubuntu /home/ubuntu/rclone/logs (ဒါနဲ့ပြောင်း)



## ✅ 6) Final check

- ✅ Folder owner = ubuntu
- ✅ Script permission = +x
- ✅ Script run OK
- ✅ Log file created OK

