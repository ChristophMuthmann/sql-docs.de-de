---
title: BULK INSERT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- BULK_TSQL
- BULK INSERT
- BULK_INSERT_TSQL
- BULK
dev_langs:
- TSQL
helpviewer_keywords:
- tables [SQL Server], importing data into
- inserting files
- views [SQL Server], importing data into
- BULK INSERT statement
- views [SQL Server], exporting data from
- importing data, bulk import
- bulk importing [SQL Server], BULK INSERT statement
- file importing [SQL Server]
ms.assetid: be3984e1-5ab3-4226-a539-a9f58e1e01e2
caps.latest.revision: 153
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: d6ac507a908d77618aa4171bc222e60cbd051ed0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="bulk-insert-transact-sql"></a>BULK INSERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Importiert eine Datendatei in eine Datenbanktabelle oder Sicht und verwendet dabei ein vom Benutzer angegebenes Format in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BULK INSERT   
   [ database_name . [ schema_name ] . | schema_name . ] [ table_name | view_name ]   
      FROM 'data_file'   
     [ WITH   
    (   
   [ [ , ] BATCHSIZE = batch_size ]   
   [ [ , ] CHECK_CONSTRAINTS ]   
   [ [ , ] CODEPAGE = { 'ACP' | 'OEM' | 'RAW' | 'code_page' } ]   
   [ [ , ] DATAFILETYPE =   
      { 'char' | 'native'| 'widechar' | 'widenative' } ]   
   [ [ , ] DATASOURCE = 'data_source_name' ]
   [ [ , ] ERRORFILE = 'file_name' ]
   [ [ , ] ERRORFILE_DATASOURCE = 'data_source_name' ]   
   [ [ , ] FIRSTROW = first_row ]   
   [ [ , ] FIRE_TRIGGERS ]   
   [ [ , ] FORMATFILE_DATASOURCE = 'data_source_name' ]
   [ [ , ] KEEPIDENTITY ]   
   [ [ , ] KEEPNULLS ]   
   [ [ , ] KILOBYTES_PER_BATCH = kilobytes_per_batch ]   
   [ [ , ] LASTROW = last_row ]   
   [ [ , ] MAXERRORS = max_errors ]   
   [ [ , ] ORDER ( { column [ ASC | DESC ] } [ ,...n ] ) ]   
   [ [ , ] ROWS_PER_BATCH = rows_per_batch ]   
   [ [ , ] ROWTERMINATOR = 'row_terminator' ]   
   [ [ , ] TABLOCK ]   

   -- input file format options
   [ [ , ] FORMAT = 'CSV' ]
   [ [ , ] FIELDQUOTE = 'quote_characters']
   [ [ , ] FORMATFILE = 'format_file_path' ]   
   [ [ , ] FIELDTERMINATOR = 'field_terminator' ]   
   [ [ , ] ROWTERMINATOR = 'row_terminator' ]   
    )]   
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Der Name der Datenbank, in der sich die angegebene Tabelle oder Sicht befindet. Fehlt die Angabe, ist dies die aktuelle Datenbank.  
  
 *schema_name*  
 Der Name der Tabelle oder des Sichtschemas. *schema_name* ist optional, wenn das Standardschema des Benutzers, der den Massenimportvorgang ausführt, das Schema der angegebenen Tabelle oder Sicht ist. Wenn *schema* nicht angegeben wird und es sich bei dem Standardschema des Benutzers, der den Massenimportvorgang ausführt, nicht um das Schema der angegebenen Tabelle oder Sicht handelt, wird in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Fehlermeldung zurückgegeben, und der Massenimportvorgang wird abgebrochen.  
  
 *table_name*  
 Der Name der Tabelle oder Sicht, in die der Massenimport von Daten erfolgen sollen. Es können nur Sichten verwendet werden, deren Spalten alle auf dieselbe Basistabelle verweisen. Weitere Informationen über die Einschränkungen beim Laden von Daten in Sichten finden Sie unter [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md).  
  
 **'** *data_file* **'**  
 Der vollständige Pfad der Datendatei mit den Daten, die in die angegebene Tabelle oder Sicht importiert werden sollen. BULK INSERT kann Daten von einem Datenträger importieren, einschließlich eines Netzwerks, einer Diskette, einer Festplatte usw.   
 
 Für *data_file* muss ein gültiger Pfad auf dem Server, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, angegeben werden. Wenn *data_file* eine Remotedatei ist, geben Sie den UNC-Namen (Universal Naming Convention) an. Ein UNC-Name weist das Format \\\\*Systemname*\\*ShareName*\\*Path*\\*FileName*. Beispiel: `\\SystemX\DiskZ\Sales\update.txt`.   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Ab [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 kann sich data_file in Azure Blob Storage befinden.

**'** *data_source_name* **'**   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Es handelt sich um eine benannte externe Datenquelle, die auf den Azure Blob-Speicherort der Datei verweist, welche importiert wird. Die externe Datenquelle muss mithilfe der in [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 hinzugefügten `TYPE = BLOB_STORAGE`-Option erstellt werden. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE (CREATE EXTERNAL DATA SOURCE)](../../t-sql/statements/create-external-data-source-transact-sql.md).    
  
 BATCHSIZE **=***batch_size*  
 Gibt die Anzahl von Zeilen in einem Batch an. Jeder Batch wird als eine Transaktion auf den Server kopiert. Falls ein Fehler erzeugt wird, führt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die Transaktion jedes Batches ein Commit oder Rollback aus. In der Standardeinstellung werden alle Daten, die sich in der angegebenen Datendatei befinden, als ein Batch behandelt. Informationen zu Leistungsaspekten finden Sie unter "Hinweise" weiter unten in diesem Thema.  
  
 CHECK_CONSTRAINTS  
 Gibt an, dass alle Einschränkungen, die für die Zieltabelle oder -sicht gelten, während des Massenimportvorgangs überprüft werden müssen. Ohne die Option CHECK_CONSTRAINTS werden alle CHECK- und FOREIGN KEY-Einschränkungen ignoriert, und nach Abschluss des Vorgangs wird die Einschränkung in der Tabelle als nicht vertrauenswürdig gekennzeichnet.  
  
> [!NOTE]  
>  UNIQUE- und PRIMARY KEY-Einschränkungen werden immer erzwungen. Beim Importieren in eine Zeichenspalte, die mit einer NOT NULL-Einschränkung definiert ist, fügt BULK INSERT eine leere Zeichenfolge ein, wenn die Textdatei keinen Wert enthält.  
  
 An gewissen Punkten müssen Sie die Einschränkungen in der gesamten Tabelle überprüfen. Wenn die Tabelle vor dem Massenimportvorgang nicht leer war, kann der Aufwand einer erneuten Überprüfung der Einschränkung höher sein als das Anwenden von CHECK-Einschränkungen auf die inkrementellen Daten.  
  
 Die Deaktivierung von Einschränkungen (das Standardverhalten) kann z. B. erwünscht sein, wenn die Eingabedaten Zeilen enthalten, die Einschränkungen verletzen. Wenn CHECK-Einschränkungen deaktiviert sind, können Sie die Daten importieren und dann [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen verwenden, um die ungültigen Daten zu entfernen.  
  
> [!NOTE]  
>  Die Option MAXERRORS kann zur Einschränkungsüberprüfung nicht verwendet werden.  
  
 CODEPAGE **=** { **'** ACP **'** | **'** OEM **'** | **'** RAW **'** | **'***code_page***'** }  
 Gibt die Codepage für die in der Datendatei enthaltenen Daten an. CODEPAGE ist nur dann von Bedeutung, wenn die Daten **char**-, **varchar**- oder **text**-Spalten mit Zeichenwerten enthalten, die größer als **127** oder kleiner als **32** sind.  

> [!IMPORTANT]
> Die Option CODEPAGE wird unter Linux nicht unterstützt.

> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, für jede Spalte einen Sortierungsnamen in einer [Formatdatei](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md) anzugeben.  
  
|CODEPAGE-Wert|Description|  
|--------------------|-----------------|  
|ACP|Spalten vom Datentyp **char**, **varchar** oder **text** werden von der [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]/[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Codepage (ISO 1252) in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Codepage konvertiert.|  
|OEM (Standard)|Spalten vom Datentyp **char**, **varchar** oder **text** werden von der OEM-Codepage des Systems in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Codepage konvertiert.|  
|RAW|Dies ist die schnellste Option, da keine Konvertierung von einer Codepage in eine andere erfolgt.|  
|*Codepage*|Bestimmte Codepagenummer, z. B. 850.<br /><br /> **\*\* Wichtig \*\*** In Versionen vor [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] wird die Codepage 65001 (UTF-8-Codierung) nicht unterstützt.|  
  
 DATAFILETYPE **=** { **'char'** | **'native'** | **'widechar'** | **'widenative'** }  
 Gibt an, dass BULK INSERT den Importvorgang mithilfe des angegebenen DATAFILETYPE-Werts ausführt.  
  
|DATAFILETYPE-Wert|Alle Daten, die dargestellt sind in:|  
|------------------------|------------------------------|  
|**char** (Standard)|Zeichenformat<br /><br /> Weitere Informationen finden Sie unter [Verwenden des Zeichenformats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md).|  
|**native**|Systemeigene (Datenbank-) Datentypen. Erstellen Sie die native Datendatei durch das Massenimportieren von Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe des Hilfsprogramms **bcp**.<br /><br /> Der Wert native bietet eine höhere Leistung als der Wert char.<br /><br /> Weitere Informationen finden Sie unter [Verwenden des nativen Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md).|  
|**widechar**|Unicode-Zeichen<br /><br /> Weitere Informationen finden Sie unter [Verwenden des Unicode-Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md).|  
|**widenative**|Native (Datenbank-) Datentypen, außer in **char**-, **varchar**- und **text**-Spalten, in denen Date als Unicode gespeichert werden. Erstellen Sie die Datendatei **widenative** durch das Massenimportieren von Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe des Hilfsprogramms **bcp**.<br /><br /> Der Wert vom Datentyp **widenative** bietet eine höhere Leistung als der **widechar**-Wert. Falls die Datendatei erweiterte [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]-Zeichen enthält, geben Sie **widenative** an.<br /><br /> Weitere Informationen finden Sie unter [Verwenden des nativen Unicode-Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md).|  
  
  ERRORFILE **='***file_name***'**  
 Gibt die Datei an, die zum Sammeln der Zeilen verwendet wird, die Formatierungsfehler enthalten und nicht in ein OLE DB-Rowset konvertiert werden können. Diese Zeilen werden aus der Datendatei unverändert in diese Fehlerdatei kopiert.  
  
 Die Fehlerdatei wird bei Ausführung des Befehls erstellt. Falls die Datei bereits vorhanden ist, tritt ein Fehler auf. Darüber hinaus wird eine Kontrolldatei mit der Erweiterung .ERROR.txt erstellt. Diese Datei enthält einen Verweis auf jede Zeile in der Fehlerdatei und stellt eine Fehlerdiagnose bereit. Sobald die Fehler korrigiert wurden, können die Daten geladen werden.   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
Ab [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] kann sich `error_file_path` im Azure Blob Storage befinden.

'errorfile_data_source_name'   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
Es handelt sich um eine benannte externe Datenquelle, die auf den Azure Blob-Speicherort der Fehlerdatei verweist, welche Fehler enthält, die während des Importierens gefunden wurden. Die externe Datenquelle muss mithilfe der in [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 hinzugefügten `TYPE = BLOB_STORAGE`-Option erstellt werden. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE (CREATE EXTERNAL DATA SOURCE)](../../t-sql/statements/create-external-data-source-transact-sql.md).
 
 FIRSTROW **=***first_row*  
 Gibt die Nummer der ersten zu ladenden Zeile an. In der Standardeinstellung ist dies die erste Zeile in der angegebenen Datendatei. FIRSTROW ist einsbasiert.  
  
> [!NOTE]  
>  Es ist nicht vorgesehen, dass das FIRSTROW-Attribut Spaltenheader überspringt. Header zu überspringen wird von der BULK INSERT-Anweisung nicht unterstützt. Wenn Zeilen ausgelassen werden, werden von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] nur die Feldabschlusszeichen berücksichtigt und die Daten in den Feldern von ausgelassenen Zeilen nicht überprüft.  
  
 FIRE_TRIGGERS  
 Gibt an, dass INSERT-Trigger, die für die Zieltabelle definiert sind, während des Massenimportvorgangs ausgeführt werden. Falls Trigger für INSERT-Vorgänge in der Zieltabelle definiert sind, werden sie für jeden abgeschlossenen Batch ausgelöst.  
  
 Wenn FIRE_TRIGGERS nicht angegeben ist, werden keine INSERT-Trigger ausgeführt.  

FORMATFILE_DATASOURCE **=** 'data_source_name'   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1   
Es handelt sich um eine benannte externe Datenquelle, die auf den Azure Blob-Speicherort der Formatatei verweist, welche das Schema der importierten Daten definiert. Die externe Datenquelle muss mithilfe der in [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 hinzugefügten `TYPE = BLOB_STORAGE`-Option erstellt werden. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE (CREATE EXTERNAL DATA SOURCE)](../../t-sql/statements/create-external-data-source-transact-sql.md).
  
 KEEPIDENTITY  
 Gibt an, dass der oder die Identitätswerte in der importierten Datendatei für die Identitätsspalte verwendet werden sollen. Wird KEEPIDENTITY nicht angegeben, werden die Identitätswerte für diese Spalte zwar überprüft, jedoch nicht importiert. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] weist dann auf der Basis von Ausgangswerten und inkrementellen Werten, die beim Erstellen der Tabelle angegeben wurden, eindeutige Werte zu. Wenn die Datendatei keine Werte für die Identitätsspalte in der Tabelle oder Sicht enthält, geben Sie mithilfe einer Formatdatei an, dass die Identitätsspalte der Tabelle oder Sicht beim Importieren von Daten ausgelassen werden soll. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] weist der Spalte automatisch eindeutige Werte zu. Weitere Informationen finden Sie unter [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md).  
  
 Weitere Informationen über das Beibehalten von Identitätswerten finden Sie unter [Beibehalten von Identitätswerten beim Massenimport von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md).  
  
 KEEPNULLS  
 Gibt an, dass in leere Spalten während des Massenimportvorgangs keine Standardwerte eingefügt, sondern ein NULL-Wert für diese Spalten beibehalten werden soll. Weitere Informationen finden Sie unter [Beibehalten von NULL-Werten oder Verwenden von Standardwerten während des Massenimports &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md).  
  
 KILOBYTES_PER_BATCH **=** *kilobytes_per_batch*  
 Gibt die ungefähre Datenmenge pro Batch in KB als *kilobytes_per_batch* an. In der Standardeinstellung ist KILOBYTES_PER_BATCH unbekannt. Informationen zu Leistungsaspekten finden Sie unter "Hinweise" weiter unten in diesem Thema.  
  
 LASTROW**=***last_row*  
 Gibt die Nummer der letzten zu ladenden Zeile an. Der Standardwert ist 0, wodurch die Daten bis zur letzten Zeile in der angegebenen Datendatei geladen werden.  
  
 MAXERRORS **=** *max_errors*  
 Gibt die maximale Anzahl von Syntaxfehlern an, die in den Daten zulässig sind, bevor der Massenimportvorgang abgebrochen wird. Jede Zeile, die beim Massenimportvorgang nicht importiert werden kann, wird ignoriert und zählt dabei als ein Fehler. Wenn *max_errors* nicht angegeben ist, wird der Standardwert 10 verwendet.  
  
> [!NOTE]  
>  Die Option MAX_ERRORS kann nicht zur Einschränkungsüberprüfung oder zum Konvertieren der Datentypen **money** und **bigint** verwendet werden.  
  
 ORDER ( { *column* [ ASC | DESC ] } [ **,**... *n* ] )  
 Gibt die Vorgehensweise beim Sortieren der Daten in der Datendatei an. Die Leistung des Massenkopierens wird verbessert, wenn die zu importierenden Daten entsprechend dem gruppierten Index der Tabelle (falls vorhanden) sortiert sind. Wenn die Datendatei in einer anderen Reihenfolge sortiert wird, die von der Reihenfolge eines Schlüssels des gruppierten Indexes abweicht, oder die Tabelle keinen gruppierten Index hat, wird die ORDER-Klausel ignoriert. Die angegebenen Spaltennamen müssen gültige Spaltennamen in der Zieltabelle sein. Standardmäßig geht der Masseneinfügevorgang davon aus, dass die Datendatei nicht sortiert ist. Beim optimierten Massenimport wird in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auch überprüft, ob die importierten Daten sortiert sind.  
  
 *n*  
 Ein Platzhalter, der anzeigt, dass mehrere Spalten angegeben werden können.  
  
 ROWS_PER_BATCH **=***rows_per_batch*  
 Gibt die ungefähre Anzahl von Datenzeilen in der Datendatei an.  
  
 Standardmäßig werden alle Daten in der Datendatei als einzelne Transaktion an den Server gesendet, und die Anzahl von Zeilen im Batch ist dem Abfrageoptimierer nicht bekannt. Wenn Sie ROWS_PER_BATCH (mit einem Wert > 0) angeben, verwendet der Server diesen Wert, um den Massenimportvorgang zu optimieren. Der für ROWS_PER_BATCH angegebene Wert sollte etwa der tatsächlichen Zeilenanzahl entsprechen. Informationen zu Leistungsaspekten finden Sie unter "Hinweise" weiter unten in diesem Thema.  
  
 
 TABLOCK  
 Gibt an, dass eine Sperre auf Tabellenebene für die Dauer des Massenimportvorgangs aktiviert wird. Eine Tabelle kann gleichzeitig von mehreren Clients geladen werden, wenn die Tabelle keine Indizes aufweist und TABLOCK angegeben ist. Standardmäßig wird das Sperrverhalten durch die Tabellenoption **table lock on bulk load**bestimmt. Da weniger Sperrkonflikte in der Tabelle auftreten, wenn diese während des Massenimportvorgangs gesperrt wird, verbessert sich in manchen Fällen die Leistung erheblich. Informationen zu Leistungsaspekten finden Sie unter "Hinweise" weiter unten in diesem Thema.  
  
 Bei einem Columnstore-Index ist das Sperrverhalten anders, da er intern in mehrere Rowsets unterteilt wird.  Jeder Thread lädt Daten ausschließlich in jedes Rowset, indem er eine X-Sperre im Rowset durchführt, die das parallele Laden von Daten mit Datenladungssitzungen zulässt. Durch die Verwendung der Option TABLOCK führt der Thread eine X-Sperre in der Tabelle durch (im Gegensatz zur BU-Sperre für traditionelle Rowsets), wodurch verhindert wird, dass andere gleichzeitige Threads Daten gleichzeitig laden.  

### <a name="input-file-format-options"></a>Formatoptionen der Eingabedatei
  
FORMAT **=** 'CSV'   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Gibt eine CSV-Datei an, die dem Standard [RFC 4180](https://tools.ietf.org/html/rfc4180) entspricht.

FIELDQUOTE **=** 'field_quote'   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Gibt ein Zeichen an, das als Anführungszeichen in der CSV-Datei verwendet wird. Wenn dies nicht angegeben ist, wird das Anführungszeichen (") so verwendet, wie es im Standard [RFC 4180](https://tools.ietf.org/html/rfc4180) definiert ist.
  
 FORMATFILE **='***format_file_path***'**  
 Gibt den vollständigen Pfad einer Formatdatei an. Eine Formatdatei beschreibt die Datendatei, die gespeicherte Antworten enthält. Diese Antworten wurden mithilfe des Hilfsprogramms **bcp** für die gleiche Tabelle oder Sicht erstellt. Die Formatdatei muss verwendet werden, wenn Folgendes zutrifft:  
  
-   Die Datendatei enthält größere oder weniger Spalten als die Tabelle oder Sicht.  
  
-   Die Spalten befinden sich in einer unterschiedlichen Reihenfolge.  
  
-   Die Spaltentrennzeichen variieren.  
  
-   Es liegen andere Änderungen im Datenformat vor. Formatdateien werden in der Regel mit dem Hilfsprogramm **bcp** erstellt und nach Bedarf mit einem Text-Editor geändert. Weitere Informationen finden Sie unter [bcp Utility](../../tools/bcp-utility.md).  

**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Ab [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 kann sich format_file_path in Azure Blob Storage befinden.

 FIELDTERMINATOR **='***Feldabschlusszeichen***'**  
 Gibt das Feldabschlusszeichen an, das für Datendateien vom Typ **char** und **widechar** verwendet werden soll. Standardmäßig wird \t (Tabstoppzeichen) als Feldabschlusszeichen verwendet. Weitere Informationen finden Sie unter [Angeben von Feld- und Zeilenabschlusszeichen &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  

 ROWTERMINATOR **='***Zeilenabschlusszeichen***'**  
 Gibt das Zeilenabschlusszeichen an, das für **char**- und **widechar**-Datendateien verwendet werden soll. Standardmäßig wird **\r\n** (Neue-Zeile-Zeichen) als Zeilenabschlusszeichen verwendet.  Weitere Informationen finden Sie unter [Angeben von Feld- und Zeilenabschlusszeichen &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  

  
## <a name="compatibility"></a>Kompatibilität  
 BULK INSERT erzwingt strenge Datenüberprüfungen für die aus einer Datei gelesenen Daten, die möglicherweise zum Fehlschlagen vorhandener Skripts führen können, wenn diese für ungültige Daten in einer Datendatei ausgeführt werden. BULK INSERT überprüft beispielsweise Folgendes:  
  
-   Die native Darstellung der Datentypen **float** oder **real** ist gültig.  
  
-   Unicode-Daten besitzen eine gerade Bytelänge.  
  
## <a name="data-types"></a>Datentypen  
  
### <a name="string-to-decimal-data-type-conversions"></a>Konvertierungen von Zeichenfolgen- in Dezimaldatentypen  
 Die in BULK INSERT-Vorgängen verwendeten Konvertierungen von Zeichenfolgen in Dezimaldatentypen folgen denselben Regeln wie die [!INCLUDE[tsql](../../includes/tsql-md.md)] [CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md)-Funktion insofern, als Zeichenfolgen mit numerischen Werten in wissenschaftlicher Schreibweise nicht akzeptiert werden. Daher behandelt BULK INSERT diese Zeichenfolgen als ungültige Werte und meldet Konvertierungsfehler.  
  
 Um dieses Verhalten zu umgehen, verwenden Sie eine Formatdatei zum Massenimport von **float**-Daten in wissenschaftlicher Schreibweise in Spalten im Dezimalformat. Beschreiben Sie in der Formatdatei diese Spalte explizit als vom Datentyp **real** oder **float**. Weitere Informationen zu diesen Datentypen finden Sie unter [float und real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
> [!NOTE]  
>  Formatdateien stellen **real**-Daten als **SQLFLT4**-Datentyp und **float**-Daten als **SQLFLT8**-Datentyp dar. Weitere Informationen über Nicht-XML-Formatdateien finden Sie unter [Angeben des Dateispeichertyps mithilfe von bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md).  
  
#### <a name="example-of-importing-a-numeric-value-that-uses-scientific-notation"></a>Beispiel: Importieren eines numerischen Werts in wissenschaftlicher Schreibweise  
 In diesem Beispiel wird die folgende Tabelle verwendet:  
  
```  
CREATE TABLE t_float(c1 float, c2 decimal (5,4));  
```  
  
 Der Benutzer möchte nun per Massenimport Daten in die `t_float`-Tabelle kopieren. Die Datendatei „C:\t_float-c.dat“ enthält **float**-Daten in wissenschaftlicher Schreibweise, wie zum Beispiel:  
  
```  
8.0000000000000002E-28.0000000000000002E-2  
```  
  
 Diese Daten können jedoch mithilfe von BULK INSERT nicht direkt in die `t_float`-Tabelle importiert werden, da die zweite Spalte der Tabelle, `c2`, den `decimal`-Datentyp verwendet. Daher ist eine Formatdatei erforderlich. In der Formatdatei müssen die **float**-Daten in wissenschaftlichem Format dem Dezimalformat der Spalte `c2` zugeordnet werden.  
  
 Die folgende Formatdatei verwendet den `SQLFLT8`-Datentyp, um der zweiten Spalte das zweite Datenfeld zuzuordnen:  
  
 ```
 <?xml version="1.0"?> 
 <BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
 <RECORD> 
 <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="30"/> 
 <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="30"/>  </RECORD>  <ROW> 
 <COLUMN SOURCE="1" NAME="c1" xsi:type="SQLFLT8"/> 
 <COLUMN SOURCE="2" NAME="c2" xsi:type="SQLFLT8"/>  </ROW> </BCPFORMAT> 
 ```
  
 Geben Sie die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung aus, und verwenden Sie dabei für diese Formatdatei den Dateinamen `C:\t_floatformat-c-xml.xml`, damit die Testdaten in die Testtabelle importiert werden:  
  
```  
BULK INSERT bulktest..t_float  
FROM 'C:\t_float-c.dat' WITH (FORMATFILE='C:\t_floatformat-c-xml.xml');  
GO  
```  
  
### <a name="data-types-for-bulk-exporting-or-importing-sqlxml-documents"></a>Datentypen für den Massenexport bzw. -import von SQLXML-Dokumenten  
 Verwenden Sie in der Formatdatei einen der folgenden Datentypen für den Massenexport oder -import von SQLXML-Daten:  
  
|Datentyp|Wirkung|  
|---------------|------------|  
|SQLCHAR oder SQLVARCHAR|Die Daten werden in der Clientcodepage gesendet bzw. in der durch die Sortierung implizierten Codeseite. Damit wird dieselbe Wirkung erzielt wie mit der Angabe von DATAFILETYPE **='char'** ohne Formatdatei.|  
|SQLNCHAR oder SQLNVARCHAR|Die Daten werden im Unicode-Format gesendet. Damit wird dieselbe Wirkung erzielt wie mit der Angabe von DATAFILETYPE **= 'widechar'** ohne Formatdatei.|  
|SQLBINARY oder SQLVARBIN|Die Daten werden ohne Konvertierung gesendet.|  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Einen Vergleich der BULK INSERT-Anweisung, der INSERT ... SELECT \* FROM OPENROWSET(BULK...)-Anweisung und des **bcp**-Befehl finden Sie unter [Massenimport und -export von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md).  
  
 Informationen zum Vorbereiten von Daten für den Massenimport finden Sie unter [Vorbereiten von Daten für den Massenexport oder -import &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
 Die BULK INSERT-Anweisung kann innerhalb einer benutzerdefinierten Transaktion ausgeführt werden, um Daten in eine Tabelle oder eine Sicht zu importieren. Damit mehrere Übereinstimmungen für den Massenimport von Daten verwendet werden, kann in einer Transaktion optional die BATCHSIZE-Klausel in der BULK INSERT-Anweisung angegeben werden. Wenn ein Rollback für eine Transaktion mit mehreren Batches ausgeführt wird, wird für jeden Batch, der bei der Transaktion an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gesendet wurde, ein Rollback ausgeführt.  
  
## <a name="interoperability"></a>Interoperabilität  
  
### <a name="importing-data-from-a-csv-file"></a>Importieren von Daten aus einer CSV-Datei  
Ab [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1. unterstützt BULK INSERT das CSV-Format.  
Vor [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 wurden CSV-Dateien von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Massenimportvorgängen nicht unterstützt. In manchen Fällen kann jedoch eine CSV-Datei als Datendatei für einen Massenimport von Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet werden. Informationen zu den Anforderungen hinsichtlich des Imports von Daten aus einer CSV-Datendatei finden Sie unter [Vorbereiten von Daten für den Massenexport oder -import &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
## <a name="logging-behavior"></a>Protokollierungsverhalten  
 Informationen dazu, wann Zeileneinfügevorgänge, die durch den Massenimport ausgeführt werden, im Transaktionsprotokoll protokolliert werden, finden Sie unter [Voraussetzungen für die minimale Protokollierung beim Massenimport](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
##  <a name="Limitations"></a> Einschränkungen  
 Bei Verwendung einer Formatdatei mit BULK INSERT können maximal 1024 Felder angegeben werden. Dieser Höchstwert entspricht der maximalen Zahl zulässiger Spalten in einer Tabelle. Wenn Sie BULK INSERT mit einer Datendatei verwenden, in der mehr als 1024 Felder enthalten sind, generiert BULK INSERT den Fehler 4822. Das [bcp-Hilfsprogramm](../../tools/bcp-utility.md) unterliegt dieser Einschränkung nicht. Verwenden Sie deshalb für Datendateien mit mehr als 1024 Feldern den **bcp**-Befehl.  
  
## <a name="performance-considerations"></a>Überlegungen zur Leistung  
 Wenn die Anzahl der in einem einzelnen Batch geleerten Seiten einen internen Schwellenwert überschreitet, könnte ein vollständiger Scan des Pufferpools ausgeführt werden, um die zu leerenden Seiten bei der Durchführung eines Commits für den Batch zu identifizieren. Dieser vollständige Scan kann sich negativ auf die Massenimportleistung auswirken. Die Überschreitung des internen Schwellenwerts ist wahrscheinlich, wenn ein großer Pufferpool mit einem langsamen E/A-Subsystem kombiniert wird. Um Pufferüberläufe auf großen Computern zu vermeiden, verwenden Sie entweder keinen TABLOCK-Hinweis (da dieser die Massenoptimierungen entfernt), oder verwenden Sie eine kleinere Batchgröße (die die Massenoptimierungen beibehält).  
  
 Da Computer unterschiedlich sind, wird empfohlen, verschiedene Batchgrößen mit den geladenen Daten zu testen, um die optimale Vorgehensweise zu bestimmen.  
  
## <a name="security"></a>Security  
  
### <a name="security-account-delegation-impersonation"></a>Delegierung von Sicherheitskonten (Identitätswechsel)  
 Wenn ein Benutzer einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldenamen verwendet, wird das Sicherheitsprofil des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozesskontos verwendet. Ein Anmeldename, für den die SQL Server-Authentifizierung verwendet wird, kann nicht außerhalb des Datenbankmoduls authentifiziert werden. Wenn ein BULK INSERT-Befehl durch einen Anmeldenamen initiiert wird, der die SQL Server-Authentifizierung verwendet, wird die Datenverbindung folglich mithilfe des Sicherheitskontexts des SQL Server-Prozesskontos (dem vom SQL Server-Datenbankmoduldienst verwendeten Konto) hergestellt. Um die Quelldaten lesen zu können, müssen Sie dem vom SQL Server-Datenbankmodul verwendeten Konto Zugriff auf die Quelldaten gewähren. Wenn sich ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Benutzer dagegen mithilfe der Windows-Authentifizierung anmeldet, kann der Benutzer nur diejenigen Dateien lesen, auf die vom Benutzerkonto zugegriffen werden kann. Das gilt unabhängig vom Sicherheitsprofil des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozesses.  
  
 Wenn die BULK INSERT-Anweisung mit **sqlcmd** oder **osql** auf einem Computer ausgeführt wird, um Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem zweiten Computer einzufügen, und *data_file* auf einem dritten Computer mithilfe eines UNC-Pfads angegeben wird, kann der Fehler 4861 ausgegeben werden.  
  
 Verwenden Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung, um diesen Fehler zu beheben, und geben Sie einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen an, der das Sicherheitsprofil des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozesskontos verwendet, oder konfigurieren Sie Windows so, dass die Delegierung von Sicherheitskonten aktiviert ist. Informationen zum Aktivieren der Delegierung für Benutzerkonten finden Sie in der Windows-Hilfe.  
  
 Weitere Informationen über diese und andere Überlegungen zur Sicherheit bei der Verwendung von BULK INSERT finden Sie unter [Importieren von Massendaten mithilfe von BULK INSERT oder OPENROWSET&#40;BULK...&#41; &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die Berechtigungen INSERT und ADMINISTER BULK OPERATIONS. In der Azure SQL-Datenbank sind INSERT- und ADMINISTER DATABASE BULK OPERATIONS-Berechtigungen erforderlich. Darüber hinaus ist die ALTER TABLE-Berechtigung erforderlich, wenn mindestens eine der folgenden Bedingungen zutrifft:  
  
-   Es sind Einschränkungen vorhanden, und die Option CHECK_CONSTRAINTS ist nicht angegeben.  
  
    > [!NOTE]  
    >  Die Deaktivierung von Einschränkungen wurde als Standardverhalten festgelegt. Verwenden Sie die Option CHECK_CONSTRAINTS, um Einschränkungen explizit zu überprüfen.  
  
-   Es sind Trigger vorhanden, und die Option FIRE_TRIGGER ist nicht angegeben.  
  
    > [!NOTE]  
    >  Standardmäßig werden Trigger nicht ausgelöst. Verwenden Sie die Option FIRE_TRIGGER, um Trigger explizit auszulösen.  
  
-   Importieren Sie Identitätswerte mithilfe der Option KEEPIDENTITY aus Datendateien.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-pipes-to-import-data-from-a-file"></a>A. Verwenden von |-Zeichen zum Importieren von Daten aus einer Datei  
 Im folgenden Beispiel werden Bestellinformationen aus der angegebenen Datendatei in die `AdventureWorks2012.Sales.SalesOrderDetail`-Tabelle importiert, wobei der senkrechte Strich (`|`) als Feldabschlusszeichen und `|\n` als Zeilenabschlusszeichen verwendet wird.  
  
```  
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail  
   FROM 'f:\orders\lineitem.tbl'  
   WITH   
      (  
         FIELDTERMINATOR =' |',  
         ROWTERMINATOR =' |\n'  
      );  
```  
  
### <a name="b-using-the-firetriggers-argument"></a>B. Verwenden des FIRE_TRIGGERS-Arguments  
 Im folgenden Beispiel wird das `FIRE_TRIGGERS`-Argument angegeben.  
  
```  
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail  
   FROM 'f:\orders\lineitem.tbl'  
   WITH  
     (  
        FIELDTERMINATOR =' |',  
        ROWTERMINATOR = ':\n',  
        FIRE_TRIGGERS  
      );  
```  
  
### <a name="c-using-line-feed-as-a-row-terminator"></a>C. Verwenden des Zeilenvorschubs als Zeilenabschlusszeichen  
 Im folgenden Beispiel wird eine Datei importiert, in der der Zeilenvorschub als ein Zeilenabschlusszeichen verwendet wird, z. B. eine UNIX-Ausgabe:  
  
```  
DECLARE @bulk_cmd varchar(1000);  
SET @bulk_cmd = 'BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail  
FROM ''<drive>:\<path>\<filename>''   
WITH (ROWTERMINATOR = '''+CHAR(10)+''')';  
EXEC(@bulk_cmd);  
```  
  
> [!NOTE]  
>  Abhängig davon, wie Textdateien von Microsoft Windows behandelt werden, wird **(\n** automatisch durch **\r\n)** ersetzt.  
  
### <a name="d-specifying-a-code-page"></a>D. Angeben einer Codepage  
 In den folgenden Beispielen wird veranschaulicht, wie eine Codepage angegeben wird.  
  
```  
BULK INSERT MyTable  
FROM 'D:\data.csv'  
WITH  
( CODEPAGE = '65001',  
    DATAFILETYPE = 'char',  
    FIELDTERMINATOR = ','  
);  
```  
### <a name="e-importing-data-from-a-csv-file"></a>E. Importieren von Daten aus einer CSV-Datei   
In den folgenden Beispielen wird veranschaulicht, wie eine CSV-Datei angegeben wird.   
```
BULK INSERT Sales.Invoices
FROM '\\share\invoices\inv-2016-07-25.csv'
WITH (FORMAT = 'CSV'); 
```

### <a name="f-importing-data-from-a-file-in-azure-blob-storage"></a>F. Importieren von Daten aus einer Datei in Azure Blob Storage   
Das folgende Beispiel zeigt, wie Daten aus einer CSV-Datei in einen Azure Blob-Speicherort geladen werden, welcher als externe Datenquelle konfiguriert wurde. Dies erfordert datenbankweit gültige Anmeldeinformationen, die SAS verwenden.    

```sql
BULK INSERT Sales.Invoices
FROM 'inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoices',
     FORMAT = 'CSV'); 
```

Vollständige `BULK INSERT`-Beispiele einschließlich der Konfiguration der Anmeldeinformation und externen Datenquelle finden Sie unter [Beispiele für Massenzugriff auf Daten in Azure Blob Storage](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).
  
### <a name="additional-examples"></a>Zusätzliche Beispiele  
 Weitere `BULK INSERT`-Beispiele finden Sie in den folgenden Themen:  
  
-   [Beispiele für den Massenimport und -export von XML-Dokumenten &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Beibehalten von Identitätswerten beim Massenimport von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Beibehalten von NULL-Werten oder Verwenden von Standardwerten während des Massenimports &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Angeben von Feld- und Zeilenabschlusszeichen &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
-   [Massenimport von Daten mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Verwenden des Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des nativen Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des Unicode-Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des nativen Unicode-Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Überspringen einer Tabellenspalte mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Verwenden einer Formatdatei zum Zuordnen von Tabellenspalten zu Datendateifeldern &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Massenimport und -export von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [bcp (Hilfsprogramm)](../../tools/bcp-utility.md)   
 [Formatdateien zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Vorbereiten von Daten für den Massenexport oder -import &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)   
 [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)  
  
  
