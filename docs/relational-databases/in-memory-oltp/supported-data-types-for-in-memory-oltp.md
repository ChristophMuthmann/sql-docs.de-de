---
title: "Unterstützte Datentypen für In-Memory OLTP | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a7380ef0-c9d7-49e4-b6de-fad34752b9f3
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a928c1f77586198fd0d33cafa445ea406a437c6b
ms.lasthandoff: 04/11/2017

---
# <a name="supported-data-types-for-in-memory-oltp"></a>Unterstützte Datentypen für In-Memory OLTP
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  In diesem Artikel werden die Datentypen aufgeführt, die keine Unterstützung erhalten für die In-Memory OLTP-Features für:  
  
-   Speicheroptimierte Tabellen  
  
-   Systemintern kompilierte gespeicherte Prozeduren  
  
## <a name="unsupported-data-types"></a>Nicht unterstützte Datentypen  
 Die folgenden Datentypen werden nicht unterstützt:  
  
||||  
|-|-|-|  
|[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)|[geography &#40;Transact-SQL&#41;](../../t-sql/spatial-geography/spatial-types-geography.md)|[geometry &#40;Transact-SQL&#41;](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md)|  
|[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)|[rowversion &#40;Transact-SQL&#41;](../../t-sql/data-types/rowversion-transact-sql.md)|[xml &#40;Transact-SQL&#41;](../../t-sql/xml/xml-transact-sql.md)|  
|[sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)|Benutzerdefinierte Typen|.|  
  
## <a name="notable-supported-data-types"></a>Wichtige unterstützte Datentypen  
 Die meisten Datentypen werden von den Features von In-Memory OLTP unterstützt. Im folgenden Typen sollten explizit beachtet werden:  
  
|Zeichenfolgen- und Binärtypen|Weitere Informationen finden Sie unter|  
|-----------------------------|--------------------------|  
|binary und varbinary*|[binary und varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|  
|char und varchar*|[char und varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)|  
|nchar und nvarchar*|[nchar und nvarchar &#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|  
  
Für die vorhergehenden Zeichenfolgen- und binären Datentypen ab SQL Server 2016:  
  
- Eine einzelne speicheroptimierte Tabelle kann auch mehrere lange Spalten wie `nvarchar(4000)`enthalten, obwohl ihre Länge die physische Zeilengröße von 8060 Bytes überschreiten würde.  
  
- Eine speicheroptimierte Tabelle kann Zeichenfolgen mit maximaler Länge und binären Spalten mit Datentypen wie `varchar(max)`beinhalten.  


### <a name="identify-lobs-and-other-columns-that-are-off-row"></a>Identifizieren von LOBs und anderen Spalten außerhalb von Zeilen

Die folgende Transact-SQL-SELECT-Anweisung gibt für speicheroptimierte Tabellen alle Spalten zurück, die sich außerhalb von Zeilen befinden. Beachten Sie dabei Folgendes:

- Alle Indexschlüsselspalten werden innerhalb von Zeilen gespeichert.
  - Nicht eindeutige Indexschlüssel in speicheroptimierten Tabellen können auf NULL festlegbare Spalten enthalten.
  - Indizes können in einer speicheroptimierte Tabelle als UNIQUE deklariert werden.
- Alle LOB-Spalten werden außerhalb von Zeilen gespeichert.
- Ein max_length-Wert „-1“ gibt eine Spalte mit großen Objekten (Large Objects, LOBs) an.


```tsql
SELECT
        OBJECT_NAME(m.object_id) as [table],
        c.name                   as [column],
        c.max_length
    FROM
             sys.memory_optimized_tables_internal_attributes AS m
        JOIN sys.columns                                     AS c
                ON  m.object_id = c.object_id
                AND m.minor_id  = c.column_id
    WHERE
        m.type = 5;
```


#### <a name="natively-compiled-modules-support-for-lobs"></a>Unterstützung für LOBs in nativ kompilierten Modulen


Wenn Sie eine integrierte Zeichenfolgenfunktion in einem nativ kompilierten Modul, beispielsweise einer nativen Prozedur, verwenden, kann die Funktion einen LOB-Typ für Zeichenfolgen akzeptieren. In einer nativen Prozedur kann die LTrim-Funktion einen Parameter vom Typ „nvarchar(max)“ oder „varbinary(max)“ eingeben.

Darüber hinaus können diese LOBs der Rückgabetyp einer nativ kompilierten Skalar-UDF (User-Defined Function, benutzerdefinierte Funktion) sein.


### <a name="other-data-types"></a>Andere Datentypen


|Andere Typen|Weitere Informationen finden Sie unter|  
|-----------------|--------------------------|  
|Tabellentypen|[Speicheroptimierte Tabellenvariablen](http://msdn.microsoft.com/library/bd102e95-53e2-4da6-9b8b-0e4f02d286d3)|  
  
## <a name="see-also"></a>Siehe auch  
 [Transact-SQL-Unterstützung für In-Memory OLTP](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)   
 [Implementieren von LOB-Spalten in einer speicheroptimierten Tabelle](http://msdn.microsoft.com/en-us/bd8df0a5-12b9-4f4c-887c-2fb78dd79f4e)   
 [Implementieren von SQL_VARIANT in einer speicheroptimierten Tabelle](../../relational-databases/in-memory-oltp/implementing-sql-variant-in-a-memory-optimized-table.md)  
  
  

