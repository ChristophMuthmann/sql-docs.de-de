---
title: 'PDO:: BeginTransaction | Microsoft Docs'
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
ms.assetid: 4d5db438-9df7-4d22-9907-3ddc63bd2220
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6c65de9c08dd4d92480c855378516850814ecd6b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="pdobegintransaction"></a>PDO::beginTransaction
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Schaltet den Autocommit-Modus aus und beginnt eine Transaktion.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
bool PDO::beginTransaction();  
```  
  
## <a name="return-value"></a>Rückgabewert  
„true“, bei erfolgreichem Aufruf der Methode; andernfalls „false“.  
  
## <a name="remarks"></a>Hinweise  
Die Transaktion, die mit PDO::beginTransaction gestartet wurde, endet, wenn [PDO::commit](../../connect/php/pdo-commit.md) oder [PDO::rollback](../../connect/php/pdo-rollback.md) aufgerufen werden.  
  
PDO::beginTransaction ist nicht betroffen von dem (und hat keinen Einfluss auf den) Wert von PDO::ATTR_AUTOCOMMIT.  
  
Sie dürfen PDO::beginTransaction nicht aufrufen, solange die vorherige PDO::beginTransaction noch nicht mit PDO::rollback oder PDO::commit beendet wurde.  
  
Die Verbindung wird zum Autocommit-Modus zurückkehren, falls diese Methode fehlschlägt.  
  
Unterstützung für PDO wurde in Version 2.0 von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt.  
  
## <a name="example"></a>Beispiel  
Im folgenden Beispiel wird eine Datenbank namens „Test“ und eine Tabelle namens „Tabelle1“ verwendet. Es startet eine Transaktion und gibt die Befehle aus, um zwei Zeilen hinzuzufügen und dann eine Zeile zu löschen. Diese Befehle werden an die Datenbank geschickt und die Transaktion wird explizit mit `PDO::commit`beendet.  
  
```  
<?php  
   $conn = new PDO( "sqlsrv:server=(local); Database = Test", "", "");  
   $conn->beginTransaction();  
   $ret = $conn->exec("insert into Table1(col1, col2) values('a', 'b') ");  
   $ret = $conn->exec("insert into Table1(col1, col2) values('a', 'c') ");  
   $ret = $conn->exec("delete from Table1 where col1 = 'a' and col2 = 'b'");  
   $conn->commit();  
   // $conn->rollback();  
   echo $ret;  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[PDO-Klasse](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

