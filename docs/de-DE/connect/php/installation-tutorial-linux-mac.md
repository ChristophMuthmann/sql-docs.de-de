---
title: Linux und MacOS Installation-Lernprogramm für Microsoft Drivers for PHP for SQL Server | Microsoft Docs
ms.date: 04/11/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.suite: sql
ms.custom: ''
ms.technology:
- drivers
ms.topic: conceptual
author: ulvii
ms.author: v-ulibra
manager: v-mabarw
ms.openlocfilehash: c9a28604fb55c81c4fcca0df542110d6347f3ee5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="linux-and-macos-installation-tutorial-for-the-microsoft-drivers-for-php-for-sql-server"></a>Linux und MacOS Installation-Lernprogramm für Microsoft Drivers for PHP for SQL Server
Die folgenden Anweisungen gehen davon aus einer Umgebung im Grundzustand und zum Installieren von PHP 7.x, Microsoft ODBC Driver Apache und Microsoft Drivers for PHP für SQL Server auf Ubuntu 16.04 und 17.10, RedHat 7, Debian 8 und 9, Suse 12 und MacOS X 10.11 und 10.12 anzeigen. Diese Anweisungen erläutern die Verwendung von PECL Treiber installieren, aber Sie können auch die vorgefertigten Binärdateien aus Herunterladen der [Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github Projektseite und installieren Sie sie entsprechend den Anweisungen im [ Laden die Microsoft-Treiber für PHP für SQLServer](../../connect/php/loading-the-php-sql-driver.md). Eine Erläuterung der Erweiterung laden und warum wir keine die Erweiterungen "PHP.ini" hinzugefügt werden, finden Sie im Abschnitt auf [laden die Treiber](../../connect/php/loading-the-php-sql-driver.md##loading-the-driver-at-php-startup).

Diese Anweisung Install PHP 7.2 standardmäßig--finden Sie Hinweise am Anfang des Abschnitts zum Installieren von PHP 7.0 oder 7.1.

## <a name="contents-of-this-page"></a>Inhalt dieser Seite:

- [Installieren die Treiber auf Ubuntu 16.04 und 17.10](#installing-the-drivers-on-ubuntu-1604-and-1710)
- [Installieren die Treiber auf Red Hat 7](#installing-the-drivers-on-red-hat-7)
- [Installieren die Treiber auf Debian 8 und 9](#installing-the-drivers-on-debian-8-and-9)
- [Installieren die Treiber auf Suse-12](#installing-the-drivers-on-suse-12)
- [Installieren die Treiber auf MacOS El Capitan und Sierra](#installing-the-drivers-on-macos-el-capitan-and-sierra)

## <a name="installing-the-drivers-on-ubuntu-1604-and-1710"></a>Installieren die Treiber auf Ubuntu 16.04 und 17.10

> [!NOTE]
> Ersetzen Sie zum Installieren von PHP 7.0 oder 7.1 7.2 mit 7.0 oder 7.1 in den folgenden Befehlen.

### <a name="step-1-install-php"></a>Schritt 1: Installieren von PHP
```
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.2 php7.2-dev php7.2-xml -y --allow-unauthenticated
```
### <a name="step-2-install-prerequisites"></a>Schritt 2: Installieren der erforderlichen Komponenten
Installieren Sie den ODBC-Treiber für Ubuntu mithilfe der folgenden Anweisungen auf der [Linux- und MacOS Installationsseite](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Schritt 3: Installieren Sie die PHP-Treiber für Microsoft SQL Server
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Schritt 4. Apache installieren und Konfigurieren von Treiber laden
```
sudo su
apt-get install libapache2-mod-php7.2 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.2
echo "extension=sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Schritt 5. Starten Sie Apache neu, und Testen Sie das Beispielskript
```
sudo service apache2 restart
```
Um Ihre Installation testen zu können, finden Sie unter [Testen Ihrer Installation](#testing-your-installation) am Ende dieses Dokuments.

## <a name="installing-the-drivers-on-red-hat-7"></a>Installieren die Treiber auf Red Hat 7

> [!NOTE]
> Ersetzen Sie zum Installieren von PHP 7.0 oder 7.1 Remi php72 mit Remi php70 oder Remi-php71 bzw. in den folgenden Befehlen.

### <a name="step-1-install-php"></a>Schritt 1: Installieren von PHP

```
sudo su
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
wget http://rpms.remirepo.net/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum-config-manager --enable remi-php72
yum update
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```
### <a name="step-2-install-prerequisites"></a>Schritt 2: Installieren der erforderlichen Komponenten
Installieren Sie den ODBC-Treiber für Red Hat 7 mithilfe der folgenden Anweisungen auf der [Linux- und MacOS Installationsseite](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

Kompilieren die PHP-Treibern mit PECL mit PHP 7.2 erfordert eine neuere GCC als den Standardwert:
```
sudo yum-config-manager --enable rhel-server-rhscl-7-rpms
sudo yum install devtoolset-7
scl enable devtoolset-7 bash
```
### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Schritt 3: Installieren Sie die PHP-Treiber für Microsoft SQL Server
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
Ein Problem in PECL möglicherweise korrekte Installation der neuesten Version der Treiber aus, selbst wenn GCC aktualisiert haben. Klicken Sie zum Installieren der Pakete herunterladen und manuell kompilieren:
```
pecl download sqlsrv
tar xvzf sqlsrv-5.2.0.tgz
cd sqlsrv-5.2.0/
phpize
./configure --with-php-config=/usr/bin/php-config
make
sudo make install
```
Sie können alternativ die vorgefertigten Binärdateien aus der [Github-Projektseite](https://github.com/Microsoft/msphpsql/releases), oder installieren Sie über das Repository Remi:
```
sudo yum install php-sqlsrv php-pdo_sqlsrv
```
### <a name="step-4-install-apache"></a>Schritt 4. Installieren von Apache
```
sudo yum install httpd
```
SELinux wird standardmäßig installiert, und im anwenden-Modus ausgeführt wird. Damit wird für die Verbindung mit Datenbanken über SELinux Apache, führen Sie den folgenden Befehl ein:
```
sudo setsebool -P httpd_can_network_connect_db 1
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Schritt 5. Starten Sie Apache neu, und Testen Sie das Beispielskript
```
sudo apachectl restart
```
Um Ihre Installation testen zu können, finden Sie unter [Testen Ihrer Installation](#testing-your-installation) am Ende dieses Dokuments.

## <a name="installing-the-drivers-on-debian-8-and-9"></a>Installieren die Treiber auf Debian 8 und 9

> [!NOTE]
> Ersetzen Sie zum Installieren von PHP 7.0 oder 7.1 7.2 in den folgenden Befehlen durch 7.0 oder 7.1 ein.

### <a name="step-1-install-php"></a>Schritt 1: Installieren von PHP
```
sudo su
apt-get install curl apt-transport-https
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install –y php7.2 php7.2-dev php7.2-xml
```
### <a name="step-2-install-prerequisites"></a>Schritt 2: Installieren der erforderlichen Komponenten
Installieren Sie den ODBC-Treiber für Debian, mithilfe der folgenden Anweisungen auf der [Linux- und MacOS Installationsseite](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

Sie müssen möglicherweise auch das richtige Gebietsschema zum Abrufen von PHP-Ausgabe in einem Browser richtigerweise generieren zu können. Führen Sie z. B. für das UTF-8 En_US-Gebietsschema angegeben, die folgenden Befehle ein:
```
sudo su
sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen
locale-gen
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Schritt 3: Installieren Sie die PHP-Treiber für Microsoft SQL Server
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Schritt 4. Apache installieren und Konfigurieren von Treiber laden
```
sudo su
apt-get install libapache2-mod-php7.2 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.2
echo "extension=sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Schritt 5. Starten Sie Apache neu, und Testen Sie das Beispielskript
```
sudo service apache2 restart
```
Um Ihre Installation testen zu können, finden Sie unter [Testen Ihrer Installation](#testing-your-installation) am Ende dieses Dokuments.

## <a name="installing-the-drivers-on-suse-12"></a>Installieren die Treiber auf Suse-12

> [!NOTE]
> Zum Installieren von PHP 7.0 ist "Skip" den folgenden Befehl die Repository - 7.0 Hinzufügen der PHP-Standard für Suse 12.
> Ersetzen Sie zum Installieren von PHP 7.1 die Repository-URL im folgenden mit dem folgenden URL ein: `http://download.opensuse.org/repositories/devel:/languages:/php:/php71/SLE_12/devel:languages:php:php71.repo`

### <a name="step-1-install-php"></a>Schritt 1: Installieren von PHP
```
sudo su
zypper -n ar -f http://download.opensuse.org/repositories/devel:languages:php/SLE_12/devel:languages:php.repo
zypper --gpg-auto-import-keys refresh
zypper -n install php7 php7-pear php7-devel
```
### <a name="step-2-install-prerequisites"></a>Schritt 2: Installieren der erforderlichen Komponenten
Installieren Sie den ODBC-Treiber für Suse 12 mithilfe der folgenden Anweisungen auf der [Linux- und MacOS Installationsseite](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Schritt 3: Installieren Sie die PHP-Treiber für Microsoft SQL Server
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Schritt 4. Apache installieren und Konfigurieren von Treiber laden
```
sudo su
zypper install apache2 apache2-mod_php7
a2enmod php7
echo "extension=sqlsrv.so" >> /etc/php7/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php7/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Schritt 5. Starten Sie Apache neu, und Testen Sie das Beispielskript
```
sudo systemctl restart apache2
```
Um Ihre Installation testen zu können, finden Sie unter [Testen Ihrer Installation](#testing-your-installation) am Ende dieses Dokuments.

## <a name="installing-the-drivers-on-macos-el-capitan-and-sierra"></a>Installieren die Treiber auf MacOS El Capitan und Sierra

Wenn Sie es noch nicht, installieren Sie Kaffee wie folgt:
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> [!NOTE]
> Ersetzen Sie zum Installieren von PHP 7.0 oder 7.1 php@7.2 mit php@7.0 oder php@7.1 bzw. in den folgenden Befehlen.

### <a name="step-1-install-php"></a>Schritt 1: Installieren von PHP

```
brew tap
brew tap homebrew/core
brew install php@7.2
```
PHP sollte jetzt in Ihrem Pfad--ausführen `php -v` , stellen Sie sicher, dass Sie die richtige Version von PHP ausgeführt werden. Wenn PHP nicht in Ihrem Pfad ist, oder es nicht die richtige Version ist, führen Sie die folgenden Schritte aus:
```
brew link --force --overwrite php@7.2
```

### <a name="step-2-install-prerequisites"></a>Schritt 2: Installieren der erforderlichen Komponenten
Installieren Sie den ODBC-Treiber für MacOS mithilfe der folgenden Anweisungen auf der [Linux- und MacOS Installationsseite](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

Darüber hinaus müssen Sie möglicherweise die GNU stellen Tools zu installieren:
```
brew install autoconf automake libtool
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Schritt 3: Installieren Sie die PHP-Treiber für Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Schritt 4. Apache installieren und Konfigurieren von Treiber laden
```
brew install apache2
```
Führen Sie zur der Apache-Konfigurationsdatei für die Apache-installation 
```
apachectl -V | grep SERVER_CONFIG_FILE
``` 
und Ersetzen Sie den Pfad für `httpd.conf` in den folgenden Befehlen:
```
echo "LoadModule php7_module /usr/local/opt/php@7.2/lib/httpd/modules/libphp7.so" >> /usr/local/etc/httpd/httpd.conf
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/httpd/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Schritt 5. Starten Sie Apache neu, und Testen Sie das Beispielskript
```
sudo apachectl restart
```
Um Ihre Installation testen zu können, finden Sie unter [Testen Ihrer Installation](#testing-your-installation) am Ende dieses Dokuments.

## <a name="testing-your-installation"></a>Testen Ihrer Installation

Um dieses Beispielskript zu testen, erstellen Sie eine Datei namens testsql.php in Ihrem System Dokumentenstamm. Dies ist `/var/www/html/` auf Debian, Ubuntu und Redhat, `/srv/www/htdocs` auf SUSE oder `/usr/local/var/www` auf MacOS. Kopieren Sie das folgende Skript aus, und Ersetzen Sie dabei die Server, Datenbank, Benutzername und Kennwort nach Bedarf.
```
<?php
$serverName = "yourServername";
$connectionOptions = array(
    "Database" => "yourDatabase",
    "Uid" => "yourUsername",
    "PWD" => "yourPassword"
);

//Establishes the connection
$conn = sqlsrv_connect($serverName, $connectionOptions);
if( $conn === false ) {
    die( FormatErrors( sqlsrv_errors()));
}

//Select Query
$tsql= "SELECT @@Version as SQL_VERSION";

//Executes the query
$getResults= sqlsrv_query($conn, $tsql);

//Error handling
if ($getResults == FALSE)
    die(FormatErrors(sqlsrv_errors()));
?>

<h1> Results : </h1>

<?php
while ($row = sqlsrv_fetch_array($getResults, SQLSRV_FETCH_ASSOC)) {
    echo ($row['SQL_VERSION']);
    echo ("<br/>");
}

sqlsrv_free_stmt($getResults);

function FormatErrors( $errors )
{
    /* Display errors. */
    echo "Error information: <br/>";
    foreach ( $errors as $error )
    {
        echo "SQLSTATE: ".$error['SQLSTATE']."<br/>";
        echo "Code: ".$error['code']."<br/>";
        echo "Message: ".$error['message']."<br/>";
    }
}
?>
```
Zeigen Sie im Browser zur http://localhost/testsql.php (http://localhost:8080/testsql.php auf Mac OS). Sie sollten jetzt mit Ihrer SQL Server/Azure SQL-Datenbank herstellen können.

## <a name="see-also"></a>Siehe auch  
[Erste Schritte mit Microsoft-Treiber für PHP für SQLServer](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Laden die Microsoft-Treiber für PHP für SQLServer](../../connect/php/loading-the-php-sql-driver.md)

[Systemanforderungen für die Microsoft-Treiber für PHP für SQLServer](../../connect/php/system-requirements-for-the-php-sql-driver.md)
