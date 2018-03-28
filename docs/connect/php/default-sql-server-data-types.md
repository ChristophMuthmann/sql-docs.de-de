---
title: SQL Server-Datentypen default | Microsoft Docs
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
helpviewer_keywords:
- default data types
- converting data types
ms.assetid: 65c7c211-96d3-4e65-a1de-1fe8d21348e7
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c1facac748e24d465144f93d2e4ccdf38608e6b3
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="default-sql-server-data-types"></a>SQL Server-Standarddatentypen
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Beim Senden von Daten an den Server konvertiert der [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] Daten aus seinem PHP-Datentyp in einen SQL Server-Datentyp, wenn vom Benutzer kein SQL Server-Datentyp angegeben wurde. Die folgende Tabelle enthält den PHP-Datentyp (der Datentyp, der an den Server gesendet wird) und den SQL Server-Standarddatentyp (der Datentyp, in den die Daten konvertiert werden). Details zum Angeben von Datentypen beim Senden von Daten an den Server finden Sie unter [Gewusst wie: Angeben von SQL Server-Datentypen, wenn der SQLSRV-Treiber verwendet wird](../../connect/php/how-to-specify-sql-server-data-types-when-using-the-sqlsrv-driver.md).  
  
|PHP-Datentyp|SQL-Standardservertyp im SQLSRV-Treiber|SQL-Standardservertyp im PDO_SQLSRV-Treiber|  
|-----------------|------------------------------------------------|-----------------------------------------------------|  
|NULL|varchar(1)|nicht unterstützt|  
|Boolean|bit|bit|  
|Integer|int|int|  
|Float|float(24)|nicht unterstützt|  
|Zeichenfolge (Länge kleiner als 8000 Bytes)|varchar(<string length>)|varchar(<string length>)|  
|Zeichenfolge (Länge größer als 8000 Bytes)|varchar(max)|varchar(max)|  
|Ressource|Nicht unterstützt.|Nicht unterstützt.|  
|Stream (Codierung: nicht binär)|varchar(max)|varchar(max)|  
|Stream (Codierung: binär)|varbinary|varbinary|  
|Array|Nicht unterstützt.|Nicht unterstützt.|  
|Objekt|Nicht unterstützt.|Nicht unterstützt.|  
|DatumUhrzeit (1)|datetime|Nicht unterstützt.|  
  
## <a name="see-also"></a>Siehe auch  
[Konstanten &#40;Microsoft-Treiber für PHP für SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[Konvertieren von Datentypen](../../connect/php/converting-data-types.md)

[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)

[PHP-Typen](http://php.net/manual/language.types.php)

[Datentypen (Transact-SQL)](https://docs.microsoft.com/en-us/sql/t-sql/data-types/data-types-transact-sql)  
  
