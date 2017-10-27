---
title: Systeminterne Kompilierung von Tabellen und gespeicherten Prozeduren | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5880fbd9-a23e-464a-8b44-09750eeb2dad
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 5f74f31531f0b3c966235396d91ce12b00428d5c
ms.openlocfilehash: 922e6a4a0df86f82012670874d49b65e1338b53c
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="native-compilation-of-tables-and-stored-procedures"></a>Systeminterne Kompilierung von Tabellen und gespeicherten Prozeduren

Mit In-Memory OLTP wird das Konzept der systeminternen Kompilierung eingeführt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann gespeicherte Prozeduren, die auf speicheroptimierte Tabellen zugreifen, nativ kompilieren. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann außerdem speicheroptimierte Tabellen nativ kompilieren. Die systeminterne Kompilierung ermöglicht einen schnelleren Datenzugriff und eine effizientere Abfrageausführung als interpretiertes (herkömmliches) [!INCLUDE[tsql](../../includes/tsql-md.md)]. Beim systeminternen Kompilieren von Tabellen und gespeicherten Prozeduren werden DLLs erzeugt.

Die systeminterne Kompilierung von speicheroptimierten Tabellentypen wird ebenfalls unterstützt. Weitere Informationen finden Sie unter [Schnellere temporäre Tabellen und Tabellenvariablen durch Speicheroptimierung](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md).

Systeminterne Kompilierung bezieht sich auf den Prozess der Konvertierung von Programmkonstrukten in systemeigenen Code, der aus Prozessoranweisungen besteht, die keine weitere Kompilierung oder Interpretation erfordern.

In-Memory OLTP kompiliert speicheroptimierte Tabellen bei deren Erstellung sowie systemintern kompilierte gespeicherte Prozeduren beim Laden in systemeigene DLLs. Außerdem werden die DLLs nach einem Datenbank- oder Serverneustart neu kompiliert. Die zum erneuten Erstellen der DLLs erforderlichen Informationen werden in den Datenbankmetadaten gespeichert. Die DLLs sind nicht Teil der Datenbank, sie sind der Datenbank aber zugeordnet. Beispielsweise sind die DLLs nicht in den Datenbanksicherungen enthalten.

> [!NOTE]
> Speicheroptimierte Tabellen werden beim jedem Serverneustart neu kompiliert. Um die Datenbankwiederherstellung zu beschleunigen, werden systemintern kompilierte gespeicherte Prozeduren beim Serverneustart nicht neu kompiliert. Sie werden stattdessen bei der ersten Ausführung kompiliert. Aufgrund dieser verzögerten Kompilierung werden systemintern kompilierte gespeicherte Prozeduren erst dann angezeigt, wenn [sys.dm_os_loaded_modules &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-loaded-modules-transact-sql.md) nach der ersten Ausführung aufgerufen wird.

## <a name="maintenance-of-in-memory-oltp-dlls"></a>Wartung von In-Memory OLTP-DLLs

Die folgende Abfrage zeigt alle DLLs für Tabellen und gespeicherte Prozeduren, die aktuell in den Arbeitsspeicher des Servers geladen sind:

```tsql
SELECT
        mod1.name,
        mod1.description
    from
        sys.dm_os_loaded_modules  as mod1
    where
        mod1.description = 'XTP Native DLL';
```

Datenbankadministratoren müssen die Dateien, die von der systeminterne Kompilierung erstellt werden, nicht manuell pflegen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernt automatisch generierte Dateien, die nicht mehr benötigt werden. Beispielsweise werden generierte Dateien gelöscht, wenn eine Tabelle und eine gespeicherte Prozedur gelöscht werden, oder wenn eine Datenbank gelöscht wird.

> [!NOTE]
> Wenn Kompilierung fehlschlägt oder unterbrochen wird, werden einige generierte Dateien nicht entfernt. Diese Dateien werden absichtlich beibehalten, um die Unterstützbarkeit zu gewährleisten. Sie werden beim Löschen der Datenbank entfernt.

> [!NOTE]
> SQL Server kompiliert die DLLs für alle Tabellen, die für die Datenbankwiederherstellung erforderlich sind. Wenn eine Tabelle unmittelbar vor einem Neustart der Datenbank gelöscht wurde, können immer noch Reste der Tabelle in den Prüfpunktdateien oder dem Transaktionsprotokoll vorhanden sein, sodass die DLL für die Tabelle beim Datenbankstart neu kompiliert werden kann. Nach dem Neustart wird die DLL entladen, und die Dateien durch den normalen Bereigungsprozess entfernt.

## <a name="native-compilation-of-tables"></a>Systeminterne Kompilierung von Tabellen

Beim Erstellen einer speicheroptimierten Tabelle mithilfe der **CREATE TABLE** -Anweisung werden die Tabelleninformationen in die Datenbankmetadaten geschrieben und die Tabellen- und Indexstrukturen im Arbeitsspeicher erstellt. Die Tabelle wird außerdem zu einer DLL kompiliert.

Betrachten Sie das folgende Beispielskript, in dem eine Datenbank und eine speicheroptimierte Tabelle erstellt werden:

```tsql
USE master;
GO

CREATE DATABASE DbMemopt3;
GO

ALTER DATABASE DbMemopt3
    add filegroup DbMemopt3_mod_memopt_1_fg
        contains memory_optimized_data
;
GO

-- You must edit the front portion of filename= path, to where your DATA\ subdirectory is,
-- keeping only the trailing portion '\DATA\DbMemopt3_mod_memopt_1_fn'!

ALTER DATABASE DbMemopt3
    add file
    (
        name     = 'DbMemopt3_mod_memopt_1_name',
        filename = 'C:\DATA\DbMemopt3_mod_memopt_1_fn'

        --filename = 'C:\Program Files\Microsoft SQL Server\MSSQL13.SQLSVR2016ID\MSSQL\DATA\DbMemopt3_mod_memopt_1_fn'
    )
        to filegroup DbMemopt3_mod_memopt_1_fg
;
GO

USE DbMemopt3;
GO

CREATE TABLE dbo.t1
(
    c1 int not null primary key nonclustered,
    c2 int
)
    with (memory_optimized = on)
;
GO



-- You can safely rerun from here to the end.

-- Retrieve the path of the DLL for table t1.


DECLARE @moduleName  nvarchar(256);

SET @moduleName =
    (
        '%xtp_t_' +
        cast(db_id() as nvarchar(16)) +
        '_' +
        cast(object_id('dbo.t1') as nvarchar(16)) +
        '%.dll'
    )
;


-- SEARCHED FOR NAME EXAMPLE:  mod1.name LIKE '%xtp_t_8_565577053%.dll'
PRINT @moduleName;


SELECT
        mod1.name,
        mod1.description
    from
        sys.dm_os_loaded_modules  as mod1
    where
        mod1.name LIKE @moduleName
    order by
        mod1.name
;
-- ACTUAL NAME EXAMPLE:  mod1.name = 'C:\Program Files\Microsoft SQL Server\MSSQL13.SQLSVR2016ID\MSSQL\DATA\xtp\8\xtp_t_8_565577053_184009305855461.dll'
GO

--   DROP DATABASE DbMemopt3;  -- Clean up.
GO
```

Durch das Erstellen der Tabelle wird auch die Tabellen-DLL erstellt und in den Arbeitsspeicher geladen. Die DMV-Abfrage unmittelbar nach der CREATE TABLE-Anweisung ruft den Pfad der Tabellen-DLL ab.

Die Tabellen-DLL kann die Indexstrukturen und das Zeilenformat der Tabelle lesen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet die DLL für das Durchsuchen von Indizes, das Abrufen von Zeilen und das Speichern von Zeileninhalten.

## <a name="native-compilation-of-stored-procedures"></a>Systeminterne Kompilierung gespeicherter Prozeduren

Gespeicherte Prozeduren, die mit NATIVE_COMPILATION markiert sind, werden systemintern kompiliert. Dies bedeutet, dass alle [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen in der Prozedur in systemeigenen Code kompiliert werden, um eine effiziente Ausführung der leistungskritischen Geschäftslogik zu gewährleisten.

Weitere Informationen zu systemintern kompilierten gespeicherten Prozeduren finden Sie unter [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).

Betrachten Sie das folgende Beispiel für eine gespeicherte Prozedur, die Zeilen in die Tabelle t1 aus dem vorherigen Beispiel einfügt:

```tsql
CREATE PROCEDURE dbo.native_sp
    with native_compilation,
         schemabinding,
         execute as owner
as
begin atomic
    with (transaction isolation level = snapshot,
          language = N'us_english')

    DECLARE @i int = 1000000;

    WHILE @i > 0
    begin
        INSERT dbo.t1 values (@i, @i+1);
        SET @i -= 1;
    end
end;
GO

EXECUTE dbo.native_sp;
GO

-- Reset.

DELETE from dbo.t1;
GO
```

Die DLL für native_sp kann direkt mit der DLL für t1 sowie mit dem Speichermodul von In-Memory OLTP interagieren, sodass Zeilen in der kürzestmöglichen Zeit eingefügt werden können.

Der Compiler von In-Memory OLTP nutzt den Abfrageoptimierer, um einen effizienten Ausführungsplan für die einzelnen Abfragen in der gespeicherten Prozedur zu erstellen. Beachten Sie, dass systemintern kompilierte gespeicherte Prozeduren nicht automatisch neu kompiliert werden, wenn sich die Daten in der Tabelle ändern. Weitere Informationen zur Verwaltung von Statistiken und gespeicherten Prozeduren mit In-Memory-OLTP finden Sie unter [Statistiken für speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md).

## <a name="security-considerations-for-native-compilation"></a>Sicherheitsüberlegungen für systeminterne Kompilierung

Die systeminterne Kompilierung von Tabellen und gespeicherten Prozeduren verwendet den In-Memory OLTP-Compiler. Dieser Compiler erzeugt Dateien, die auf den Datenträger geschrieben und in den Arbeitsspeicher geladen werden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet die folgenden Mechanismen, um den Zugriff auf diese Dateien einzuschränken.

### <a name="native-compiler"></a>Systemeigener Compiler

Die ausführbare Compilerdatei sowie die Binärdateien und Headerdateien, die für die systeminterne Kompilierung erforderlich sind, werden als Teil der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz unter dem Ordner MSSQL\Binn\Xtp installiert. Wenn die Standardinstanz unter „C:\Programme“ installiert wird, werden die Compilerdateien in „C:\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL13.MSSQLSERVER\MSSQL\Binn\Xtp“ installiert.

Um den Zugriff auf den Compiler einzuschränken, verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Zugriffssteuerungslisten (ACLs), um den Zugriff auf die Binärdateien einzuschränken. Alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Binärdateien sind vor Änderungen oder Manipulation durch ACLs geschützt. Die ACLs des systemeigenen Compilers schränken auch das Verwenden des Compilers ein; nur das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto und Systemadministratoren haben Lese- und Ausführungsberechtigungen für systemeigene Compilerdateien.

### <a name="files-generated-by-a-native-compilation"></a>Durch eine systeminterne Kompilierung generierte Dateien

Die Dateien, die erzeugt werden, wenn eine Tabelle oder eine gespeicherte Prozedur kompiliert wird, umfassen die DLL und Zwischendateien, einschließlich Dateien mit den folgenden Erweiterungen: .c, .obj, .xml und .pdb. Die generierten Dateien werden in einem Unterordner des standardmäßigen Datenordners gespeichert. Der Unterordner wird Xtp genannt. Wenn Sie die Standardinstanz mit dem standardmäßigen Datenordner installieren, werden die generierten Dateien in „C:\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL13.MSSQLSERVER\MSSQL\DATA\Xtp“ abgelegt.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verhindert eine Manipulation der generierten DLLs auf drei Arten:

- Wenn eine Tabelle oder eine gespeicherte Prozedur zu einer DLL kompiliert wird, wird diese DLL sofort in den Arbeitsspeicher geladen und mit dem sqlserver.exe-Prozess verknüpft. Eine DLL kann nicht geändert werden, während sie mit einem Prozess verknüpft ist.

- Wenn eine Datenbank neu gestartet wird, werden alle Tabellen und gespeicherten Prozeduren auf der Grundlage der Datenbankmetadaten neu kompiliert (entfernt und neu erstellt). Hierdurch werden alle Änderungen, die von einem böswilligen Benutzer an einer generierten Datei vorgenommen wurden, entfernt.

- Die generierten Dateien werden als Teil der Benutzerdaten betrachtet und verfügen über die gleichen Sicherheitseinschränkungen (über ACLs) wie Datenbankdateien: Nur das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto und Systemadministratoren können auf diese Dateien zugreifen.

Zum Verwalten dieser Dateien ist keine Benutzerinteraktion erforderlich. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt und entfernt die Dateien nach Bedarf.

## <a name="see-also"></a>Siehe auch

[Speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)

[Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)

