---
title: PDOStatement::fetchAll | Microsoft Docs
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
ms.assetid: be74188a-77cd-4d19-b16e-77278373c979
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2eb146247b4180549aeaa595a8d18a94d5116ae6
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="pdostatementfetchall"></a>PDOStatement::fetchAll
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Gibt die Zeilen in einem Resultset in einem Array zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
array PDOStatement::fetchAll([ $fetch_style[, $column_index ][, ctor_args]] );  
```  
  
#### <a name="parameters"></a>Parameter  
$*Fetch_style*: ein Symbol (ganze Zahl), welches das Format der Zeilendaten angibt. Unter [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md) finden Sie eine Liste der Werte. PDO::FETCH_COLUMN ist ebenfalls zulässig. PDO::FETCH_BOTH ist der Standard.  
  
$*Spaltenindex*: einen ganzzahligen Wert, der die Spalte wird zurückgegeben, wenn $*Fetch_style* PDO:: fetch_column ist. Der Standardwert ist 0.  
  
$*Ctor_args*: ein Array der Parameter für einen Klassenkonstruktor, wenn $*Fetch_style* ist PDO:: fetch_class oder PDO:: fetch_obj ist.  
  
## <a name="return-value"></a>Rückgabewert  
Ein Array der verbleibenden Zeilen im Resultset oder „false“ falls der Methodenaufruf fehlschlägt.  
  
## <a name="remarks"></a>Hinweise  
Unterstützung für PDO wurde in Version 2.0 von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt.  
  
## <a name="example"></a>Beispiel  
  
```  
<?php  
   $server = "(local)";  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
   print "-----------\n";  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetchall(PDO::FETCH_BOTH);  
   print_r( $result );  
   print "\n-----------\n";  
  
   print "-----------\n";  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetchall(PDO::FETCH_NUM);  
   print_r( $result );  
   print "\n-----------\n";  
  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetchall(PDO::FETCH_COLUMN, 1);  
   print_r( $result );  
   print "\n-----------\n";  
  
   class cc {  
      function __construct( $arg ) {  
         echo "$arg\n";  
      }  
  
      function __toString() {  
         echo "To string\n";  
      }  
   };  
  
   $stmt = $conn->query( 'SELECT TOP(2) * FROM Person.ContactType' );  
   $all = $stmt->fetchAll( PDO::FETCH_CLASS, 'cc', array( 'Hi!' ));  
   var_dump( $all );  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[PDOStatement-Klasse](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
