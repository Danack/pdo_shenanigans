Developing is working?
Developing is working?
Developing is working?
Developing is working?
Developing is working?
Developing is working?


docker-compose up mysql postgres developing --build

git@github.com:Imagick/php-src.git

cd php-src

git checkout pdo_sub_classing

./buildconf

./configure \
  --enable-mbstring \
  --without-iconv \
  --with-curl \
  --with-pdo-mysql \
  --with-pdo-pgsql \
  --with-pdo-sqlite


make install -j8

php run-tests.php ext/pdo ext/pdo_mysql/ ext/pdo_pgsql/ ext/pdo_sqlite/


psql "sslmode=disable dbname=phptest user=postgresuser host=host.docker.internal"



---------------------


PDO_DBLIB DSN examples

The following examples show a PDO_DBLIB DSN for connecting to Microsoft SQL Server and Sybase databases:

mssql:host=localhost;dbname=testdb
sybase:host=localhost;dbname=testdb
dblib:host=localhost;dbname=testdb

  --with-pdo-firebird \
  --with-pdo-dblib

--with-pdo-dblib[=DIR]  PDO: DBLIB-DB support. DIR is the FreeTDS home
--with-pdo-firebird[=DIR]
--with-pdo-mysql[=DIR]  PDO: MySQL support. DIR is the MySQL base directory.
--with-pdo-oci[=DIR]    PDO: Oracle OCI support. DIR defaults to
--with-pdo-oci=instantclient,/path/to/instant/client/lib

[=DIR]  PDO: PostgreSQL support. DIR is the PostgreSQL base
--without-pdo-sqlite    PDO: sqlite 3 support.

