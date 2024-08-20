# debutant recipe `oracle-instantclient`

This recipe repackages the oracle-instantclient RPM packages from 
https://www.oracle.com/de/database/technologies/instant-client/linux-x86-64-downloads.html
into Debian packages.

Without further arguments `debutant oracle-instantclient` will download and package the
[`oracle-instantclient-basic` package](https://download.oracle.com/otn_software/linux/instantclient/oracle-instantclient-basic-linuxx64.rpm).

The additional `-devel`, `-tools` and `-sqlplus` packages have to be downloaded manually:
* [devel](https://download.oracle.com/otn_software/linux/instantclient/oracle-instantclient-devel-linuxx64.rpm)
* [tools](https://download.oracle.com/otn_software/linux/instantclient/oracle-instantclient-tools-linuxx64.rpm)
* [sqlplus](https://download.oracle.com/otn_software/linux/instantclient/oracle-instantclient-sqlplus-linuxx64.rpm)

The packages are then build with `debutant oracle-instantclient <oracle-instantclient-<type>-linuxx64.rpm`.
Inbeforehand the matching `oracle-instantclient-basic` package has to be installed locally for the packaging to work.

The packaging of the -basiclight, -jdbc and -odbc packages will most probably also work but hasn't been tested.
