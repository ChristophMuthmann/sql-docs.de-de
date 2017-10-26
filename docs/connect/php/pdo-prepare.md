---
title: 'PDO:: Prepare | Microsoft Docs'
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a8b16fdc-c748-49be-acf2-a6ac7432d16b
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7a83fabca6866e8e3b106d8696ef03514a93aa62
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="pdoprepare"></a>PDO::prepare
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Bereitet eine Anweisung für die Ausführung vor.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
PDOStatement PDO::prepare ( $statement [, array(key_pair)] )  
```  
  
#### <a name="parameters"></a>Parameter  
$*statement*: Eine Zeichenfolge, die die SQL-Anweisung enthält.  
  
*Key_pair*: ein Array, das einen Attributnamen und Wert enthält. Weitere Informationen finden Sie im Abschnitt zu den Hinweisen.  
  
## <a name="return-value"></a>Rückgabewert  
Bei Erfolg wird ein PDOStatement-Objekt zurückgegeben. Bei einem Fehler wird entweder ein PDOException-Objekt oder „false“ zurückgegeben, abhängig vom Wert für PDO::ATTR_ERRMODE.  
  
## <a name="remarks"></a>Hinweise  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] wertet keine vorbereiteten Anweisungen vor der Ausführung aus.  
  
Die folgende Tabelle enthält die möglichen *Key_pair* Werte.  
  
|Key|Description|  
|-------|---------------|  
|PDO::ATTR_CURSOR|Definiert das Cursorverhalten. Der Standardwert ist „PDO::CURSOR_FWDONLY“. Mit „PDO::CURSOR_SCROLL“ ist der Cursor statisch.<br /><br />Beispiel: `array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY )`.<br /><br />Wenn Sie „PDO::CURSOR_SCROLL“ verwenden, können wie nachstehend beschrieben Sie auch „PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE“ verwenden.<br /><br />Finden Sie unter [Cursortypen &#40; PDO_SQLSRV-Treiber &#41; ](../../connect/php/cursor-types-pdo-sqlsrv-driver.md) für Weitere Informationen zu Resultsets und Cursorn im PDO_SQLSRV-Treiber.|  
|PDO::ATTR_EMULATE_PREPARES|Wenn PDO:: attr_emulate_prepares aktiviert ist, wird die Platzhalter in einer vorbereiteten Anweisung von gebundenen Parametern ersetzt. Eine vollständige SQL-Anweisung mit keine Platzhalter wird dann auf die Datenbank beim Ausführen gesendet. <br /><br />PDO:: attr_emulate_prepares kann verwendet werden, um einige Einschränkungen in SQL Server zu umgehen. SQL Server unterstützt beispielsweise keine benannten oder positionellen Parameter in einige Transact-SQL-Klauseln. Darüber hinaus muss SQL Server maximal 2100 Bindungsparameter.<br /><br />Sie können das PDO:: attr_emulate_prepares-Attribut auf "true" festlegen. Beispiel:<br /><br />`PDO::ATTR_EMULATE_PREPARES => true`<br /><br />Standardmäßig ist dieses Attribut auf "false" festgelegt.<br /><br />**Hinweis:** Bei der Verwendung von `PDO::ATTR_EMULATE_PREPARES => true`kommt der Sicherheitsgewinn durch parametrisierte Anfragen nicht zum Tragen. Ihre Anwendung sollte sicherstellen, dass die Daten, die an die Parameter gebunden ist, nicht böswilligen Transact-SQL-Code enthält.<br /><br />**Einschränkungen:**: Da die Parameter nicht gebunden werden mithilfe der Datenbankfunktion parametrisierte Abfrage, wird Input_output und Ausgabeparameter werden nicht unterstützt.|  
|PDO::SQLSRV_ATTR_ENCODING|PDO::SQLSRV_ENCODING_UTF8 (Standard)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|  
|PDO::SQLSRV_ATTR_DIRECT_QUERY|Wird hierfür der Wert „true“ festgelegt, werden Abfragen direkt ausgeführt. Der Wert „false“ sorgt dafür, dass vorbereitete Anweisungen ausgeführt werden. Weitere Informationen zu PDO:: sqlsrv_attr_direct_query finden Sie unter [direkte Anweisungsausführung und vorbereitete Anweisungsausführung im PDO_SQLSRV-Treiber](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|Weitere Informationen finden Sie unter [PDO::setAttribute](../../connect/php/pdo-setattribute.md).|  
  
Wenn Sie „PDO::CURSOR_SCROLL“ verwenden, können Sie auch „PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE“ verwenden. Beispiel:  
  
```  
array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_DYNAMIC));  
```  
  
In der folgenden Tabelle sind die möglichen Werte für „PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE“ aufgelistet.  
  
|Wert|Description|  
|---------|---------------|  
|PDO::SQLSRV_CURSOR_BUFFERED|Erstellt einen clientseitigen statischen Cursor (gepuffert). Weitere Informationen zu clientseitigen Cursorn finden Sie unter [Cursortypen &#40; PDO_SQLSRV-Treiber &#41; ](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_CURSOR_DYNAMIC|Erstellt einen serverseitigen (gepufferten) dynamischen Cursor, der es Ihnen erlaubt, auf Zeilen in beliebiger Reihenfolge zuzugreifen und Änderungen in der Datenbank widerspiegelt.|  
|PDO::SQLSRV_CURSOR_KEYSET_DRIVEN|Erstellt einen serverseitigen Keysetcursor. Ein Keysetcursor aktualisiert nach dem Löschen einer Zeile aus einer Tabelle nicht die Zeilenanzahl (eine gelöschte Zeile wird ohne Werte zurückgegeben).|  
|PDO::SQLSRV_CURSOR_STATIC|Erstellt einen serverseitigen statischen Cursor, der es Ihnen zwar erlaubt, auf Zeilen in beliebiger Reihenfolge zuzugreifen, aber die Änderungen in der Datenbank nicht widerspiegelt.<br /><br />„PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL“ ist standardmäßig mit „PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_STATIC“ vorbelegt.|  
  
Sie können ein PDOStatement-Objekt schließen, indem Sie dafür den Wert NULL festlegen.  
  
## <a name="example"></a>Beispiel  
In diesem Beispiel wird erläutert, wie Sie die Methode „PDO::prepare“ mit Parametermarkern und einem Vorwärtscursor verwenden.  
  
```  
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$col1 = 'a';  
$col2 = 'b';  
  
$query = "insert into Table1(col1, col2) values(?, ?)";  
$stmt = $conn->prepare( $query, array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY, PDO::SQLSRV_ATTR_QUERY_TIMEOUT => 1  ) );  
$stmt->execute( array( $col1, $col2 ) );  
print $stmt->rowCount();  
echo "\n";  
  
$query = "insert into Table1(col1, col2) values(:col1, :col2)";  
$stmt = $conn->prepare( $query, array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY, PDO::SQLSRV_ATTR_QUERY_TIMEOUT => 1  ) );  
$stmt->execute( array( ':col1' => $col1, ':col2' => $col2 ) );  
print $stmt->rowCount();  
  
$stmt = null  
?>  
```  
  
## <a name="example"></a>Beispiel  
In diesem Beispiel wird veranschaulicht, wie Sie die PDO::prepare-Methode mit einem clientseitigen Cursor verwenden. Ein Beispiel mit einem serverseitigen Cursor finden Sie unter [Cursortypen &#40; PDO_SQLSRV-Treiber &#41; ](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL));  
$stmt->execute();  
  
echo "\n";  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
echo "\n..\n";  
  
$row = $stmt->fetch( PDO::FETCH_BOTH, PDO::FETCH_ORI_FIRST );  
print_r($row);  
  
$row = $stmt->fetch( PDO::FETCH_ASSOC, PDO::FETCH_ORI_REL, 1 );  
print "$row[Name]\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT );  
print "$row[1]\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_PRIOR );  
print "$row[1]..\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_ABS, 0 );  
print_r($row);  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_LAST );  
print_r($row);  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[PDO-Klasse](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

