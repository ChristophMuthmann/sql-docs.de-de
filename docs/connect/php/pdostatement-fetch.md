---
title: 'Pdostatement:: FETCH | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4368e362-5bda-4da1-8462-33714683c39f
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 787f84791c12ceada7e3e4598b3fae387e51430b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="pdostatementfetch"></a>PDOStatement::fetch
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Ruft eine Zeile aus einem Resultset ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
mixed PDOStatement::fetch ([ $fetch_style[, $cursor_orientation[, $cursor_offset]]] );  
```  
  
#### <a name="parameters"></a>Parameter  
$*Fetch_style*: eine optionale (Integer-)-Symbol, das das Format der Zeilendaten angibt. Finden Sie im Abschnitt "Hinweise" der Liste der möglichen Werte für $*Fetch_style*. Der Standardwert ist PDO::FETCH_BOTH. $*Fetch_style* in der Abrufmethode überschreibt die $*Fetch_style* in der PDO:: Query-Methode angegeben.  
  
$*Cursor_orientation*: eine optionale (Integer-)-Symbol, der angibt, der Zeile abzurufen, wenn die Prepare-Anweisung gibt `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL`. Finden Sie im Abschnitt "Hinweise" der Liste der möglichen Werte für $*Cursor_orientation*. Ein Beispiel mit einem bildlauffähigen Cursor finden Sie unter [PDO::prepare](../../connect/php/pdo-prepare.md) .  
  
$*Cursor_offset*: eine optionale (Integer-)-Symbol, das Angeben der Zeile, um beim Abrufen von $*Cursor_orientation* ist PDO:: fetch_ori_abs oder PDO:: fetch_ori_rel und PDO:: attr_cursor PDO:: cursor_scroll.  
  
## <a name="return-value"></a>Rückgabewert  
Ein gemischter Wert, der eine Zeile oder „false“ zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
Der Cursor wird automatisch vorgerückt, wenn FETCH aufgerufen wird. Die folgende Tabelle enthält die Liste der möglichen $*Fetch_style* Werte.  
  
|$*fetch_style*|Description|  
|-------------------|---------------|  
|PDO::FETCH_ASSOC|Gibt ein Array an, das von einem Spaltennamen indiziert ist.|  
|PDO::FETCH_BOTH|Gibt ein Array an, das von einem Spaltennamen und einer 0-basierten Reihenfolge indiziert ist. Dies ist die Standardeinstellung.|  
|PDO::FETCH_BOUND|Gibt „true“ zurück und weist die Werte gemäß [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md)zu.|  
|PDO::FETCH_CLASS|Erstellt eine Instanz und ordnet Spalten den benannten Eigenschaften zu.<br /><br />Rufen Sie [PDOStatement::setFetchMode](../../connect/php/pdostatement-setfetchmode.md) auf, bevor Sie FETCH aufrufen.|  
|PDO::FETCH_INTO|Aktualisiert eine Instanz der angeforderten Klasse.<br /><br />Rufen Sie [PDOStatement::setFetchMode](../../connect/php/pdostatement-setfetchmode.md) auf, bevor Sie FETCH aufrufen.|  
|PDO::FETCH_LAZY|Erstellt Namen von Variablen während des Zugriffs sowie ein unbenanntes Objekt.|  
|PDO::FETCH_NUM|Gibt ein Array an, das von einer nullbasierten Spaltenreihenfolge indiziert ist.|  
|PDO::FETCH_OBJ|Gibt ein unbenanntes Objekt mit Eigenschaftennamen an, die Spaltennamen zugeordnet sind.|  
  
Wenn sich der Cursor am Ende des Resultsets befindet (die letzte Zeile wurde abgerufen und der Cursor befindet sich außerhalb der Begrenzung des Resultsets) und es sich um einen Vorwärtscursor handelt (PDO::ATTR_CURSOR = PDO::CURSOR_FWDONLY), schlagen nachfolgende FETCH-Aufrufe fehl.  
  
Wenn der Cursor bildlauffähig ist (PDO::ATTR_CURSOR = PDO::CURSOR_SCROLL), wird FETCH den Cursor innerhalb der Begrenzung des Resultsets bewegen. Die folgende Tabelle enthält die Liste der möglichen $*Cursor_orientation* Werte.  
  
|$*cursor_orientation*|Description|  
|--------------------------|---------------|  
|PDO::FETCH_ORI_NEXT|Ruft die nächste Zeile ab. Dies ist die Standardeinstellung.|  
|PDO::FETCH_ORI_PRIOR|Ruft die vorherige Zeile ab.|  
|PDO::FETCH_ORI_FIRST|Ruft die erste Zeile ab.|  
|PDO::FETCH_ORI_LAST|Ruft die letzte Zeile ab.|  
|PDO:: fetch_ori_abs, *Num*|Ruft die Zeile in der $ angeforderte ab*Cursor_offset* Zeilennummer.|  
|PDO:: fetch_ori_rel, *Num*|Ruft die Zeile in der $ angeforderte ab*Cursor_offset* über die relative Position von der aktuellen Position.|  
  
Wenn der angegebene Wert für $*Cursor_offset* oder $*Cursor_orientation* eine Position außerhalb der Begrenzung des Resultsets ergibt, schlägt Fetch fehl.  
  
Unterstützung für PDO wurde in Version 2.0 von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt.  
  
## <a name="example"></a>Beispiel  
  
```  
<?php  
   $server = "(local)";  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
   print( "\n---------- PDO::FETCH_CLASS -------------\n" );  
   $stmt = $conn->query( "select * from HumanResources.Department order by GroupName" );  
  
   class cc {  
      function __construct( $arg ) {  
         echo "$arg";  
      }  
  
      function __toString() {  
         return $this->DepartmentID . "; " . $this->Name . "; " . $this->GroupName;  
      }  
   }  
  
   $stmt->setFetchMode(PDO::FETCH_CLASS, 'cc', array( "arg1 " ));  
   while ( $row = $stmt->fetch(PDO::FETCH_CLASS)) {   
      print($row . "\n");   
   }  
  
   print( "\n---------- PDO::FETCH_INTO -------------\n" );  
   $stmt = $conn->query( "select * from HumanResources.Department order by GroupName" );  
   $c_obj = new cc( '' );  
  
   $stmt->setFetchMode(PDO::FETCH_INTO, $c_obj);  
   while ( $row = $stmt->fetch(PDO::FETCH_INTO)) {   
      echo "$c_obj\n";  
   }  
  
   print( "\n---------- PDO::FETCH_ASSOC -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_ASSOC );  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_NUM -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_NUM );  
   print_r ($result );  
  
   print( "\n---------- PDO::FETCH_BOTH -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_BOTH );  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_LAZY -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_LAZY );  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_OBJ -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_OBJ );  
   print $result->Name;  
   print( "\n \n" );  
  
   print( "\n---------- PDO::FETCH_BOUND -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $stmt->bindColumn('Name', $name);  
   $result = $stmt->fetch( PDO::FETCH_BOUND );  
   print $name;  
   print( "\n \n" );  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[PDOStatement-Klasse](../../connect/php/pdostatement-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

