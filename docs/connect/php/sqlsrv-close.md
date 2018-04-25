---
title: Sqlsrv_close | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
apiname:
- sqlsrv_close
apitype: NA
helpviewer_keywords:
- sqlsrv_close
- API Reference, sqlsrv_close
ms.assetid: 6ac6209c-a134-4f8f-b88b-8eefaa1cbc7f
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: acee29ec49e4bd0d8e303248a2a527d5697b42aa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MTE
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsrvclose"></a>sqlsrv_close
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Schließt die angegebene Verbindung und gibt die zugeordneten Ressourcen frei.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sqlsrv_close( resource $conn )  
```  
  
#### <a name="parameters"></a>Parameter  
*$conn*: Die Verbindung, die geschlossen werden soll.  
  
## <a name="return-value"></a>Rückgabewert  
Der boolesche Wert **true** , außer die Funktion wird mit einem ungültigen Parameter aufgerufen. Wenn die Funktion mit einem ungültigen Parameter aufgerufen wird, wird **false** zurückgegeben.  
  
> [!NOTE]  
> **NULL** ist ein gültiger Parameter für diese Funktion. Dadurch kann die Funktion mehrmals in einem Skript aufgerufen werden. Wenn Sie z. B. eine Verbindung in einem Fehlerzustand schließen und sie erneut am Ende des Skripts schließen, wird der zweite Aufruf von sqlsrv_close **den Wert true** zurückgeben, da der erste Aufruf von sqlsrv_close **(im Fehlerzustand) die Verbindungsressource auf NULL** setzt.  
  
## <a name="example"></a>Beispiel  
Im folgenden Beispiel wird eine Verbindung geschlossen. Das Beispiel setzt voraus, dass SQL Server auf dem lokalen Computer installiert ist. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$conn = sqlsrv_connect( $serverName);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
//-----------------------------------------------  
// Perform operations with connection here.  
//-----------------------------------------------  
  
/* Close the connection. */  
sqlsrv_close( $conn);  
echo "Connection closed.\n";  
?>  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)

[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)  
  
