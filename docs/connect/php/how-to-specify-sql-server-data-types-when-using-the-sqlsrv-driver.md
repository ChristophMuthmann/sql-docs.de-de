---
title: 'Vorgehensweise: Angeben von SQL Server-Datentypen bei Verwendung des SQLSRV-Treibers | Microsoft Docs'
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
helpviewer_keywords:
- converting data types
- streaming data
ms.assetid: 1fcf73cb-5634-4d89-948f-9326f1dbd030
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f7e10688144a78d7ab897d0d4354e49b7bb2e26e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="how-to-specify-sql-server-data-types-when-using-the-sqlsrv-driver"></a>Vorgehensweise: Angeben von SQL Server-Datentypen, wenn der SQLSRV-Treiber verwendet wird.
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

In diesem Thema wird veranschaulicht, wie der SQLSRV-Treiber verwendet wird, um den SQL Server-Datentyp für Daten anzugeben, die an den Server gesendet werden. Dieses Thema gilt nicht, wenn der PDO_SQLSRV-Treiber verwendet wird.  
  
Um den SQL Server-Datentyp anzugeben, müssen Sie das optionale *$params* -Array verwenden, wenn Sie eine Abfrage, die Daten einfügt oder aktualisiert, vorbereiten oder ausführen möchten. Weitere Informationen zur Struktur und Syntax des *$params* -Arrays, finden Sie unter [sqlsrv_query](../../connect/php/sqlsrv-query.md) oder [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
Die folgenden Schritte fassen zusammen, wie der SQL Server-Datentyp angegeben wird, wenn Daten an den Server gesendet werden:  
  
> [!NOTE]  
> Wenn kein SQL Server-Datentyp angegeben ist, werden die Standardtypen verwendet. Informationen zu den SQL Server-Standarddatentypen finden Sie unter [Default SQL Server Data Types](../../connect/php/default-sql-server-data-types.md).  
  
1.  Definieren Sie eine Transact-SQL-Abfrage, die Daten einfügt oder aktualisiert. Verwenden Sie das Fragezeichen (?) als Platzhalter für Parameterwerte in der Abfrage.  
  
2.  Initialisieren oder aktualisieren Sie PHP-Variablen, die den Platzhaltern in der Transact-SQL-Abfrage entsprechen.  
  
3.  Erstellen Sie das *$params* -Array, das beim Vorbereiten oder Ausführen der Abfrage verwendet werden soll. Beachten Sie, dass jedes Element des *$params* -Arrays auch ein Array sein muss, wenn Sie den SQL Server-Datentyp angeben.  
  
4.  Geben Sie die gewünschte SQL Server-Datentyp mit der entsprechenden **SQLSRV_SQLTYPE_\***  -Konstanten als vierten Parameter in jedes Teilarray von der *$params* Array. Eine vollständige Liste der **SQLSRV_SQLTYPE_\***  -Konstanten finden Sie im Abschnitt SQLTYPEs von [Konstanten &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md). Im folgenden Code werden z. B. *$changeDate*, *$rate*, und *$payFrequency* jeweils als die SQL Server-Datentypen **datetime**, **money**, und **tinyint** im *$params* -Array angegeben. Da kein SQL Server-Typ für *$employeeId* angegeben ist, und da er mit einem Integer initialisiert wird, wird der  SQL Server-Standardtyp **integer** verwendet.  
  
    ```  
    $employeeId = 5;  
    $changeDate = "2005-06-07";  
    $rate = 30;  
    $payFrequency = 2;  
    $params = array(  
                array($employeeId, null),  
                array($changeDate, null, null, SQLSRV_SQLTYPE_DATETIME),  
                array($rate, null, null, SQLSRV_SQLTYPE_MONEY),  
                array($payFrequency, null, null, SQLSRV_SQLTYPE_TINYINT)  
              );  
    ```  
  
## <a name="example"></a>Beispiel  
Das folgende Beispiel fügt Daten in die *HumanResources.EmployeePayHistory* Tabelle der AdventureWorks-Datenbank. SQL Server-Datentypen werden für die Parameter *$changeDate*, *$rate*, und *$payFrequency* angegeben. Für den Parameter *$employeeId* wird der SQL Server-Standardtyp verwendet. Um sicherzustellen, dass die Daten erfolgreich eingefügt wurden, werden dieselben Daten abgerufen und angezeigt.  
  
In diesem Beispiel wird vorausgesetzt, dass SQL Server und die [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
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
  
/* Define the query. */  
$tsql1 = "INSERT INTO HumanResources.EmployeePayHistory (EmployeeID,  
                                                        RateChangeDate,  
                                                        Rate,  
                                                        PayFrequency)  
           VALUES (?, ?, ?, ?)";  
  
/* Construct the parameter array. */  
$employeeId = 5;  
$changeDate = "2005-06-07";  
$rate = 30;  
$payFrequency = 2;  
$params1 = array(  
               array($employeeId, null),  
               array($changeDate, null, null, SQLSRV_SQLTYPE_DATETIME),  
               array($rate, null, null, SQLSRV_SQLTYPE_MONEY),  
               array($payFrequency, null, null, SQLSRV_SQLTYPE_TINYINT)  
           );  
  
/* Execute the INSERT query. */  
$stmt1 = sqlsrv_query($conn, $tsql1, $params1);  
if( $stmt1 === false )  
{  
     echo "Error in execution of INSERT.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve the newly inserted data. */  
/* Define the query. */  
$tsql2 = "SELECT EmployeeID, RateChangeDate, Rate, PayFrequency  
          FROM HumanResources.EmployeePayHistory  
          WHERE EmployeeID = ? AND RateChangeDate = ?";  
  
/* Construct the parameter array. */  
$params2 = array($employeeId, $changeDate);  
  
/*Execute the SELECT query. */  
$stmt2 = sqlsrv_query($conn, $tsql2, $params2);  
if( $stmt2 === false )  
{  
     echo "Error in execution of SELECT.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the results. */  
$row = sqlsrv_fetch_array( $stmt2 );  
if( $row === false )  
{  
     echo "Error in fetching data.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
echo "EmployeeID: ".$row['EmployeeID']."\n";  
echo "Change Date: ".date_format($row['RateChangeDate'], "Y-m-d")."\n";  
echo "Rate: ".$row['Rate']."\n";  
echo "PayFrequency: ".$row['PayFrequency']."\n";  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt($stmt1);  
sqlsrv_free_stmt($stmt2);  
sqlsrv_close($conn);  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[Abrufen von Daten](../../connect/php/retrieving-data.md)

[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)

[Gewusst wie: Festlegen von PHP-Datentypen](../../connect/php/how-to-specify-php-data-types.md)

[Konvertieren von Datentypen](../../connect/php/converting-data-types.md)

[Vorgehensweise: Senden und Abrufen von UTF-8-Daten mithilfe der integrierten UTF-8-Unterstützung](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)  
  
