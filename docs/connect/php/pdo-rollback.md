---
title: 'PDO:: Rollback | Microsoft Docs'
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
ms.assetid: d918c1e3-1be0-4001-b3b0-000db6d9e8b8
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bdb5d1e59e1b2d29225568abf53d3f6bf90d03d0
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="pdorollback"></a>PDO::rollback
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Verwirft Datenbankbefehle, die nach dem Aufrufen von [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) ausgegeben wurden, und setzt die Verbindung in den Autocommit-Modus zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
bool PDO::rollBack ();  
```  
  
## <a name="return-value"></a>Rückgabewert  
„true“, bei erfolgreichem Aufruf der Methode; andernfalls „false“.  
  
## <a name="remarks"></a>Hinweise  
PDO::rollback ist nicht betroffen von (und hat keinen Einfluss auf) den Wert von PDO::ATTR_AUTOCOMMIT.  
  
Unter [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) finden Sie ein Beispiel, das PDO::rollback verwendet.  
  
Unterstützung für PDO wurde in Version 2.0 von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt.  
  
## <a name="see-also"></a>Siehe auch  
[PDO-Klasse](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
