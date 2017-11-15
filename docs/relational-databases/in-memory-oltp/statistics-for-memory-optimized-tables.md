---
title: "Statistiken für speicheroptimierte Tabellen | Microsoft Dokumentation"
ms.custom: 
ms.date: 10/23/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e644766d-1d1c-43d7-83ff-8ccfe4f3af9f
caps.latest.revision: "18"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ef309831ab19ef8e69a27e8fefa3313f444ce147
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="statistics-for-memory-optimized-tables"></a>Statistiken für speicheroptimierte Tabellen
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Der Abfrageoptimierer verwendet Statistiken zu Spalten zum Erstellen von Abfrageplänen, die die Abfrageleistung verbessern. Die Statistiken werden aus den Tabellen in der Datenbank gesammelt und in den Datenbankmetadaten gespeichert.  
  
 Statistiken werden automatisch erstellt, sie können jedoch auch manuell erstellt werden. Beispielsweise werden Statistiken automatisch für Indexschlüsselspalten erstellt, wenn der Index erstellt wird. Weitere Informationen zum Erstellen von Statistiken finden Sie unter [Statistics](../../relational-databases/statistics/statistics.md).  
  
 Tabellendaten ändern sich normalerweise mit der Zeit, wenn Zeilen eingefügt, aktualisiert und gelöscht werden. Dies bedeutet, dass Statistiken regelmäßig aktualisiert werden müssen. Standardmäßig werden Statistiken zu Tabellen automatisch aktualisiert, wenn sie vom Abfrageoptimierer als möglicherweise veraltet eingestuft werden.  
  
 Überlegungen zu Statistiken für speicheroptimierte Tabellen:  
  
-   Ab SQL Server 2016 und in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]wird bei Verwendung eines Datenbank-Kompatibilitätsgrads von mindestens 130 die automatische Aktualisierung von Statistiken für speicheroptimierte Tabellen unterstützt. Siehe [ALTER DATABASE-Kompatibilitätsgrad (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md). Wenn eine Datenbank Tabellen enthält, die zuvor mit einem niedrigeren Kompatibilitätsgrad erstellt wurden, müssen die Statistiken einmal manuell aktualisiert werden, um die zukünftige automatische Aktualisierung von Statistiken zu aktivieren.
  
-   Für systemintern kompilierte gespeicherte Prozeduren werden Ausführungspläne für Abfragen in der Prozedur optimiert, wenn die Prozedur kompiliert wird, was bei der Erstellung geschieht. Sie werden nicht automatisch erneut kompiliert, wenn Statistiken aktualisiert werden. Daher müssen die Tabellen eine repräsentative Menge von Daten enthalten, bevor die Prozeduren erstellt werden.  
  
-   Systemintern kompilierte gespeicherte Prozeduren können mit [sp_recompile (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md)manuell neu kompiliert werden, und sie werden automatisch neu kompiliert, wenn die Datenbank offline und dann wieder online geschaltet wird, oder falls ein Datenbank-Failover oder ein Serverneustart stattfindet.  
  
## <a name="enabling-automatic-update-of-statistics-in-existing-tables"></a>Aktivieren der automatischen Aktualisierung von Statistiken in bestehenden Tabellen

Wenn Tabellen in einer Datenbank erstellt werden, deren Kompatibilitätsgrad mindestens 130 beträgt, wird die automatische Aktualisierung von Statistiken für alle Statistiken dieser Tabelle aktiviert, und keine weitere Aktion ist erforderlich.

Wenn eine Datenbank speicheroptimierte Tabellen enthält, die in einer früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder mit einem niedrigeren Kompatibilitätsgrad als 130 erstellt wurden, müssen die Statistiken einmal manuell aktualisiert werden, um die zukünftige automatische Aktualisierung von Statistiken zu aktivieren.

Um die automatische Aktualisierung von Statistiken für speicheroptimierte Tabellen zu aktivieren, die unter einem älteren Kompatibilitätsgrad erstellt wurden, gehen Sie folgendermaßen vor:

1. Aktualisieren Sie den Datenbank-Kompatibilitätsgrad: `ALTER DATABASE CURRENT SET COMPATIBILITY_LEVEL=130`

2. Aktualisieren Sie die Statistiken der speicheroptimierten Tabellen manuell. Im Folgenden finden Sie ein entsprechendes Beispielskript.

3. Kompilieren Sie die systemintern kompilierten gespeicherten Prozeduren manuell neu, um die aktualisierten Statistiken zu nutzen.

*Einmaliges Skript für Statistiken:* Für speicheroptimierte Tabellen, die unter einem niedrigeren Kompatibilitätsgrad erstellt wurden, können Sie das folgende Transact-SQL-Skript einmal zum Aktualisieren der Statistiken aller speicheroptimierten Tabellen und zum Aktivieren der zukünftigen automatischen Aktualisierung von Statistiken (sofern AUTO_UPDATE_STATISTICS für die Datenbank aktiviert ist) ausführen:

```
-- Assuming AUTO_UPDATE_STATISTICS is already ON for your database:
-- ALTER DATABASE CURRENT SET AUTO_UPDATE_STATISTICS ON;

ALTER DATABASE CURRENT SET COMPATIBILITY_LEVEL = 130;
GO
DECLARE @sql NVARCHAR(MAX) = N'';
SELECT
      @sql += N'UPDATE STATISTICS '
         + quotename(schema_name(t.schema_id))
         + N'.'
         + quotename(t.name)
         + ';' + CHAR(13) + CHAR(10)
   FROM sys.tables AS t
   WHERE t.is_memory_optimized = 1 AND 
        t.object_id IN (SELECT object_id FROM sys.stats WHERE no_recompute=1)
;
EXECUTE sp_executesql @sql;
GO
-- Each row appended to @sql looks roughly like:
-- UPDATE STATISTICS [dbo].[MyMemoryOptimizedTable];
```

*Überprüfen, ob die automatische Aktualisierung aktiviert ist:* Das folgende Skript überprüft, ob die automatische Aktualisierung für Statistiken zu speicheroptimierten Tabellen aktiviert ist. Nach der Ausführung des vorherigen Skripts wird `1` in der Spalte `auto-update enabled` für alle Statistikobjekte zurückgegeben.

```
SELECT 
    quotename(schema_name(o.schema_id)) + N'.' + quotename(o.name) AS [table],
    s.name AS [statistics object],
    1-s.no_recompute AS [auto-update enabled]
FROM sys.stats s JOIN sys.tables o ON s.object_id=o.object_id
WHERE o.is_memory_optimized=1
```

## <a name="guidelines-for-deploying-tables-and-procedures"></a>Richtlinien für die Bereitstellung von Tabellen und Prozeduren  
 Um sicherzustellen, dass der Abfrageoptimierer beim Erstellen von Abfrageplänen über aktuelle Statistiken verfügt, führen Sie die folgenden vier Schritte aus, um speicheroptimierte Tabellen und systemintern kompilierte gespeicherte Prozeduren bereitzustellen:  
  
1.  Stellen Sie sicher, dass der Kompatibilitätsgrad der Datenbank mindestens 130 beträgt. Siehe [ALTER DATABASE-Kompatibilitätsgrad (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).

2.  Erstellen Sie Tabellen und Indizes. Indizes müssen inline in den **CREATE TABLE** -Anweisungen angegeben werden.  
  
3.  Laden Sie Daten in die Tabellen.  
  
4.  Erstellen Sie gespeicherte Prozeduren, die auf die Tabellen zugreifen.  
  
 Indem Sie systemintern kompilierte gespeicherten Prozeduren erstellen, nachdem die Daten geladen wurden, wird sichergestellt, dass der Abfrageoptimierer über die für die speicheroptimierten Tabellen erforderlichen Statistiken verfügt. Damit liegen effiziente Abfragepläne vor, wenn die Prozedur kompiliert wird.  

## <a name="see-also"></a>Siehe auch  
 [Speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
