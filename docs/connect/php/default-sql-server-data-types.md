---
title: SQL Server-Datentypen default | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- default data types
- converting data types
ms.assetid: 65c7c211-96d3-4e65-a1de-1fe8d21348e7
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b71a28f48cdbfe9e70079abfc392f53976c90c87
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
|Zeichenfolge (Länge kleiner als 8000 Bytes)|Varchar (<string length>)|Varchar (<string length>)|  
|Zeichenfolge (Länge größer als 8000 Bytes)|varchar(max)|varchar(max)|  
|Ressource|Wird nicht unterstützt.|Wird nicht unterstützt.|  
|Stream (Codierung: nicht binär)|varchar(max)|varchar(max)|  
|Stream (Codierung: binär)|varbinary|varbinary|  
|Array|Wird nicht unterstützt.|Wird nicht unterstützt.|  
|Objekt|Wird nicht unterstützt.|Wird nicht unterstützt.|  
|DatumUhrzeit (1)|datetime|Wird nicht unterstützt.|  
  
## <a name="see-also"></a>Siehe auch  
[Konstanten &#40;Microsoft-Treiber für PHP für SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[Converting Data Types](../../connect/php/converting-data-types.md)  
[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)  
[PHP-Typen](http://go.microsoft.com/fwlink/?LinkId=109071)  
[Datentypen (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=109068)  
  

