
---
title: PHP Driver for SQL Serversupport for LocalDB | Microsoft Docs
ms.custom: 
ms.date: 02/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a54071c75ca4437974be7b742ee3285972850e0a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="php-driver-for-sql-server-support-for-localdb"></a>PHP Driver for SQL Server Support for LocalDB (PHP-Treiber für SQL Server-Unterstützung für LocalDB)

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Ab [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)], eine vereinfachte Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], LocalDB aufgerufen wird, werden zur Verfügung stehen. In diesem Thema wird erläutert, wie in einer LocalDB-Instanz eine Verbindung mit einer Datenbank hergestellt wird.

## <a name="remarks"></a>Hinweise

Weitere Informationen zu LocalDB, z. B. wie Sie LocalDB installieren und Konfigurieren der LocalDB-Instanz finden Sie unter der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] onlinedokumentationsthema auf [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Express LocalDB.

Zusammenfassend erlaubt LocalDB Ihnen Folgendes:

-   Verwenden Sie **sqllocaldb.exe i** , um den Namen der Standardinstanz zu ermitteln.

-   Verwenden Sie das Schlüsselwort der **AttachDBFilename** -Verbindungszeichenfolge, um anzugeben, welche Datenbankdatei der Server anfügen soll. Wenn Sie **AttachDBFilename**verwenden und den Namen der Datenbank nicht mit dem Schlüsselwort der **Database** -Verbindungszeichenfolge angeben, wird die Datenbank aus der LocalDB-Instanz entfernt, wenn die Anwendung geschlossen wird.

-   Geben Sie in der Verbindungszeichenfolge eine LocalDB-Instanz. Hier ist z. B. eine Beispielverbindungszeichenfolge für den SQLSRV:

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    Als Nächstes wird eine Beispielverbindungszeichenfolge für den PDO_SQLSRV:  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

Falls notwendig können Sie eine LocalDB-Instanz mit "sqllocaldb.exe" erstellen. Sie können auch "sqlcmd.exe" verwenden, um Datenbanken in einer LocalDB-Instanz hinzuzufügen und zu ändern. Beispiel: `sqlcmd -S (localdb)\v11.0`. (Bei Ausführung unter IIS müssen Sie für die Ausführung unter das richtige Konto erhalten dieselben Ergebnisse wie beim Ausführen der Befehlszeile; finden Sie unter [mithilfe von LocalDB mit vollständigem IIS, Teil 2: Instanz den Besitz](http://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-2-instance-ownership.aspx) für Weitere Informationen.)

Es folgen Beispiele für Verbindungszeichenfolgen mit dem SQLSRV-Treiber, die mit einer Datenbank in eine benannte Instanz, die Bezeichnung "MyInstance" LocalDB herzustellen:

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

Es folgen Beispiele für Verbindungszeichenfolgen mit dem PDO_SQLSRV-Treiber, die mit einer Datenbank in eine benannte Instanz, die Bezeichnung "MyInstance" LocalDB herzustellen:  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

Sie können LocalDB aus dem [SQL Server 2012 Feature Pack-Seite](http://go.microsoft.com/fwlink/?LinkID=236805), oder aus der [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Express Edition. Wenn Sie sqlcmd.exe verwenden, um Daten in der LocalDB-Instanz zu ändern, benötigen Sie Sqlcmd aus [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)], die Sie aus dem Download-Befehlszeilen-Hilfsprogramme in abrufen können die [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Feature Pack-Seite.

## <a name="see-also"></a>Siehe auch

[Verbinden mit dem Server](../../connect/php/connecting-to-the-server.md)

