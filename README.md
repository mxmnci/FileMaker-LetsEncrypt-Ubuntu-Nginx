# FileMakerServer-LetsEncrypt-Ubuntu-Nginx-Certbot
Bash scripts for fetching and renewing Let's Encrypt (certbot) certificates for FileMaker Server running on Linux (Ubuntu) using the default system timers installed by snap when you install certbot and hooks to restart FMS only when the certificate is renewed and at a certain time of day to avoid disruption of access to users.

### Initial Setup Instructions:
1. Setup Ubuntu + install FMS (as of now, its 19.6.3)
2. Install `certbot`

sudo snap install core; sudo snap refresh core
sudo apt-get remove certbot
sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/certbot

3. Logged in as root:

cd ~/
mkdir fms-ssl
cd fms-ssl/

3. Download

wget https://github.com/mhtawfiq/FileMaker-LetsEncrypt-Ubuntu-Nginx/blob/main/fms-ssl/get-ssl.sh
wget https://github.com/mhtawfiq/FileMaker-LetsEncrypt-Ubuntu-Nginx/blob/main/fms-ssl/renew-cert.sh
wegt https://github.com/mhtawfiq/FileMaker-LetsEncrypt-Ubuntu-Nginx/blob/main/fms-ssl/renew-cert-at.sh

4. chmod +x get-ssl.sh renew-cert.sh renew-cert-at.sh 
5. Edit content of scripts

nano get-ssl.sh
Set domain, fms admin username and password and email

nano renew-cert.sh
Set domain, fms admin username and password

nano renew-cert-at.sh
Set the time of day to schedule FileMaker Server restart when the certificate is renewed by certbot systemctl timer

6. Run `sudo ./get-ssl.sh` to generate the ssl certificate for the first time.


### Renewal Setup Instructions:
The certbot systemctl timer installed by certbot by default checks twice a day at a random time if the certificate needs renewal, only if the certificate is renewed will it run pre and post hooks for additional processing.

We will add a post hook to run renew-cert-at.sh
ln -s ~/fms-ssl/renew-cert-at.sh /etc/letsencrypt/renewal-hooks/post/

This insures that once the certificate is renewed by the systemctl timer, FileMaker Server will only restart the time scheduled in renew-cert-at.sh to avoid disruption of access to users at an undesired time.

Forked from https://github.com/jon91/FileMaker-LetsEncrypt-CentOS-7
