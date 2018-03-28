---
title: PDOStatement::fetchColumn | Microsoft Docs
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
ms.assetid: 6ebf385c-ddb0-4c53-9dc6-7df0d3740b04
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bf7b22c70200c4bb1e216dfb77d4c6f16216987a
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="pdostatementfetchcolumn"></a>PDOStatement::fetchColumn
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Gibt eine Spalte in einer Zeile zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
string PDOStatement::fetchColumn ([ $column_number ] );  
```  
  
#### <a name="parameters"></a>Parameter  
$*Zeile/relative*: eine optionale ganze Zahl, die die nullbasierte Spaltennummer angibt. Der Standardwert ist 0 (die erste Spalte in der Zeile).  
  
## <a name="return-value"></a>Rückgabewert  
Eine Spalte oder „false“, wenn keine weiteren Zeilen vorhanden sind.  
  
## <a name="remarks"></a>Hinweise  
Unterstützung für PDO wurde in Version 2.0 von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt.  
  
## <a name="example"></a>Beispiel  
  
```  
<?php  
   $server = "(local)";  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   while ( $result = $stmt->fetchColumn(1)) {   
      print($result . "\n");   
   }  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[PDOStatement-Klasse](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
