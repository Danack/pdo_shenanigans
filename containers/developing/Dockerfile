FROM debian:11-slim

USER root

# Get Debian up-to-date
RUN apt-get update -qq \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    apt-transport-https autoconf bison bsdmainutils ca-certificates curl \
    gcc git gnupg lsb-release make pkg-config re2c wget \
    libpng-dev libjpeg-dev ghostscript libxml2-dev libfreetype6-dev \
    libonig-dev  libcurl4-openssl-dev libwebp-dev vim \
    strace valgrind libtiff5-dev libfftw3-dev libde265-dev libheif-dev \
    libssl-dev libzip-dev unzip libpq-dev mycli libsqlite3-dev libsqlite3-mod-spatialite \
    inetutils-ping postgresql-contrib \
    # PDO_DBLIB dependencies
    freetds-dev freetds-bin \
    # PDO_ODBC dependencies
    unixodbc-dev \
    # Needed to set up MySQL's ODBC packages
    dpkg-dev \
    # PDO_FIREBIRD dependencies
    firebird-dev \
    # PDO_OCI dependencies
    libaio1

# Install ODBC connector for MySQL
RUN set -eux; \
    cd /tmp; \
    wget https://dev.mysql.com/get/Downloads/Connector-ODBC/8.0/mysql-connector-odbc-8.0.33-linux-glibc2.28-aarch64.tar.gz; \
    tar xf mysql-connector-odbc-8.0.33-linux-glibc2.28-aarch64.tar.gz; \
    cd mysql-connector-odbc-8.0.33-linux-glibc2.28-aarch64; \
    cp bin/* /usr/local/bin; \
    cp lib/* /usr/local/lib; \
    cd /tmp; \
    rm -rf /tmp/mysql-connector-odbc-8.0.33-linux-glibc2.28-aarch64; \
    myodbc-installer -a -d -n "MySQL ODBC 8.0 Unicode Driver" -t "Driver=/usr/local/lib/libmyodbc8w.so"; \
    myodbc-installer -a -d -n "MySQL ODBC 8.0 ANSI Driver" -t "Driver=/usr/local/lib/libmyodbc8a.so";

# Install Oracle client SDK
# This doesn't work on arm
#RUN set -eux; \
#    mkdir -p /opt/oracle; \
#    cd /opt/oracle; \
#    wget https://download.oracle.com/otn_software/linux/instantclient/2110000/instantclient-basic-linux.x64-21.10.0.0.0dbru.zip; \
#    wget https://download.oracle.com/otn_software/linux/instantclient/2110000/instantclient-sdk-linux.x64-21.10.0.0.0dbru.zip; \
#    unzip instantclient-basic-linux.x64-21.10.0.0.0dbru.zip; \
#    unzip instantclient-sdk-linux.x64-21.10.0.0.0dbru.zip; \
#    echo /opt/oracle/instantclient_21_10 > /etc/ld.so.conf.d/oracle-instantclient.conf; \
#    ln -s /opt/oracle/instantclient_21_10 /opt/oracle/instantclient; \
#    ldconfig;

# Make the default directory a useful one
WORKDIR /var/app

CMD tail -f -n 1000 /var/app/README.md

