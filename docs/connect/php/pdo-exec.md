---
title: 'PDO:: EXEC | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 359a87c6-c13a-4518-8f23-a922e7f3b171
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: faf387371d9d9f49fbba4cae466ef8b52f4e08c4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="pdoexec"></a>PDO::exec
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Bereitet eine SQL-Anweisung vor, führt diese in einem einzelnen Funktionsaufruf aus und gibt die Anzahl der von dieser Anweisung betroffenen Zeilen zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
int PDO::exec ($statement)  
```  
  
#### <a name="parameters"></a>Parameter  
*$statement*: Eine Zeichenfolge, die die auszuführende SQL-Anweisung enthält.  
  
## <a name="return-value"></a>Rückgabewert  
Eine ganze Zahl, die über die Anzahl der betroffenen Zeilen Auskunft gibt.  
  
## <a name="remarks"></a>Hinweise  
Wenn *$statement* mehrere SQL-Anweisungen enthält, wird nur die Anzahl der von der letzten Anweisung betroffenen Zeilen in der Zahl widergespiegelt.  
  
PDO::exec Gibt keine Ergebnisse für eine SELECT Anweisung zurück.  
  
Die folgenden Attribute beeinflussen das Verhalten der PDO::exec:  
  
-   PDO::ATTR_DEFAULT_FETCH_MODE  
  
-   PDO::SQLSRV_ATTR_ENCODING  
  
-   PDO::SQLSRV_ATTR_QUERY_TIMEOUT  
  
Weitere Informationen finden Sie unter [PDO::setAttribute](../../connect/php/pdo-setattribute.md) .  
  
Unterstützung für PDO wurde in Version 2.0 von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt.  
  
## <a name="example"></a>Beispiel  
Dieses Beispiel löscht Zeilen in Tabelle 1, die in Spalte 1 „xxxyy“ aufweisen. Anschließend meldet das Beispiel, wie viele Zeilen gelöscht wurden.  
  
```  
<?php  
   $c = new PDO( "sqlsrv:server=(local)");  
  
   $c->exec("use Test");  
   $ret = $c->exec("delete from Table1 where col1 = 'xxxyy'");  
   echo $ret;  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[PDO-Klasse](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

