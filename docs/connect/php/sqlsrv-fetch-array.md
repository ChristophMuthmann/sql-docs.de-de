---
title: Sqlsrv_fetch_array | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- sqlsrv_fetch_array
apitype: NA
helpviewer_keywords:
- sqlsrv_fetch_array
- retrieving data, as an array
- API Reference, sqlsrv_fetch_array
ms.assetid: 69270b9e-0791-42f4-856d-412da39dea63
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 368a104bfd531e7cf9071ba1f0b5bb1ca16442b5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvfetcharray"></a>sqlsrv_fetch_array
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Gibt die nächste Datenzeile als numerisch indiziertes Array, assoziatives Array oder beides zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sqlsrv_fetch_array( resource $stmt[, int $fetchType [, row[, ]offset]])  
```  
  
#### <a name="parameters"></a>Parameter  
*$stmt*: Eine Anweisungsressource, die einer ausgeführten Anweisung entspricht.  
  
*$fetchType* [OPTIONAL]: eine vordefinierte Konstante. Dieser Parameter kann einen der in der folgenden Tabelle aufgeführten Werte annehmen:  
  
|Wert|Description|  
|---------|---------------|  
|SQLSRV_FETCH_NUMERIC|Die nächste Datenzeile wird als numerisches Array zurückgegeben.|  
|SQLSRV_FETCH_ASSOC|Die nächste Datenzeile wird als assoziatives Array zurückgegeben. Die Array-Schlüssel sind die Spaltennamen im Resultset.|  
|SQLSRV_FETCH_BOTH|Die nächste Datenzeile wird als numerisches und assoziatives Array zurückgegeben. Dies ist der Standardwert.|  
  
*Zeile* [OPTIONAL]: in Version 1.1 hinzugefügt. Einer der folgenden Werte, der spezifiziert, auf welche Zeile in einem Resultset zuzugreifen ist, welches einen bildlauffähigen Cursor verwendet: (Wenn *Zeile* angegeben wird, *Fetchtype* muss explizit angegeben werden, auch wenn Sie den Standardwert angeben.)  
  
-   SQLSRV_SCROLL_NEXT  
-   SQLSRV_SCROLL_PRIOR  
-   SQLSRV_SCROLL_FIRST  
-   SQLSRV_SCROLL_LAST  
-   SQLSRV_SCROLL_ABSOLUTE  
-   SQLSRV_SCROLL_RELATIVE  
  
Weitere Informationen zu diesen Werten finden Sie unter [Festlegen eines Cursortyps und Zeilenauswahl](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md). Unterstützung für einen bildlauffähigen Cursor wurde in Version 1.1 der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt.  
  
*Offset* [OPTIONAL]: SQLSRV_SCROLL_ABSOLUTE und sqlsrv_scroll_relative verwenden verwendet wird, um die abzurufende Zeile anzugeben. Der erste Datensatz im Resultset ist „0“.  
  
## <a name="return-value"></a>Rückgabewert  
Wenn eine Datenzeile abgerufen wird, wird ein **Array** zurückgegeben. Wenn keine weiteren Zeilen mehr abgerufen werden können, wird **NULL** zurückgegeben. Wenn ein Fehler auftritt, wird **false** zurückgegeben.  
  
Basierend auf dem Wert des *$fetchType* -Parameters, kann das zurückgegebene **Array** ein numerisch indiziertes **Array**, ein assoziatives **Array**oder beides sein. In der Standardeinstellung wird ein **Array** mit numerischen und assoziativen Schlüsseln zurückgegeben. Der Datentyp eines Werts im zurückgegebenen Array wird der PHP-Standarddatentyp sein. Informationen zu PHP-Datentypen finden Sie unter [Default PHP Data Types](../../connect/php/default-php-data-types.md).  
  
## <a name="remarks"></a>Hinweise  
Wenn eine Spalte ohne Namen zurückgegeben wird, ist der assoziative Schlüssel für das Arrayelement eine leere Zeichenfolge (""). Betrachten Sie beispielsweise diese Transact-SQL-Anweisung, die einen Wert in eine Datenbanktabelle einfügt und den vom Server generierten Primärschlüssel abruft:  
  
```
INSERT INTO Production.ProductPhoto (LargePhoto) VALUES (?);  
SELECT SCOPE_IDENTITY()
```
  
Wenn das Resultset, durch zurückgegeben die `SELECT SCOPE_IDENTITY()` -Teil dieser Anweisung wird als assoziatives Array abgerufen wird, der Schlüssel des zurückgegebenen Werts eine leere Zeichenfolge (""), da die zurückgegebene Spalte keinen Namen hat. Um dies zu vermeiden, können Sie das Ergebnis als numerisches Array abrufen oder Sie können einen Namen für die zurückgegebene Spalte in der Transact-SQL-Anweisung angeben. Im Folgenden finden Sie eine Möglichkeit, einen Spaltennamen in Transact-SQL anzugeben:  
  
```
SELECT SCOPE_IDENTITY() AS PictureID
```
  
Wenn ein Resultset mehrere Spalten ohne Namen enthält, wird der Wert der letzten unbenannten Spalte dem Schlüssel einer leeren Zeichenfolge ("") zugewiesen.  
  
## <a name="example"></a>Beispiel  
Das folgende Beispiel ruft jede Zeile eines Resultsets als assoziatives **Array**auf. Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
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
  
/* Set up and execute the query. */  
$tsql = "SELECT FirstName, LastName  
         FROM Person.Contact  
         WHERE LastName='Alan'";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false)  
{  
     echo "Error in query preparation/execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve each row as an associative array and display the results.*/  
while( $row = sqlsrv_fetch_array( $stmt, SQLSRV_FETCH_ASSOC))  
{  
      echo $row['LastName'].", ".$row['FirstName']."\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>Beispiel  
Das folgende Beispiel ruft jede Zeile eines Resultsets als numerisch indiziertes Array auf.  
  
Im Beispiel wird die Produktinformation aus der *Purchasing.PurchaseOrderDetail* Tabelle der AdventureWorks-Datenbank für Produkte mit einem angegebenen Datum und einer gelagerten Menge (*StockQty*) kleiner als ein angegebener Wert.  
  
Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
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
$tsql = "SELECT ProductID,  
                UnitPrice,  
                StockedQty   
         FROM Purchasing.PurchaseOrderDetail  
         WHERE StockedQty < 3   
         AND DueDate='2002-01-29'";  
  
/* Execute the query. */  
$stmt = sqlsrv_query( $conn, $tsql);  
if ( $stmt )  
{  
     echo "Statement executed.\n";  
}   
else   
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Iterate through the result set printing a row of data upon each  
iteration.*/  
while( $row = sqlsrv_fetch_array( $stmt, SQLSRV_FETCH_NUMERIC))  
{  
     echo "ProdID: ".$row[0]."\n";  
     echo "UnitPrice: ".$row[1]."\n";  
     echo "StockedQty: ".$row[2]."\n";  
     echo "-----------------\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
Die **sqlsrv_fetch_array** Funktion gibt immer die Daten gemäß der [Default PHP Data Types](../../connect/php/default-php-data-types.md). Weitere Informationen zur Angabe des PHP-Datentyps finden Sie unter [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
Wenn ein Feld ohne Namen abgerufen wird, ist der assoziative Schlüssel für das Arrayelement eine leere Zeichenfolge (""). Weitere Informationen finden Sie unter [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md).  
  
## <a name="see-also"></a>Siehe auch  
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)  
[Abrufen von Daten](../../connect/php/retrieving-data.md)  
[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)  
[Programmierhandbuch für den PHP-SQL-Treiber](../../connect/php/programming-guide-for-php-sql-driver.md)
  

