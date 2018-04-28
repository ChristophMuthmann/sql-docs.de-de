---
title: Laden die Microsoft-Treiber für PHP für SQLServer | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: a4caa5d7b3d233bd42b5cbaec651c514de45f2cc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>Laden von Microsoft Drivers for PHP for SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Diese Seite enthält Anweisungen für das Laden der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] in den PHP verarbeitenden Speicherplatz.  
  
Sie können die vorgefertigten Treiber für Ihre Plattform aus der [Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github-Projektseite. Jedem Installationspaket enthält die SQLSRV- und PDO_SQLSRV-Treiber-Dateien in Threads und nicht-threaded Varianten. Unter Windows sind auch verfügbar in 32-Bit und 64-Bit-Varianten. Finden Sie unter [System Requirements for Microsoft Drivers for PHP for SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md) eine Liste der Treiberdateien abzurufen, die in jedem Paket enthalten sind. Der Treiberdatei muss es sich um die PHP-Version, Architektur und Threadedness Ihrer PHP-Umgebung übereinstimmen.

Auf Linux- und MacOS der Treiber können alternativ mit installiert werden PECL, wie in der [Installation Lernprogramm](../../connect/php/installation-tutorial-linux-mac.md).
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>Verschieben Sie die Treiberdatei in Ihr Erweiterungsverzeichnis  
Der Treiberdatei muss in einem Verzeichnis befinden, wo die PHP-Laufzeit sie finden kann. Es ist am einfachsten, legen die Treiberdatei in Ihr Standardwert PHP-Erweiterungsverzeichnis - suchen das Standardverzeichnis, führen Sie `php -i | sls extension_dir` unter Windows oder `php -i | grep extension_dir` auf Linux/MacOS. Wenn Sie das Standardverzeichnis für die Erweiterung nicht verwenden, geben Sie ein Verzeichnis in der PHP-Konfigurationsdatei (php.ini) an, mit der **"extension_dir"** Option. Beispielsweise unter Windows, wenn Sie die Treiberdatei, in abgelegt haben Ihrem `c:\php\ext` Verzeichnis, fügen Sie die folgende Zeile auf die Datei "PHP.ini":
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>Laden des Treibers beim Starten von PHP  
Verschieben Sie zunächst eine Treiberdatei in Ihr Erweiterungsverzeichnis, um SQLSRV-Treiber zu laden, wenn PHP gestartet wird. Dann führen Sie folgende Schritte aus:  
  
1.  So aktivieren Sie die **SQLSRV** -Treibers ändern **"PHP.ini"** durch die folgende Zeile den Abschnitt "Erweiterung" hinzufügen, ändern Sie den Dateinamen entsprechend:  
  
    Unter Windows: 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    Unter Linux, wenn Sie die vorgefertigten Binärdateien für Ihre Distribution heruntergeladen haben: 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    Wenn Sie die binäre SQLSRV aus Quelle oder mit PECL kompiliert haben, wird er stattdessen sqlsrv.so benannt werden:
    ```
    extension=sqlsrv.so
    ```
  
2.  So aktivieren Sie die **PDO_SQLSRV** -Treiber verwenden, die Erweiterung PHP Data Objects (PDO) muss verfügbar sein, entweder als integrierte Erweiterung oder als dynamisch geladene Erweiterung.

    Unter Windows stammen vorgefertigten PHP-Binärdateien mit PDO integriert, daher keine Notwendigkeit zum Ändern der Datei "PHP.ini" besteht, um diese zu laden. Wenn Sie haben jedoch kompiliert PHP aus Quelle und eine separate PDO-Erweiterung zu erstellenden angegeben, es den Namen `php_pdo.dll`, und Sie müssen in Ihr Erweiterungsverzeichnis kopieren und fügen Sie die folgende Zeile auf die Datei "PHP.ini":  
    ```
    extension=php_pdo.dll  
    ```
    Wenn Sie PHP mit Ihrem System-Paket-Manager installiert haben, wird unter Linux wahrscheinlich PDO als dynamisch geladene Erweiterung mit dem Namen pdo.so installiert. Die PDO-Erweiterung geladen werden muss, bevor Sie die PDO_SQLSRV-Erweiterung, oder das Laden fehl. Erweiterungen werden in der Regel mithilfe von einzelnen INI-Dateien geladen, und diese Dateien werden nach der Datei "PHP.ini" gelesen. Wenn pdo.so über einen eigenen INI-Datei geladen wird, ist daher eine separate Datei laden den PDO_SQLSRV-Treiber nach PDO erforderlich. 

    Um herauszufinden, welches Verzeichnis die erweiterungsspezifische INI-Dateien gespeichert sind, führen Sie `php --ini` und notieren Sie sich das Verzeichnis, die unter aufgeführten `Scan for additional .ini files in:`. Suchen Sie die Datei, die pdo.so lädt, denn es wahrscheinlich eine Zahl, z. B. 10 pdo.ini vorangestellt ist. Das numerische Präfix gibt die Ladereihenfolge von der INI-Dateien an, während Dateien, die keine numerischen Präfix sind in alphabetischer Reihenfolge geladen werden. Erstellen Sie eine Datei zum Laden Sie die PDO_SQLSRV-Treiber-Datei als 30-pdo_sqlsrv.ini (beliebige Anzahl größer ist als diejenige, die Präfixe pdo.ini Works) oder pdo_sqlsrv.ini (sofern keine Zahl pdo.ini vorangestellt ist), und fügen die folgende Zeile hinzu, ändern den Dateinamen als geeignet:  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    Als mit SQLSRV, wird Wenn Sie die binäre PDO_SQLSRV aus Quelle oder mit PECL, kompiliert haben es stattdessen pdo_sqlsrv.so benannt werden:
    ```
    extension=pdo_sqlsrv.so
    ```
    Kopieren Sie diese Datei in das Verzeichnis, das die INI-Dateien enthält. 

    Wenn Sie PHP von der Quelle mit integrierter Unterstützung für PDO kompiliert haben, Sie erfordern keine separate INI-Datei, und Sie können die entsprechende Zeile oberhalb "PHP.ini" hinzufügen.
  
3.  Starten Sie den Webserver neu.  
  
> [!NOTE]  
> Um zu bestimmen, ob der Treiber erfolgreich geladen wurde, führen Sie ein Skript aufruft [phpinfo()](http://php.net/manual/en/function.phpinfo.php).  
  
Weitere Informationen zu **"PHP.ini"** -Direktiven finden Sie unter [Beschreibung der wichtigsten php.ini-Direktiven](http://php.net/manual/en/ini.core.php).  
  
## <a name="see-also"></a>Siehe auch  
[Erste Schritte mit Microsoft-Treiber für PHP für SQLServer](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Systemanforderungen für die Microsoft-Treiber für PHP für SQLServer](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[Programmierhandbuch für den Microsoft-Treiber für PHP für SQLServer](../../connect/php/programming-guide-for-php-sql-driver.md)

[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)

[API-Referenz zum Treiber PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
