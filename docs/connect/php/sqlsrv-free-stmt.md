---
title: Sqlsrv_free_stmt | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- sqlsrv_free_stmt
apitype: NA
helpviewer_keywords:
- sqlsrv_free_stmt
- API Reference, sqlsrv_free_stmt
ms.assetid: 3c71f432-36ad-41e1-8ac7-587c82539448
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2debeb602c6432a273ae194dd2715a8e8d5239bd
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="sqlsrvfreestmt"></a>sqlsrv_free_stmt
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Gibt alle der angegebenen Anweisung zugeordneten Ressourcen frei. Die Anweisung kann nicht erneut verwendet werden, nachdem diese Funktion aufgerufen wurde.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sqlsrv_free_stmt( resource $stmt)  
```  
  
#### <a name="parameters"></a>Parameter  
*$stmt*: Die Anweisung, die geschlossen werden soll.  
  
## <a name="return-value"></a>Rückgabewert  
Der boolesche Wert **true** , außer die Funktion wird mit einem ungültigen Parameter aufgerufen. Wenn die Funktion mit einem ungültigen Parameter aufgerufen wird, wird **false** zurückgegeben.  
  
> [!NOTE]  
> **NULL** ist ein gültiger Parameter für diese Funktion. Dadurch kann die Funktion mehrmals in einem Skript aufgerufen werden. Beispielsweise, wenn Sie eine Anweisung in einem Fehlerzustand freigeben und sie erneut am Ende des Skripts, der zweite Aufruf von **Sqlsrv_free_stmt** zurück **"true"** , da der erste Aufruf von **Sqlsrv_ Free_stmt** (im Fehlerzustand) Sie die Verbindungsressource auf **null**.  
  
## <a name="example"></a>Beispiel  
Das folgende Beispiel erstellt eine Anwendungsressource, führt eine einfache Abfrage durch und ruft **sqlsrv_free_stmt** auf, um alle der Anweisung zugeordneten Ressourcen freizugeben. Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
$stmt = sqlsrv_query( $conn, "SELECT * FROM Person.Contact");  
if( $stmt )  
{  
     echo "Statement executed.\n";  
}  
else  
{  
     echo "Query could not be executed.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/*-------------------------------  
     Process query results here.  
-------------------------------*/  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)  

[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)  

[sqlsrv_cancel](../../connect/php/sqlsrv-cancel.md)  
  
