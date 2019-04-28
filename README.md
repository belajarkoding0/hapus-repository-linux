# hapus-repository-linux
Cara hapus repository di linux fedora

Remove YUM/DNF Repo (Repository) Permanently
Before deleting repository permanently is a good idea to check that is the repository installed using rpm package.
As many repos usually are, like RPM-Fusion, Epel, etc.

Search Repository RPM-package with following command:
rpm -qa |grep -i repo-name
Example:

rpm -qa |grep -i rpmfusion
rpmfusion-free-release-28-1
rpmfusion-nonfree-release-28-1

## OR ##

rpm -qa |grep -i pgdg
pgdg-fedora10-10-4.noarch
If RPM-package found then simply remove whole RPM-package with following command:
rpm -e some-repository-rpm-package
Example:

rpm -e rpmfusion-free-release-28-1 rpmfusion-nonfree-release-28-1
If RPM-package not found then simply remove repo file with following command:
rm /etc/yum.repos.d/repo-file.repo

## OR just rename it (without repo file extension) ##
mv /etc/yum.repos.d/repo-file.repo /etc/yum.repos.d/repo-file.repo.bak
Example:

rm /etc/yum.repos.d/skype-stable.repo

## OR just rename it (without repo file extension) ##
mv /etc/yum.repos.d/skype-stable.repo /etc/yum.repos.d/skype-stable.repo.bak
Disable YUM/DNF Repository (3 methods)
Disable YUM/DNF Repo manually editing repo file
Edit repo file on /etc/yum.repos.d/ as root and change enabled to 0

## Change
enabled=1

## To
enabled=0
Example:


# Change
[skype-stable]
name=skype (stable)
baseurl=https://repo.skype.com/rpm/stable/
enabled=1
gpgcheck=1
gpgkey=https://repo.skype.com/data/SKYPE-GPG-KEY

# To
[skype-stable]
name=skype (stable)
baseurl=https://repo.skype.com/rpm/stable/
enabled=0
gpgcheck=1
gpgkey=https://repo.skype.com/data/SKYPE-GPG-KEY
Enable disabled repo quickly with YUM/DNF:

## YUM ##
yum --enablerepo=some-disabled-repository install some-package

## DNF ##
dnf --enablerepo=some-disabled-repository install some-package
Disable YUM/DNF repo using config-manager
This command just change repo file(s) enabled=1 to enabled=0.

## YUM ##
yum-config-manager --disable repo

## DNF ##
dnf config-manager --disablerepo repo
Example:

## YUM ##
yum-config-manager --disable skype-stable

## DNF ##
dnf config-manager --disablerepo skype-stable

 
Disable YUM Repo (Repository) using YUM/DNF
## YUM ##
yum --disablerepo=some-repository install some-package

## DNF ##
dnf --disablerepo=some-repository install some-package
Example:

## YUM ##
yum --disablerepo=skype-stable install some-package

## DNF ##
dnf --disablerepo=skype-stable install some-package
