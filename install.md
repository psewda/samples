# Centos 8

- **VM Configuration**
  - CPU: 2
  - RAM: 4GB
  - Disk: 20GB (thin provision)
- **Install Configuration**
  - Hostname: centos
  - DHCP: Yes
  - Software Selection: Minimal Install
  - Disk/Storage Configuration: Automatic
  - Credentials: root/**~pwd** & psewda/**~pwd**
  - Master Server IP: **[master-server-ip]**
  - CHANGE MASTER TO MASTER_HOST='**[master-instance-ip]**', MASTER_PORT=3306;
- **Activities**
  - Disable Firewall
    - check status: `sudo firewall-cmd --state`
    - stop service: `sudo systemctl stop firewalld`
    - disable service: `sudo systemctl disable firewalld`
  - Disable SElinux
    - check status: `sestatus`
    - open config file: `sudo vi /etc/selinux/config`
    - update options
      - SELINUX=disabled
    - restart machine: `sudo shutdown -r now`
    - more-info: ref [link](https://linuxize.com/post/how-to-disable-selinux-on-centos-8) here
  - Setup EPEL (Extra Packages for Enterprise Linux) Repo:
  
