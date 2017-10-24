---
title: DBCC (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC
- DBCC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transactional consistency
- Database Console Command statements
- status information [SQL Server], DBCC statements
- snapshots [SQL Server database snapshots], DBCC statements
- emergency database state [SQL Server]
- TABLOCK
- internal database snapshots [SQL Server]
- reporting DBCC statement progress
- logical consistency of data [SQL Server]
- DBCC statements
- validation statements [SQL Server]
- miscellaneous statements [SQL Server]
- statements [SQL Server], DBCC statements
- DBCC commands [SQL Server]
- result sets [SQL Server], DBCC statements
- maintenance statements [SQL Server]
- physical consistency of data [SQL Server]
- current DBCC statement status
- progress reporting [DBCC statements]
- informational statements [SQL Server]
ms.assetid: c6da8c04-5b6b-459a-9f76-110c92ca8b29
caps.latest.revision: 50
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8e8750f4b44ec206bb5a26586acd6b567f7dac37
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-transact-sql"></a>DBCC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Die Programmiersprache [!INCLUDE[tsql](../../includes/tsql-md.md)] stellt DBCC-Anweisungen bereit, die als Datenbankkonsolenbefehle (Database Console Commands, DBCC) für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dienen.
  
DBCC-Anweisungen sind in die folgenden Kategorien eingeteilt.
  
|Befehlskategorie|Funktion|  
|---|---|
|Verwaltung|Aufgaben zur Verwaltung von Datenbanken, Indizes und Dateigruppen.|  
|Sonstiges|Verschiedene Aufgaben wie das Aktivieren von Ablaufverfolgungsflags oder das Entfernen einer DLL aus dem Arbeitsspeicher.|  
|Nur zu Informationszwecken|Aufgaben zum Sammeln und Anzeigen verschiedener Arten von Informationen.|  
|Überprüfung|Überprüfungsvorgänge für Datenbanken, Tabellen, Indizes, Kataloge, Dateigruppen oder das Zuordnen von Datenbankseiten.|  
  
DBCC-Befehle akzeptieren Eingabeparameter und geben Werte zurück. Alle Parameter für DBCC-Befehle nehmen sowohl Unicode- als auch DBCS-Literale (Double-Byte Character Set, Doppelbyte-Zeichensatz) an.
  
## <a name="dbcc-internal-database-snapshot-usage"></a>Verwenden einer internen Datenbank-Momentaufnahme mit DBCC  
Die folgenden DBCC-Befehle werden für eine von [!INCLUDE[ssDE](../../includes/ssde-md.md)] erstellte interne schreibgeschützte Datenbank-Momentaufnahme ausgeführt. Auf diese Weise werden beim Ausführen dieser Befehle Blockierungs- und Parallelitätsprobleme verhindert. Weitere Informationen finden Sie unter [Datenbankmomentaufnahmen &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).
- DBCC CHECKALLOC
- DBCC CHECKCATALOG
- DBCC CHECKDB
- DBCC CHECKFILEGROUP
- DBCC CHECKTABLE

Wenn Sie einen dieser DBCC-Befehle ausführen, erstellt [!INCLUDE[ssDE](../../includes/ssde-md.md)] eine Datenbankmomentaufnahme und versetzt diese hinsichtlich der Transaktionen in einen konsistenten Status. Der DBCC-Befehl führt die Überprüfungen dann auf dieser Momentaufnahme durch. Wenn die Ausführung des DBCC-Befehls abgeschlossen ist, wird die Momentaufnahme gelöscht.
  
Manchmal ist eine interne Datenbankmomentaufnahme nicht erforderlich oder kann nicht erstellt werden. In diesem Fall wird der DBCC-Befehl für die aktuelle Datenbank ausgeführt. Wenn die Datenbank online ist, verwendet der DBCC-Befehl Tabellensperren, um die Konsistenz der zu überprüfenden Objekte sicherzustellen. Dieses Verhalten ist identisch mit der WITH TABLOCK-Option.
  
Es wird keine interne Datenbankmomentaufnahme erstellt, wenn unter folgenden Bedingungen ein DBCC-Befehl ausgeführt wird:  
-   Für **master**, und die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im Einzelbenutzermodus ausgeführt wird.  
-   Für eine andere Datenbank als **master**, aber die Datenbank wurde versetzt im Einzelbenutzermodus, indem Sie mit der ALTER DATABASE-Anweisung.  
-   Der Befehl wird für eine schreibgeschützte Datenbank ausgeführt.  
-   Der Befehl wird für eine Datenbank ausgeführt, für die mithilfe der ALTER DATABASE-Anweisung der Notfallmodus festgelegt wurde.  
-   Für **Tempdb**. In diesem Fall kann aufgrund interner Einschränkungen keine Datenbankmomentaufnahme erstellt werden.  
-   Der Befehl wird mit der WITH TABLOCK-Option ausgeführt. In diesem Fall berücksichtigt DBCC die Anforderung und erstellt keine Datenbankmomentaufnahme.  
  
Die DBCC-Befehle verwenden Tabellensperren anstelle der internen Datenbankmomentaufnahmen, wenn der Befehl für folgende Komponenten ausgeführt wird:
-   Eine schreibgeschützte Dateigruppe  
-   Ein FAT-Dateisystem  
-   Ein Volume, das 'benannte Datenströme' nicht unterstützt  
-   Ein Volume, das 'alternative Datenströme' nicht unterstützt  
  
> [!NOTE]  
>  Wird DBCC CHECKALLOC oder der entsprechende Teil von DBCC CHECKDB mithilfe der WITH TABLOCK-Option ausgeführt, muss hierfür die Datenbank exklusiv gesperrt (X) werden. Diese Datenbanksperre kann nicht festgelegt werden, auf **Tempdb** oder **master** und erzeugt wahrscheinlich bei allen anderen Datenbanken einen Fehler.  
  
> [!NOTE]  
>  DBCC CHECKDB schlägt fehl, wenn es sich bei der Ausführung für **master** Wenn eine interne Datenbankmomentaufnahme erstellt werden kann.  
  
## <a name="progress-reporting-for-dbcc-commands"></a>Statusmeldungen für DBCC-Befehle  
Die **Sys. dm_exec_requests** -Katalogsicht enthält Informationen zum Fortschritt und zur aktuellen Ausführungsphase der Befehle DBCC CHECKDB, CHECKFILEGROUP und CHECKTABLE. Die **Percent_complete** Spalte zeigt den Fortschritt des Befehls, und die **Befehl** Spalte meldet die aktuelle Phase der Ausführung des Befehls.
  
Die Definition einer Statuseinheit hängt von der aktuellen Ausführungsphase des DBCC-Befehls ab. Manchmal wird der Status mit der Granularität einer Datenbankseite angezeigt, in anderen Phasen wird er mit der Granularität einer einzelnen Datenbank oder Zuordnungsreparatur gemeldet. In der folgenden Tabelle werden die einzelnen Ausführungsphasen beschrieben sowie die Granularität, mit der der Status der Befehlsausführung gemeldet wird.
  
|Ausführungsphase|Description|Granularität der Statusmeldungen|  
|---------------------|-----------------|------------------------------------|  
|DBCC TABLE CHECK|Während dieser Phase wird die logische und physische Konsistenz der Objekte in der Datenbank geprüft.|Der Status wird auf Datenbankseitenebene angezeigt.<br /><br /> Wert der Statusmeldung wird für jede 1000 Datenbankseiten aktualisiert, die überprüft werden.|  
|DBCC TABLE REPAIR|Während dieser Phase werden Datenbankreparaturen ausgeführt, sofern REPAIR_FAST, REPAIR_REBUILD oder REPAIR_ALLOW_DATA_LOSS angegeben ist und Objektfehler vorliegen, die behoben werden müssen.|Der Status wird auf der Ebene einzelner Reparaturvorgänge angezeigt.<br /><br /> Der Zähler wird für jeden abgeschlossenen Reparaturvorgang aktualisiert.|  
|DBCC ALLOC CHECK|Während dieser Phase werden Zuordnungsstrukturen in der Datenbank geprüft.<br /><br /> Hinweis: DBCC CHECKALLOC überprüft die gleichen.|Der Status wird nicht gemeldet. |  
|DBCC ALLOC REPAIR|Während dieser Phase werden Datenbankreparaturen ausgeführt, sofern REPAIR_FAST, REPAIR_REBUILD oder REPAIR_ALLOW_DATA_LOSS angegeben ist und Zuordnungsfehler vorliegen, die behoben werden müssen.|Der Status wird nicht angezeigt.|  
|DBCC SYS CHECK|Während dieser Phase werden die Datenbanksystemtabellen geprüft.|Der Status wird auf Datenbankseitenebene angezeigt.<br /><br /> Der Wert der Statusmeldung wird nach jeweils 1000 geprüften Datenbankseiten aktualisiert.|  
|DBCC SYS REPAIR|Während dieser Phase werden Datenbankreparaturen ausgeführt, sofern REPAIR_FAST, REPAIR_REBUILD oder REPAIR_ALLOW_DATA_LOSS angegeben ist und Systemtabellenfehler vorliegen, die behoben werden müssen.|Der Status wird auf der Ebene einzelner Reparaturvorgänge angezeigt.<br /><br /> Der Zähler wird für jeden abgeschlossenen Reparaturvorgang aktualisiert.|  
|DBCC SSB CHECK|Während dieser Phase werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Broker-Objekte geprüft.<br /><br /> Hinweis: Diese Phase wird nicht ausgeführt, wenn DBCC CHECKTABLE ausgeführt wird.|Der Status wird nicht angezeigt.|  
|DBCC CHECKCATALOG|Während dieser Phase wird die Konsistenz von Datenbankkatalogen überprüft.<br /><br /> Hinweis: Diese Phase wird nicht ausgeführt, wenn DBCC CHECKTABLE ausgeführt wird.|Der Status wird nicht angezeigt.|  
|DBCC IVIEW CHECK|Während dieser Phase wird die logische Konsistenz aller in der Datenbank vorhandenen indizierten Sichten geprüft.|Der Status wird auf Ebene der einzelnen geprüften Datenbanksichten gemeldet.|  
  
## <a name="informational-statements"></a>Informative Anweisungen  
  
|||  
|-|-|  
|[DBCC INPUTBUFFER](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)|[DBCC SHOWCONTIG](../../t-sql/database-console-commands/dbcc-showcontig-transact-sql.md)|  
|[DBCC OPENTRAN](../../t-sql/database-console-commands/dbcc-opentran-transact-sql.md)|[DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)|  
|[DBCC OUTPUTBUFFER DARGESTELLTEN](../../t-sql/database-console-commands/dbcc-outputbuffer-transact-sql.md)|[DBCC TRACESTATUS](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)|  
|[DBCC PROCCACHE](../../t-sql/database-console-commands/dbcc-proccache-transact-sql.md)|[DBCC USEROPTIONS](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)|  
|[DBCC SHOW_STATISTICS](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)||  
  
## <a name="validation-statements"></a>Überprüfungsanweisungen  
  
|||  
|-|-|  
|[DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)|[DBCC CHECKFILEGROUP](../../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md)|  
|[DBCC CHECKCATALOG](../../t-sql/database-console-commands/dbcc-checkcatalog-transact-sql.md)|[DBCC CHECKIDENT](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)|  
|[DBCC CHECKCONSTRAINTS](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md)|[DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)|  
|[DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)||  
  
## <a name="maintenance-statements"></a>Verwaltungsanweisungen  
  
|||  
|-|-|  
|[DBCC CLEANTABLE](../../t-sql/database-console-commands/dbcc-cleantable-transact-sql.md)|[DBCC INDEXDEFRAG](../../t-sql/database-console-commands/dbcc-indexdefrag-transact-sql.md)|  
|[DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)|[DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)|  
|[DBCC DROPCLEANBUFFERS](../../t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql.md)|[DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)|  
|[DBCC FREEPROCCACHE](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)|[DBCC UPDATEUSAGE](../../t-sql/database-console-commands/dbcc-updateusage-transact-sql.md)|  
  
## <a name="miscellaneous-statements"></a>Sonstige Anweisungen  
  
|||  
|-|-|  
|[DBCC-DLL-Namen (FREE)](../../t-sql/database-console-commands/dbcc-dllname-free-transact-sql.md)|[DBCC HELP](../../t-sql/database-console-commands/dbcc-help-transact-sql.md)|  
|[DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)|[DBCC TRACEOFF](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)|  
|[DBCC FREESESSIONCACHE.](../../t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)|[DBCC TRACEON](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)|  
|[DBCC FREESYSTEMCACHE](../../t-sql/database-console-commands/dbcc-freesystemcache-transact-sql.md)|[DBCC ' CLONEDATABASE '](https://support.microsoft.com/en-us/kb/3177838) <br /><br /> **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Service Pack 2.|  
  
  

