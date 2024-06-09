

\## <p align="center">How to Compiling and installing postgis 3.4.2 from source in Rocky Linux 9.4 and PostgreSQL 16.3</p>



#### 1、Compiling and installing postgis 3.4.2 from source

```sql
 PostGIS is now configured for x86_64-pc-linux-gnu

 -------------- Compiler Info -------------
  C compiler:           gcc -std=gnu99 -g -O2 -fno-math-errno -fno-signed-zeros -Wall
  C++ compiler (Wagyu): gcc -std=c++11 -x c++
  C++ compiler (FlatGeobuf): gcc -std=c++11 -x c++
  CPPFLAGS:              -I/usr/local/include   -I/usr/include/libxml2 -I/usr/local/include -I/usr/local/include/json-c   -DNDEBUG
  LDFLAGS:               -lm
  SQL preprocessor:     /usr/bin/cpp -traditional-cpp -w -P -Upixel -Ubool
  Archiver:             gcc-ar rs

 -------------- Additional Info -------------
  Interrupt Tests:   ENABLED

 -------------- Dependencies --------------
  GEOS config:          /usr/local/bin/geos-config
  GEOS version:         3.12.2
  GDAL config:          /usr/local/bin/gdal-config
  GDAL version:         3.9.0
  SFCGAL config:        /usr/local/bin/sfcgal-config
  SFCGAL version:       1.5.1
  PostgreSQL config:    /postgresql/app/pg163/bin/pg_config
  PostgreSQL version:   PostgreSQL 16.3
  PROJ4 version:        93
  Libxml2 config:       /usr/bin/xml2-config
  Libxml2 version:      2.9.13
  JSON-C support:       yes
  protobuf support:     yes
  protobuf-c version:   1005000
  PCRE support:         Version 2
  Perl:                 /usr/bin/perl

 --------------- Extensions ---------------
  PostgreSQL EXTENSION support:       enabled
  PostGIS Raster:                     enabled
  PostGIS Topology:                   enabled
  SFCGAL support:                     enabled
  Address Standardizer support:       enabled

 -------- Documentation Generation --------
  xsltproc:             /usr/bin/xsltproc
  xsl style sheets:     /usr/share/sgml/docbook/xsl-stylesheets
  dblatex:
  convert:
  mathml2.dtd:          http://www.w3.org/Math/DTD/mathml2/mathml2.dtd

[root@pgdb01 postgis-3.4.2]# make
...
PostGIS was built successfully. Ready to install.

[root@pgdb01 postgis-3.4.2]# make install
```



#### 2、check

```sql
[root@pgdb01 ~]# cat /etc/rocky-release
Rocky Linux release 9.4 (Blue Onyx)

[root@pgdb01 ~]# su - postgres
[postgres@pgdb01:/home/postgres]$psql pgis
psql (16.3)
Type "help" for help.

pgis=# SELECT name, default_version,installed_version FROM pg_available_extensions WHERE name LIKE 'postgis%' or name LIKE 'address%';
             name             | default_version | installed_version
------------------------------+-----------------+-------------------
 postgis_raster               | 3.4.2           | 3.4.2
 postgis_tiger_geocoder       | 3.4.2           | 3.4.2
 postgis_topology             | 3.4.2           | 3.4.2
 address_standardizer         | 3.4.2           | 3.4.2
 postgis_sfcgal               | 3.4.2           | 3.4.2
 address_standardizer_data_us | 3.4.2           | 3.4.2
 postgis                      | 3.4.2           | 3.4.2
(7 rows)

pgis=# \dx
                                                                       List of installed extensions
             Name             | Version |   Schema   |                                                     Description
------------------------------+---------+------------+---------------------------------------------------------------------------------------------------------------------
 address_standardizer         | 3.4.2   | public     | Used to parse an address into constituent elements. Generally used to support geocoding address normalization step.
 address_standardizer_data_us | 3.4.2   | public     | Address Standardizer US dataset example
 fuzzystrmatch                | 1.2     | public     | determine similarities and distance between strings
 plpgsql                      | 1.0     | pg_catalog | PL/pgSQL procedural language
 postgis                      | 3.4.2   | public     | PostGIS geometry and geography spatial types and functions
 postgis_raster               | 3.4.2   | public     | PostGIS raster types and functions
 postgis_sfcgal               | 3.4.2   | public     | PostGIS SFCGAL functions
 postgis_tiger_geocoder       | 3.4.2   | tiger      | PostGIS tiger geocoder and reverse geocoder
 postgis_topology             | 3.4.2   | topology   | PostGIS topology spatial types and functions
```

