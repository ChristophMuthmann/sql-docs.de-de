---
title: Computed_column_definition (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: ALTER TABLE statement
ms.assetid: 746eabda-3b4f-4940-b0b5-1c379f5cf7a5
caps.latest.revision: "62"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: faff7cbb4f4eec1cf68601805d0dbbe1a3a84b3e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="alter-table-computedcolumndefinition-transact-sql"></a>ALTER TABLE Computed_column_definition (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Eigenschaften einer berechneten Spalte, die zu einer Tabelle hinzugefügt wird [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
column_name AS computed_column_expression  
[ PERSISTED [ NOT NULL ] ]  
[   
    [ CONSTRAINT constraint_name ]  
    { PRIMARY KEY | UNIQUE }  
        [ CLUSTERED | NONCLUSTERED ]  
        [ WITH FILLFACTOR = fillfactor ]  
        [ WITH ( <index_option> [, ...n ] ) ]  
        [ ON { partition_scheme_name ( partition_column_name ) | filegroup   
            | "default" } ]  
    | [ FOREIGN KEY ]   
        REFERENCES ref_table [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE } ]   
        [ ON UPDATE { NO ACTION } ]   
        [ NOT FOR REPLICATION ]   
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )  
]  
```  
  
## <a name="arguments"></a>Argumente  
*Spaltenname*  
 Der Name der Spalte, die geändert, hinzugefügt oder gelöscht werden soll. *Column_name* kann zwischen 1 und 128 Zeichen sein. Bei neuen Spalten *Column_name* kann ausgelassen werden, für Spalten erstellt, die mit einem **Zeitstempel** -Datentyp. Wenn kein *Column_name* für angegeben wird eine **Zeitstempel** Spalte mit dem Datentyp, den Namen **Zeitstempel** verwendet wird.  
  
*computed_column_expression*  
 Ein Ausdruck, der den Wert einer berechneten Spalte definiert. Eine berechnete Spalte ist eine virtuelle Spalte, die nicht physisch in der Tabelle gespeichert ist, sondern anhand anderer Spalten in derselben Tabelle aus einem Ausdruck berechnet wird. Eine berechnete Spalte könnte z. B. die Definition besitzen: cost AS Price * qty. Der Ausdruck kann der Name einer nicht berechneten Spalte, eine Konstante, eine Funktion, eine Variable oder eine beliebige durch einen oder mehrere Operatoren verbundene Kombination der genannten Möglichkeiten sein. Der Ausdruck kann weder eine Unterabfrage sein noch einen Aliasdatentyp einschließen.  
  
 Berechnete Spalten können in Auswahllisten, WHERE-Klauseln, ORDER BY-Klauseln oder an anderen Stellen verwendet werden, an denen reguläre Ausdrücke verwendet werden. Dabei gelten folgende Ausnahmen:  
  
-   Eine berechnete Spalte kann nicht als DEFAULT- oder FOREIGN KEY-Einschränkungsdefinition oder mit einer NOT NULL-Einschränkungsdefinition verwendet werden. Eine berechnete Spalte kann jedoch als Schlüsselspalte in einem Index oder als Teil einer PRIMARY KEY- oder UNIQUE-Einschränkung verwendet werden, wenn der Wert der berechneten Spalte durch einen deterministischen Ausdruck definiert ist und der Datentyp des Ergebnisses in Indexspalten zulässig ist.  
  
     Falls die Tabelle z. B. die Spalten "a" und "b" vom Datentyp int aufweist, kann die berechnete Spalte "a + b" indiziert werden. Dagegen kann die berechnete Spalte "a + DATEPART(dd, GETDATE())" nicht indiziert werden, da sich der Wert in späteren Aufrufen ändern kann.  
  
-   Eine berechnete Spalte kann nicht das Ziel einer INSERT- oder UPDATE-Anweisung sein.  
  
    > [!NOTE]  
    >  Da jede Zeile in einer Tabelle unterschiedliche Werte für Spalten besitzen kann, die in einer berechneten Spalte verwendet werden, weist die berechnete Spalte möglicherweise auch nicht für jede Zeile das gleiche Ergebnis auf.  
  
PERSISTED  
 Gibt an, dass das [!INCLUDE[ssDE](../../includes/ssde-md.md)] die berechneten Werte physisch in der Tabelle speichert und die Werte aktualisiert, wenn Spalten, von denen die berechnete Spalte abhängt, aktualisiert werden. Durch das Markieren einer berechneten Spalte als PERSISTED kann ein Index für eine berechnete Spalte erstellt werden, die deterministisch, aber nicht präzise ist. Weitere Informationen finden Sie unter [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md). Alle berechneten Spalten, die als Partitionierungsspalten einer partitionierten Tabelle verwendet werden, müssen explizit als PERSISTED gekennzeichnet sein. *Computed_column_expression* muss deterministisch sein, wenn PERSISTED angegeben wird.  
NULL | NOT NULL  
 Gibt an, ob NULL-Werte in der Spalte zulässig sind. NULL ist genau genommen keine Einschränkung, kann jedoch auf die gleiche Weise verwendet werden wie NOT NULL. NOT NULL kann nur für berechnete Spalten angegeben werden, wenn auch PERSISTED angegeben ist.  
  
CONSTRAINT  
 Gibt den Beginn der Definition für eine PRIMARY KEY- oder UNIQUE-Einschränkung an.  
  
*constraint_name*  
 Die neue Einschränkung. Einschränkungsnamen müssen die Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md), außer dass der Name nicht werden mit einem Nummernzeichen gestartet (#). Wenn *Constraint_name* ist nicht angegeben wird, wird die Einschränkung eine vom System generierter Name zugewiesen.  
  
PRIMARY KEY  
 Eine Einschränkung, die Entitätsintegrität für eine angegebene Spalte (oder Spalten) mithilfe eines eindeutigen Index erzwingt. Es kann nur eine PRIMARY KEY-Einschränkung für jede Tabelle erstellt werden.  
  
UNIQUE  
 Eine Einschränkung, die Entitätsintegrität für eine angegebene Spalte (oder Spalten) mithilfe eines eindeutigen Index bereitstellt.  
  
CLUSTERED | NONCLUSTERED  
 Gibt an, dass ein gruppierter oder nicht gruppierter Index für die PRIMARY KEY- oder UNIQUE-Einschränkung erstellt wird. Für PRIMARY KEY-Einschränkungen wird standardmäßig CLUSTERED verwendet. Für UNIQUE-Einschränkungen wird standardmäßig NONCLUSTERED verwendet.  
  
 Wenn bereits eine gruppierte Einschränkung oder ein gruppierter Index für eine Tabelle vorhanden ist, kann CLUSTERED nicht angegeben werden. Wenn bereits eine gruppierte Einschränkung oder ein gruppierter Index für eine Tabelle vorhanden ist, wird für PRIMARY KEY-Einschränkungen standardmäßig NONCLUSTERED verwendet.  
  
MIT FILLFACTOR =*Fillfactor*  
 Gibt an, wie weit [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] die einzelnen Indexseiten füllen soll, die zum Speichern der Indexdaten verwendet werden. Benutzerdefiniertes *Fillfactor* Werte können zwischen 1 und 100 sein. Wenn kein Wert angegeben ist, lautet der Standardwert 0.  
  
> [!IMPORTANT]  
>  Dokumentieren mit FILLFACTOR = *Fillfactor* als einzige Indexoption, für die PRIMARY KEY- oder UNIQUE-Einschränkungen gilt wird aus Gründen der Abwärtskompatibilität beibehalten, jedoch nicht auf diese Weise in Zukunft dokumentiert wird frei. Andere Indexoptionen können angegeben werden, der [Index_option &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-index-option-transact-sql.md) -Klausel der ALTER TABLE.  
  
FOREIGN KEY REFERENCES  
 Eine Einschränkung, die referenzielle Integrität für die Daten in der Spalte oder den Spalten bereitstellt. FOREIGN KEY-Einschränkungen erfordern, dass jeder Wert in der Spalte in den entsprechenden Spalten, auf die verwiesen wird, in der Tabelle, auf die verwiesen wird, vorhanden ist. FOREIGN KEY-Einschränkungen können nur auf Spalten verweisen, die PRIMARY KEY- oder UNIQUE-Einschränkungen in der Tabelle sind, auf die verwiesen wird; oder auf Spalten, auf die in einer UNIQUE INDEX-Einschränkung in der Tabelle, auf die verwiesen wird, verwiesen wird. Fremdschlüssel für berechnete Spalten müssen auch als PERSISTED markiert werden.  
  
*ref_table*  
 Der Name der Tabelle, auf die die FOREIGN KEY-Einschränkung verweist.  
  
(*Ref_column* )  
 Eine Spalte aus der Tabelle, auf die die FOREIGN KEY-Einschränkung verweist.  
  
ON DELETE { **NICHTS** | CASCADE}  
 Gibt an, welche Aktion für Zeilen in der Tabelle ausgeführt werden soll, wenn diese Zeilen eine referenzielle Beziehung aufweisen und die Zeile, auf die verwiesen wird, aus der übergeordneten Tabelle gelöscht wird. Der Standardwert ist NO ACTION.  
  
NO ACTION  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] löst einen Fehler aus, und für die Aktion zum Löschen der Zeile in der übergeordneten Tabelle wird ein Rollback ausgeführt.  
CASCADE  
 Wenn diese Zeile aus der übergeordneten Tabelle gelöscht wird, werden die entsprechenden Zeilen aus der verweisenden Tabelle gelöscht.  
  
 In der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank verfügt die ProductVendor-Tabelle beispielsweise über eine referenzielle Beziehung zur Vendor-Tabelle. Der ProductVendor.BusinessEntityID-Fremdschlüssel verweist auf den Vendor.BusinessEntityID-Primärschlüssel.  
  
 Wenn eine DELETE-Anweisung für eine Zeile in der Vendor-Tabelle ausgeführt wird und eine ON DELETE CASCADE-Aktion für ProductVendor.BusinessEntityID festgelegt ist, sucht das [!INCLUDE[ssDE](../../includes/ssde-md.md)] nach mindestens einer abhängigen Zeile in der ProductVendor-Tabelle. Falls vorhanden, werden die abhängigen Zeilen in der ProductVendor-Tabelle gelöscht, ebenso wie die Zeile, auf die in der Vendor-Tabelle verwiesen wird.  
  
 Ist hingegen NO ACTION angegeben, löst das [!INCLUDE[ssDE](../../includes/ssde-md.md)] einen Fehler aus und führt ein Rollback für die Löschaktion der Vendor-Zeile aus, wenn in der ProductVendor-Tabelle mindestens eine Zeile vorhanden ist, die auf diese Zeile verweist.  
  
 Geben Sie CASCADE nicht an, wenn die Tabelle in eine Mergeveröffentlichung einbezogen werden soll, bei der logische Datensätze verwendet werden. Weitere Informationen zu logischen Datensätzen finden Sie unter [Gruppieren von Änderungen an verknüpften Zeilen mithilfe von logischen Datensätzen](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
BEI UPDATE { **NICHTS** }  
 Gibt an, welche Aktion für Zeilen in der Tabelle ausgeführt werden soll, wenn diese Zeilen eine referenzielle Beziehung aufweisen und die Zeile, auf die verwiesen wird, in der übergeordneten Tabelle aktualisiert wird. Wenn jedoch NO ACTION angegeben ist, löst das [!INCLUDE[ssDE](../../includes/ssde-md.md)] einen Fehler aus und führt für die Aktion zum Aktualisieren der Vendor-Zeile ein Rollback aus, falls sich mindestens eine Zeile in der ProductVendor-Tabelle befindet, die auf diese Zeile verweist.  
  
NOT FOR REPLICATION  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Kann für FOREIGN KEY- und CHECK-Einschränkungen festgelegt werden. Wenn diese Klausel für eine Einschränkung angegeben wird, wird die Einschränkung nicht erzwungen, wenn Replikations-Agents Einfüge-, Update- oder Löschvorgänge ausführen.  
  
CHECK  
 Eine Einschränkung, die Domänenintegrität erzwingt, indem die möglichen Eingabewerte für eine oder mehrere Spalten beschränkt wird. CHECK-Einschränkungen für berechnete Spalten müssen auch als PERSISTED markiert werden.  
  
*Logical_Expression*  
 Ein logischer Ausdruck, der TRUE oder FALSE zurückgibt. Der Ausdruck kann nicht über einen Verweis auf einen Aliasdatentyp enthalten.  
  
ON { *Partition_scheme_name*(*Partition_column_name*) | *Dateigruppe*| "Default"}  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt den Speicherort des Indexes an, der für die Einschränkung erstellt wurde. Wenn *Partition_scheme_name* angegeben wird, wird der Index partitioniert und die Partitionen werden den Dateigruppen, die vom angegebenen zugeordnet *Partition_scheme_name*. Wenn *Dateigruppe* angegeben ist, wird der Index in der genannten Dateigruppe erstellt. Wenn "default" angegeben ist, oder wenn ON für alle festgelegt ist, wird der Index in derselben Dateigruppe erstellt wie die Tabelle. Wenn ON beim Hinzufügen eines gruppierten Index für eine PRIMARY KEY- oder UNIQUE-Einschränkung angegeben ist, wird die gesamte Tabelle beim Erstellen des gruppierten Index in die angegebene Dateigruppe verschoben.  
  
> [!NOTE]  
>  In diesem Zusammenhang ist DEFAULT kein Schlüsselwort. Es handelt sich dabei um einen Bezeichner für die Standarddateigruppe, der begrenzt sein muss, wie in ON "default" oder ON [default]. Wenn "default" angegeben wird, muss die Option QUOTED_IDENTIFIER für die aktuelle Sitzung auf ON festgelegt sein. Dies ist die Standardeinstellung. Weitere Informationen finden Sie unter [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
## <a name="remarks"></a>Hinweise  
 Jede PRIMARY KEY- und UNIQUE-Einschränkung generiert einen Index. Die Anzahl der UNIQUE- und PRIMARY KEY-Einschränkungen darf nicht dazu führen, dass die Anzahl der Indizes der Tabelle 999 nicht gruppierte Indizes und 1 gruppierten Index übersteigt.  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
