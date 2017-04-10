---
title: "So konvertiert FOR JSON SQL Server-Datentypen in JSON-Datentypen (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "07/07/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FOR JSON, Datentypkonvertierung"
ms.assetid: da356f06-efd0-4ea3-8157-77395bf790d7
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 11
---
# So konvertiert FOR JSON SQL Server-Datentypen in JSON-Datentypen (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Die **FOR JSON**-Klausel verwendet die folgenden Regeln, um SQL Server-Datentypen in JSON-Typen in der JSON-Ausgabe zu konvertieren.  
  
|Kategorie|SQL Server-Datentyp|JSON-Datentyp|  
|--------------|--------------|---------------|  
|Zeichen- und Zeichenfolgetypen|(n)(var)(char)|Zeichenfolge|  
|Numerische Typen|int, bigint, float, decimal, numeric|number|  
|Bit-Typ|bit|Boolesche Werte ("true" oder "false")|  
|Datum- und Uhrzeittypen|date, datetime, datetime2, time, datetimeoffset|Zeichenfolge|  
|Binärtypen|varbinary, binary, image, timestamp, rowversion|BASE64-codierte Zeichenfolge|  
|CLR-Typen|CLR, geometry, geography|Wird nicht unterstützt. Diese Typen geben einen Fehler zurück.<br /><br /> Verwenden Sie in der SELECT-Anweisung CAST oder CONVERT, oder verwenden Sie eine CLR-Eigenschaft oder -Methode, um die Daten in einen Datentyp zu konvertieren, der in einen JSON-Typ konvertiert werden kann. Verwenden Sie z.B. **ToString()** für alle CLR-Typen oder **STAsText()** für den Geometrietyp. Der Typ des JSON-Ausgabewerts wird dann abgeleitet aus dem Rückgabetyp der Konvertierung, die Sie in der SELECT-Anweisung verwenden.|  
|Andere Typen|uniqueidentifier, money|Zeichenfolge|  
  
## Siehe auch  
 [Formatieren von Abfrageergebnisse als JSON mit FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  