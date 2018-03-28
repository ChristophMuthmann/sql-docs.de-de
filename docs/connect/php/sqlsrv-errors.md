---
title: Sqlsrv_errors | Microsoft Docs
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
- sqlsrv_errors
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_errors
- sqlsrv_errors
- errors and warnings
ms.assetid: d1fcffec-f34f-46de-9a0e-343f3b5dbae2
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 439ea8c2730f777bc531d03a2db00b3ba54021e3
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="sqlsrverrors"></a>sqlsrv_errors
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Gibt erweiterte Fehler führen, und/oder Warnungsinformationen zu den letzten **Sqlsrv** Vorgang ausgeführt.  
  
Die **Sqlsrv_errors** Funktion kann durch Aufrufen dieser mit einem der Parameterwerte, die im Abschnitt Parameter angegebenen Fehler führen, und/oder Warnungsinformationen zurückgeben.  
  
Standardmäßig werden Warnungen, die bei einem Aufruf einer **sqlsrv** -Funktion generiert werden, als Fehler behandelt. Wenn eine Warnung bei einem Aufruf einer **sqlsrv** -Funktion auftritt, gibt die Funktion „false“ zurück. Jedoch werden Warnungen, die den SQLSTATE-Werten 01000, 01001, 01003 und 01S02 entsprechen, nie als Fehler behandelt.  
  
Die folgende Codezeile deaktiviert das oben genannte Verhalten. Eine Warnung, die durch einen Aufruf einer **sqlsrv** -Funktion generiert wurde, führt nicht dazu, dass die Funktion „false“ zurückgibt:  
  
```  
sqlsrv_configure("WarningsReturnAsErrors", 0);  
```  
  
Die folgende Codezeile aktiviert wieder das Standardverhalten; Warnungen (mit Ausnahmen wie oben beschrieben) werden als Fehler behandelt:  
  
```  
sqlsrv_configure("WarningsReturnAsErrors", 1);  
```  
  
Unabhängig von der Einstellung können Warnungen nur durch den Aufruf abgerufen werden **Sqlsrv_errors** entweder mit der **SQLSRV_ERR_ALL** oder **SQLSRV_ERR_WARNINGS** Parameterwert (Siehe Im Parameterabschnitt unten).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sqlsrv_errors( [int $errorsAndOrWarnings] )  
```  
  
#### <a name="parameters"></a>Parameter  
*$errorsAndOrWarnings*[OPTIONAL]: eine vordefinierte Konstante. Dieser Parameter kann einen der in der folgenden Tabelle aufgeführten Werte annehmen:  
  
|Wert|Description|  
|---------|---------------|  
|SQLSRV_ERR_ALL|Fehler und Warnungen, die beim letzten **sqlsrv** -Funktionsaufruf generiert wurden, werden zurückgegeben.|  
|SQLSRV_ERR_ERRORS|Fehler und Warnungen aus dem letzten **sqlsrv** -Funktionsaufruf werden zurückgegeben.|  
|SQLSRV_ERR_WARNINGS|Warnungen aus dem letzten **sqlsrv** -Funktionsaufruf werden zurückgegeben.|  
  
Wenn kein Parameterwert angegeben wird, werden Fehler und Warnungen zurückgegeben, die durch den letzten **sqlsrv** -Funktionsaufruf generiert wurden.  
  
## <a name="return-value"></a>Rückgabewert  
Ein **Array** von Arrays oder **NULL**. Jede **Array** im zurückgegebenen **Array** enthält drei Schlüssel-Wert-Paaren. In der folgenden Tabelle wird jeder Schlüssel und dessen Beschreibung aufgelistet.  
  
|Key|Description|  
|-------|---------------|  
|SQLSTATE|Für Fehler, die aus dem ODBC-Treiber stammen, wird von ODBC der Wert SQLSTATE zurückgegeben Weitere Informationen zu SQLSTATE-Werten für ODBC, finden Sie unter [ODBC-Fehlercodes](../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md).<br /><br />Für Fehler, die aus den [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]stammen, ein SQLSTATE von IMSSP<br /><br />Für Warnungen, die aus den [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]stammen, ein SQLSTATE von 01SSP|  
|Code|Für Fehler, die vom SQL Server stammen, den systemeigenen SQL Server-Fehlercode<br /><br />Für Fehler, die aus dem ODBC-Treiber stammen, wird von ODBC der Fehlercode zurückgegeben<br /><br />Für Fehler, die aus den [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]oder dem [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] -Fehlercode stammen Weitere Informationen finden Sie unter [Handling Errors and Warnings](../../connect/php/handling-errors-and-warnings.md).|  
|message|Eine Beschreibung des Fehlers|  
  
Auf die Arraywerte kann auch mit den numerischen Schlüsseln 0, 1 und 2 zugegriffen werden. Wenn keine Fehler oder Warnungen auftreten, wird **NULL** zurückgegeben.  
  
## <a name="example"></a>Beispiel  
Das folgende Beispiel zeigt auftretende Fehler, die während einer fehlgeschlagene Anweisungsausführung entstehen. (Die Anweisung schlägt fehl, da **InvalidColumName** ist kein gültiger Spaltenname in der angegebenen Tabelle.) Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
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
  
/* Set up a query to select an invalid column name. */  
$tsql = "SELECT InvalidColumnName FROM Sales.SalesOrderDetail";  
  
/* Attempt execution. */  
/* Execution will fail because of the invalid column name. */  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
      if( ($errors = sqlsrv_errors() ) != null)  
      {  
         foreach( $errors as $error)  
         {  
            echo "SQLSTATE: ".$error[ 'SQLSTATE']."\n";  
            echo "code: ".$error[ 'code']."\n";  
            echo "message: ".$error[ 'message']."\n";  
         }  
      }  
}  
  
/* Free connection resources */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)

[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)  
  
