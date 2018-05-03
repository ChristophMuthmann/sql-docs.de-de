---
title: PDO::getAvailableDrivers | Microsoft Docs
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
ms.topic: conceptual
ms.assetid: eab561e6-1229-401a-9482-008c23f9a4e6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ccc7d27f4e96c2e0694b40edd3b0d9644831f6c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="pdogetavailabledrivers"></a>PDO::getAvailableDrivers
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Gibt ein Array der PDO-Treiber in Ihrer PHP-Installation zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
array PDO::getAvailableDrivers ();  
```  
  
## <a name="return-value"></a>Rückgabewert  
Ein Array mit der Liste der PDO-Treiber.  
  
## <a name="remarks"></a>Hinweise  
Der Name des PDO-Treibers wird verwendet in PDO::__construct, um eine PDO-Instanz zu erstellen.  
  
PDO::getAvailableDrivers muss nicht von PHP-Treibern implementiert werden. Weitere Informationen zu dieser Methode finden Sie in der PHP-Dokumentation.  
  
Unterstützung für PDO wurde in Version 2.0 von [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]hinzugefügt.  
  
## <a name="example"></a>Beispiel  
  
```  
<?php  
print_r(PDO::getAvailableDrivers());  
?>  
```  
  
## <a name="see-also"></a>Siehe auch  
[PDO-Klasse](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
