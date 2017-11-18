---
title: Laden des PHP-SQL-Treibers | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cb2200b2c5d151981e9dcdf8322dd7c43b91c6ee
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="loading-the-php-sql-driver"></a>Laden des PHP-SQL-Treibers
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Dieses Thema enthält Anweisungen für das Laden der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] in den PHP verarbeitenden Speicherplatz.  
  
Es gibt zwei Optionen, um einen Treiber zu laden. Der Treiber kann geladen werden, wenn PHP gestartet wird oder während der PHP-Skriptlaufzeit.  
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>Verschieben Sie die Treiberdatei in Ihr Erweiterungsverzeichnis  
Unabhängig davon, welches Verfahren Sie verwenden, wird im ersten Schritt die Treiberdatei in einem Verzeichnis abgelegt, wo die PHP-Laufzeit sie finden kann. Legen Sie also die Treiberdatei in Ihr PHP-Erweiterungsverzeichnis. Auf [Systemanforderungen für den PHP-SQL-Treiber](../../connect/php/system-requirements-for-the-php-sql-driver.md) können Sie eine Liste der Treiberdateien abrufen, die mit dem [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]installiert werden.  
  
Geben Sie bei Bedarf den Speicherort der Treiberdatei in der PHP-Konfigurationsdatei (php.ini) an, mit der **"extension_dir"** Option. Wenn Sie beispielsweise die Treiberdatei in Ihr Verzeichnis „c:\php\ext“ einfügen, verwenden Sie diese Option:  
  
```  
extension_dir = "c:\PHP\ext"  
```  
  
## <a name="loading-the-driver-at-php-startup"></a>Laden des Treibers beim Starten von PHP  
Beim Laden der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] beim Starten von PHP, verschieben Sie zunächst eine Treiberdatei in das Erweiterungsverzeichnis. Dann führen Sie folgende Schritte aus:  
  
1.  So aktivieren Sie die **SQLSRV** -Treibers ändern **"PHP.ini"** durch die folgende Zeile den Abschnitt "Erweiterung" hinzufügen oder ändern Sie die Zeile, die bereits vorhanden ist:  
  
    Unter Windows (dieses Beispiel verwendet die Version 4.0 threadsicherer Treiber für PHP-7): 
    ```  
    extension=php_sqlsrv_7_ts.dll  
    ```  
    Unter Linux (dieses Beispiel verwendet die Version, wie vom PECL installiert): 
    ```  
    extension=sqlsrv.so  
    ```  
    So aktivieren Sie die **PDO_SQLSRV** -Treibers ändern **"PHP.ini"** durch die folgende Zeile den Abschnitt "Erweiterung" hinzufügen oder ändern Sie die Zeile, die bereits vorhanden ist:  
  
    Unter Windows (dieses Beispiel verwendet die Version 4.0 threadsicherer Treiber für PHP-7):
    ```  
    extension=php_pdo_sqlsrv_7_ts.dll  
    ```  
    Unter Linux (dieses Beispiel verwendet die Version, wie vom PECL installiert):
    ```  
    extension=pdo_sqlsrv.so  
    ```  
  
2.  Wenn Sie verwenden möchten die **PDO_SQLSRV** -Treiber verwenden, die Erweiterung PHP Data Objects (PDO) muss verfügbar sein, entweder als integrierte Erweiterung oder als dynamisch geladene Erweiterung. Wenn Sie den PDO_SQLSRV-Treiber dynamisch laden müssen, die Datei php_pdo.dll (oder pdo.so unter Linux) muss im Erweiterungsverzeichnis vorhanden sein, und die folgende Zeile muss in der Datei "PHP.ini" sein:

    Unter Windows:  
    ```
    extension=php_pdo.dll  
    ```  
    Unter Linux:  
    ```
    extension=pdo.so  
    ```  
  
3.  Starten Sie den Webserver neu.  
  
> [!NOTE]  
> Um zu bestimmen, ob der Treiber erfolgreich geladen wurde, führen Sie ein Skript aufruft [phpinfo()](http://go.microsoft.com/fwlink/?LinkId=108678).  
  
Weitere Informationen zu **php.ini** -Direktiven finden Sie unter [Beschreibung der wichtigsten php.ini-Direktiven](http://go.microsoft.com/fwlink/?LinkId=105817).  
  
## <a name="loading-the-driver-at-php-script-runtime"></a>Laden des Treibers während der PHP-Skriptlaufzeit  
Beim Laden der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] während der Skriptlaufzeit verschieben Sie zunächst eine Treiberdatei in Ihr Erweiterungsverzeichnis. Fügen Sie die folgende Zeile am Anfang des PHP-Skripts, die den Dateinamen des Treibers entspricht:  
  
```  
dl('php_pdo_sqlsrv_7_ts.dll');  
```  
  
Weitere Informationen zu PHP-Funktionen, die im Zusammenhang mit der dynamischen Laden von Erweiterungen finden Sie unter [dl](http://go.microsoft.com/fwlink/?LinkId=105818) und [Extension_loaded.](http://go.microsoft.com/fwlink/?LinkId=105819)  
  
## <a name="see-also"></a>Siehe auch  
[Erste Schritte mit dem PHP-SQL-Treiber](../../connect/php/getting-started-with-the-php-sql-driver.md)
[Systemanforderungen für den PHP-SQL-Treiber](../../connect/php/system-requirements-for-the-php-sql-driver.md)
[Programmierhandbuch für den PHP-SQL-Treiber](../../connect/php/programming-guide-for-php-sql-driver.md)
[SQLSRV-Treiber – API-Referenz](../../connect/php/sqlsrv-driver-api-reference.md)  
  

