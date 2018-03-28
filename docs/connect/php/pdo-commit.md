---
title: PDO::commit | Microsoft Docs
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
ms.assetid: a0db4a00-9700-4f49-ab16-6522dd1101d3
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f734c30d7b4577229f9e69e05291ab8305b19407
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="pdocommit"></a>PDO::commit
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Sendet Befehle an die Datenbank, die nach dem Aufruf von [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) ausgegeben wurden und setzt die Verbindung in den Autocommit-Modus zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
bool PDO::commit();  
```  
  
## <a name="return-value"></a>Rückgabewert  
„true“, bei erfolgreichem Aufruf der Methode; andernfalls „false“.  
  
## <a name="remarks"></a>Hinweise  
PDO::commit ist nicht betroffen von dem Wert des PDO::ATTR_AUTOCOMMIT (und hat keinen Einfluss auf diesen).  
  
Ein Beispiel, das PDO::commit verwendet, finden Sie unter [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) .  
  
Unterstützung für PDO wurde in Version 2.0 von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt.  
  
## <a name="see-also"></a>Siehe auch  
[PDO-Klasse](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
