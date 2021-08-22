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
  - Credentials: root/**[password]** & psewda/**[password]**

- **Activities**
  - Disable Firewall
    - **check status**: `sudo firewall-cmd --state`
    - **stop service**: `sudo systemctl stop firewalld`
    - **disable service**: `sudo systemctl disable firewalld`
  
  - Disable SElinux
    - **check status**: `sestatus`
    - **open config file**: `sudo vi /etc/selinux/config`
    - **update options**
      - SELINUX=disabled
    - **restart machine**: `sudo shutdown -r now`
    - **more info**: [click](https://linuxize.com/post/how-to-disable-selinux-on-centos-8) here
  
  - Setup EPEL (Extra Packages for Enterprise Linux) Repo
    - **install**: `sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm`
    - **enable powertools repo**: `sudo dnf config-manager --set-enabled powertools`
    - **verify**: `yum repolist`
  
  - Install Important Packages
	  - **network tools**: `sudo yum install net-tools`
	  - **binding utils**: `sudo yum install bind-utils`
  
  - Update All Packages
	  - **run**: `sudo yum update && sudo yum upgrade`