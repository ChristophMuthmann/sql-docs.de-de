---
title: 'Pdostatement:: Bindcolumn | Microsoft Docs'
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
ms.assetid: bbdcea53-d23d-4769-89a0-95c7cf4d5390
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f77fdb089f83d1d8d8f866be4a0a7ef99b9fa155
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="pdostatementbindcolumn"></a>PDOStatement::bindColumn
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Bindet eine Variable an eine Spalte im Resultset.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
bool PDOStatement::bindColumn($column, &$param[, $type[, $maxLen[, $driverdata ]]] );  
```  
  
#### <a name="parameters"></a>Parameter  
$*Spalte*: der (gemischte) Nummer der Spalte (Index 1-basiert) oder der Name der Spalte im Resultset.  
  
&$*Param*: der (gemischte) Name der PHP-Variable, die an die Spalte gebunden werden.  
  
$*Typ*: der optionale Datentyp des Parameters, durch eine Konstante PDO:: param_ * dargestellt wird.  
  
$*maxLen*: Optionale ganze Zahl, die von den Microsoft-Treibern für PHP für SQL Server nicht verwendet wird.  
  
$*Driverdata*: optionale(r) gemischte(r) Parameter für den Treiber. Beispielsweise können Sie PDO::SQLSRV_ENCODING_UTF8 angeben, um die Spalte an eine Variable als UTF-8-codierte Zeichenfolge zu binden.  
  
## <a name="return-value"></a>Rückgabewert  
TRUE bei Erfolg, andernfalls FALSE.  
  
## <a name="remarks"></a>Hinweise  
Unterstützung für PDO wurde in Version 2.0 von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt.  
  
## <a name="example"></a>Beispiel  
Dieses Beispiel zeigt, wie eine Variable an eine Spalte im Resultset gebunden werden kann.  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "SELECT Title, FirstName, EmailAddress FROM Person.Contact where LastName = 'Estes'";  
$stmt = $conn->prepare($query);  
$stmt->execute();  
  
$stmt->bindColumn('EmailAddress', $email);  
while ( $row = $stmt->fetch( PDO::FETCH_BOUND ) ){  
   echo "$email\n";  
}  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[PDOStatement-Klasse](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
