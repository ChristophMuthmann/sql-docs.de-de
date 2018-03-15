---
title: DATABASEPROPERTYEX (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATABASEPROPERTYEX
- DATABASEPROPERTYEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DATABASEPROPERTYEX function
- displaying database properties
- database properties [SQL Server]
ms.assetid: 8a9e0ffb-28b5-4640-95b2-a54e3e5ad941
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a67b74ad595fdf7b6f3a63dbd2ea2c9e5793f54f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="databasepropertyex-transact-sql"></a>DATABASEPROPERTYEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt die aktuelle Einstellung der angegebenen Datenbankoption oder -eigenschaft für die angegebene Datenbank in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DATABASEPROPERTYEX ( database , property )  
```  
  
## <a name="arguments"></a>Argumente  
*database*  
Ein Ausdruck, der den Namen der Datenbank darstellt, für die Informationen über die benannte Eigenschaft zurückgegeben werden sollen. *database* ist vom Datentyp **nvarchar(128)**.  
Für [!INCLUDE[ssSDS](../../includes/sssds-md.md)] muss dies der Name der aktuellen Datenbank sein. Gibt NULL für alle Eigenschaften zurück, wenn ein anderer Datenbanknamen bereitgestellt wird.
  
*property*  
Ein Ausdruck, der den Namen der zurückzugebenden Datenbankeigenschaft darstellt. *property* ist vom Datentyp **varchar(128)**. Die folgenden Werte sind möglich. Der Rückgabetyp ist **sql_variant**. In der folgenden Tabelle ist der Basisdatentyp für die einzelnen Eigenschaftswertswerte aufgeführt.
  
> [!NOTE]  
>  Wenn die Datenbank nicht gestartet wurde, geben die Eigenschaften, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durch direkten Datenbankzugriff anstatt durch Abrufen des Werts aus den Metadaten abruft, NULL zurück. Das gilt, solange für die Datenbank AUTO_CLOSE auf ON festgelegt oder die Datenbank offline ist.  
  
|Eigenschaft|Description|Zurückgegebener Wert|  
|---|---|---|
|Sortierung|Standardsortierungsname der Datenbank|Sortierungsname<br /><br /> NULL = Die Datenbank wurde nicht gestartet.<br /><br /> Basisdatentyp: **nvarchar(128)**|  
|ComparisonStyle|Die Windows-Vergleichsart der Sortierung. ComparisonStyle ist eine Bitmap, die mit den folgenden Werten für die möglichen Formate berechnet wird.<br /><br /> Groß-/Kleinschreibung ignorieren: 1<br /><br /> Akzente ignorieren: 2<br /><br /> Kana ignorieren: 65536<br /><br /> Breite ignorieren: 131072<br /><br /> <br /><br /> Der Standardwert 196.609 ist beispielsweise das Ergebnis der Kombination der Optionen Groß-/Kleinschreibung ignorieren, Kana ignorieren und Breite ignorieren.|Gibt die Vergleichsart zurück.<br /><br /> Gibt für alle binären Sortierungen 0 zurück.<br /><br /> Basisdatentyp: **int**|  
|Edition|Die Edition oder Dienstebene der Datenbank.|**Gilt für**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].<br /><br /> <br /><br /> Web = Web Edition-Datenbank<br /><br /> Business = Business Edition-Datenbank<br /><br /> Standard<br /><br /> Standard<br /><br /> Premium<br /><br /> System (für die master-Datenbank)<br /><br /> NULL = Die Datenbank wurde nicht gestartet.<br /><br /> Basisdatentyp: **nvarchar**(64)|  
|IsAnsiNullDefault|Die Datenbank befolgt ISO-Regeln für das Zulassen von NULL-Werten.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsAnsiNullsEnabled|Alle Vergleiche mit einem NULL-Wert werden zu einem unbekannten Wert ausgewertet.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsAnsiPaddingEnabled|Zeichenfolgen werden vor dem Vergleich oder Einfügen auf dieselbe Länge aufgefüllt.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsAnsiWarningsEnabled|Fehler- oder Warnmeldungen werden ausgegeben, wenn Standardfehlerbedingungen auftreten.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsArithmeticAbortEnabled|Abfragen werden beendet, wenn während der Abfrageausführung ein Überlauffehler oder ein Fehler aufgrund einer Division durch Null auftritt.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsAutoClose|Die Datenbank wird ordnungsgemäß heruntergefahren, und Ressourcen werden freigegeben, nachdem der letzte Benutzer die Anwendung beendet hat.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsAutoCreateStatistics|Der Abfrageoptimierer erstellt Statistiken für einzelne Spalten nach Bedarf, um die Abfrageleistung zu verbessern.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsAutoCreateStatisticsIncremental|Automatisch erstellte Statistiken für einzelne Spalten sind inkrementell, falls möglich.|**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> <br /><br /> 1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsAutoShrink|Datenbankdateien sind Kandidaten für das automatische periodische Verkleinern.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsAutoUpdateStatistics|Der Abfrageoptimierer aktualisiert vorhandene Statistiken, wenn sie von einer Abfrage verwendet werden und veraltet sein könnten.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|
|IsClone|Die Datenbank ist nur eine Kopie der Schemas und Statistiken einer Benutzerdatenbank.|**Gilt für:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Service Pack 2<br /><br /> <br /><br /> 1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**| 
|IsCloseCursorsOnCommitEnabled|Cursor, die beim Ausführen eines Commits für eine Transaktion geöffnet sind, werden geschlossen.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsFulltextEnabled|Die Datenbank ist für die Volltext- und semantische Indizierung aktiviert.|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> <br /><br /> 1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**<br /><br /> **Hinweis:** Der Wert dieser Eigenschaft hat keine Auswirkungen. In Benutzerdatenbanken ist die Volltextsuche standardmäßig aktiviert. Diese Spalte wird in zukünftigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht mehr bereitgestellt. Verwenden Sie diese Spalte nicht beim Entwickeln neuer Anwendungen, und planen Sie zum frühstmöglichen Zeitpunkt die Umstellung von Anwendungen, in denen diese Spalten zurzeit verwendet werden.|  
|IsInStandBy|Die Datenbank ist im Schreibschutzmodus online. Die Wiederherstellung des Protokolls ist zulässig.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsLocalCursorsDefault|Cursordeklarationen werden standardmäßig auf LOCAL festgelegt.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsMemoryOptimizedElevateToSnapshotEnabled|Auf speicheroptimierte Tabellen wird mit der SNAPSHOT-Isolation zugegriffen, wenn die Sitzungseinstellung TRANSACTION ISOLATION LEVEL auf eine niedrigere Isolationsstufe festgelegt ist (READ COMMITTED oder READ UNCOMMITTED).|**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> <br /><br /> 1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> Basisdatentyp: **int**|  
|IsMergePublished|Die Tabellen einer Datenbank können zur Mergereplikation veröffentlicht werden, wenn die Replikation installiert ist.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsNullConcat|Der Operand für die NULL-Verkettung ergibt NULL.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsNumericRoundAbortEnabled|Fehler werden generiert, wenn ein Genauigkeitsverlust in Ausdrücken auftritt.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsParameterizationForced|Die SET-Option PARAMETERIZATION wurde für die Datenbank auf FORCED festgelegt.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe|  
|IsQuotedIdentifiersEnabled|Für Bezeichner können doppelte Anführungszeichen verwendet werden.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsPublished|Falls die Replikation installiert ist, können die Tabellen der Datenbank für die Momentaufnahme- oder Transaktionsreplikation veröffentlicht werden.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsRecursiveTriggersEnabled|Das rekursive Auslösen von Triggern ist aktiviert.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsSubscribed|Die Datenbank wurde für eine Veröffentlichung abonniert.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsSyncWithBackup|Die Datenbank ist entweder eine veröffentlichte oder eine Verteilungsdatenbank. Sie kann ohne Unterbrechung der Transaktionsreplikation wiederhergestellt werden.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsTornPageDetectionEnabled|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] erkennt unvollständige E/A-Vorgänge, die durch Stromausfälle oder andere Systemunterbrechungen verursacht wurden.|1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Ungültige Eingabe<br /><br /> Basisdatentyp: **int**|  
|IsXTPSupported|Gibt an, ob die Datenbank In-Memory-OLTP unterstützt, d.h. das Erstellen und Verwenden von speicheroptimierten Tabellen und nativ kompilierten Modulen.<br /><br /> Spezifisch für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:<br /><br /> IsXTPSupported ist unabhängig von der Existenz von MEMORY_OPTIMIZED_DATA-Dateigruppen, die für die Erstellung von In-Memory-OLTP-Objekten benötigt werden.|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[ssSDS](../../includes/sssds-md.md)].<br /><br /> **Gilt für**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] and [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].<br /><br /> <br /><br /> 1 = TRUE,<br /><br /> 0 = FALSE<br /><br /> NULL = Eingabe ist ungültig, ein Fehler oder nicht anwendbar.<br /><br /> Basisdatentyp: **int**|  
|LCID|Der Windows-Gebietsschemabezeichner (Locale Identifier, LCID) der Sortierung.|LCID-Wert (im Dezimalformat).<br /><br /> Basisdatentyp: **int**|  
|MaxSizeInBytes|Maximale Datenbankgröße in Bytes.|**Gilt für**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].<br /><br /> <br /><br /> 1073741824<br /><br /> 5368709120<br /><br /> 10737418240<br /><br /> 21474836480<br /><br /> 32212254720<br /><br /> 42949672960<br /><br /> 53687091200<br /><br /> NULL = Die Datenbank wurde nicht gestartet<br /><br /> Basisdatentyp: **bigint**|  
|Wiederherstellung|Wiederherstellungsmodell für die Datenbank.|FULL = Vollständiges Wiederherstellungsmodell<br /><br /> BULK_LOGGED = Massenprotokolliertes Modell<br /><br /> SIMPLE = Einfaches Wiederherstellungsmodell<br /><br /> Basisdatentyp: **nvarchar(128)**|  
|ServiceObjective|Beschreibt die Leistungsstufe der Datenbank in [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] oder [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].|Kann einen der folgenden Werte annehmen:<br /><br /> NULL = Die Datenbank wurde nicht gestartet.<br /><br /> Freigegeben (für Web/Business-Editionen)<br /><br /> Standard<br /><br /> S0<br /><br /> S1<br /><br /> S2<br /><br /> S3<br /><br /> P1<br /><br /> P2<br /><br /> P3<br /><br /> ElasticPool<br /><br /> System (für die master-Datenbank)<br /><br /> Basisdatentyp: **nvarchar(32)**|  
|ServiceObjectiveId|Die ID des Dienstziels in [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].|**uniqueidentifier**, die das Dienstziel identifiziert.|  
|SQLSortOrder|Die ID der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sortierreihenfolge, die in früheren Versionen von SQL Server unterstützt wurde.|0 = Die Datenbank verwendet die Windows-Sortierung<br /><br /> >0 = ID der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sortierreihenfolge<br /><br /> NULL = Ungültige Eingabe, oder die Datenbank wurde nicht gestartet<br /><br /> Basisdatentyp: **tinyint**|  
|Status|Der Status der Datenbank.|ONLINE = Die Datenbank ist für die Abfrage verfügbar.<br /><br /> **Hinweis:** Der ONLINE-Status kann zurückgegeben werden, während die Datenbank geöffnet wird, auch wenn sie noch nicht wiederhergestellt ist. Um zu ermitteln, wann eine Datenbank Verbindungen akzeptieren kann, fragen Sie die Collation-Eigenschaft von **DATABASEPROPERTYEX** ab. Die Datenbank kann Verbindungen akzeptieren, wenn die Datenbanksortierung einen Wert ungleich NULL zurückgibt. Fragen Sie bei Always On-Datenbanken die database_state-Spalte oder die database_state_desc-Spalte von sys.dm_hadr_database_replica_states ab.<br /><br /> OFFLINE = Die Datenbank wurde explizit offline geschaltet.<br /><br /> RESTORING = Die Datenbank wird wiederhergestellt.<br /><br /> RECOVERING = die Datenbank wird wiederhergestellt und ist noch nicht für Abfragen bereit.<br /><br /> SUSPECT = Die Datenbank wurde nicht wiederhergestellt.<br /><br /> EMERGENCY = Die Datenbank befindet sich im schreibgeschützten Notfallmodus. Der Zugriff ist auf sysadmin-Mitglieder beschränkt.<br /><br /> Basisdatentyp: **nvarchar(128)**|  
|Updateability|Zeigt an, ob Daten geändert werden können.|READ_ONLY = Die Daten können gelesen, jedoch nicht geändert werden.<br /><br /> READ_WRITE = Die Daten können gelesen und geändert werden.<br /><br /> Basisdatentyp: **nvarchar(128)**|  
|UserAccess|Zeigt an, welche Benutzer auf die Datenbank zugreifen können.|SINGLE_USER = Jeweils nur ein db_owner-, dbcreator- oder sysadmin-Benutzer<br /><br /> RESTRICTED_USER = Nur Mitglieder der Rollen db_owner, dbcreator und sysadmin<br /><br /> MULTI_USER = Alle Benutzer<br /><br /> Basisdatentyp: **nvarchar(128)**|  
|Versionsoptionen|Die interne Versionsnummer des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Codes, mit dem die Datenbank erstellt wurde. [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|Versionsnummer = Die Datenbank ist geöffnet.<br /><br /> NULL = Die Datenbank wurde nicht gestartet.<br /><br /> Basisdatentyp: **int**|  
  
## <a name="return-types"></a>Rückgabetypen
**sql_variant**
  
## <a name="exceptions"></a>Ausnahmen  
Gibt NULL bei einem Fehler zurück oder wenn ein Aufrufer nicht über Berechtigungen zum Anzeigen des Objekts verfügt.
  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann ein Benutzer nur die Metadaten sicherungsfähiger Elemente anzeigen, bei denen der Benutzer entweder der Besitzer ist oder für die dem Benutzer eine Berechtigung erteilt wurde. Dies bedeutet, dass integrierte Funktionen (z. B. OBJECT_ID), die Metadaten ausgeben, möglicherweise NULL zurückgeben, wenn dem Benutzer für das Objekt keine Berechtigung erteilt wurde. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).
  
## <a name="remarks"></a>Remarks  
DATABASEPROPERTYEX gibt jeweils nur eine Eigenschaftseinstellung zurück. Verwenden Sie die [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)-Katalogsicht, um mehrere Eigenschaftseinstellungen anzuzeigen.
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-retrieving-the-status-of-the-autoshrink-database-option"></a>A. Abrufen des Status der Datenbankoption AUTO_SHRINK  
Das folgende Beispiel gibt den Status der AUTO_SHRINK-Datenbankoption für die `AdventureWorks`-Datenbank zurück.
  
```sql
SELECT DATABASEPROPERTYEX('AdventureWorks2014', 'IsAutoShrink');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)] Dies gibt an, dass AUTO_SHRINK auf OFF festgelegt ist.
  
```sql
------------------  
0  
```  
  
### <a name="b-retrieving-the-default-collation-for-a-database"></a>B. Abrufen der Standardsortierung für eine Datenbank  
Im folgenden Beispiel werdeneinige Attribute der `AdventureWorks`-Datenbank zurückgegeben.
  
```sql
SELECT   
    DATABASEPROPERTYEX('AdventureWorks2014', 'Collation') AS Collation,  
    DATABASEPROPERTYEX('AdventureWorks2014', 'Edition') AS Edition,  
    DATABASEPROPERTYEX('AdventureWorks2014', 'ServiceObjective') AS ServiceObjective,  
    DATABASEPROPERTYEX('AdventureWorks2014', 'MaxSizeInBytes') AS MaxSizeInBytes  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Collation                     Edition        ServiceObjective  MaxSizeInBytes  
----------------------------  -------------  ----------------  --------------  
SQL_Latin1_General_CP1_CI_AS  DataWarehouse  DW1000            5368709120  
```  
  
## <a name="see-also"></a>Siehe auch
[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[Datenbankstatus](../../relational-databases/databases/database-states.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
[sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)
  
  
