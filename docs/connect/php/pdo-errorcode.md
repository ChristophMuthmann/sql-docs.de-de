---
title: 'PDO:: ErrorCode | Microsoft Docs'
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
ms.topic: article
ms.assetid: 5864b1d8-6814-41cd-a88d-415124484c13
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ae53a9f20cf910bdd7b303417fca140e20cbb111
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="pdoerrorcode"></a>PDO::errorCode
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO::errorCode ruft den SQLSTATE der letzten Operation auf dem Datenbankhandle ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
mixed PDO::errorCode();  
```  
  
## <a name="return-value"></a>Rückgabewert  
PDO::errorCode gibt einen fünf Zeichen umfassenden SQLSTATE als eine Zeichenfolge oder NULL zurück, falls es auf dem Datenbankhandle keine Operation gab.  
  
## <a name="remarks"></a>Hinweise  
PDO:: ErrorCode gibt im PDO_SQLSRV-Treiber gibt Warnungen für einige erfolgreichen Operationen zurück. Z. B. auf einer erfolgreichen Verbindung PDO:: ErrorCode gibt "01000", um SQL_SUCCESS_WITH_INFO.  
  
PDO::errorCode ruft nur die Fehlercodes ab, die diejenigen Operationen betreffen, die direkt auf der Datenbankverbindung durchgeführt wurden. Wenn Sie eine PDOStatement-Instanz mit PDO:: Prepare erstellen oder PDO:: Query und ein Fehler im Anweisungsobjekt generiert wird, wird PDO:: ErrorCode diesen Fehler nicht abrufen. Sie müssen einen PDOStatement::errorCode aufrufen, um den Fehlercode für eine auf einem bestimmten Anweisungsobjekt durchgeführte Operation auszugeben.  
  
Unterstützung für PDO wurde in Version 2.0 von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt.  
  
## <a name="example"></a>Beispiel  
In diesem Beispiel wird der Name der Spalte falsch geschrieben (`Cityx` anstelle von `City`), verursacht einen Fehler, der dann gemeldet wird.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[PDO-Klasse](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
