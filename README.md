# FileMakerServer-LetsEncrypt-Ubuntu-Nginx
Bash scripts for fetching and renewing Let's Encrypt (certbot) certificates for FileMaker Server running Linux (Ubuntu) using the default system timers installed by snap and hooks to restart FMS only when the certificate is renewed and at a certain time of day.

### Initial Setup Instructions:
1. Setup Ubuntu + install FMS (as of now, its 19.6.3)
2. Install `certbot`
3. download `wget https://raw.githubusercontent.com/jon91/FileMaker-LetsEncrypt-CentOS-7/main/get-ssl.sh`
4. chmod +x get-ssl.sh renew-cert.sh renew-cert-at.sh 
5. edit content of script `nano get-ssl.sh'
6. run `sudo ./get-ssl.sh`


### Renewal Setup Instructions:
1. download `wget https://raw.githubusercontent.com/jon91/FileMaker-LetsEncrypt-CentOS-7/main/renew-cert.sh`
2. add execution `chmod ./renew-cert.sh`
3. edit content of script `nano ./renew-cert.sh` (only fms usr/pwd edit needed)
4. run `sudo ./renew-cert.sh`

Forked from https://github.com/jon91/FileMaker-LetsEncrypt-CentOS-7
