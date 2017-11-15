---
title: So konvertiert FOR JSON SQL Server-Datentypen in JSON-Datentypen (SQL Server) | Microsoft-Dokumentation
ms.custom: SQL2016_New_Updated
ms.date: 07/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: FOR JSON, data type conversion
ms.assetid: da356f06-efd0-4ea3-8157-77395bf790d7
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b1744d9300d7a27087ebac6d7ef3f5dc00805750
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server"></a>So konvertiert FOR JSON SQL Server-Datentypen in JSON-Datentypen (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Die **FOR JSON** -Klausel verwendet die folgenden Regeln, um SQL Server-Datentypen in JSON-Typen in der JSON-Ausgabe zu konvertieren.  
  
|Kategorie|SQL Server-Datentyp|JSON-Datentyp|  
|--------------|--------------|---------------|  
|Zeichen- und Zeichenfolgetypen|char, nchar, varchar, nvarchar|Zeichenfolge|  
|Numerische Typen|int, bigint, float, decimal, numeric|number|  
|Bit-Typ|bit|Boolesche Werte ("true" oder "false")|  
|Datum- und Uhrzeittypen|date, datetime, datetime2, time, datetimeoffset|Zeichenfolge|  
|Binärtypen|varbinary, binary, image, timestamp, rowversion|BASE64-codierte Zeichenfolge|  
|CLR-Typen|geometry, geography, andere CLR-Typen|Nicht unterstützt. Diese Typen geben einen Fehler zurück.<br /><br /> Verwenden Sie in der SELECT-Anweisung CAST oder CONVERT, oder verwenden Sie eine CLR-Eigenschaft oder -Methode, um die Quelldaten in einen SQL Server-Datentyp zu konvertieren, der erfolgreich in einen JSON-Typ konvertiert werden kann. Verwenden Sie z.B. **STAsText()** für den Geometrietyp oder **ToString()** für alle CLR-Typen. Der Typ des JSON-Ausgabewerts wird dann abgeleitet aus dem Rückgabetyp der Konvertierung, die Sie auf die SELECT-Anweisung anwenden.|  
|Andere Typen|uniqueidentifier, money|Zeichenfolge|  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Erfahren Sie mehr über die integrierte JSON-Unterstützung in SQL Server  
Viele spezifische Lösungen, Anwendungsfälle und Empfehlungen finden Sie in SQL Server und in der Azure SQL-Daten im [Blogbeitrag über die integrierte JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) von Jovan Popovic, Program Manager bei Microsoft.
  
## <a name="see-also"></a>Siehe auch  
 [Formatieren von Abfrageergebnisse als JSON mit FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  
