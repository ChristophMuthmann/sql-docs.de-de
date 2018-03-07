---
title: "ALTER DATABASE-Kompatibilitätsgrad (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/30/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COMPATIBILITY_LEVEL_TSQL
- COMPATIBILITY_LEVEL
dev_langs:
- TSQL
helpviewer_keywords:
- 80 compatibility level
- ALTER DATABASE statement, compatibility levels
- 90 compatibility level
- compatibility levels [SQL Server]
- 100 compatibility level
- db compatibility level
- db compat level
ms.assetid: ca5fd220-d5ea-4182-8950-55d4101a86f6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 750578d028077079b051a08cc2a0ed4276983cda
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="alter-database-transact-sql-compatibility-level"></a>ALTER DATABASE (Transact-SQL) Compatibility Level
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Legt für bestimmte Verhalten der Datenbank fest, dass sie mit der angegebenen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kompatibel sein müssen. Weitere ALTER DATABASE-Optionen finden Sie unter [ALTER DATABASE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ALTER DATABASE database_name   
SET COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 | 90 }  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Der Name der Datenbank, die geändert werden soll.  
  
 COMPATIBILITY_LEVEL {140 | 130 | 120 | 110 | 100 | 90 | 80}  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Version, mit der die Datenbank kompatibel sein soll. Die folgenden Compatibility Level-Werte können konfiguriert werden:  
  
|Product|Datenbank-Engine-Version|Compatibility Level-Bezeichnung|Unterstützte Werte für die Kompatibilität|  
|-------------|-----------------------------|-------------------------------------|------------------------------------------|  
|[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]|14|140|140, 130, 120, 110, 100|
|[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|12|130|140, 130, 120, 110, 100|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|13|130|130, 120, 110, 100|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|12|120|120, 110, 100|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|11|110|110, 100, 90|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|10.5|100|100, 90, 80|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|10|100|100, 90, 80|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|9|90|90, 80|  
|SQL Server 2000|8|80|80|  
  
> [!NOTE]  
> **Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)]**  V12 vom Dezember 2014 veröffentlicht wurde. Ein Aspekt dieser Version wurden neu erstellte Datenbanken ihren Kompatibilitätsgrad auf jeweils 120 festgelegt wurde. 2015 begann SQL-Datenbank-Unterstützung für Kompatibilitätsgrad 130, obwohl die Standardeinstellung 120 verblieben sind.  
> 
> Ab **Mitte Juni 2016**im [!INCLUDE[ssSDS](../../includes/sssds-md.md)], der Standardkompatibilitätsgrad sind 130 anstelle von 120 für **neu erstellten** Datenbanken. Vorhandene Datenbanken erstellt, bevor Sie Mitte Juni 2016 sind nicht betroffen und verwalten ihren aktuellen Kompatibilitätsgrad (100, 110 und 120). 
> 
> Wenn Sie Kompatibilitätsgrad 130 für Ihre Datenbank in der Regel, jedoch Grund die Ebene 110 bevorzugt haben **Schätzung der Kardinalität** -Algorithmus finden Sie unter [ALTER DATABASE SCOPED CONFIGURATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md), insbesondere das Schlüsselwort `LEGACY_CARDINALITY_ESTIMATION = ON`.  
>  
>  Weitere Informationen dazu, wie bewerten Sie die Leistungsunterschiede zwischen beiden Kompatibilitätsgrade Ihrer wichtigsten Abfragen in [!INCLUDE[ssSDS](../../includes/sssds-md.md)], finden Sie unter [verbessert die Abfrageleistung mit Kompatibilität Ebene 130 in Azure SQL-Datenbank](http://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/).


 Führen Sie die folgende Abfrage zum Ermitteln der Version von den [!INCLUDE[ssDE](../../includes/ssde-md.md)] , der Sie verbunden sind.  
  
```sql  
SELECT SERVERPROPERTY('ProductVersion');  
```  
  
> [!NOTE]  
> Unterstützt nicht alle Funktionen, die auf den Kompatibilitätsgrad variieren auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  

 Um den aktuellen Kompatibilitätsgrad zu ermitteln, Fragen den **Compatibility_level** Spalte [sys.databases &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
```sql  
SELECT name, compatibility_level FROM sys.databases;  
```  
  
## <a name="remarks"></a>Hinweise  
Für alle Installationen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], der standardmäßige Kompatibilitätsgrad festgelegt ist, auf die Version von den [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Datenbanken werden auf diesen Grad festgelegt, es sei denn, die **Modell** Datenbank hat einen niedrigeren Kompatibilitätsgrad. Beim Upgrade einer Datenbank aus einer früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die Datenbank behält den vorhandenen Kompatibilitätsgrad, wenn es mindestens minimale zulässig, die für diese Instanz von ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eine Datenbank mit einem Kompatibilitätsgrad kleiner als die zulässige Ebene aktualisiert wurde, wird die Datenbank auf die niedrigste Kompatibilität Ebene zulässig. Dies gilt sowohl für die System- als auch für die Benutzerdatenbanken. Verwendung **ALTER DATABASE** so ändern Sie den Kompatibilitätsgrad der Datenbank. Um den aktuellen Kompatibilitätsgrad einer Datenbank anzuzeigen, Fragen Sie die **Compatibility_level** Spalte in der [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht angezeigt.  
  
## <a name="using-compatibility-level-for-backward-compatibility"></a>Verwenden des Kompatibilitätsgrads für die Abwärtskompatibilität  
 Der Kompatibilitätsgrad wirkt sich nicht auf den gesamten Server, sondern nur auf das Verhalten der angegebenen Datenbank aus. Der Kompatibilitätsgrad bietet nur partielle Abwärtskompatibilität mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Beginnend mit Kompatibilitätsmodus 130, wurden keine neuen Abfrage-Plan beeinflussende Funktionen nur für den neuen Kompatibilitätsmodus hinzugefügt. Dies wurde bereits durchgeführt, um das Risiko, dass während des Upgrades zu minimieren, die von Leistungseinbußen aufgrund von Änderungen an Abfrageplänen auftreten. Aus Sicht einer Anwendung ist das Ziel weiterhin mit den neuesten Kompatibilitätsgrad um einige der neuen Funktionen als auch leistungsverbesserungen, die in der Optimierer abfrageumgebung fertig erben jedoch dazu kontrolliert werden. Verwenden Sie den Kompatibilitätsgrad als vorläufige Migrationshilfe, um versionsbedingte Unterschiede in den Verhaltensweisen zu umgehen, die über die jeweilige Einstellung für den Kompatibilitätsgrad gesteuert werden. Weitere Informationen finden Sie in das Upgrade best Practices später in diesem Artikel.  
  
 Wenn vorhandener [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anwendungen auswirken, Verhaltensunterschiede in Ihrer Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Konvertieren der Anwendung in die nahtlose Zusammenarbeit mit den neuen Kompatibilitätsmodus. Verwenden Sie dann `ALTER DATABASE` so ändern Sie den Kompatibilitätsgrad in "130". Die neue kompatibilitätseinstellung für eine Datenbank in Kraft, wenn eine `USE <database>` ausgegeben wird oder eine neue Anmeldung für diese Datenbank als Standarddatenbank verarbeitet wird.  
 
> [!IMPORTANT]
> Nicht mehr unterstützte Funktionen, eingeführt in einer bestimmten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Version ist nicht auf den Kompatibilitätsgrad geschützt.
> 
> Z. B. die `FASTFIRSTROW` Hinweis wurde in nicht mehr [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und durch die `OPTION (FAST n )` Hinweis. Der Datenbank-Kompatibilitätsgrad auf 110 festlegen, wird nicht mehr unterstützte Hinweis nicht wiederhergestellt.
> Weitere Informationen zu nicht mehr unterstützte Funktionen finden Sie unter [nicht mehr unterstützte Datenbankmodul-Funktionalität in SQL Server 2016](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md), [nicht mehr unterstützte Datenbankmodul-Funktionalität in SQL Server 2014](http://msdn.microsoft.com/library/ms144262(v=sql.120)), [Nicht mehr unterstützte Datenbankmodul-Funktionalität in SQLServer 2012](http://msdn.microsoft.com/library/ms144262(v=sql.110)), und [nicht mehr unterstützte Datenbankmodul-Funktionalität in SQLServer 2008](http://msdn.microsoft.com/library/ms144262(v=sql.100)).

> [!IMPORTANT]
> Wichtige Änderungen in eingeführte einer bestimmten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Version **möglicherweise** nicht geschützt werden, auf den Kompatibilitätsgrad. [!INCLUDE[tsql](../../includes/tsql-md.md)]das Verhalten wird normalerweise auf den Kompatibilitätsgrad geschützt. Allerdings Systemobjekte geändert oder entfernt werden **nicht** auf den Kompatibilitätsgrad geschützt.
>
> Ein Beispiel für eine wichtige Änderung **geschützt** Compatibility Level ist eine implizite Konvertierung von "DateTime" in datetime2-Datentypen. Unter Datenbank-Kompatibilitätsgrad 130 zur Verfügung werden diese Verbesserte Genauigkeit unter Berücksichtigung der Bruchteilen von Millisekunden, führt verschiedene Werte konvertiert. Legen Sie zum Wiederherstellen der vorherigen Konvertierungsverhalten Kompatibilitätsgrad der Datenbank auf 120 oder niedriger.
>
> Beispiele für Änderungen, die die **nicht geschützt** Compatibility Level sind:
> -  Geänderte Spaltennamen in Systemobjekten. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Spalte *Single_pages_kb* in Sys. dm_os_sys_info wurde umbenannt in *Pages_kb*. Unabhängig vom Kompatibilitätsgrad der Abfrage `SELECT single_pages_kb FROM sys.dm_os_sys_info` Fehler 207 (Ungültiger Spaltenname) erzeugt.
> -  Entfernte Objekte. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] der `sp_dboption` wurde entfernt. Unabhängig vom Kompatibilitätsgrad der Anweisung `EXEC sp_dboption 'AdventureWorks2016CTP3', 'autoshrink', 'FALSE';` tritt Fehler 2812 (nicht gefunden gespeicherte Prozedur 'Sp_dboption').
>
> Weitere Informationen über wichtige Änderungen finden Sie unter [fehlerhafte Änderungen an Funktionen des Datenbankmoduls in SQL Server-2017](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2017.md), [fehlerhafte Änderungen an Funktionen des Datenbankmoduls in SQL Server 2016](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md), [ Wichtige Änderungen an der Datenbank-Engine-Funktionen in SQLServer 2014](http://msdn.microsoft.com/library/ms143179(v=sql.120)), [fehlerhafte Änderungen an Funktionen des Datenbankmoduls in SQLServer 2012](http://msdn.microsoft.com/library/ms143179(v=sql.110)), und [fehlerhafte Änderungen an Funktionen des Datenbankmoduls in SQL Server 2008](http://msdn.microsoft.com/library/ms143179(v=sql.100)).
  
## <a name="best-practices"></a>Bewährte Methoden  
Der empfohlene Workflow für den Kompatibilitätsgrad aktualisieren, finden Sie unter [Ändern des Datenbank-Kompatibilitätsmodus und Verwenden des Abfragespeichers](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md).  
  
## <a name="compatibility-levels-and-stored-procedures"></a>Kompatibilitätsgrade und gespeicherte Prozeduren  
 Wenn eine gespeicherte Prozedur ausgeführt wird, verwendet sie den aktuellen Kompatibilitätsgrad der Datenbank, in der sie definiert ist. Wenn die Kompatibilitätseinstellung einer Datenbank geändert wird, werden alle zugehörigen gespeicherten Prozeduren automatisch entsprechend neu kompiliert.  

## <a name="differences-between-compatibility-level-130-and-level-140"></a>Unterschiede zwischen Kompatibilitätsgrad 130 und 140 Ebene  
In diesem Abschnitt wird beschrieben, neue Verhaltensweisen, die mit Kompatibilitätsgrad 140 eingeführt wurde.

|Kompatibilitätsgradeinstellung von 130 oder niedriger|Kompatibilitätsgradeinstellung von 140|  
|--------------------------------------------------|-----------------------------------------|  
|Kardinalität geschätzt für Anweisungen, die auf die Tabellenwertfunktion mit mehreren Anweisungen verweist, Funktionen eine festen Zeile Schätzung.|Kardinalitätsschätzung für geeignete Anweisungen, die auf die Tabellenwertfunktion mit mehreren Anweisungen verweist, dass Funktionen, die tatsächliche Kardinalität der Funktion Ausgabe verwendet werden.  Dies erfolgt über **interleaved Ausführung** für mit mehreren Anweisungen Tabellenwertfunktionen.|
|Batchmodus Abfragen, von die nicht genügend Arbeitsspeicher angefordert erteilen Größen, die weiterhin haben Probleme auf aufeinander folgenden Ausführungen führen zu auf den Datenträger überlaufen.|Batchmodus Abfragen, die nicht genügend Arbeitsspeicher Grant Größen anfordern, dass auf den Datenträger überlaufen führen eine verbesserte Leistung auf aufeinander folgenden Ausführungen aufweisen kann. Dies erfolgt über **Batch Modus arbeitsspeicherzuweisungen Feedback** aktualisiert die der Größe der arbeitsspeicherzuweisung eines zwischengespeicherten Plans überlaufen für batchmodusoperatoren aufgetreten sind. |
|Batchmodus Abfragen, die eine übermäßig viel Arbeitsspeicher anfordern erteilen, Größe, die Ergebnisse in Parallelitätsprobleme weiterhin Probleme von aufeinander folgenden Ausführungen aufweisen.|Batchmodus Abfragen, die eine übermäßig viel Arbeitsspeicher anfordern gewähren Größe, die zu Parallelitätsprobleme führt Parallelität in aufeinander folgenden Ausführungen verbessert haben kann. Dies erfolgt über **Batch Modus arbeitsspeicherzuweisungen Feedback** die können die Größe der arbeitsspeicherzuweisung eines zwischengespeicherten Plans werden aktualisiert, wenn es sich bei extrem ursprünglich angefordert wurde.|
|Batchmodus Abfragen, die Joins enthalten, sind für drei physischen joinalgorithmen, einschließlich geschachtelter Schleifen, HashJoin und MergeJoin geeignet. Wenn kardinalitätsschätzungen für joineingaben falsch sind, kann ein ungeeignete Join-Algorithmus ausgewählt werden. In diesem Fall wird die Leistung darunter leiden und bleibt die ungeeigneten Join-Algorithmus verwendet, bis der zwischengespeicherte Plan erneut kompiliert wird.|Es wird eine weitere Join-Operator aufgerufen **adaptive Join**. Wenn kardinalitätsschätzungen für die äußere Join Erstellungseingabe falsch sind, kann ein ungeeignete Join-Algorithmus ausgewählt werden. Wenn dies auftritt, und die Anweisung für eine adaptive Join berechtigt ist, eine geschachtelte Schleife wird für kleinere joineingaben verwendet werden, und ein HashJoin wird ohne Neukompilierung dynamisch für größere joineingaben verwendet werden. |
|Trivial Pläne verweisen auf columnstore-Indizes sind nicht für die batchmodusausführung geeignet. |Ein trivialer Plan verweisen auf columnstore-Indizes werden zugunsten eines Plans verworfen, die für die batchmodusausführung geeignet sind.|
|Die `sp_execute_external_script` UDX-Operator kann nur im Zeilenmodus ausgeführt.|Die `sp_execute_external_script` UDX-Operator für die batchmodusausführung geeignet ist.|  
|Mit mehreren Anweisungen Tabellenwertfunktionen (TVF) müssen keine verschachtelten Ausführung |Verschachtelte Ausführung für Tabellenwertfunktionen mit mehreren Anweisungen, zur Verbesserung der Qualität des Abfrageplans. |

Updates, die unter dem Ablaufverfolgungsflag 4199 in früheren Versionen von SQL Server vor SQL Server 2017 wurden sind jetzt standardmäßig aktiviert. Mit Kompatibilitätsmodus 140. Das Ablaufverfolgungsflag 4199 können immer noch für die neuen Fehlerbehebungen durch Abfrageoptimierer Objekte umgesetzt werden, die nach dem SQL Server-2017 veröffentlicht werden. Informationen zum Ablaufverfolgungsflag 4199 finden Sie unter [Ablaufverfolgungsflag 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199).  
  
## <a name="differences-between-compatibility-level-120-and-level-130"></a>Unterschiede zwischen Kompatibilitätsgrad 120 und 130 Ebene  
In diesem Abschnitt wird beschrieben, neue Verhaltensweisen, die mit Kompatibilitätsgrad 130 eingeführt wurde.   

|Kompatibilitätsgradeinstellung 120 oder niedriger|Kompatibilitätsgradeinstellung von 130|  
|--------------------------------------------------|-----------------------------------------|  
|Die INSERT-Anweisung in einer Insert Select-Anweisung ist eine Singlethread.|Die INSERT-Anweisung in einer Insert Select-Anweisung mit mehreren Threads ist oder einen parallelen Plan haben.|  
|Abfragen für eine Speicheroptimierte Tabelle ausführen Singlethread.|Abfragen für eine Speicheroptimierte Tabelle haben jetzt parallele Pläne.|  
|SQL 2014-kardinalitätsschätzung eingeführt **CardinalityEstimationModelVersion = "120"**|Weitere Kardinalität planen Schätzung (CE)-Verbesserungen mit der Kardinalität Schätzung Modell 130 der aus einer Abfrage angezeigt wird. **CardinalityEstimationModelVersion="130"**|  
|Batch-Modus im Vergleich zu Zeilenmodus Änderungen mit columnstore-Indizes<br /><br /> Für eine Tabelle mit columnstore-Index sortiert sind, im Zeilenmodus<br /><br /> Arbeiten im Zeilenmodus fensteraggregate-Funktion z. B. `LAG` oder`LEAD`<br /><br /> Abfragen für columnstore-Tabellen mit mehrere distinct-Klauseln, die für den Betrieb in Zeilenmodus<br /><br /> Abfragen unter MAXDOP 1 oder mit einem seriellen Plan ausgeführt wird, im Zeilenmodus | Batch-Modus im Vergleich zu Zeilenmodus Änderungen mit columnstore-Indizes<br /><br /> Sortierungen in einer Tabelle mit einem columnstore-Index befinden sich jetzt im Batchmodus<br /><br /> Fensteraggregate verarbeiten nun im Batchmodus ausgeführt wie z. B. `LAG` oder`LEAD`<br /><br /> Abfragen für columnstore-Tabellen mit mehrere distinct-Klauseln, die im Batchmodus ausgeführt werden<br /><br /> Abfragen oder mit einem seriellen Plan unter Maxdop1 abfrageplanausführung im Batchmodus|  
| Statistiken können automatisch aktualisiert werden. | Die Logik, die Statistiken automatisch aktualisiert wird, ist bei umfangreichen Tabellen aggressiver.  In der Praxis sollten dies verringern, Fälle, in denen Kunden Leistungsprobleme auf Abfragen ermittelt wurden, auf dem neu eingefügte Zeilen abgefragt werden, oft, aber, in dem die Statistiken nicht aktualisiert wurde, die Werte enthalten sind. |  
| Trace 2371 ist standardmäßig in deaktiviert [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. | [Verfolgen Sie 2371](https://blogs.msdn.microsoft.com/psssql/2016/10/04/default-auto-statistics-update-threshold-change-for-sql-server-2016/) ist standardmäßig in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Das Ablaufverfolgungsflag 2371 weist des automatisch Statistiken Updaters auf eine kleinere noch weiser Teilmenge von Zeilen in einer Tabelle Beispieldaten, die eine hervorragende viele Zeilen enthält. <br/> <br/> Eine Verbesserung besteht darin, in der Stichprobe mehr Zeilen enthalten, die vor kurzem eingefügt wurden. <br/> <br/> Eine andere Verbesserung ist, können Abfragen ausgeführt werden, während der Update Statistics-Prozess wird ausgeführt, anstatt Sperren der Abfrage. |  
| Für Kompatibilitätsgrad 120 Statistiken aufgenommen werden, indem eine *einzelne*-Thread des Prozesses. | Für Kompatibilitätsgrad 130 Statistiken aufgenommen werden, indem eine *Multi*-Thread des Prozesses. |  
| 253 eingehende Fremdschlüssel liegt die Beschränkung. | Eine bestimmte Tabelle kann bis zu 10.000 eingehende Fremdschlüsseln oder ähnliche Verweise verweist. Einschränkungen finden Sie unter [Create Foreign Key Relationships](../../relational-databases/tables/create-foreign-key-relationships.md). |  
|Die als veraltet markierte Hashalgorithmen MD2, MD4, MD5, SHA und SHA1 sind zulässig.|Nur SHA2_256 und SHA2_512 Hashalgorithmen sind zulässig.|
||[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bietet Verbesserungen in einige Typen datenkonvertierungen sowie bei einigen Vorgängen (hauptsächlich ungewöhnlich). Weitere Informationen finden Sie [SQL Server 2016-Verbesserungen bei der Verarbeitung von einigen Datentypen und ungewöhnlich, dass Vorgänge](https://support.microsoft.com/help/4010261/sql-server-2016-improvements-in-handling-some-data-types-and-uncommon).|
  
Korrekturen, die unter Trace flag 4199 in früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] sind jetzt standardmäßig aktiviert. Mit Kompatibilitätsmodus 130. Das Ablaufverfolgungsflag 4199 zur Verfügung gestellt werden trotzdem gilt für das neue Fehlerbehebungen durch Abfrageoptimierer, die nach der Veröffentlichung sind [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Verwenden den älteren Abfrageoptimierer [!INCLUDE[ssSDS](../../includes/sssds-md.md)] müssen Sie den Kompatibilitätsgrad 110 auswählen. Informationen zum Ablaufverfolgungsflag 4199 finden Sie unter [Ablaufverfolgungsflag 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md#4199).  
  
## <a name="differences-between-lower-compatibility-levels-and-level-120"></a>Unterschiede zwischen niedrigeren Kompatibilitätsgraden und Kompatibilitätsgrad 120  
 In diesem Abschnitt werden neue mit Kompatibilitätsgrad 120 eingeführte Verhaltensweisen beschrieben.  
  
|Kompatibilitätsgradeinstellung 110 oder niedriger|Kompatibilitätsgradeinstellung 120|  
|--------------------------------------------------|-----------------------------------------|  
|Der ältere Abfrageoptimierer wird verwendet.|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bietet erhebliche Verbesserungen an die Komponente, die erstellt und optimiert die Abfragepläne. Diese neue Funktion des Abfrageoptimierers ist nur bei Verwendung des Datenbank-Kompatibilitätsgrads 120 verfügbar. Damit diese Verbesserungen optimal genutzt werden können, sollten neue Datenbankanwendungen mit dem Datenbank-Kompatibilitätsgrad 120 entwickelt werden. Von früheren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Versionen migrierte Anwendungen sollten sorgfältig daraufhin überprüft werden, ob die bisherige gute Leistung aufrechterhalten bzw. verbessert wird. Wird die Leistung beeinträchtigt, können Sie den Kompatibilitätsgrad der Datenbank auf 110 oder einen niedrigeren Wert festlegen, um die ältere Methodologie des Abfrageoptimierers zu nutzen.<br /><br /> Der Datenbank-Kompatibilitätsgrad 120 verwendet eine neue Kardinalitätsschätzung, die für moderne Data Warehousing- und OLTP-Arbeitsauslastungen optimiert ist. Vor dem Festlegen von Datenbank-Kompatibilitätsgrad auf 110 aufgrund von Leistungsproblemen, finden Sie die Empfehlungen im Abschnitt Abfragepläne, der die [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [Neuigkeiten im Datenbankmodul](../../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md) Thema.|  
|Bei Kompatibilitätsgraden unter 120, wird die Language-Einstellung ignoriert, beim Konvertieren einer **Datum** Wert in einen Zeichenfolgenwert. Beachten Sie, dass dieses Verhalten nur für bestimmte ist die **Datum** Typ. Siehe Beispiel B im Abschnitt "Beispiele" weiter unten.|Die Language-Einstellung wird nicht ignoriert werden, bei der Konvertierung einer **Datum** Wert in einen Zeichenfolgenwert.|  
|Rekursive Verweise auf die rechte Seite des ein `EXCEPT` Klausel erzeugen eine Endlosschleife. Beispiel C im Abschnitt "Beispiele" weiter unten veranschaulicht dieses Verhalten.|Rekursive Verweise in einem `EXCEPT` -Klausel generiert einen Fehler in Übereinstimmung mit dem ANSI SQL-Standard.|  
|Rekursive allgemeine Tabellenausdruck (CTE) lässt doppelte Spaltennamen.|Der rekursive CTE lässt keine doppelten Spaltennamen zu.|  
|Deaktivierte Trigger werden aktiviert, wenn die Trigger geändert werden.|Das Ändern eines Triggers ändert nicht den Status (deaktiviert oder aktiviert) des Triggers.|  
|Die OUTPUT INTO-Tabellenklausel ignoriert die `IDENTITY_INSERT SETTING = OFF` und ermöglicht, dass explizite Werte eingefügt werden soll.|Sie können keine expliziten Werte für eine Identitätsspalte in einer Tabelle einfügen beim `IDENTITY_INSERT` auf OFF festgelegt ist.|  
|Wenn die datenbankkapselung auf partial festgelegt ist, Überprüfen der `$action` -Feld in der `OUTPUT` -Klausel eine `MERGE` Anweisung kann einen Sortierung Fehler zurückgeben.|Die Sortierung der Werte zurückgegeben werden, indem Sie die `$action` -Klausel eine `MERGE` -Anweisung ist die Sortierung der Datenbank anstelle der serversortierung und ein sortierungskonfliktfehler wird nicht zurückgegeben.|  
|Durch eine `SELECT INTO`-Anweisung wird immer ein Singlethread-Einfügevorgang erstellt.|Durch eine `SELECT INTO`-Anweisung kann ein paralleler Einfügevorgang erstellt werden. Beim Einfügen großer Zeilenanzahlen kann die Leistung durch den parallelen Vorgang verbessert werden.|  
  
## <a name="differences-between-lower-compatibility-levels-and-levels-110-and-120"></a>Unterschiede zwischen niedrigeren Kompatibilitätsgraden und Kompatibilitätsgraden 110 und 120  
 In diesem Abschnitt werden neue mit Kompatibilitätsgrad 110 eingeführte Verhaltensweisen beschrieben.   Dieser Abschnitt bezieht sich auch auf Kompatibilitätsgrad 120.  
  
|Kompatibilitätsgradeinstellung 100 oder niedriger|Kompatibilitätsgradeinstellung 110 oder höher|  
|--------------------------------------------------|--------------------------------------------------|  
|Common Language Runtime (CLR)-Datenbankobjekte werden mit Version 4 der CLR ausgeführt. Einige in Version 4 der CLR eingeführte Verhaltensänderungen werden jedoch vermieden. Weitere Informationen finden Sie unter [Neuigkeiten in CLR-Integration](../../relational-databases/clr-integration/clr-integration-what-s-new.md).|CLR-Datenbankobjekte werden mit Version 4 der CLR ausgeführt.|  
|Die XQuery-Funktionen **Zeichenfolgenlängen** und **Teilzeichenfolge** betrachten jedes Ersatzzeichen als zwei Zeichen.|Die XQuery-Funktionen **Zeichenfolgenlängen** und **Teilzeichenfolge** betrachten jedes Ersatzzeichen als ein Zeichen.|  
|`PIVOT`in einer rekursiven-Abfrage (Expression, CTE) gemeinsamen Tabelle ist zulässig. Die Abfrage gibt jedoch falsche Ergebnisse zurück, wenn mehrere Zeilen pro Gruppierung vorhanden sind.|`PIVOT`ist in einer rekursiven-Abfrage (Expression, CTE) gemeinsamen Tabelle nicht zulässig. Es wird ein Fehler zurückgegeben.|  
|Der RC4-Algorithmus wird nur aus Gründen der Abwärtskompatibilität unterstützt. Neues Material kann nur mit RC4 oder RC4_128 verschlüsselt werden, wenn die Datenbank den Kompatibilitätsgrad 90 oder 100 besitzt. (Nicht empfohlen.) In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], mit RC4 oder RC4_128 verschlüsseltes Material in jedem Kompatibilitätsgrad entschlüsselt werden kann.|Neues Material kann nicht mit RC4 oder RC4_128 verschlüsselt werden. Verwenden Sie stattdessen einen neueren Algorithmus, z. B. einen der AES-Algorithmen. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], mit RC4 oder RC4_128 verschlüsseltes Material in jedem Kompatibilitätsgrad entschlüsselt werden kann.|  
|Das Standardformat für `CAST` und `CONVERT` Vorgänge für **Zeit** und **datetime2** Datentypen ist 121, wenn einer der Typen in einem berechneten Spaltenausdruck verwendet wird. Für berechnete Spalten ist das Standardformat 0. Dieses Verhalten wirkt sich auf berechnete Spalten aus, wenn sie erstellt werden und in Abfragen mit automatischer Parametrisierung oder in Einschränkungsdefinitionen verwendet werden.<br /><br /> Beispiel D im Abschnitt "Beispiele" weiter unten zeigt den Unterschied zwischen den Formaten 0 und 121. Das oben beschriebene Verhalten wird nicht veranschaulicht. Weitere Informationen zu Datums- und Zeitformaten finden Sie unter [CAST und CONVERT &#40; Transact-SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).|Unter Kompatibilitätsgrad 110, das Standardformat für `CAST` und `CONVERT` Vorgänge für **Zeit** und **datetime2** Datentypen ist immer 121. Basiert die Abfrage auf dem alten Verhalten, verwenden Sie einen Kompatibilitätsgrad unter 110, oder geben Sie in der betroffenen Abfrage explizit das Format 0 an.<br /><br /> Ein Update der Datenbank auf Kompatibilitätsgrad 110 ändert keine Benutzerdaten, die auf dem Datenträger gespeichert wurden. Sie müssen diese Daten entsprechend manuell korrigieren. Wenn Sie verwendet, z. B. `SELECT INTO` zum Erstellen einer Tabelle aus einer Quelle, die oben beschriebenen Ausdruck für eine berechnete Spalte enthalten, würde die Daten, die (mit dem Format 0) anstelle der Definition der berechneten Spalte selbst gespeichert werden. Sie müssen diese Daten manuell aktualisieren, um sie an das Format 121 anzupassen.|  
|Alle Spalten in Remotetabellen vom Typ **Smalldatetime** verwiesen wird, werden in einer partitionierten Sicht zugeordnet sind, als **"DateTime"**. Entsprechende Spalten in lokalen Tabellen (in derselben Ordnungsposition in der Auswahlliste) muss vom Typ **"DateTime"**.|Alle Spalten in Remotetabellen vom Typ **Smalldatetime** verwiesen wird, werden in einer partitionierten Sicht zugeordnet sind, als **Smalldatetime**. Entsprechende Spalten in lokalen Tabellen (in derselben Ordnungsposition in der Auswahlliste) muss vom Typ **Smalldatetime**.<br /><br /> Nach dem Upgrade auf 110 schlägt die verteilte partitionierte Sicht wegen des Datentypkonflikts fehl. Sie können dieses Problem beheben, wenn Sie ändern den Datentyp für die Remotetabelle zu **"DateTime"** oder den Kompatibilitätsgrad der lokalen Datenbank auf 100 oder niedriger.|  
|`SOUNDEX`Funktion implementiert die folgenden Regeln:<br /><br /> (1) Großbuchstaben H oder W in Großbuchstaben werden ignoriert, wenn zwei Konsonanten trennen, die die gleiche Anzahl in der `SOUNDEX` Code.<br /><br /> 2) Wenn die ersten 2 Zeichen des *Character_expression* verfügen über die gleiche Anzahl der `SOUNDEX` Code, der beide Zeichen sind enthalten. Andernfalls, wenn eine Reihe von Seite-an-Seite Konsonanten dieselbe Anzahl der `SOUNDEX` Code alle außer der ersten ausgeschlossen werden.|`SOUNDEX`Funktion implementiert die folgenden Regeln:<br /><br /> (1) Wenn Großbuchstaben H oder Großbuchstaben W zwei Konsonanten trennt, die die gleiche Anzahl in haben der `SOUNDEX` Code, wird der Konsonant rechts wird ignoriert.<br /><br /> (2) Wenn eine Reihe von Seite-an-Seite Konsonanten dieselbe Anzahl der `SOUNDEX` Code alle außer der ersten ausgeschlossen werden.<br /><br /> <br /><br /> Die zusätzlichen Regeln können dazu führen, dass die Werte berechnet, indem die `SOUNDEX` Funktion, die unter früheren Kompatibilitätsgraden berechneten Werten abweichen. Nach dem Upgrade auf Kompatibilitätsgrad 110, Sie müssen möglicherweise neu erstellen der Indizes, heaps oder CHECK-Einschränkungen, mit denen die `SOUNDEX` Funktion. Weitere Informationen finden Sie unter [SOUNDEX &#40; Transact-SQL &#41;](../../t-sql/functions/soundex-transact-sql.md)|  
  
## <a name="differences-between-compatibility-level-90-and-level-100"></a>Unterschiede zwischen Kompatibilitätsgrad 90 und Kompatibilitätsgrad 100  
 In diesem Abschnitt werden neue mit Kompatibilitätsgrad 100 eingeführte Verhaltensweisen beschrieben.  
  
|Kompatibilitätsgradeinstellung 90|Kompatibilitätsgradeinstellung 100|Mögliche Auswirkung|  
|----------------------------------------|-----------------------------------------|---------------------------|  
|Die Einstellung QUOTED_IDENTIFER ist für Tabellenwertfunktionen mit mehreren Anweisungen immer auf ON festgelegt, wenn diese erstellt werden, unabhängig von der Einstellung auf Sitzungsebene.|Die QUOTED IDENTIFIER-Sitzungseinstellung wird berücksichtigt, wenn Tabellenwertfunktionen mit mehreren Anweisungen erstellt werden.|Medium|  
|Beim Erstellen oder ändern eine Partitionsfunktion **"DateTime"** und **Smalldatetime** Literale in der Funktion werden ausgewertet, wie die Spracheinstellung US_English vorausgesetzt.|Die aktuelle Spracheinstellung wird zur Auswertung **"DateTime"** und **Smalldatetime** Literale in der Partitionsfunktion.|Medium|  
|Die `FOR BROWSE` -Klausel ist zulässig (und ignoriert) in `INSERT` und `SELECT INTO` Anweisungen.|Die `FOR BROWSE` -Klausel ist nicht zulässig `INSERT` und `SELECT INTO` Anweisungen.|Medium|  
|Volltextprädikate dürfen den `OUTPUT` Klausel.|Volltextprädikate dürfen nicht der `OUTPUT` Klausel.|Low|  
|`CREATE FULLTEXT STOPLIST`, `ALTER FULLTEXT STOPLIST`, und `DROP FULLTEXT STOPLIST` werden nicht unterstützt. Die Systemstoppliste wird automatisch neuen Volltextindizes zugeordnet.|`CREATE FULLTEXT STOPLIST`, `ALTER FULLTEXT STOPLIST`, und `DROP FULLTEXT STOPLIST` werden unterstützt.|Low|  
|`MERGE`wird nicht als reserviertes Schlüsselwort erzwungen.|MERGE ist ein vollständig reserviertes Schlüsselwort. Die `MERGE` Anweisung Kompatibilitätsgraden 100 und 90 unterstützt wird.|Low|  
|Mithilfe der \<Dml_table_source >-Argument der INSERT-Anweisung löst einen Syntaxfehler.|Sie können die Ergebnisse einer OUTPUT-Klausel in einer geschachtelten INSERT-, UPDATE-, DELETE- oder MERGE-Anweisung aufzeichnen und diese Ergebnisse in eine Zieltabelle oder -sicht einfügen. Dies erfolgt mithilfe der \<Dml_table_source >-Argument der INSERT-Anweisung.|Low|
|Es sei denn, `NOINDEX` angegeben wird, `DBCC CHECKDB` oder `DBCC CHECKTABLE` führt sowohl physische und logische konsistenzprüfungen für eine einzelne Tabelle oder indizierte Sicht und für alle nicht gruppierten und XML-Indizes. Räumliche Indizes werden nicht unterstützt.|Es sei denn, `NOINDEX` angegeben wird, `DBCC CHECKDB` oder `DBCC CHECKTABLE` führt sowohl physische und logische konsistenzprüfungen für eine einzelne Tabelle und alle nicht gruppierten Indizes. Allerdings werden für XML-Indizes, räumliche Indizes und indizierte Sichten standardmäßig nur physische Konsistenzprüfungen ausgeführt.<br /><br /> Wenn `WITH EXTENDED_LOGICAL_CHECKS` angegeben wird, werden logische konsistenzprüfungen für indizierte Sichten, XML-Indizes und räumliche Indizes ausgeführt, sofern vorhanden. Standardmäßig werden physische Konsistenzprüfungen vor den logischen Konsistenzprüfungen ausgeführt. Wenn `NOINDEX` ebenfalls angegeben wird, werden nur die logischen Prüfungen ausgeführt.|Low|  
|Wenn eine OUTPUT-Klausel mit einer DML-Anweisung (Data Manipulation Language, Datenbearbeitungssprache) verwendet wird und während der Ausführung der Anweisung ein Laufzeitfehler auftritt, wird die gesamte Transaktion beendet, und es wird ein Rollback für sie ausgeführt.|Wenn ein `OUTPUT` -Klausel mit einer Anweisung für das Data Manipulation Language (DML) verwendet wird und ein Laufzeitfehler tritt auf, während der Ausführung der Anweisung, hängt das Verhalten der `SET XACT_ABORT` Einstellung. Wenn `SET XACT_ABORT` ist OFF, ein anweisungsabbruchfehler generiert, die vom DML-Anweisung mit der `OUTPUT` Klausel wird die Anweisung beendet aber die Ausführung des Batches fortgesetzt und die Transaktion kein Rollback. Wenn `SET XACT_ABORT` auf ON festgelegt ist, alle Laufzeitfehler, die von der DML-Anweisung mit der OUTPUT-Klausel generiert, werden den Batch beendet und ein Rollback der Transaktions.|Low|  
|CUBE und ROLLUP werden nicht als reservierte Schlüsselwörter erzwungen.|`CUBE`und `ROLLUP` sind reservierte Schlüsselwörter innerhalb der GROUP BY-Klausel.|Low|  
|Strenge Überprüfung angewendet, um Elemente des XML- **AnyType** Typ.|Lax-Überprüfung angewendet wird, auf Elemente in der **AnyType** Typ. Weitere Informationen finden Sie unter [Platzhalterkomponenten und Inhaltsüberprüfung](../../relational-databases/xml/wildcard-components-and-content-validation.md).|Low|  
|Die speziellen Attribute **xsi: nil** und **xsi: Type** kann nicht abgefragt oder durch Anweisungen Data Manipulation Language geändert werden.<br /><br /> Dies bedeutet, dass `/e/@xsi:nil` fehlschlägt, während `/e/@*` ignoriert die **xsi: nil** und **xsi: Type** Attribute. Allerdings `/e` gibt die **xsi: nil** und **xsi: Type** Attribute aus Gründen der Konsistenz mit `SELECT xmlCol`, selbst wenn `xsi:nil = "false"`.|Die speziellen Attribute **xsi: nil** und **xsi: Type** werden als reguläre Attribute gespeichert und können abgefragt und geändert werden.<br /><br /> Z. B. die Ausführung der Abfrage `SELECT x.query('a/b/@*')` gibt alle Attribute einschließlich **xsi: nil** und **xsi: Type**. Um diese Typen in der Abfrage auszuschließen, ersetzen `@*` mit `@*[namespace-uri(.) != "` *Xsi-Namespace-Uri einfügen* `"` und nicht `(local-name(.) = "type"` oder`local-name(.) ="nil".`|Low|  
|Eine benutzerdefinierte Funktion, die eine XML-Zeichenfolgenkonstante in einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-datetime-Typ konvertiert, wird als deterministisch gekennzeichnet.|Eine benutzerdefinierte Funktion, die eine XML-Zeichenfolgenkonstante in einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-datetime-Typ konvertiert, wird als nicht deterministisch gekennzeichnet.|Low|  
|Die XML-Datentypen "union" und "list" werden nicht vollständig unterstützt.|Die XML-Datentypen "union" und "list" werden vollständig unterstützt, einschließlich der folgenden Funktionalität:<br /><br /> "union" von "list"<br /><br /> "union" von "union"<br /><br /> Liste der atomaren Typen<br /><br /> "list" von "union"|Low|  
|Die für eine xQuery-Methode erforderlichen SET-Optionen werden nicht überprüft, wenn die Methode in einer Sicht oder Inline-Tabellenwertfunktion enthalten ist.|Die für eine xQuery-Methode erforderlichen SET-Optionen werden überprüft, wenn die Methode in einer Sicht oder Inline-Tabellenwertfunktion enthalten ist. Wenn die SET-Optionen der Methode nicht ordnungsgemäß festgelegt sind, wird ein Fehler ausgegeben.|Low|  
|XML-Attributwerte, die Zeilenendezeichen enthalten (Wagenrücklauf und Zeilenvorschub) werden nicht gemäß dem XML-Standard normalisiert. Somit werden anstelle eines einzelnen Zeilenvorschubzeichens beide Zeichen zurückgegeben.|XML-Attributwerte, die Zeilenendezeichen enthalten (Wagenrücklauf und Zeilenvorschub) werden gemäß dem XML-Standard normalisiert. Somit werden alle Zeilenumbrüche in extern analysierten Entitäten (einschließlich der Dokumententität) bei Eingabe normalisiert, indem sowohl die aus zwei Zeichen bestehende Folge #xD #xA als auch alle Vorkommnisse von #xD, die nicht von #xA gefolgt werden, in das einzelne Zeichen #xA übersetzt werden.<br /><br /> Anwendungen, die mithilfe von Attributen Zeichenfolgenwerte transportieren, die Zeilenendezeichen enthalten, erhalten diese Zeichen nicht wie gesendet zurück. Um die Normalisierung zu verhindern, müssen für die Codierung aller Zeilenendezeichen numerische XML-Zeichenentitäten verwendet werden.|Low|  
|Die Spalteneigenschaften `ROWGUIDCOL` und `IDENTITY` können als Einschränkung falsch benannt werden. Beispielsweise wird die Anweisung `CREATE TABLE T (C1 int CONSTRAINT MyConstraint IDENTITY)` ausgeführt, doch wird der Einschränkungsname nicht beibehalten und ist für den Benutzer nicht verfügbar.|Die Spalteneigenschaften `ROWGUIDCOL` und `IDENTITY` nicht als Einschränkung benannt werden. Der Fehler 156 wird zurückgegeben.|Low|  
|Aktualisieren von Spalten mithilfe einer zweiseitigen Zuweisung wie z. B. `UPDATE T1 SET @v = column_name = <expression>` kann zu unerwarteten Ergebnissen führen, da der aktuelle Wert der Variablen wie z. B. in anderen Klauseln verwendet werden kann die `WHER`E und `ON` Klausel während der anweisungsausführung anstelle der Anfangswert der Anweisung. Dies kann dazu führen, dass sich die Bedeutungen der Prädikate für jede Zeile einzeln unvorhersehbar ändern.<br /><br /> Dieses Verhalten gilt nur, wenn der Kompatibilitätsgrad auf 90 festgelegt ist.|Die Aktualisierung von Spalten mithilfe einer zweiseitigen Zuweisung liefert die erwarteten Ergebnisse, weil während der Ausführung der Anweisung nur auf den Anweisungsanfangswert der Spalte zugegriffen wird.|Low|  
|Siehe Beispiel E im Abschnitt "Beispiele" weiter unten.|Siehe Beispiel F im Abschnitt "Beispiele" weiter unten.|Low|  
|Die ODBC-Funktion {fn CONVERT ()} verwendet das Standarddatumsformat der Sprache. Für einige Sprachen ist das Standardformat YDM, was zu Konvertierungsfehlern führen kann, wenn CONVERT() mit anderen Funktionen, wie z. B. kombiniert wird `{fn CURDATE()}`, die ein YMD-Format erwarten.|Der ODBC-Funktion `{fn CONVERT()}` verwendet Stil 121 (ein sprachenunabhängiger-YMD-Format) beim Konvertieren in die ODBC-Datentypen SQL_TIMESTAMP, SQL_DATE, SQL_TIME, SQLDATE, SQL_TYPE_TIME und SQL_TYPE_TIMESTAMP.|Low|  
|Für systeminterne datetime-Funktionen, wie z.&#160;B. DATEPART, ist es nicht erforderlich, dass Zeichenfolgeneingabewerte gültige datetime-Literale sind. Beispielsweise `SELECT DATEPART (year, '2007/05-30')` erfolgreich kompiliert.|Systeminterne DateTime-Funktionen wie z. B. `DATEPART` erfordern Zeichenfolgeneingabewerte gültige Datetime-Literale sein. Fehler 241 wird zurückgegeben, wenn ein ungültiges datetime-Literal verwendet wird.|Low|  
  
## <a name="reserved-keywords"></a>Reservierte Schlüsselwörter  
 Die Kompatibilitätseinstellung bestimmt außerdem die für das [!INCLUDE[ssDE](../../includes/ssde-md.md)] reservierten Schlüsselwörter. In der folgenden Tabelle sind die reservierten Schlüsselwörter aufgeführt, die mit den einzelnen Kompatibilitätsgraden eingeführt werden.  
  
|Einstellung für den Kompatibilitätsgrad|Reservierte Schlüsselwörter|  
|----------------------------------|-----------------------|  
|130|Bestimmt werden soll.|  
|120|Keine.|  
|110|WITHIN GROUP, TRY_CONVERT, SEMANTICKEYPHRASETABLE, SEMANTICSIMILARITYDETAILSTABLE, SEMANTICSIMILARITYTABLE|  
|100|CUBE, MERGE, ROLLUP|  
|90|EXTERNAL, PIVOT, UNPIVOT, REVERT, TABLESAMPLE|  
  
 Bei einem bestimmten Kompatibilitätsgrad schließen die reservierten Schlüsselwörter alle Schlüsselwörter ein, die mit diesem oder einem niedrigeren Grad eingeführt wurden. So stellen z. B. bei Anwendungen mit dem Kompatibilitätsgrad 110 alle in der vorherigen Tabelle aufgeführten Schlüsselwörter reservierte Schlüsselwörter dar. Bei den niedrigeren Kompatibilitätsgraden stellen die Schlüsselwörter von Grad 100 weiterhin gültige Objektnamen dar; die Sprachfunktionen von Grad 110, die diesen Schlüsselwörtern entsprechen, sind jedoch nicht verfügbar.  
  
 Nach der Einführung bleibt ein Schlüsselwort reserviert. So stellt z. B. das reservierte Schlüsselwort PIVOT, das mit dem Kompatibilitätsgrad 90 eingeführt wurde, auch bei Grad 100, 110 und 120 ein reserviertes Schlüsselwort dar.  
  
 Wenn eine Anwendung einen Bezeichner verwendet, der für den Kompatibilitätsgrad der Anwendung als Schlüsselwort reserviert ist, erzeugt die Anwendung einen Fehler. Um dieses Problem umgehen, indem Sie den Bezeichner Klammern entweder (**[]**) oder Anführungszeichen (**""**); z. B. eine Anwendung zu aktualisieren, die den Bezeichner verwendet **EXTERNEN** auf den Kompatibilitätsgrad 90, können Sie die Bezeichner, der entweder ändern **[EXTERNAL]** oder **"EXTERNAL"**.  
  
 Weitere Informationen finden Sie unter [Reservierte Schlüsselwörter &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Datenbank.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-changing-the-compatibility-level"></a>A. Ändern des Kompatibilitätsgrads  
 Im folgenden Beispiel wird den Kompatibilitätsgrad der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] Datenbank `110,` [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET COMPATIBILITY_LEVEL = 110;  
GO  
```  
  
 Das folgende Beispiel gibt den Kompatibilitätsgrad der aktuellen Datenbank zurück.  
  
```sql  
SELECT name, compatibility_level   
FROM sys.databases   
WHERE name = db_name();  
```  
  
### <a name="b-ignoring--the-set-language-statement-except-under-compatibility-level-120"></a>B. Ignorieren die SET LANGUAGE-Anweisung außer für Kompatibilitätsgrad 120  
 Die folgende Abfrage ignoriert die Anweisung SET LANGUAGE außer Kompatibilitätsgrad unter 120.  
  
```sql  
SET DATEFORMAT dmy;   
DECLARE @t2 date = '12/5/2011' ;  
SET LANGUAGE dutch;   
SELECT CONVERT(varchar(11), @t2, 106);   
  
-- Results when the compatibility level is less than 120.   
12 May 2011   
  
-- Results when the compatibility level is set to 120).  
12 mei 2011  
```  
  
### <a name="c"></a>C.  
 Erstellen Sie für kompatibilitätsgradeinstellung 110 oder niedriger, rekursive Verweise auf die rechte Seite des EXCEPT-Klausel eine Endlosschleife.  
  
```sql  
WITH   
cte AS (SELECT * FROM (VALUES (1),(2),(3)) v (a)),  
r   
AS (SELECT a FROM Table1  
UNION ALL  
(SELECT a FROM Table1 EXCEPT SELECT a FROM r) )   
SELECT a   
FROM r;  
  
```  
  
### <a name="d"></a>D.  
 Dieses Beispiel zeigt den Unterschied zwischen den Formaten 0 und 121. Weitere Informationen zu Datums- und Zeitformaten finden Sie unter [CAST und CONVERT &#40; Transact-SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
```sql  
CREATE TABLE t1 (c1 time(7), c2 datetime2);   
  
INSERT t1 (c1,c2) VALUES (GETDATE(), GETDATE());  
  
SELECT CONVERT(nvarchar(16),c1,0) AS TimeStyle0  
       ,CONVERT(nvarchar(16),c1,121)AS TimeStyle121  
       ,CONVERT(nvarchar(32),c2,0) AS Datetime2Style0  
       ,CONVERT(nvarchar(32),c2,121)AS Datetime2Style121  
FROM t1;  
  
-- Returns values such as the following.  
TimeStyle0       TimeStyle121       
Datetime2Style0      Datetime2Style121  
---------------- ----------------   
-------------------- --------------------------  
3:15PM           15:15:35.8100000   
Jun  7 2011  3:15PM  2011-06-07 15:15:35.8130000  
```  
  
### <a name="e"></a>E.  
 Die Variablenzuweisung ist in einer Anweisung mit einem UNION-Operator auf der obersten Ebene zulässig, kann jedoch unerwartete Ergebnisse zurückgeben. Beispielsweise wird in den folgenden Anweisungen der lokalen Variable `@v` der Wert der Spalte `BusinessEntityID` aus der Vereinigung von zwei Tabellen zugewiesen. Wenn die SELECT-Anweisung mehr als einen Wert zurückgibt, wird der Variablen definitionsgemäß der zuletzt zurückgegebene Wert zugewiesen. In diesem Fall wird der Variablen der letzte Wert richtig zugewiesen, es wird jedoch auch das Resultset der SELECT UNION-Anweisung zurückgegeben.  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET compatibility_level = 90;  
GO  
USE AdventureWorks2012;  
GO  
DECLARE @v int;  
SELECT @v = BusinessEntityID FROM HumanResources.Employee  
UNION ALL  
SELECT @v = BusinessEntityID FROM HumanResources.EmployeeAddress;  
SELECT @v;  
```  
  
### <a name="f"></a>F.  
 Die Variablenzuweisung ist in einer Anweisung mit einem UNION-Operator auf der obersten Ebene nicht zulässig. Der Fehler 10734 wird zurückgegeben. Um den Fehler zu beheben, müssen Sie die Abfrage umschreiben, wie im folgenden Beispiel gezeigt.  
  
```sql  
DECLARE @v int;  
SELECT @v = BusinessEntityID FROM   
    (SELECT BusinessEntityID FROM HumanResources.Employee  
     UNION ALL  
     SELECT BusinessEntityID FROM HumanResources.EmployeeAddress) AS Test;  
SELECT @v;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Reserved Keywords &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
 [Anzeigen oder Ändern des Kompatibilitätsgrads einer Datenbank](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) 
  
