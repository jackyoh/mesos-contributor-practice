## Mesos source code download and build on the CentOS 7.3
### Preinstalled
* Close firewalld
```
# systemctl stop firewalld
# systemctl disable firewalld
```

* Disable SELinux
```
# vi /etc/sysconfig/selinux
```
selinux檔案如下設定
```
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=disabled
# SELINUXTYPE= can take one of three two values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes are protected.
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted
```

* reboot
```
# reboot
```

### 從 Apache git repository clone source code 回 local
```
# git clone https://git-wip-us.apache.org/repos/asf/mesos.git
```

### 安裝在 Build Mesos 會使用到的套件
```
# wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
# yum install -y epel-release
# vi /etc/yum.repos.d/wandisco-svn.repo
[WANdiscoSVN]
name=WANdisco SVN Repo 1.9
enabled=1
baseurl=http://opensource.wandisco.com/centos/7/svn-1.9/RPMS/\$basearch/
gpgcheck=1
gpgkey=http://opensource.wandisco.com/RPM-GPG-KEY-WANdisco

# yum update systemd
# yum groupinstall -y "Development Tools"
# yum install -y apache-maven python-devel python-virtualenv java-1.8.0-openjdk-devel zlib-devel libcurl-devel openssl-devel cyrus-sasl-devel cyrus-sasl-md5 apr-devel subversion-devel apr-util-devel python-pip
# pip install --upgrade pytz
```

### 開始 Build Mesos
```
# cd mesos
# ./bootstrap
# mkdir build
# cd build
# ../configure
# make
# make install
```