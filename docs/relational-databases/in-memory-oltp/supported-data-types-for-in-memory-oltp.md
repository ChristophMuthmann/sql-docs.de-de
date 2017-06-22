---
title: "Unterstützte Datentypen für In-Memory OLTP | Microsoft-Dokumentation"
ms.custom: 
ms.date: 06/05/2017
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
ms.translationtype: Human Translation
ms.sourcegitcommit: 1d363db8e8bd0e1460cdea3c3a7add68e48714c9
ms.openlocfilehash: 0095d4e8ab9f3dc48e9414dc888213b79b3c34c6
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="supported-data-types-for-in-memory-oltp"></a>Unterstützte Datentypen für In-Memory OLTP
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  In diesem Artikel werden die Datentypen aufgeführt, die keine Unterstützung erhalten für die In-Memory OLTP-Features für:  
  
-   Speicheroptimierte Tabellen  
  
-   Nativ kompilierte T-SQL-Module  
  
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

Beginnend mit SQL Server 2016, unterstützen Speicheroptimierte Tabellen Spalten außerhalb von Zeilen, die eine einzelne Tabellenzeile größer sein als 8060 Bytes zu ermöglichen. Die folgende Transact-SQL-SELECT-Anweisung gibt für speicheroptimierte Tabellen alle Spalten zurück, die sich außerhalb von Zeilen befinden. Beachten Sie dabei Folgendes:

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


### <a name="other-data-types"></a>Andere Datentypen


|Andere Typen|Weitere Informationen finden Sie unter|  
|-----------------|--------------------------|  
|Tabellentypen|[Speicheroptimierte Tabellenvariablen](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Transact-SQL-Unterstützung für In-Memory OLTP](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)   
 [Implementieren von SQL_VARIANT in einer speicheroptimierten Tabelle](../../relational-databases/in-memory-oltp/implementing-sql-variant-in-a-memory-optimized-table.md)  
  
  

