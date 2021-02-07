# centos-squid

## Reference URLs

[Squidで検証用のプロキシを作ってみた](https://dev.classmethod.jp/articles/squid-proxy-setup/)
[G Suiteで、会社のみを許可する方法](https://oa.oreda.net/system/groupware/gsuite/allowed-domains)
[allow-google-apps-and-block-consumer-google-accounts-using-squid-proxy](https://serverfault.com/questions/647892/allow-google-apps-and-block-consumer-google-accounts-using-squid-proxy)

## Install pkgs

```
yum install perl-Crypt-OpenSSL-X509 squid squid-helpers
```

## Work

```
mkdir /etc/squid/ssl_cert
cd /etc/squid/ssl_cert
openssl req -new -newkey rsa:2048 -sha256 -days 3650 -nodes -x509 -keyout oreoreCA.pem  -out myA.pem
openssl x509 -in myCA.pem -outform DER -out myCA.der
cp myCA.pem /usr/lib64/squid/
/usr/lib64/squid/ssl_crtd -c -s /var/lib/ssl_db
chown -R squid /var/lib/ssl_db
```

## CentOS7

```
# cat /etc/os-release
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"

#
```

## Squid

```
# squid -v
Squid Cache: Version 3.5.20
Service Name: squid
configure options:
'--build=x86_64-redhat-linux-gnu'
'--host=x86_64-redhat-linux-gnu'
'--program-prefix='
'--prefix=/usr'
'--exec-prefix=/usr'
'--bindir=/usr/bin'
'--sbindir=/usr/sbin'
'--sysconfdir=/etc'
'--datadir=/usr/share'
'--includedir=/usr/include'
'--libdir=/usr/lib64'
'--libexecdir=/usr/libexec'
'--sharedstatedir=/var/lib'
'--mandir=/usr/share/man'
'--infodir=/usr/share/info'
'--disable-strict-error-checking'
'--exec_prefix=/usr'
'--libexecdir=/usr/lib64/squid'
'--localstatedir=/var'
'--datadir=/usr/share/squid'
'--sysconfdir=/etc/squid'
'--with-logdir=$(localstatedir)/log/squid'
'--with-pidfile=$(localstatedir)/run/squid.pid'
'--disable-dependency-tracking'
'--enable-eui'
'--enable-follow-x-forwarded-for'
'--enable-auth'
'--enable-auth-basic=DB,LDAP,MSNT-multi-domain,NCSA,NIS,PAM,POP3,RADIUS,SASL,SMB,SMB_LM,getpwnam'
'--enable-auth-ntlm=smb_lm,fake'
'--enable-auth-digest=file,LDAP,eDirectory'
'--enable-auth-negotiate=kerberos'
'--enable-external-acl-helpers=file_userip,LDAP_group,time_quota,session,unix_group,wbinfo_group,kerberos_ldap_group'
'--enable-cache-digests'
'--enable-cachemgr-hostname=localhost'
'--enable-delay-pools'
'--enable-epoll'
'--enable-ident-lookups'
'--enable-linux-netfilter'
'--enable-removal-policies=heap,lru'
'--enable-snmp'
'--enable-ssl-crtd'
'--enable-storeio=aufs,diskd,rock,ufs'
'--enable-wccpv2'
'--enable-esi'
'--enable-ecap'
'--with-aio'
'--with-default-user=squid'
'--with-dl'
'--with-openssl'
'--with-pthreads'
'--disable-arch-native'
'build_alias=x86_64-redhat-linux-gnu'
'host_alias=x86_64-redhat-linux-gnu'
'CFLAGS=-O2 -g -pipe -Wall -Wp,-D_FORTIFY_SOURCE=2 -fexceptions -fstack-protector-strong --param=ssp-buffer-size=4 -grecord-gcc-switches   -m64 -mtune=generic -fpie'
'LDFLAGS=-Wl,-z,relro  -pie -Wl,-z,relro -Wl,-z,now'
'CXXFLAGS=-O2 -g -pipe -Wall -Wp,-D_FORTIFY_SOURCE=2 -fexceptions -fstack-protector-strong --param=ssp-buffer-size=4 -grecord-gcc-switches   -m64 -mtune=generic -fpie'
'PKG_CONFIG_PATH=:/usr/lib64/pkgconfig:/usr/share/pkgconfig'
#
```
