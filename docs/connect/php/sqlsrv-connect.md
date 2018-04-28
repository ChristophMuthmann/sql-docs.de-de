---
title: Sqlsrv_connect | Microsoft Docs
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
apiname:
- sqlsrv_connect
apitype: NA
helpviewer_keywords:
- connecting to the server
- API Reference, sqlsrv_connect
- connection pooling support
- sqlsrv_connect
ms.assetid: 37836b49-258e-45ce-9549-b8bd85d6952d
caps.latest.revision: 67
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d67d861be25e9e81c19ca9ac3a34427650101b47
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsrvconnect"></a>sqlsrv_connect
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Erstellt eine Verbindungsressource und öffnet eine Verbindung. Standardmäßig wird versucht, die Verbindung unter Verwendung der Windows-Authentifizierung herzustellen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sqlsrv_connect( string $serverName [, array $connectionInfo])  
```  
  
#### <a name="parameters"></a>Parameter  
*$serverName*: Eine Zeichenfolge, die den Namen des Servers angibt, zu dem eine Verbindung erstellt werden soll. Ein Instanzname (z. B. „MeinServer\InstanzName“) oder Port (z. B. „MeinServer, 1521“) kann als Teil dieser Zeichenfolge enthalten sein. Eine vollständige Beschreibung der Optionen für diesen Parameter, finden Sie unter Server-Schlüsselwort in der ODBC-Treiber Connection String Keywords Codeabschnitt [Using Connection String Keywords with SQL Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
Ab Version 3.0 der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]können Sie auch eine LocalDB-Instanz mit `"(localdb)\instancename"`angeben. Weitere Informationen finden Sie unter [-Unterstützung für LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md).  
  
Zusätzlich können Sie ab der Version 3.0 der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]einen virtuellen Netzwerknamen angeben, um sich mit einer AlwaysOn-Verfügbarkeitsgruppe zu verbinden. Weitere Informationen zu [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] Unterstützung für [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], finden Sie unter [Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).  
  
*$connectionInfo* [OPTIONAL]: ein assoziatives **Array** , das Verbindungsattribute enthält (z. B. **Array**("Database" = > "AdventureWorks")). Unter [Connection Options](../../connect/php/connection-options.md) finden Sie eine Liste der unterstützten Schlüssel für das Array.  
  
## <a name="return-value"></a>Rückgabewert  
Eine PHP-Verbindungsressource. Wenn eine Verbindung nicht erfolgreich erstellt und geöffnet werden kann, wird **false** zurückgegeben.  
  
## <a name="remarks"></a>Hinweise  
Wenn im optionalen *$connectionInfo* -Parameter keine Werte für die Schlüssel *UID* und *PWD* angegeben sind, wird versucht, die Verbindung mithilfe der Windows-Authentifizierung herzustellen. Weitere Informationen zur Herstellung einer Verbindung mit dem Server finden Sie unter [How to: Connect Using Windows Authentication](../../connect/php/how-to-connect-using-windows-authentication.md) und [How to: Connect Using SQL Server Authentication](../../connect/php/how-to-connect-using-sql-server-authentication.md).  
  
## <a name="example"></a>Beispiel  
Das folgende Beispiel erstellt und öffnet eine Verbindung mit Windows-Authentifizierung. Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks-Datenbank](http://www.codeplex.com/SqlServerSamples) auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
```  
<?php  
/*  
Connect to the local server using Windows Authentication and specify  
the AdventureWorks database as the database in use. To connect using  
SQL Server Authentication, set values for the "UID" and "PWD"  
 attributes in the $connectionInfo parameter. For example:  
$connectionInfo = array("UID" => $uid, "PWD" => $pwd, "Database"=>"AdventureWorks");  
*/  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if( $conn )  
{  
     echo "Connection established.\n";  
}  
else  
{  
     echo "Connection could not be established.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
//-----------------------------------------------  
// Perform operations with connection.  
//-----------------------------------------------  
  
/* Close the connection. */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)

[Connecting to the Server](../../connect/php/connecting-to-the-server.md)

[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)  
  
