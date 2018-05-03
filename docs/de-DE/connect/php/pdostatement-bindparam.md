---
title: 'Pdostatement:: Bindparam | Microsoft Docs'
ms.custom: ''
ms.date: 04/11/2017
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
ms.assetid: 65212058-2632-47a4-ba7d-2206883abf09
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b2a351fa6e916d37c38e2ed3beb1cea8190183e7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="pdostatementbindparam"></a>PDOStatement::bindParam
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Bindet einen Parameter an einen benannten Platzhalter oder Fragezeichenplatzhalter in der SQL-Anweisung.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
bool PDOStatement::bindParam($parameter, &$variable[, $data_type[, $length[, $driver_options]]]);  
```  
  
#### <a name="parameters"></a>Parameter  
$*Parameter*: ein (gemischter) Parameterbezeichner. Für Sie Platzhalter mit einer Anweisung mit dem Namen, verwenden Sie einen Parameternamen an (: Name). Für eine vorbereitete Anweisung mit der fragezeichensyntax ist es der 1-basierte Index des Parameters.  
  
&$*Variable*: der (gemischte) Name der PHP-Variablen, die an den SQL-Anweisungsparameter zu binden.  
  
$*Data_type*: eine optionale (Integer-) PDO:: param_ * Konstanten. Der Standardwert ist PDO:: param_str.  
  
$*Länge*: eine optionale (Integer-) Länge des Datentyps. Sie können angeben, um die Standardgröße anzugeben, wenn PDO:: param_int oder PDO:: param_bool in $ PDO::SQLSRV_PARAM_OUT_DEFAULT_SIZE*Data_type*.  
  
$*Driver_options*: die optionalen (gemischten) treiberspezifischen Optionen. Beispielsweise können Sie PDO::SQLSRV_ENCODING_UTF8 angeben, um die Spalte an eine Variable als UTF-8-codierte Zeichenfolge zu binden.  
  
## <a name="return-value"></a>Rückgabewert  
„true“ bei Erfolg, andernfalls „false“.  
  
## <a name="remarks"></a>Hinweise  
Beim Binden von null-Daten an Serverspalten vom Typ Varbinary, Binary oder varbinary(max) sollten Sie angeben, binäre Codierung (PDO:: sqlsrv_encoding_binary) unter Verwendung der $*Driver_options*. Weitere Informationen zur Codierung Konstanten finden Sie unter [Konstanten](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).  
  
Unterstützung für PDO wurde in Version 2.0 von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt.  

## <a name="example"></a>Beispiel  
Dieses Codebeispiel zeigt, dass, nachdem $contact an den Parameter gebunden wurde, das Ändern des Werts nicht den in der Abfrage übergebenen Wert ändert.  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  
  
$contact = "Sales Agent";  
$stmt = $conn->prepare("select * from Person.ContactType where name = ?");  
$stmt->bindParam(1, $contact);  
$contact = "Owner";  
$stmt->execute();  
  
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {  
   print "$row[Name]\n\n";  
}  
  
$stmt = null;  
$contact = "Sales Agent";  
$stmt = $conn->prepare("select * from Person.ContactType where name = :contact");  
$stmt->bindParam(':contact', $contact);  
$contact = "Owner";  
$stmt->execute();  
  
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {  
   print "$row[Name]\n\n";  
}  
?>  
```  
  
## <a name="example"></a>Beispiel  
In diesem Codebeispiel wird veranschaulicht, wie auf einen Output-Parameter zugegriffen wird.  
  
```  
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  
  
$input1 = 'bb';  
  
$stmt = $conn->prepare("select ? = count(*) from Sys.tables");  
$stmt->bindParam(1, $input1, PDO::PARAM_STR, 10);  
$stmt->execute();  
echo $input1;  
?>  
```  
  
> [!NOTE]
> Beim Binden von eines Output-Parameters an einen Typ "bigint", wenn der Wert außerhalb des Bereichs der annehmen kann ein [Ganzzahl](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md), PDO:: param_int mit PDO::SQLSRV_PARAM_OUT_DEFAULT_SIZE möglicherweise ergeben eine Ausnahme "der Wert außerhalb des gültigen Bereichs". Daher verwenden Sie stattdessen den Standard-PDO:: param_str, und geben Sie die Größe der resultierenden Zeichenfolge, die höchstens 21 ist. Es ist die maximale Anzahl von Ziffern, z. B. die negativen Vorzeichen ausnahmslos "bigint". 

## <a name="example"></a>Beispiel  
In diesem Codebeispiel wird veranschaulicht, wie ein Input/Output-Parameter verwendet wird.  
  
```  
<?php  
   $database = "AdventureWorks";  
   $server = "(local)";  
   $dbh = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  
  
   $dbh->query("IF OBJECT_ID('dbo.sp_ReverseString', 'P') IS NOT NULL DROP PROCEDURE dbo.sp_ReverseString");  
   $dbh->query("CREATE PROCEDURE dbo.sp_ReverseString @String as VARCHAR(2048) OUTPUT as SELECT @String = REVERSE(@String)");  
   $stmt = $dbh->prepare("EXEC dbo.sp_ReverseString ?");  
   $string = "123456789";  
   $stmt->bindParam(1, $string, PDO::PARAM_STR | PDO::PARAM_INPUT_OUTPUT, 2048);  
   $stmt->execute();  
   print $string;   // Expect 987654321  
?>  
```  

> [!NOTE]
> Es wird empfohlen, die Zeichenfolgen als Eingaben zu verwenden, wenn Werte zum Binden einer [decimal oder numeric-Spalte](../../t-sql/data-types/decimal-and-numeric-transact-sql.md) und Genauigkeit sichergestellt werden, wie Sie PHP mit eingeschränkter Genauigkeit für [Gleitkommazahlen](http://php.net/manual/en/language.types.float.php).

## <a name="example"></a>Beispiel  
In diesem Codebeispiel wird gezeigt, wie einen decimal-Wert als Eingabeparameter gebunden werden.  

```
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");  

// Assume TestTable exists with a decimal field 
$input = 9223372036854.80000;
$stmt = $conn->prepare("INSERT INTO TestTable (DecimalCol) VALUES (?)");
// by default it is PDO::PARAM_STR, rounding of a large input value may
// occur if PDO::PARAM_INT is specified
$stmt->bindParam(1, $input, PDO::PARAM_STR);
$stmt->execute();
```


## <a name="see-also"></a>Siehe auch  
[PDOStatement-Klasse](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
