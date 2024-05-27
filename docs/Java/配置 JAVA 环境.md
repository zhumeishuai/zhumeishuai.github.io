## Oracle JDK 下载地址

[Java Archive | Oracle](https://www.oracle.com/java/technologies/downloads/archive/)

## 安装 JDK-8

```shell
mkdir -p /data/environment
tar xvf jdk-8u391-linux-x64.tar.gz -C /data/environment/

cat <<- 'EOF' >> /etc/profile

export JAVA_HOME=/data/environment/jdk1.8.0_391
export JRE_HOME=${JAVA_HOME}/jre
export PATH=${JAVA_HOME}/bin:$PATH
export CLASSPATH=${JAVA_HOME}/lib:${JRE_HOME}/lib
EOF

source /etc/profile
java -version
```

## 安装 JDK-11

```shell
mkdir -p /data/environment
tar -xvf jdk-11.0.22_linux-x64_bin.tar.gz -C /data/environment/

cat <<- 'EOF' >> /etc/profile

# Java-11 环境
export JAVA_HOME=/data/environment/jdk-11.0.22
export PATH=${JAVA_HOME}/bin:$PATH
export CLASSPATH=${JAVA_HOME}/lib
EOF

source /etc/profile
java -version
```

## 安装 JDK-17

```shell
mkdir -p /data/environment
tar xvf jdk-17_linux-x64_bin.tar.gz -C /data/environment/

cat <<- 'EOF' >> /etc/profile
# Java-17 环境
export JAVA_HOME=/data/environment/jdk-17.0.10
export PATH=${JAVA_HOME}/bin:$PATH
export CLASSPATH=${JAVA_HOME}/lib
EOF

source /etc/profile
java -version
```

