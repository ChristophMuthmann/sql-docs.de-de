---
title: 'Pdostatement:: Execute | Microsoft Docs'
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
ms.assetid: c2e80566-fa41-4918-8521-cf2e05374cbd
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d42e077796f59f2ea4a628264628fbe9a68da1f4
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="pdostatementexecute"></a>PDOStatement::execute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Führt eine Anweisung aus.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
bool PDOStatement::execute ([ $input ] );  
```  
  
#### <a name="parameters"></a>Parameter  
*$input*: (Optional) ein assoziatives Array, das die Werte für Parametermarker enthält.  
  
## <a name="return-value"></a>Rückgabewert  
„true“ bei Erfolg, andernfalls „false“.  
  
## <a name="remarks"></a>Hinweise  
Anweisungen, die mit PDOStatement::execute ausgeführt werden, müssen erst mit [PDO::prepare](../../connect/php/pdo-prepare.md)vorbereitet werden. Informationen zum Angeben der direkten oder vorbereiteten Ausführung von Anweisungen finden Sie unter [Direkte Anweisungsausführung und vorbereitete Anweisungsausführung im PDO_SQLSRV-Treiber](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md) .  
  
Alle Werte de Eingabeparameterarrays werden als PDO::PARAM_STR-Werte behandelt.  
  
Falls die vorbereitete Anweisung Parametermarker enthält, müssen Sie entweder PDOStatement::bindParam aufrufen, um die PHP-Variablen an die Parametermarker zu binden, oder ein Array, das nur aus Eingabeparameterwerten besteht, weitergeben.  
  
Unterstützung für PDO wurde in Version 2.0 von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt.  
  
## <a name="example"></a>Beispiel  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query );  
$stmt->execute();  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
  
echo "\n";  
$param = "Owner";  
$query = "select * from Person.ContactType where name = ?";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param));  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[PDOStatement-Klasse](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
