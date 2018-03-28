---
title: PDO::errorInfo | Microsoft Docs
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
ms.assetid: 9d5481d5-13bc-4388-b3aa-78676c0fc709
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 41051d4425903e1a59392187e48c5defef4620c5
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="pdoerrorinfo"></a>PDO::errorInfo
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Ruft erweiterte Fehlerinformationen des zuletzt ausgeführten Vorgangs des Datenbankhandles ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
array PDO::errorInfo();  
```  
  
## <a name="return-value"></a>Rückgabewert  
Ein Array mit Fehlerinformationen über den zuletzt ausgeführten Vorgang des Datenbankhandles. Dieses Array besteht aus den folgenden Feldern:  
  
-   Der SQLSTATE-Fehlercode  
  
-   Der treiberspezifische Fehlercode  
  
-   Die treiberspezifische Fehlermeldung.  
  
Wenn kein Fehler vorliegt oder wenn der SQLSTATE nicht festgelegt ist, sind die treiberspezifischen Felder NULL.  
  
## <a name="remarks"></a>Hinweise  
PDO::errorInfo ruft nur die Fehlerinformationen für Vorgänge ab, die direkt in der Datenbank ausgeführt werden. Verwenden Sie PDOStatement::errorInfo, wenn eine PDOStatement-Instanz mit PDO::prepare oder PDO::query erstellt wird.  
  
Unterstützung für PDO wurde in Version 2.0 von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt.  
  
## <a name="example"></a>Beispiel  
In diesem Beispiel wird der Name der Spalte falsch geschrieben (`Cityx` anstelle von `City`), verursacht einen Fehler, der dann gemeldet wird.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
echo "\n";  
print_r ($conn->errorInfo());  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[PDO-Klasse](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
