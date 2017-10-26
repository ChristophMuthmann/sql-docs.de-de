---
title: PDO::lastInsertId | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0c617b53-a74b-4d5b-b76b-3ec7f1b8e8de
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6a3dd9f6c007f4f528a657230e198397331cb24b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="pdolastinsertid"></a>PDO::lastInsertId
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Gibt den Bezeichner für eine Zeile an, die zuletzt in eine Tabelle in der Datenbank eingefügt wurde. Die Tabelle muss eine IDENTITY NOT NULL-Spalte enthalten.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
string PDO::lastInsertId ([ $name ] );  
```  
  
#### <a name="parameters"></a>Parameter  
$*name*: Eine optionale Zeichenfolge, mit der Sie die Tabelle angeben können.  
  
## <a name="return-value"></a>Rückgabewert  
Eine Zeichenfolge des Bezeichners für die Zeile, die zuletzt hinzugefügt wurde. Eine leere Zeichenfolge, wenn der Methodenaufruf fehlschlägt.  
  
## <a name="remarks"></a>Hinweise  
Unterstützung für PDO wurde in Version 2.0 von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt.  
  
## <a name="example"></a>Beispiel  
  
```  
<?php  
   $database = "test";  
   $server = "(local)";  
   $conn = new PDO( "sqlsrv:server=$server; Database = $database", "", "");  
  
   $conn->exec("use Test");  
  
   $ret = $conn->exec("INSERT INTO Table1 VALUES( '19' )");  
   $ret = $conn->exec("INSERT INTO ScrollTest VALUES( 1, '19' )");  
  
   $lastRow = $conn->lastInsertId('Table1');  
   echo $lastRow . "\n";  
  
   // defaults to ScrollTest  
   $lastRow = $conn->lastInsertId();  
   echo $lastRow . "\n";  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[PDO-Klasse](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

