### 1、升级 OPENSSL 到 1.1.1v

```bash
yum -y install gcc gcc-c++ glibc make zlib zlib-devel perl pam pam-devel openssl-devel
cd /usr/local/src
curl -O https://www.openssl.org/source/openssl-1.1.1v.tar.gz
tar vxf openssl-1.1.1v.tar.gz 
cd openssl-1.1.1v/
mv /usr/bin/openssl{,-bak-$(date +%F)}
mv /usr/include/openssl{,-bak-$(date +%F)}
mv /usr/lib64/libssl.so{,-bak-$(date +%F)}
./config --prefix=/usr/local/openssl
make && make install
ln -s /usr/local/openssl/bin/openssl /usr/bin/openssl
ln -s /usr/local/openssl/include/openssl /usr/include/openssl
ln -s /usr/local/openssl/lib/libssl.so /usr/lib64/libssl.so
ln -s /usr/local/openssl/lib/libssl.so.1.1 /usr/lib64/libssl.so.1.1
ln -s /usr/local/openssl/lib/libcrypto.so.1.1 /usr/lib64/libcrypto.so.1.1
echo "/usr/local/openssl/lib" >> /etc/ld.so.conf
ldconfig -v
openssl version
```

### 2、安装 Python 3.12.0

```bash
yum -y remove python3
```

```bash
yum -y install gcc zlib zlib-devel libffi libffi-devel
```

```bash
cd /usr/local/src
curl -O https://www.python.org/ftp/python/3.12.0/Python-3.12.0.tgz
tar xvf Python-3.12.0.tgz
cd Python-3.12.0/
./configure --prefix=/usr/local/python3.12.0 --with-openssl=/usr/local/openssl --with-openssl-rpath=auto
make && make install
ln -s /usr/local/python3.12.0/bin/python3 /usr/bin/python3
ln -s /usr/local/python3.12.0/bin/pip3 /usr/bin/pip3
python3 -V
pip3 -V
```

