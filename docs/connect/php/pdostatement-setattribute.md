---
title: 'Pdostatement:: SetAttribute | Microsoft Docs'
ms.custom: ''
ms.date: 07/13/2017
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
ms.assetid: 329d9b5e-1c5d-40b0-9127-1051d0646fc7
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fba09d6c9e9e3b9806943802466628f820bece8f
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="pdostatementsetattribute"></a>PDOStatement::setAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Legt einen Attributwert fest. Entweder ein vordefiniertes PDO-Attribut oder ein benutzerdefiniertes Treiberattribut.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
bool PDOStatement::setAttribute ($attribute, $value );  
```  
  
#### <a name="parameters"></a>Parameter  
$*Attribut*: eine ganze Zahl, eine der Konstanten PDO:: attr_ * oder PDO:: sqlsrv_attr_\* Konstanten. Eine Liste der verfügbaren Attribute finden Sie im Abschnitt „Anmerkungen“.  
  
$*Wert*: der (gemischte) Wert festgelegt werden, für die angegebene $*Attribut*.  
  
## <a name="return-value"></a>Rückgabewert  
„true“ bei Erfolg, andernfalls „false“.  
  
## <a name="remarks"></a>Hinweise  
Die folgende Tabelle enthält die Liste mit den verfügbaren Attributen:  
  
|attribute|Werte|Description|  
|-------------|----------|---------------|  
|PDO::SQLSRV_ATTR_CLIENT_BUFFER_MAX_KB_SIZE|1 bis zur Grenze des PHP-Speichers.|Konfiguriert die Größe des Puffers, der das Resultset für einen clientseitigen Cursor enthält.<br /><br />Der Standardwert ist 10,240 KB (10 MB).<br /><br />Weitere Informationen zu clientseitigen Cursorn finden Sie unter [Cursortypen &#40;PDO_SQLSRV-Treiber&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_ENCODING|Integer<br /><br />PDO:: sqlsrv_encoding_utf8 (Standard)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|Legt die Zeichensatzcodierung fest, die vom Treiber verwendet wird, um mit dem Server zu kommunizieren.|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|true oder false|Verarbeitet die numerische Abrufvorgängen von Spalten mit numerischen SQL-Typen (Bit, ganze Zahl, "smallint", "tinyint", "float" oder Echtzeit).<br /><br />Wenn Optionsflag für Verbindung "ATTR_STRINGIFY_FETCHES aktiviert ist, ist der Rückgabewert eine Zeichenfolge an, selbst wenn SQLSRV_ATTR_FETCHES_NUMERIC_TYPE auf.<br /><br />Wenn der zurückgegebene PDO-Typ in der Spalte binden PDO_PARAM_INT ist, ist der Rückgabewert aus einer Spalte mit ganzen Zahlen ein "Int", selbst wenn SQLSRV_ATTR_FETCHES_NUMERIC_TYPE deaktiviert ist.|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|Integer|Legt das Abfragetimeout in Sekunden fest.<br /><br />Standardmäßig wartet der Treiber unbegrenzt auf Ergebnisse. Negative Zahlen sind nicht zulässig.<br /><br />„0“ bedeutet „kein Timeout“.|  
  
## <a name="example"></a>Beispiel  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "", array('MultipleActiveResultSets'=>false )  );  
  
$stmt = $conn->prepare('SELECT * FROM Person.ContactType');  
  
echo $stmt->getAttribute( constant( "PDO::ATTR_CURSOR" ) );  
  
echo "\n";  
  
$stmt->setAttribute(PDO::SQLSRV_ATTR_QUERY_TIMEOUT, 2);  
echo $stmt->getAttribute( constant( "PDO::SQLSRV_ATTR_QUERY_TIMEOUT" ) );  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[PDOStatement-Klasse](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
