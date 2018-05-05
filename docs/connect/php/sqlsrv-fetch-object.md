---
title: Sqlsrv_fetch_object | Microsoft Docs
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
ms.topic: conceptual
apiname:
- sqlsrv_fetch_object
apitype: NA
helpviewer_keywords:
- sqlsrv_fetch_object
- API Reference, sqlsrv_fetch_object
- retrieving data, as an object
ms.assetid: 4ce2df2c-083a-4a4d-a1e2-e866e63707d5
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d77c725535cec8846d864fd4e85113d99892cda7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsrvfetchobject"></a>sqlsrv_fetch_object
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Ruft die nächste Datenzeile als PHP-Objekt ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sqlsrv_fetch_object( resource $stmt [, string $className [, array $ctorParams[, row[, ]offset]]])  
```  
  
#### <a name="parameters"></a>Parameter  
*$stmt*: Eine Anweisungsressource, die einer ausgeführten Anweisung entspricht.  
  
*$className* [OPTIONAL]: eine Zeichenfolge, die den Namen der zu instanziierenden Klasse angibt. Falls der Wert für den *$className* -Parameter nicht festgelegt ist, wird eine Instanz der PHP **stdClass** instanziiert.  
  
*$ctorParams* [OPTIONAL]: ein Array, das Werte enthält, übergeben wird, an den Konstruktor der Klasse angegeben, mit der *$className* Parameter. Falls der Konstruktor der angegebenen Klasse Parameterwerte akzeptiert, muss der *$ctorParams* -Parameter verwendet werden, wenn **sqlsrv_fetch_object**aufgerufen wird.  
  
*Zeile* [OPTIONAL]: einer der folgenden Werte, die Zeile spezifiziert, die auf in einem Resultset zugegriffen wird, welches einen bildlauffähigen Cursor verwendet. (Wenn *Zeile* angegeben wird, *$className* und *$ctorParams* muss explizit angegeben werden, auch wenn Sie null angeben müssen *$className*und *$ctorParams*.)  
  
-   SQLSRV_SCROLL_NEXT  
  
-   SQLSRV_SCROLL_PRIOR  
  
-   SQLSRV_SCROLL_FIRST  
  
-   SQLSRV_SCROLL_LAST  
  
-   SQLSRV_SCROLL_ABSOLUTE  
  
-   SQLSRV_SCROLL_RELATIVE  
  
Weitere Informationen zu diesen Werten finden Sie unter [Festlegen eines Cursortyps und Zeilenauswahl](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md).  
  
*Offset* [OPTIONAL]: SQLSRV_SCROLL_ABSOLUTE und sqlsrv_scroll_relative verwenden verwendet wird, um die abzurufende Zeile anzugeben. Der erste Datensatz im Resultset ist „0“.  
  
## <a name="return-value"></a>Rückgabewert  
Ein PHP-Objekt mit Eigenschaften, die zu den Feldnamen des Resultsets passen. Eigenschaftswerte werden mit den passenden Werten aus den Resultsetfeldern befüllt. Wenn die mit dem optionalen *$className* -Parameter spezifizierte Klasse nicht existiert, oder wenn es kein aktives Resultset zu der angegebenen Anweisung gibt, wird **false** zurückgegeben. Wenn keine weiteren Zeilen mehr abgerufen werden können, wird **NULL** zurückgegeben.  
  
Der Datentyp eines Werts im zurückgegebenen Objekt wird der PHP-Standarddatentyp sein. Informationen zu PHP-Standarddatentypen finden Sie unter [Default PHP Data Types](../../connect/php/default-php-data-types.md).  
  
## <a name="remarks"></a>Hinweise  
Falls ein Klassenname mit dem optionalen *$className* -Parameter festgelegt ist, wird ein Objekt diesen Klassentyps instanziiert. Falls die Klasse Eigenschaften aufweist, deren Namen zu den Namen der Resultsetfelder passen, werden die entsprechenden Resultsetwerte auf die Eigenschaften angewendet. Falls ein Resultsetfeldname mit keiner Klasseneigenschaft übereinstimmt, wird dem Objekt eine Eigenschaft mit dem Resultsetfeldnamen hinzugefügt und der Wert aus dem Resultset wird auf die Eigenschaft angewendet.  
  
Die folgenden Regeln gelten, wenn eine Klasse mit einem *$className* -Parameter spezifiziert wird:  
  
-   Beim Abgleich wird die Groß- und Kleinschreibung beachtet. So stimmt beispielsweise der Eigenschaftenname „KundenId“ nicht mit dem Feldnamen „KundenID“ überein. In diesem Fall würde dem Objekt eine „KundenID“-Eigenschaft hinzugefügt und der Wert des Feldes „KundenID“ würde an die „KundenID“-Eigenschaft gegeben werden.  
  
-   Der Abgleich erfolgt unabhängig von Zugriffsmodifizierern. Falls beispielsweise die spezifizierte Klasse eine private Eigenschaft mit demselben Namen wie ein Resultsetfeld hat, wird der Wert aus dem Resultsetfeld auf die Eigenschaft angewendet.  
  
-   Klasseneigenschaftendatentypen werden ignoriert. Falls das Feld „KundenID“ im Resultset eine Zeichenfolge, aber die „KundenID“-Eigenschaft der Klasse ein Integer-Datentyp ist, wird der Zeichenfolgewert des Resultsets auf die „KundenID“-Eigenschaft geschrieben.  
  
-   Falls die spezifizierte Klasse nicht existiert, gibt die Funktion **false** zurück und fügt der Fehlersammlung einen Fehler hinzu. Informationen zum Abrufen von Fehlerinformationen finden Sie unter [sqlsrv_errors](../../connect/php/sqlsrv-errors.md).  
  
Falls ein Feld ohne Name zurückgegeben wird, wird **sqlsrv_fetch_object** den Wert des Feldes verwerfen und eine Warnung ausgeben. Betrachten Sie beispielsweise diese Transact-SQL-Anweisung, die einen Wert in eine Datenbanktabelle einfügt und den vom Server generierten Primärschlüssel abruft:  
  
<pre>INSERT INTO Production.ProductPhoto (LargePhoto) VALUES (?);  
SELECT SCOPE_IDENTITY()</pre>  
  
Falls die Ergebnisse dieser Abfrage mit **sqlsrv_fetch_object**abgerufen werden, wird der von `SELECT SCOPE_IDENTITY()` zurückgegebene Wert verworfen und eine Warnung ausgegeben. Um dies zu vermeiden, können Sie einen Namen für das zurückgegebene Feld in der Transact-SQL-Anweisung spezifizieren. Im Folgenden finden Sie eine Möglichkeit, einen Spaltennamen in Transact-SQL anzugeben:  
  
`SELECT SCOPE_IDENTITY() AS PictureID`  
  
## <a name="example"></a>Beispiel  
Im folgenden Beispiel wird jede Zeile eines Resultsets als PHP-Objekt abgerufen. Das Beispiel setzt voraus, dass die SQL Server und die [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
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
if( $stmt === false )  
{  
     echo "Error in query preparation/execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve each row as a PHP object and display the results.*/  
while( $obj = sqlsrv_fetch_object( $stmt))  
{  
      echo $obj->LastName.", ".$obj->FirstName."\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>Beispiel  
Im folgenden Beispiel wird jede Zeile eines Resultsets als eine Instanz der im Skript definierten *Product* -Klasse abgerufen. Im Beispiel wird die Produktinformation aus der *Purchasing.PurchaseOrderDetail* und *Production.Product* Tabellen der AdventureWorks-Datenbank für Produkte mit einem angegebenen Fälligkeitsdatum ( *DueDate*), und einer gelagerten Menge (*StockQty*) kleiner als ein angegebener Wert. In diesem Beispiel sind einige der Regeln, die beim Spezifizieren einer Klasse in einem Aufruf an **sqlsrv_fetch_object**zur Anwendung kommen, noch einmal deutlich herausgestellt:  
  
-   Die *$product* -Variable ist eine Instanz der *Product* -Klasse, da „Produkt“ mit dem *$className* -Parameter spezifiziert wurde und die *Product* -Klasse existiert.  
  
-   Die *Name* -Eigenschaft wird der *$product* -Instanz hinzugefügt, da die bestehende *name* -Eigenschaft nicht übereinstimmt.  
  
-   Die *Color* -Eigenschaft wird der *$product* -Instanz hinzugefügt, weil es keine übereinstimmende Eigenschaft gibt.  
  
-   Die private Eigenschaft *UnitPrice* wird mit dem Wert aus dem *UnitPrice* -Feld aufgefüllt.  
  
Das Beispiel setzt voraus, dass SQL Server und die [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) -Datenbank auf dem lokalen Computer installiert sind. Wenn das Beispiel über die Befehlszeile ausgeführt wird, werden alle Ausgaben in die Konsole geschrieben.  
  
```  
<?php  
/* Define the Product class. */  
class Product  
{  
     /* Constructor */  
     public function Product($ID)  
     {  
          $this->objID = $ID;  
     }  
     public $objID;  
     public $name;  
     public $StockedQty;  
     public $SafetyStockLevel;  
     private $UnitPrice;  
     function getPrice()  
     {  
          return $this->UnitPrice;  
     }  
}  
  
/* Connect to the local server using Windows Authentication, and  
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
$tsql = "SELECT Name,  
                SafetyStockLevel,  
                StockedQty,  
                UnitPrice,  
                Color  
         FROM Purchasing.PurchaseOrderDetail AS pdo  
         JOIN Production.Product AS p  
         ON pdo.ProductID = p.ProductID  
         WHERE pdo.StockedQty < ?  
         AND pdo.DueDate= ?";  
  
/* Set the parameter values. */  
$params = array(3, '2002-01-29');  
  
/* Execute the query. */  
$stmt = sqlsrv_query( $conn, $tsql, $params);  
if ( $stmt )  
{  
     echo "Statement executed.\n";  
}   
else   
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Iterate through the result set, printing a row of data upon each  
 iteration. Note the following:  
     1) $product is an instance of the Product class.  
     2) The $ctorParams parameter is required in the call to  
        sqlsrv_fetch_object, because the Product class constructor is  
        explicity defined and requires parameter values.  
     3) The "Name" property is added to the $product instance because  
        the existing "name" property does not match.  
     4) The "Color" property is added to the $product instance  
        because there is no matching property.  
     5) The private property "UnitPrice" is populated with the value  
        of the "UnitPrice" field.*/  
$i=0; //Used as the $objID in the Product class constructor.  
while( $product = sqlsrv_fetch_object( $stmt, "Product", array($i)))  
{  
     echo "Object ID: ".$product->objID."\n";  
     echo "Product Name: ".$product->Name."\n";  
     echo "Stocked Qty: ".$product->StockedQty."\n";  
     echo "Safety Stock Level: ".$product->SafetyStockLevel."\n";  
     echo "Product Color: ".$product->Color."\n";  
     echo "Unit Price: ".$product->getPrice()."\n";  
     echo "-----------------\n";  
     $i++;  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
Die **sqlsrv_fetch_object** -Funktion gibt immer die Daten gemäß der [Default PHP Data Types](../../connect/php/default-php-data-types.md)aufgerufen wird. Weitere Informationen zur Angabe des PHP-Datentyps finden Sie unter [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
Falls ein Feld ohne Name zurückgegeben wird, wird **sqlsrv_fetch_object** den Wert des Feldes verwerfen und eine Warnung ausgeben. Betrachten Sie beispielsweise diese Transact-SQL-Anweisung, die einen Wert in eine Datenbanktabelle einfügt und den vom Server generierten Primärschlüssel abruft:  
  
<pre>INSERT INTO Production.ProductPhoto (LargePhoto) VALUES (?);  
SELECT SCOPE_IDENTITY()</pre>  
  
Falls die Ergebnisse dieser Abfrage mit **sqlsrv_fetch_object**abgerufen werden, wird der von `SELECT SCOPE_IDENTITY()` zurückgegebene Wert verworfen und eine Warnung ausgegeben. Um dies zu vermeiden, können Sie einen Namen für das zurückgegebene Feld in der Transact-SQL-Anweisung spezifizieren. Im Folgenden finden Sie eine Möglichkeit, einen Spaltennamen in Transact-SQL anzugeben:  
  
`SELECT SCOPE_IDENTITY() AS PictureID`  
  
## <a name="see-also"></a>Siehe auch  
[Abrufen von Daten](../../connect/php/retrieving-data.md)  

[Informationen zu den Codebeispielen in der Dokumentation](../../connect/php/about-code-examples-in-the-documentation.md)  

[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)  
  
