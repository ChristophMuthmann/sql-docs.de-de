---
title: Unterstützung für LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.reviewer: ''
ms.suite: sql
ms.prod_service: drivers
ms.component: php
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9315847a8e36520b360d16681ffe5b00f08d6975
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="support-for-localdb"></a>Unterstützung für LocalDB

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

LocalDB ist eine vereinfachte Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] die ist seit verfügbaren [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]. In diesem Thema wird erläutert, wie in einer LocalDB-Instanz eine Verbindung mit einer Datenbank hergestellt wird.

## <a name="remarks"></a>Hinweise

Weitere Informationen zu LocalDB, z. B. wie Sie LocalDB installieren und Konfigurieren der LocalDB-Instanz finden Sie unter der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] onlinedokumentationsthema auf [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Express LocalDB.

Kurz gesagt, erlaubt LocalDB Ihnen Folgendes:

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

Anleitungen zum Installieren von LocalDB finden Sie unter der [LocalDB Dokumentation](../../database-engine/configure-windows/sql-server-2016-express-localdb.md). Wenn Sie sqlcmd.exe verwenden, um Daten in der LocalDB-Instanz zu ändern, müssen Sie die [Hilfsprogramms "Sqlcmd"](../../tools/sqlcmd-utility.md).

## <a name="see-also"></a>Siehe auch

[Verbinden mit dem Server](../../connect/php/connecting-to-the-server.md)
