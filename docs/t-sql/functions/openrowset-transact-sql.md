---
title: OPENROWSET (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENROWSET_TSQL
- OPENROWSET
dev_langs:
- TSQL
helpviewer_keywords:
- data sources [SQL Server]
- OPENROWSET function
- remote data access [SQL Server], OPENROWSET
- ad hoc distributed queries
- OPENROWSET function, Transact-SQL
- OPENROWSET statement
- OLE DB data sources [SQL Server]
- ad hoc connection information
ms.assetid: f47eda43-33aa-454d-840a-bb15a031ca17
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 68db78ede26c3e7f8c60ced655d89d0fc9a615ac
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="openrowset-transact-sql"></a>OPENROWSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]


  Enthält alle für einen Zugriff auf Remotedaten von einer OLE DB-Datenquelle notwendigen Verbindungsinformationen. Diese Methode ist eine Alternative zum Zugriff auf Tabellen eines Verbindungsservers. Sie ist eine einmalig verwendete Ad-hoc-Methode zum Verbinden und Zugreifen auf Remotedaten mithilfe von OLE DB. Für häufigere Verweise auf OLE DB-Datenquellen verwenden Sie stattdessen Verbindungsserver. Weitere Informationen finden Sie unter [Verbindungsserver &#40;Datenbankmodul&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md). Die `OPENROWSET` Funktion kann in der FROM-Klausel einer Abfrage verwiesen werden, als handele es sich um einen Tabellennamen an. Die `OPENROWSET` -Funktion kann auch als Zieltabelle verwiesen werden ein `INSERT`, `UPDATE`, oder `DELETE` unterliegen den Funktionen des OLE DB-Provider-Anweisung. Obwohl die Abfrage mehrere Resultsets zurückgeben könnte `OPENROWSET` nur der erste Entitätencontainer zurückgegeben.  
  
 `OPENROWSET`unterstützt auch Massenvorgänge über einen integrierten BULK-Anbieter, der Daten aus einer Datei gelesen und als Rowset zurückgegeben werden können.  

  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
OPENROWSET   
( { 'provider_name' , { 'datasource' ; 'user_id' ; 'password'   
   | 'provider_string' }   
   , {   [ catalog. ] [ schema. ] object   
       | 'query'   
     }   
   | BULK 'data_file' ,   
       { FORMATFILE = 'format_file_path' [ <bulk_options> ]  
       | SINGLE_BLOB | SINGLE_CLOB | SINGLE_NCLOB }  
} )   
  
<bulk_options> ::=  
   [ , CODEPAGE = { 'ACP' | 'OEM' | 'RAW' | 'code_page' } ]   
   [ , DATASOURCE = 'data_source_name' ]
   [ , ERRORFILE = 'file_name' ]  
   [ , ERRORFILE_DATASOURCE = 'data_source_name' ]   
   [ , FIRSTROW = first_row ]   
   [ , LASTROW = last_row ]   
   [ , MAXERRORS = maximum_errors ]   
   [ , ROWS_PER_BATCH = rows_per_batch ]  
   [ , ORDER ( { column [ ASC | DESC ] } [ ,...n ] ) [ UNIQUE ] ]
  
   -- bulk_options related to input file format
   [ , FORMAT = 'CSV' ]
   [ , FIELDQUOTE = 'quote_characters']
   [ , FORMATFILE = 'format_file_path' ]   
```

  
## <a name="arguments"></a>Argumente  
 "*Provider_name*"  
 Eine Zeichenfolge für den Anzeigenamen (oder die PROGID) des OLE DB-Anbieters, wie er in der Registrierung angegeben wurde. *Provider_name* hat keinen Standardwert.  
  
 "*Datasource*"  
 Eine Zeichenfolgenkonstante, die einer bestimmten OLE DB-Datenquelle entspricht. *DataSource* ist die DBPROP_INIT_DATASOURCE-Eigenschaft, die an die IDBProperties-Schnittstelle des Anbieters zum Initialisieren des Anbieters übergeben werden. Normalerweise enthält diese Zeichenfolge den Namen der Datenbankdatei, den Namen des Datenbankservers oder einen Namen, mit dem der Anbieter die Datenbank(en) suchen kann.  
  
 "*User_id*"  
 Eine Zeichenfolgenkonstante für den Benutzernamen, der an den angegebenen OLE DB-Anbieter übergeben wird. *USER_ID* gibt den Sicherheitskontext für die Verbindung und wird als DBPROP_AUTH_USERID-Eigenschaft zum Initialisieren des Anbieters übergeben. *USER_ID* nicht mit einem Microsoft Windows-Anmeldename.  
  
 "*Kennwort*"  
 Eine Zeichenfolgenkonstante für das Benutzerkennwort, das an den OLE DB-Anbieter übergeben wird. *Kennwort* in als DBPROP_AUTH_PASSWORD-Eigenschaft übergeben wird, beim Initialisieren des Anbieters. *Kennwort* ein Microsoft Windows-Kennwort ist nicht möglich.  
  
 "*Provider_string*"  
 Eine anbieterspezifische Verbindungszeichenfolge, die als DBPROP_INIT_PROVIDERSTRING-Eigenschaft übergeben wird, um den OLE DB-Anbieter zu initialisieren. *Provider_string* kapselt normalerweise alle zum Initialisieren des Anbieters benötigten Verbindungsinformationen. Eine Liste von Schlüsselwörtern, die von erkannt werden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter finden Sie unter [Initialisierungs- und Autorisierungseigenschaften](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
 *Katalog*  
 Der Name des Katalogs oder der Datenbank, zu dem bzw. der das angegebene Objekt gehört.  
  
 *Schema*  
 Der Name des Schemas oder des Besitzers für das angegebene Objekt.  
  
 *Objekt*  
 Der Objektname, der das zu verwendende Objekt eindeutig identifiziert.  
  
 "*Abfrage*"  
 Eine Zeichenfolgenkonstante, die zum Anbieter geschickt und von ihm ausgeführt wird. Die lokale Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verarbeitet nicht diese Abfrage, sondern die vom Anbieter zurückgegebenen Abfrageergebnisse (eine Pass-Through-Abfrage). Pass-Through-Abfragen eignen sich bei Anbietern, die ihre Tabellendaten nicht über Tabellennamen verfügbar machen, sondern nur über eine Befehlssprache. Pass-Through-Abfragen werden auf dem Remoteserver unterstützt, solange der Abfrageanbieter jedoch stattdessen das OLE DB-Befehl und seiner obligatorischen Schnittstellen unterstützt. Weitere Informationen finden Sie unter [SQL Server Native Client &#40; OLE DB &#41; Verweis](../../relational-databases/native-client-ole-db-interfaces/sql-server-native-client-ole-db-interfaces.md).  
  
 BULK  
 Verwendet den BULK-Rowsetanbieter für OPENROWSET, um Daten aus einer Datei zu lesen. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann OPENROWSET aus einer Datendatei lesen, ohne die Daten in eine Zieltabelle zu laden. Dadurch können Sie OPENROWSET mit einer einfachen SELECT-Anweisung verwenden.  
  
 Die Argumente der Option BULK ermöglichen eine erhebliche Kontrolle darüber, wo das Lesen von Daten begonnen und beendet werden soll, wie mit Fehlern umgegangen wird und wie Daten interpretiert werden sollen. Sie können beispielsweise angeben, dass die Datendatei als einzeiliges, einspaltiges Rowset vom Typ gelesen werden **Varbinary**, **Varchar**, oder **Nvarchar**. Das Standardverhalten ist in den folgenden Argumentbeschreibungen erläutert.  
  
 Informationen zum Verwenden der BULK-Option finden Sie unter "Hinweise" weiter unten in diesem Thema. Informationen zu den für die Option BULK erforderlichen Berechtigungen finden Sie im Abschnitt "Berechtigungen" weiter unten in diesem Thema.  
  
> [!NOTE]  
>  Wenn OPENROWSET (BULK ...) zum Importieren von Daten mit dem vollständigen Wiederherstellungsmodell verwendet wird, wird die Protokollierung nicht optimiert.  
  
 Informationen zum Vorbereiten von Daten für den Massenimport finden Sie unter [Vorbereiten von Daten für den Massenexport oder-Import &#40; SQLServer &#41; ](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
 "*Data_file*"  
 Der vollständige Pfad der Datendatei, deren Daten in die Zieltabelle kopiert werden sollen.   
 **Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Beginnend mit [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP-Version 1.1, kann die Data_file in Azure BLOB Storage. Beispiele finden Sie unter [Beispiele von Bulk Zugriff auf Daten in Azure Blob-Speicher](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).
  
 \<Bulk_options >  
 Gibt mindestens ein Argument für die Option BULK an.  
  
 CODEPAGE = {"ACP" | "OEM" | "ROHEN" | "*Codepage*'}  
 Gibt die Codepage für die in der Datendatei enthaltenen Daten an. CODEPAGE ist nur relevant, wenn die Daten enthält **Char**, **Varchar**, oder **Text** -Spalten mit Zeichenwerten enthalten mehr als 127 oder kleiner als 32.  
  
> [!NOTE]  
>  Es wird empfohlen, dass Sie für jede Spalte in einer Formatdatei einen Sortierungsnamen außer angeben, wenn die 65001-Option Priorität vor der Sortierung/Codepage haben soll.  
  
|CODEPAGE-Wert|Description|  
|--------------------|-----------------|  
|ACP|Konvertiert Spalten vom **Char**, **Varchar**, oder **Text** Datentyp von der ANSI-/[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Codepage (ISO 1252) an die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Codepage.|  
|OEM (Standard)|Konvertiert Spalten vom **Char**, **Varchar**, oder **Text** Datentyp von dem System OEM-Codepage in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Codepage.|  
|RAW|Es erfolgt keine Konvertierung in eine andere Codepage. Dies ist die schnellste Option.|  
|*Codepage*|Gibt die Quellcodepage an, nach der die Zeichendaten in der Datendatei codiert werden, beispielsweise 850.<br /><br /> **\*\*Wichtige \* \***  Versionen vor [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Codepage 65001 (UTF-8-Codierung) nicht unterstützt.|  
  
 ERRORFILE = "*File_name*"  
 Gibt die Datei an, die zum Sammeln der Zeilen verwendet wird, die Formatierungsfehler enthalten und nicht in ein OLE DB-Rowset konvertiert werden können. Diese Zeilen werden aus der Datendatei unverändert in diese Fehlerdatei kopiert.  
  
 Die Fehlerdatei wird zu Beginn der Ausführung des Befehls erstellt. Falls die Datei bereits vorhanden ist, wird ein Fehler ausgelöst. Darüber hinaus wird eine Kontrolldatei mit der Erweiterung .ERROR.txt erstellt. Diese Datei verweist auf jede Zeile in der Fehlerdatei und stellt eine Fehlerdiagnose bereit. Sobald die Fehler korrigiert wurden, können die Daten geladen werden.  
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
Beginnend mit [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], die `error_file_path` in Azure BLOB Storage ist möglich. 

"Errorfile_data_source_name"   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
Eine benannte externe Datenquelle auf den Azure-Blob-Speicherort der Fehlerdatei verweist, die während des Imports gefundenen Fehler enthält. Die externen Datenquelle muss erstellt werden, mithilfe der `TYPE = BLOB_STORAGE` hinzugefügt, die Option [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP-Version 1.1. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).
  
 FIRSTROW =*erste_zeile*  
 Gibt die Nummer der ersten zu ladenden Zeile an. Der Standardwert lautet 1. Damit wird die erste Zeile in der festgelegten Datendatei angegeben. Die Zeilennummern werden durch Zählen der Zeilenabschlusszeichen bestimmt. FIRSTROW ist einsbasiert.  
  
 LASTROW =*letzte_zeile*  
 Gibt die Nummer der letzten zu ladenden Zeile an. Die Standardeinstellung ist 0. Damit wird die letzte Zeile in der festgelegten Datendatei angegeben.  
  
 MAXERRORS =*Maximum_errors*  
 Gibt an, nach wie vielen Syntaxfehlern oder nicht übereinstimmenden Zeilen gemäß der Definition im Dateiformat OPENROWSET eine Ausnahme auslöst. Bis zum Erreichen von MAXERRORS ignoriert OPENROWSET fehlerhafte Zeilen und lädt diese nicht, wobei jede fehlerhafte Zeile als ein Fehler gezählt wird.  
  
 Die Standardeinstellung für *Maximum_errors* ist 10.  
  
> [!NOTE]  
>  MAX_ERRORS gilt nicht für CHECK-Einschränkungen oder zum Konvertieren **Money** und **"bigint"** -Datentypen.  
  
 ROWS_PER_BATCH =*Rows_per_batch*  
 Gibt die ungefähre Anzahl von Datenzeilen in der Datendatei an. Der Wert sollte von der gleichen Größenordnung sein wie die tatsächliche Zeilenanzahl.  
  
 OPENROWSET importiert eine Datendatei immer als einzelnen Batch. Allerdings bei Angabe von *Rows_per_batch* mit einem Wert > 0, verwendet der Abfrageprozessor den Wert der *Rows_per_batch* als Hinweis für die Zuordnung von Ressourcen im Abfrageplan.  
  
 Standardmäßig ist ROWS_PER_BATCH unbekannt. ROWS_PER_BATCH = 0 hat den gleichen Effekt, als würden Sie ROWS_PER_BATCH nicht angeben.  
  
 Reihenfolge ({ *Spalte* [ASC | "DESC"]} [,...  *n*  ] [UNIQUE])  
 Ein optionaler Hinweis, der angibt, wie die Daten in der Datendatei sortiert sind. Standardmäßig geht der Massenvorgang davon aus, dass die Datendatei nicht sortiert ist. Die Leistung kann verbessert werden, wenn die festgelegte Reihenfolge vom Abfrageoptimierer zur Generierung eines effizienteren Abfrageplans verwendet werden kann. Folgendes sind Beispiele dafür, wann die Festlegung einer Sortierung von Vorteil sein kann:  
  
-   Einfügen von Zeilen in eine Tabelle mit einem gruppierten Index, in der die Rowsetdaten nach dem Schlüssel des gruppierten Index sortiert sind.  
  
-   Verknüpfen des Rowsets mit einer anderen Tabelle, in der die Sortierungs- und Joinspalten übereinstimmen.  
  
-   Aggregieren der Rowsetdaten nach den Sortierspalten.  
  
-   Verwenden des Rowsets als Quelltabelle in der FROM-Klausel einer Abfrage, wobei die Sortierungs- und Joinspalten übereinstimmen.  
  
 UNIQUE gibt an, dass die Datendatei keine doppelten Einträge aufweist.  
  
 Wenn die tatsächlichen Zeilen in der Datendatei nicht entsprechend der angegebenen Reihenfolge sortiert sind oder wenn der UNIQUE-Hinweis angegeben wird und doppelte Schlüssel vorhanden sind, wird ein Fehler zurückgegeben.  
  
 Spaltenaliase sind erforderlich, wenn ORDER verwendet wird. Die Spaltenaliasliste muss auf die abgeleitete Tabelle verweisen, auf die von der BULK-Klausel zugegriffen wird. Die Spaltennamen, die in der ORDER-Klausel angegeben sind, verweisen auf diese Spaltenaliasliste. Große Werttypen (**varchar(max)**, **nvarchar(max)**, **varbinary(max)**, und **Xml**) und große Objekttypen (LOB) (**Text**, **Ntext**, und **Image**) können keine Spalten angegeben werden.  
  
 SINGLE_BLOB  

 Gibt den Inhalt von *data_file* als einzeiliges, einspaltiges Rowset vom Typ **varbinary(max)** zurück.  
  
> [!IMPORTANT]  
>  Es wird empfohlen, XML-Daten mit SINGLE_CLOB und SINGLE_NCLOB ausschließlich unter Verwendung der SINGLE_BLOB-Option zu importieren, da nur SINGLE_BLOB alle Windows-Codierungskonvertierungen unterstützt.  
  
 SINGLE_CLOB
 Durch Lesen *Data_file* als ASCII-Daten, gibt Sie den Inhalt als einzeiliges, einspaltiges Rowset vom Typ **varchar(max)**, wobei die Sortierung der aktuellen Datenbank.  
  
 SINGLE_NCLOB  
 Gibt *data_file* als einzeiliges, einspaltiges Rowset vom Typ **nvarchar(max)** zurück, weil die Zeichen in data_file als UNICODE gelesen werden. Hierbei wird die Sortierung der aktuellen Datenbank verwendet.  


### <a name="input-file-format-options"></a>Format der Eingabedatei (Optionen)
  
FORMAT  **=**  "CSV"   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Gibt eine Datei mit kommagetrennten Werten an, die mit [RFC 4180](https://tools.ietf.org/html/rfc4180) kompatibel ist.

 FORMATFILE = "*Format_file_path*"  
 Gibt den vollständigen Pfad einer Formatdatei an. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt zwei Typen von Formatdateien: XML- und Nicht-XML-Formatdateien.  
  
 Eine Formatdatei ist erforderlich, um Spaltentypen im Resultset zu definieren. Die einzige Ausnahme hierzu ist, dass SINGLE_CLOB, SINGLE_BLOB oder SINGLE_NCLOB angegeben ist. In diesem Fall ist die Formatdatei nicht erforderlich.  
  
 Informationen zu Formatdateien finden Sie unter [mithilfe einer Formatdatei zum Massenimport von Daten &#40; SQLServer &#41; ](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).  

**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Beginnend mit [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP-Version 1.1, kann die Format_file_path in Azure BLOB Storage. Beispiele finden Sie unter [Beispiele von Bulk Zugriff auf Daten in Azure Blob-Speicher](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).

FIELDQUOTE  **=**  "Field_quote"   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Gibt ein Zeichen, das als das Anführungszeichen in CSV-Datei verwendet wird. Wenn nicht angegeben, das Anführungszeichen (") verwendet werden als das Angebot Zeichen gemäß der [RFC 4180](https://tools.ietf.org/html/rfc4180) standard.

  
## <a name="remarks"></a>Hinweise  
 `OPENROWSET`kann verwendet werden, um den Zugriff auf Remotedaten von OLE DB-Datenquellen nur, wenn die **DisallowAdhocAccess** Registrierungsoption für den angegebenen Anbieter explizit auf 0 festgelegt ist, und die Ad Hoc Distributed Queries erweiterte Konfigurationsoption ist aktiviert. Wenn diese Optionen nicht festgelegt sind, ermöglicht das Standardverhalten keinen Ad-hoc-Zugriff.  
  
 Beim Zugriff auf OLE DB-Remotedatenquellen wird die Anmelde-ID vertrauenswürdiger Verbindungen nicht automatisch von dem Server delegiert, auf dem der Client mit dem Server verbunden ist, der abgefragt wird. Die Authentifizierungsdelegierung muss konfiguriert sein.  
  
 Der Katalog- und Schemaname sind erforderlich, falls der OLE DB-Anbieter mehrere Kataloge und Schemas in der angegebenen Datenquelle unterstützt. Werte für *Katalog* und *Schema* kann ausgelassen werden, wenn der OLE DB-Anbieter nicht unterstützt wird. Wenn der Anbieter nur Schemanamen, einen zweiteiligen Namen im Format *Schema***.** *Objekt* muss angegeben werden. Wenn der Anbieter nur Katalognamen, einen dreiteiligen Namen im Format *Katalog***.** *Schema***.** *Objekt* muss angegeben werden. Dreiteilige Namen müssen angegeben werden, für Pass-Through-Abfragen verwenden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter. Weitere Informationen finden Sie unter [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41; ](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
 `OPENROWSET`akzeptiert keine Variablen Argumente.  
  
 Jeder Aufruf von `OPENDATASOURCE`, `OPENQUERY`, oder `OPENROWSET` in die `FROM` -Klausel wird ausgewertet einzeln und unabhängig von anderen Aufrufen dieser Funktionen, die als Ziel des Updates verwendet, auch wenn die beiden Aufrufe identische Argumente bereitgestellt werden. Insbesondere haben Filter- oder Joinbedingungen, die auf das Ergebnis eines dieser Aufrufe angewendet werden, keine Auswirkungen auf die Ergebnisse des jeweils anderen.  
  
## <a name="using-openrowset-with-the-bulk-option"></a>Verwenden von OPENROWSET mit der Option BULK  
 Die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Erweiterungen unterstützen die OPENROWSET(BULK...)-Funktion:  
  
-   Eine FROM-Klausel, die mit `SELECT` Aufrufen `OPENROWSET(BULK...)` mit vollständigen eines Tabellennamens `SELECT` Funktionalität.  
  
     `OPENROWSET`mit der `BULK` Option erfordert ein abhängiger Name, auch bekannt als Bereichsvariable oder Alias in der `FROM` Klausel. Spaltenaliase können angegeben werden. Wenn keine Spaltenaliasliste angegeben wird, sind für die Formatdatei Spaltennamen notwendig. Durch das Angeben von Spaltenaliasen werden die Spaltennamen in der Formatdatei wie folgt überschrieben:  
  
     `FROM OPENROWSET(BULK...) AS table_alias`  
  
     `FROM OPENROWSET(BULK...) AS table_alias(column_alias,...n)`  
>    [!IMPORTANT]  
>    Fehler beim Hinzufügen der `AS <table_alias>` führt zu dem Fehler:    
>    Meldung 491, Ebene 16, Status 1, Zeile 20    
>    Für das Massenrowset in der FROM-Klausel muss ein abhängiger Name angegeben werden.    
  
-   Ein `SELECT...FROM OPENROWSET(BULK...)` Anweisung direkt abgefragt werden die Daten in einer Datei, ohne die Daten in eine Tabelle importiert. `SELECT…FROM OPENROWSET(BULK...)`-Anweisungen können auch bulkspaltenaliase aufführen, mithilfe einer Formatdatei, um Spaltennamen und auch Datentypen anzugeben.  
  
-   Mit `OPENROWSET(BULK...)` als Quelltabelle in eine `INSERT` oder `MERGE` Anweisung Massenimport von Daten aus einer Datendatei in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle. Weitere Informationen finden Sie unter [Importieren von Massendaten durch Verwenden von BULK INSERT oder OPENROWSET &#40; BULK... &#41; &#40; SQLServer &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md) .  
  
-   Wenn die `OPENROWSET BULK` Option zusammen mit einer `INSERT` -Anweisung, die BULK-Klausel Tabellenhinweise unterstützt. Zusätzlich zum normalen Tabellenhinweise, z. B. `TABLOCK`, `BULK` Klausel kann die folgenden speziellen Tabellenhinweise akzeptiert: `IGNORE_CONSTRAINTS` (ignoriert nur die `CHECK` und `FOREIGN KEY` Einschränkungen), `IGNORE_TRIGGERS`, `KEEPDEFAULTS`, und `KEEPIDENTITY`. Weitere Informationen finden Sie unter [Tabellenhinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Informationen zur Verwendung von `INSERT...SELECT * FROM OPENROWSET(BULK...)` -Anweisungen finden Sie unter [Massenimport und-Export von Daten &#40; SQLServer &#41; ](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md). Informationen dazu, wann Zeileneinfügevorgänge, die durch den Massenimport ausgeführt werden, im Transaktionsprotokoll protokolliert werden, finden Sie unter [Voraussetzungen für die minimale Protokollierung beim Massenimport](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
> [!NOTE]  
>  Bei Verwendung von `OPENROWSET`, es ist wichtig zu verstehen, wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Identitätswechseln umgegangen. Informationen zu Sicherheitsaspekten finden Sie unter [Importieren von Massendaten durch Verwenden von BULK INSERT oder OPENROWSET &#40; BULK... &#41; &#40; SQLServer &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
### <a name="bulk-importing-sqlchar-sqlnchar-or-sqlbinary-data"></a>Massenimport von SQLCHAR-, SQLNCHAR- oder SQLBINARY-Daten  
 Wenn keine maximale Länge für SQLCHAR-, SQLNCHAR- oder SQLBINARY-Daten angegeben wird, geht OPENROWSET(BULK...) davon aus, dass sie 8000 Bytes nicht überschreitet. Wenn die zu importierenden Daten in einem LOB-Datenfeld ist, das eine enthält **varchar(max)**, **nvarchar(max)**, oder **varbinary(max)** Objekte, die 8000 Bytes nicht überschreiten, müssen Sie verwenden ein XML-Formatdatei, die die maximale Länge für das Feld "Daten" definiert. Um die maximale Länge anzugeben, bearbeiten Sie die Formatdatei, und deklarieren Sie das Attribut MAX_LENGTH.  
  
> [!NOTE]  
>  Bei einer automatisch generierten Formatdatei wird die Länge oder maximale Länge für ein LOB-Feld nicht angeben. Sie können eine Formatdatei jedoch bearbeiten und die Länge oder maximale Länge manuell angeben.  
  
### <a name="bulk-exporting-or-importing-sqlxml-documents"></a>Massenexportieren und -importieren von SQLXML-Dokumenten  
 Verwenden Sie in der Formatdatei einen der folgenden Datentypen für den Massenexport oder -import von SQLXML-Daten.  
  
|Datentyp|Wirkung|  
|---------------|------------|  
|SQLCHAR oder SQLVARYCHAR|Die Daten werden in der Clientcodepage gesendet bzw. in der durch die Sortierung implizierten Codeseite.|  
|SQLNCHAR oder SQLNVARCHAR|Die Daten werden im Unicode-Format gesendet.|  
|SQLBINARY oder SQLVARYBIN|Die Daten werden ohne Konvertierung gesendet.|  
  
## <a name="permissions"></a>Berechtigungen  
 `OPENROWSET`Berechtigungen werden durch die Berechtigungen des Benutzernamens bestimmt, die an dem OLE DB-Anbieter übergeben wird. Verwenden der `BULK` Option erfordert `ADMINISTER BULK OPERATIONS` Berechtigung.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-openrowset-with-select-and-the-sql-server-native-client-ole-db-provider"></a>A. Verwenden von OPENROWSET mit SELECT und dem SQL Server Native Client OLE DB-Anbieter  
 Im folgenden Beispiel wird die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter, den Zugriff auf die `HumanResources.Department` -Tabelle in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] Datenbank auf dem Remoteserver `Seattle1`. (Wenn Sie SQLNCLI verwenden, leitet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zur neuesten Version des OLE DB-Anbieters von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client um.) Mithilfe einer `SELECT`-Anweisung wird das zurückgegebene Rowset definiert. Die Anbieterzeichenfolge enthält die Schlüsselwörter `Server` und `Trusted_Connection`. Diese Schlüsselwörter werden erkannt, durch die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter.  
  
```sql  
SELECT a.*  
FROM OPENROWSET('SQLNCLI', 'Server=Seattle1;Trusted_Connection=yes;',  
     'SELECT GroupName, Name, DepartmentID  
      FROM AdventureWorks2012.HumanResources.Department  
      ORDER BY GroupName, Name') AS a;  
```  
  
### <a name="b-using-the-microsoft-ole-db-provider-for-jet"></a>B. Verwenden des Microsoft OLE DB-Anbieters für Jet  
 Im folgenden Beispiel wird mithilfe des [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB-Anbieters für Jet auf die `Customers`-Tabelle in der `Northwind`-Datenbank von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access zugegriffen.  
  
> [!NOTE]  
>  In diesem Beispiel wird vorausgesetzt, dass Access installiert ist. Um dieses Beispiel auszuführen, müssen Sie die Northwind-Datenbank installieren.  
  
```sql  
SELECT CustomerID, CompanyName  
   FROM OPENROWSET('Microsoft.Jet.OLEDB.4.0',  
      'C:\Program Files\Microsoft Office\OFFICE11\SAMPLES\Northwind.mdb';  
      'admin';'',Customers);  
GO  
```  
  
### <a name="c-using-openrowset-and-another-table-in-an-inner-join"></a>C. Verwenden von OPENROWSET und einer weiteren Tabelle in einem INNER JOIN  
 Das folgende Beispiel wählt alle Daten aus der `Customers` Tabelle aus der lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `Northwind` Datenbank und von der `Orders` Tabelle aus der Access `Northwind` -Datenbank auf demselben Computer gespeichert.  
  
> [!NOTE]  
>  In diesem Beispiel wird vorausgesetzt, dass Access installiert ist. Um dieses Beispiel auszuführen, müssen Sie die Northwind-Datenbank installieren.  
  
```sql  
USE Northwind  ;  
GO  
SELECT c.*, o.*  
FROM Northwind.dbo.Customers AS c   
   INNER JOIN OPENROWSET('Microsoft.Jet.OLEDB.4.0',   
   'C:\Program Files\Microsoft Office\OFFICE11\SAMPLES\Northwind.mdb';'admin';'', Orders)      
   AS o   
   ON c.CustomerID = o.CustomerID ;  
GO  
```  
  
### <a name="d-using-openrowset-to-bulk-insert-file-data-into-a-varbinarymax-column"></a>D. Verwenden von OPENROWSET zum Masseneinfügen von Dateidaten in eine Spalte vom Typ varbinary(max)  
 Das folgende Beispiel erstellt eine kleine Tabelle für Demonstrationszwecke und fügt Dateidaten aus der Datei `Text1.txt`, die im Stammverzeichnis `C:` gespeichert ist, in eine Spalte vom Datentyp `varbinary(max)` ein.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTable(FileName nvarchar(60),   
  FileType nvarchar(60), Document varbinary(max));  
GO  
  
INSERT INTO myTable(FileName, FileType, Document)   
   SELECT 'Text1.txt' AS FileName,   
      '.txt' AS FileType,   
      * FROM OPENROWSET(BULK N'C:\Text1.txt', SINGLE_BLOB) AS Document;  
GO  
```  
  
### <a name="e-using-the-openrowset-bulk-provider-with-a-format-file-to-retrieve-rows-from-a-text-file"></a>E. Verwenden des OPENROWSET BULK-Anbieters mit einer Formatdatei zum Abrufen von Zeilen aus einer Textdatei  
 Im folgenden Beispiel werden mithilfe einer Formatdatei Zeilen aus der durch Tabstopps getrennten Textdatei `values.txt` abgerufen, die die folgenden Daten enthält:  
  
```sql  
1     Data Item 1  
2     Data Item 2  
3     Data Item 3  
```  
  
 Die Formatdatei `values.fmt` beschreibt die Spalten in `values.txt`:  
  
```sql  
9.0  
2  
1  SQLCHAR  0  10 "\t"        1  ID                SQL_Latin1_General_Cp437_BIN  
2  SQLCHAR  0  40 "\r\n"      2  Description        SQL_Latin1_General_Cp437_BIN  
```  
  
 In der folgenden Abfrage werden diese Daten abgerufen:  
  
```sql  
SELECT a.* FROM OPENROWSET( BULK 'c:\test\values.txt',   
   FORMATFILE = 'c:\test\values.fmt') AS a;  
```  
  
### <a name="f-specifying-a-format-file-and-code-page"></a>F. Angabe Format der Datei und code  
 Im folgenden Beispiel wird gezeigt, wie sowohl die Datei- und Code Seite Formatoptionen gleichzeitig verwenden.  
  
```sql  
INSERT INTO MyTable SELECT a.* FROM  
OPENROWSET (BULK N'D:\data.csv', FORMATFILE =   
    'D:\format_no_collation.txt', CODEPAGE = '65001') AS a;  
```  
### <a name="g-accessing-data-from-a-csv-file-with-a-format-file"></a>G. Zugriff auf Daten aus einer CSV-Datei mit einer Formatdatei  
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
```sql
SELECT *
FROM OPENROWSET(BULK N'D:\XChange\test-csv.csv',
    FORMATFILE = N'D:\XChange\test-csv.fmt', 
    FIRSTROW=2, 
    FORMAT='CSV') AS cars;  
```

### <a name="h-accessing-data-from-a-csv-file-without-a-format-file"></a>H. Zugriff auf Daten aus einer CSV-Datei ohne eine Formatdatei

```sql
SELECT * FROM OPENROWSET(
   BULK 'C:\Program Files\Microsoft SQL Server\MSSQL14.CTP1_1\MSSQL\DATA\inv-2017-01-19.csv',
   SINGLE_CLOB) AS DATA;
```

### <a name="i-accessing-data-from-a-file-stored-on-azure-blob-storage"></a>I. Zugriff auf Daten aus einer Datei auf Azure-Blob-Speicher   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Im folgenden Beispiel wird eine externe Datenquelle, die auf einen Container im Azure-Speicherkonten und datenbankweit gültigen Anmeldeinformationen für eine shared Access Signature erstellt verweist.     

```sql
SELECT * FROM OPENROWSET(
   BULK  'inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoices',
   SINGLE_CLOB) AS DataFile;
```   
Führen Sie für `OPENROWSET` Konfigurieren der Anmeldeinformationen und die externe Datenquelle, einschließlich Beispielen finden Sie unter [Beispiele von Bulk Zugriff auf Daten in Azure Blob-Speicher](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).
 
### <a name="additional-examples"></a>Zusätzliche Beispiele  
 Zusätzliche Beispiele zur Verwendung `INSERT...SELECT * FROM OPENROWSET(BULK...)`, finden Sie unter den folgenden Themen:  
  
-   [Beispiele für den Massenimport und -export von XML-Dokumenten &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Beibehalten von Identitätswerten beim Massenimport von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Beibehalten von NULL-Werten oder Verwenden von Standardwerten während des Massenimports &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Massenimport von Daten mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Verwenden des Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Überspringen einer Tabellenspalte mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Auslassen eines Datenfelds mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Verwenden einer Formatdatei zum Zuordnen von Tabellenspalten zu Datendateifeldern &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>Siehe auch  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [Massenimport und -export von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENDATASOURCE (Transact-SQL)](../../t-sql/functions/opendatasource-transact-sql.md)   
 [OPENQUERY &#40; Transact-SQL &#41;](../../t-sql/functions/openquery-transact-sql.md)   
 [Rowset-Funktionen &#40; Transact-SQL &#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [Sp_serveroption &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [WOBEI &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
