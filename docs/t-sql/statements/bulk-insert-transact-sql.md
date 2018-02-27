---
title: BULK INSERT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/04/2017
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: ec29eaa73339980516f4a3de4b67fa195953d80a
ms.sourcegitcommit: 7673ad0e84a6de69420e19247a59e39ca751a8aa
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/03/2018
---
# <a name="bulk-insert-transact-sql"></a>BULK INSERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Importiert eine Datendatei in eine Datenbanktabelle oder Sicht und verwendet dabei ein vom Benutzer angegebenes Format in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
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
 Der Name der Tabelle oder des Sichtschemas. *Schema_name* ist optional, wenn das Standardschema des Benutzers den Massenimportvorgang ausführt Schema der angegebenen Tabelle oder Sicht ist. Wenn *Schema* nicht angegeben wird und das Standardschema des Benutzers, der den Massenimportvorgang durchführen unterscheidet sich von der angegebenen Tabelle oder Sicht, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt eine Fehlermeldung angezeigt, und der Massenimportvorgang wird abgebrochen.  
  
 *table_name*  
 Der Name der Tabelle oder Sicht, in die der Massenimport von Daten erfolgen sollen. Es können nur Sichten verwendet werden, deren Spalten alle auf dieselbe Basistabelle verweisen. Weitere Informationen zu den Einschränkungen beim Laden von Daten in Sichten, finden Sie unter [INSERT &#40; Transact-SQL &#41; ](../../t-sql/statements/insert-transact-sql.md).  
  
 **"** *Data_file* **"**  
 Der vollständige Pfad der Datendatei mit den Daten, die in die angegebene Tabelle oder Sicht importiert werden sollen. BULK INSERT kann Daten von einem Datenträger importieren, einschließlich eines Netzwerks, einer Diskette, einer Festplatte usw.   
 
 *Data_file* muss einen gültigen Pfad auf dem Server angeben, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Wenn *Data_file* ist eine Datei, geben Sie den Namen (UNC = Universal Naming Convention). Ein UNC-Name weist folgendes Format \\ \\ *Systemname*\\*ShareName*\\*Pfad* \\ *FileName*. Beispiel: `\\SystemX\DiskZ\Sales\update.txt`.   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Beginnend mit [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP1.1, kann die Data_file im Azure-Blob-Speicher.

**"** *Data_source_name* **"**   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Eine benannte externe Datenquelle auf den Azure-Blob-Speicherort der Datei verweist, die importiert werden sollen. Die externen Datenquelle muss erstellt werden, mithilfe der `TYPE = BLOB_STORAGE` hinzugefügt, die Option [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP-Version 1.1. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).    
  
 BATCHSIZE  **=**  *Batch_size*  
 Gibt die Anzahl von Zeilen in einem Batch an. Jeder Batch wird als eine Transaktion auf den Server kopiert. Falls ein Fehler erzeugt wird, führt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die Transaktion jedes Batches ein Commit oder Rollback aus. In der Standardeinstellung werden alle Daten, die sich in der angegebenen Datendatei befinden, als ein Batch behandelt. Informationen zu Leistungsaspekten finden Sie unter "Hinweise" weiter unten in diesem Thema.  
  
 CHECK_CONSTRAINTS  
 Gibt an, dass alle Einschränkungen, die für die Zieltabelle oder -sicht gelten, während des Massenimportvorgangs überprüft werden müssen. Ohne die Option CHECK_CONSTRAINTS werden alle CHECK- und FOREIGN KEY-Einschränkungen ignoriert, und nach Abschluss des Vorgangs wird die Einschränkung in der Tabelle als nicht vertrauenswürdig gekennzeichnet.  
  
> [!NOTE]  
>  Unique- und PRIMARY KEY-Einschränkungen werden immer erzwungen. Beim Importieren in eine Zeichenspalte, die mit einer NOT NULL-Einschränkung definiert ist, fügt BULK INSERT eine leere Zeichenfolge ein, wenn die Textdatei keinen Wert enthält.  
  
 An gewissen Punkten müssen Sie die Einschränkungen in der gesamten Tabelle überprüfen. Wenn die Tabelle vor dem Massenimportvorgang nicht leer war, kann der Aufwand einer erneuten Überprüfung der Einschränkung höher sein als das Anwenden von CHECK-Einschränkungen auf die inkrementellen Daten.  
  
 Die Deaktivierung von Einschränkungen (das Standardverhalten) kann z. B. erwünscht sein, wenn die Eingabedaten Zeilen enthalten, die Einschränkungen verletzen. Wenn CHECK-Einschränkungen deaktiviert sind, können Sie die Daten importieren und dann [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen verwenden, um die ungültigen Daten zu entfernen.  
  
> [!NOTE]  
>  Die Option MAXERRORS kann zur Einschränkungsüberprüfung nicht verwendet werden.  
  
 CODEPAGE  **=**  { **"**ACP**"** | **"**OEM**"**  |  **"**RAW**"** | **"***Codepage***"** }  
 Gibt die Codepage für die in der Datendatei enthaltenen Daten an. CODEPAGE ist nur relevant, wenn die Daten enthält **Char**, **Varchar**, oder **Text** -Spalten mit Zeichenwerten enthalten, die größer als **127** oder weniger als **32**.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)]empfiehlt, dass Sie für jede Spalte einen Sortierungsnamen angeben einer [Formatdatei](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).  
  
|CODEPAGE-Wert|Description|  
|--------------------|-----------------|  
|ACP|Spalten des **Char**, **Varchar**, oder **Text** -Datentyp konvertiert werden, aus der [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)] / [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Codepage (ISO 1252) an den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Codepage.|  
|OEM (Standard)|Spalten des **Char**, **Varchar**, oder **Text** -Datentyp konvertiert werden, von dem System OEM-Codepage in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Codepage.|  
|RAW|Dies ist die schnellste Option, da keine Konvertierung von einer Codepage in eine andere erfolgt.|  
|*Codepage*|Bestimmte Codepagenummer, z. B. 850.<br /><br /> **\*\*Wichtige \* \***  Versionen vor [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Codepage 65001 (UTF-8-Codierung) nicht unterstützt.|  
  
 DATAFILETYPE  **=**  { **'Char'** | **'native'** | **'Widechar'**  |  **"widenative"** }  
 Gibt an, dass BULK INSERT den Importvorgang mithilfe des angegebenen DATAFILETYPE-Werts ausführt.  
  
|DATAFILETYPE-Wert|Alle Daten, die dargestellt sind in:|  
|------------------------|------------------------------|  
|**Char** (Standard)|Zeichenformat.<br /><br /> Weitere Informationen finden Sie unter [Verwenden des Zeichenformats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md).|  
|**systemeigene**|Systemeigene (Datenbank-) Datentypen. Erstellen Sie die systemeigene Datendatei durch das massenimportieren von Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe der **Bcp** Hilfsprogramm.<br /><br /> Der Wert native bietet eine höhere Leistung als der Wert char.<br /><br /> Weitere Informationen finden Sie unter [Verwenden des nativen Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md).|  
|**widechar**|Unicode-Zeichen<br /><br /> Weitere Informationen finden Sie unter [Verwenden des Unicode-Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md).|  
|**widenative**|Systemeigene (Datenbank-) Datentypen, außer bei **Char**, **Varchar**, und **Text** Spalten, in dem Daten im Unicode-Format gespeichert werden. Erstellen der **widenative** Datendatei durch das massenimportieren von Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe der **Bcp** Hilfsprogramm.<br /><br /> Die **widenative** Wert bietet ein besseres Leistungsverhalten als **Widechar**. Wenn die Datendatei enthält [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)] Geben Sie die Sonderzeichen, **widenative**.<br /><br /> Weitere Informationen finden Sie unter [Verwenden des nativen Unicode-Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md).|  
  
  ERRORFILE **= "***File_name***"**  
 Gibt die Datei an, die zum Sammeln der Zeilen verwendet wird, die Formatierungsfehler enthalten und nicht in ein OLE DB-Rowset konvertiert werden können. Diese Zeilen werden aus der Datendatei unverändert in diese Fehlerdatei kopiert.  
  
 Die Fehlerdatei wird bei Ausführung des Befehls erstellt. Falls die Datei bereits vorhanden ist, tritt ein Fehler auf. Darüber hinaus wird eine Kontrolldatei mit der Erweiterung .ERROR.txt erstellt. Diese Datei enthält einen Verweis auf jede Zeile in der Fehlerdatei und stellt eine Fehlerdiagnose bereit. Sobald der Fehler korrigiert wurden, können die Daten geladen werden.   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
Beginnend mit [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], die `error_file_path` im Azure-Blob-Speicher werden können.

"Errorfile_data_source_name"   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
Eine benannte externe Datenquelle auf den Azure-Blob-Speicherort der Fehlerdatei verweist, die während des Imports gefundenen Fehler enthält. Die externen Datenquelle muss erstellt werden, mithilfe der `TYPE = BLOB_STORAGE` hinzugefügt, die Option [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP-Version 1.1. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).
 
 FIRSTROW  **=**  *erste_zeile*  
 Gibt die Nummer der ersten zu ladenden Zeile an. In der Standardeinstellung ist dies die erste Zeile in der angegebenen Datendatei. FIRSTROW ist einsbasiert.  
  
> [!NOTE]  
>  Es ist nicht vorgesehen, dass das FIRSTROW-Attribut Spaltenheader überspringt. Header zu überspringen wird von der BULK INSERT-Anweisung nicht unterstützt. Wenn Zeilen ausgelassen werden, werden von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] nur die Feldabschlusszeichen berücksichtigt und die Daten in den Feldern von ausgelassenen Zeilen nicht überprüft.  
  
 FIRE_TRIGGERS  
 Gibt an, dass INSERT-Trigger, die für die Zieltabelle definiert sind, während des Massenimportvorgangs ausgeführt werden. Falls Trigger für INSERT-Vorgänge in der Zieltabelle definiert sind, werden sie für jeden abgeschlossenen Batch ausgelöst.  
  
 Wenn FIRE_TRIGGERS nicht angegeben ist, werden keine INSERT-Trigger ausgeführt.  

FORMATFILE_DATASOURCE  **=**  "Data_source_name"   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1.   
Eine benannte externe Datenquelle auf den Azure-Blob-Speicherort der Formatdatei verweist, die das Schema der importierten Daten definieren. Die externen Datenquelle muss erstellt werden, mithilfe der `TYPE = BLOB_STORAGE` hinzugefügt, die Option [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP-Version 1.1. Weitere Informationen finden Sie unter [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).
  
 KEEPIDENTITY  
 Gibt an, dass der oder die Identitätswerte in der importierten Datendatei für die Identitätsspalte verwendet werden sollen. Wird KEEPIDENTITY nicht angegeben, werden die Identitätswerte für diese Spalte zwar überprüft, jedoch nicht importiert. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] weist dann auf der Basis von Ausgangswerten und inkrementellen Werten, die beim Erstellen der Tabelle angegeben wurden, eindeutige Werte zu. Enthält die Datendatei keine Werte für die Identitätsspalte in der Tabelle oder Sicht, nicht mit einer Formatdatei angeben, dass die Identity-Spalte in der Tabelle oder Sicht beim Importieren von Daten ausgelassen werden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] weist automatisch eindeutige Werte für die Spalte. Weitere Informationen finden Sie unter [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md).  
  
 Weitere Informationen zum beibehalten Identitätswerten finden Sie unter Identifizieren [behalten Identität Werte beim Massenimport von Daten &#40; SQLServer &#41; ](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md).  
  
 KEEPNULLS  
 Gibt an, dass in leere Spalten während des Massenimportvorgangs keine Standardwerte eingefügt, sondern ein NULL-Wert für diese Spalten beibehalten werden soll. Weitere Informationen finden Sie unter [Beibehalten von NULL-Werten oder Verwenden von Standardwerten während des Massenimports &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md).  
  
 KILOBYTES_PER_BATCH  **=**  *Kilobytes_per_batch*  
 Gibt die ungefähre Anzahl der Kilobytes (KB) an Daten pro Batch als *Kilobytes_per_batch*. In der Standardeinstellung ist KILOBYTES_PER_BATCH unbekannt. Informationen zu Leistungsaspekten finden Sie unter "Hinweise" weiter unten in diesem Thema.  
  
 LASTROW**=***letzte_zeile*  
 Gibt die Nummer der letzten zu ladenden Zeile an. Der Standardwert ist 0, wodurch die Daten bis zur letzten Zeile in der angegebenen Datendatei geladen werden.  
  
 MAXERRORS  **=**  *max_fehler*  
 Gibt die maximale Anzahl von Syntaxfehlern an, die in den Daten zulässig sind, bevor der Massenimportvorgang abgebrochen wird. Jede Zeile, die beim Massenimportvorgang nicht importiert werden kann, wird ignoriert und zählt dabei als ein Fehler. Wenn *max_fehler* nicht angegeben ist, wird der Standard ist 10.  
  
> [!NOTE]  
>  Die Option MAX_ERRORS gilt nicht zur einschränkungsüberprüfung oder zum Konvertieren **Money** und **"bigint"** -Datentypen.  
  
 Reihenfolge ({ *Spalte* [ASC | "DESC"]} [ **,**... *n* ] )  
 Gibt die Vorgehensweise beim Sortieren der Daten in der Datendatei an. Die Leistung des Massenkopierens wird verbessert, wenn die zu importierenden Daten entsprechend dem gruppierten Index der Tabelle (falls vorhanden) sortiert sind. Wenn die Datendatei in einer anderen Reihenfolge sortiert wird, die von der Reihenfolge eines Schlüssels des gruppierten Indexes abweicht, oder die Tabelle keinen gruppierten Index hat, wird die ORDER-Klausel ignoriert. Die angegebenen Spaltennamen müssen gültige Spaltennamen in der Zieltabelle sein. Standardmäßig geht der Masseneinfügevorgang davon aus, dass die Datendatei nicht sortiert ist. Beim optimierten Massenimport wird in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auch überprüft, ob die importierten Daten sortiert sind.  
  
 *n*  
 Ein Platzhalter, der anzeigt, dass mehrere Spalten angegeben werden können.  
  
 ROWS_PER_BATCH  **=**  *Rows_per_batch*  
 Gibt die ungefähre Anzahl von Zeilen mit Daten in der Datendatei an.  
  
 Standardmäßig werden alle Daten in der Datendatei als einzelne Transaktion an den Server gesendet, und die Anzahl von Zeilen im Batch ist dem Abfrageoptimierer nicht bekannt. Wenn Sie ROWS_PER_BATCH (mit einem Wert > 0) angeben, verwendet der Server diesen Wert, um den Massenimportvorgang zu optimieren. Der für ROWS_PER_BATCH angegebene Wert sollte etwa der tatsächlichen Zeilenanzahl entsprechen. Informationen zu Leistungsaspekten finden Sie unter "Hinweise" weiter unten in diesem Thema.  
  
 
 TABLOCK  
 Gibt an, dass eine Sperre auf Tabellenebene für die Dauer des Massenimportvorgangs aktiviert wird. Eine Tabelle kann gleichzeitig von mehreren Clients geladen werden, wenn die Tabelle keine Indizes aufweist und TABLOCK angegeben ist. Standardmäßig wird das Sperrverhalten durch die Tabellenoption **table lock on bulk load**bestimmt. Da weniger Sperrkonflikte in der Tabelle auftreten, wenn diese während des Massenimportvorgangs gesperrt wird, verbessert sich in manchen Fällen die Leistung erheblich. Informationen zu Leistungsaspekten finden Sie unter "Hinweise" weiter unten in diesem Thema.  
  
 Für columnstore-Index. Das Sperre Verhalten ist anders, weil er intern in mehrere Rowsets unterteilt ist.  Jeder Thread lädt Daten ausschließlich in jedes Rowset, ergreifen Sie hierzu eine X-Sperre für das Rowset Paralleles Laden von Daten mit gleichzeitiger-Load-Sitzungen zu ermöglichen. Die Verwendung von TABLOCK-Option bewirkt, dass Threads für eine X-Sperre für die Tabelle (im Gegensatz zu BU-Sperre für herkömmliche Rowsets) annehmen und somit die verhindert, andere gleichzeitige Threads dass um gleichzeitig Daten zu laden.  

### <a name="input-file-format-options"></a>Format der Eingabedatei (Optionen)
  
FORMAT  **=**  "CSV"   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Gibt eine Datei mit kommagetrennten Werten kompatibel ist die [RFC 4180](https://tools.ietf.org/html/rfc4180) standard.

FIELDQUOTE  **=**  "Field_quote"   
**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Gibt ein Zeichen, das als das Anführungszeichen in CSV-Datei verwendet wird. Wenn nicht angegeben, das Anführungszeichen (") verwendet werden als das Angebot Zeichen gemäß der [RFC 4180](https://tools.ietf.org/html/rfc4180) standard.
  
 FORMATFILE **= "***Format_file_path***"**  
 Gibt den vollständigen Pfad einer Formatdatei an. Eine Formatdatei beschreibt die Datendatei, die gespeicherte Antworten mit enthält die **Bcp** Utility auf die gleiche Tabelle oder Sicht. Die Formatdatei muss verwendet werden, wenn Folgendes zutrifft:  
  
-   Die Datendatei enthält größere oder weniger Spalten als die Tabelle oder Sicht.  
  
-   Die Spalten befinden sich in einer unterschiedlichen Reihenfolge.  
  
-   Die Spaltentrennzeichen variieren.  
  
-   Es liegen andere Änderungen im Datenformat vor. Formatdateien sind in der Regel erstellt, mit der **Bcp** Utility und mit einem Text-Editor nach Bedarf geändert. Weitere Informationen finden Sie unter [bcp Utility](../../tools/bcp-utility.md).  

**Gilt für:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Beginnend mit [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP-Version 1.1, kann die Format_file_path im Azure-Blob-Speicher.

 FIELDTERMINATOR **='***Feldabschlusszeichen***'**  
 Gibt das Feldabschlusszeichen für zu verwendende **Char** und **Widechar** Datendateien. Standardmäßig wird \t (Tabstoppzeichen) als Feldabschlusszeichen verwendet. Weitere Informationen finden Sie unter [Angeben von Feld- und Zeilenabschlusszeichen &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  

 ROWTERMINATOR **='***Zeilenabschlusszeichen***'**  
 Gibt das Zeilenabschlusszeichen für zu verwendende **Char** und **Widechar** Datendateien. Das standardmäßige Zeilenabschlusszeichen ist **\r\n** (neue Zeilenumbruchzeichen).  Weitere Informationen finden Sie unter [Angeben von Feld- und Zeilenabschlusszeichen &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  

  
## <a name="compatibility"></a>Kompatibilität  
 BULK INSERT erzwingt strenge Datenüberprüfungen für die aus einer Datei gelesenen Daten, die möglicherweise zum Fehlschlagen vorhandener Skripts führen können, wenn diese für ungültige Daten in einer Datendatei ausgeführt werden. BULK INSERT überprüft beispielsweise Folgendes:  
  
-   Die einheitliche Darstellung der **"float"** oder **echte** Datentypen sind gültig.  
  
-   Unicode-Daten besitzen eine gerade Bytelänge.  
  
## <a name="data-types"></a>Datentypen  
  
### <a name="string-to-decimal-data-type-conversions"></a>Konvertierungen von Zeichenfolgen- in Dezimaldatentypen  
 Die Zeichenfolge-Dezimal-datentypkonvertierungen, die in BULK INSERT verwendet, gelten dieselben Regeln wie die [!INCLUDE[tsql](../../includes/tsql-md.md)] [konvertieren](../../t-sql/functions/cast-and-convert-transact-sql.md) -Funktion, die Zeichenfolgen mit numerische Werten, die wissenschaftliche Schreibweise verwenden. Daher behandelt BULK INSERT diese Zeichenfolgen als ungültige Werte und meldet Konvertierungsfehler.  
  
 Um dieses Verhalten zu umgehen, Sie mithilfe einer Formatdatei zum Massenladen von Import wissenschaftliche Schreibweise **"float"** Daten in Spalten im Dezimalformat. In der Formatdatei beschreiben Sie explizit die Spalte als **echte** oder **"float"** Daten. Weitere Informationen zu diesen Datentypen finden Sie unter [Float und Real &#40; Transact-SQL &#41; ](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
> [!NOTE]  
>  Formatdateien stellen **echte** Daten als die **SQLFLT4** -Datentyp und **"float"** Daten als die **SQLFLT8** -Datentyp. Informationen zu nicht-XML-Formatdateien finden Sie unter [Dateispeichertyp angeben, mithilfe von Bcp &#40; SQLServer &#41; ](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md).  
  
#### <a name="example-of-importing-a-numeric-value-that-uses-scientific-notation"></a>Beispiel: Importieren eines numerischen Werts in wissenschaftlicher Schreibweise  
 In diesem Beispiel wird die folgende Tabelle verwendet:  
  
```  
CREATE TABLE t_float(c1 float, c2 decimal (5,4));  
```  
  
 Der Benutzer möchte nun per Massenimport Daten in die `t_float`-Tabelle kopieren. Die Datendatei C:\t_float-c.dat enthält wissenschaftliche Schreibweise **"float"** Daten, z. B.:  
  
```  
8.0000000000000002E-28.0000000000000002E-2  
```  
  
 Diese Daten können jedoch mithilfe von BULK INSERT nicht direkt in die `t_float`-Tabelle importiert werden, da die zweite Spalte der Tabelle, `c2`, den `decimal`-Datentyp verwendet. Daher ist eine Formatdatei erforderlich. Die Formatdatei muss die wissenschaftliche Schreibweise zuordnen **"float"** Daten an das Dezimalformat der Spalte `c2`.  
  
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
|SQLCHAR oder SQLVARCHAR|Die Daten werden in der Clientcodepage gesendet bzw. in der durch die Sortierung implizierten Codeseite. Der Effekt ist derselbe, als wenn DATAFILETYPE **= "Char"** ohne eine Formatdatei angegeben.|  
|SQLNCHAR oder SQLNVARCHAR|Die Daten werden im Unicode-Format gesendet. Der Effekt ist derselbe, als wenn DATAFILETYPE **= 'Widechar'** ohne eine Formatdatei angegeben.|  
|SQLBINARY oder SQLVARBIN|Die Daten werden ohne Konvertierung gesendet.|  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Einen Vergleich der BULK INSERT-Anweisung, der INSERT ... SELECT \* FROM OPENROWSET(Bulk...)-Anweisung und dem **Bcp** Befehl, finden Sie unter [Massenimport und-Export von Daten &#40; SQLServer &#41; ](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md).  
  
 Informationen zur Vorbereitung der Daten für den Massenimport finden Sie unter [Vorbereiten von Daten für den Massenexport oder-Import &#40; SQLServer &#41; ](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
 Die BULK INSERT-Anweisung kann innerhalb einer benutzerdefinierten Transaktion ausgeführt werden, um Daten in eine Tabelle oder eine Sicht zu importieren. Damit mehrere Übereinstimmungen für den Massenimport von Daten verwendet werden, kann in einer Transaktion optional die BATCHSIZE-Klausel in der BULK INSERT-Anweisung angegeben werden. Wenn ein Rollback für eine Transaktion mit mehreren Batches ausgeführt wird, wird für jeden Batch, der bei der Transaktion an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gesendet wurde, ein Rollback ausgeführt.  
  
## <a name="interoperability"></a>Interoperabilität  
  
### <a name="importing-data-from-a-csv-file"></a>Importieren von Daten aus einer CSV-Datei  
Beginnend mit [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP-Version 1.1, BULK INSERT unterstützt das CSV-Format.  
Vor dem [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP-Version 1.1, durch Trennzeichen getrennte Werten (CSV)-Dateien können nicht von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Massenimportvorgängen. In manchen Fällen kann jedoch eine CSV-Datei als Datendatei für einen Massenimport von Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet werden. Informationen zu den Anforderungen für das Importieren von Daten aus einer CSV-Datendatei finden Sie unter [Vorbereiten von Daten für den Massenexport oder-Import &#40; SQLServer &#41; ](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
## <a name="logging-behavior"></a>Protokollierungsverhalten  
 Informationen dazu, wann Zeileneinfügevorgänge, die durch den Massenimport ausgeführt werden, im Transaktionsprotokoll protokolliert werden, finden Sie unter [Voraussetzungen für die minimale Protokollierung beim Massenimport](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
##  <a name="Limitations"></a> Einschränkungen  
 Bei Verwendung einer Formatdatei mit BULK INSERT können maximal 1024 Felder angegeben werden. Dieser Höchstwert entspricht der maximalen Zahl zulässiger Spalten in einer Tabelle. Wenn Sie BULK INSERT mit einer Datendatei verwenden, in der mehr als 1024 Felder enthalten sind, generiert BULK INSERT den Fehler 4822. Die [Hilfsprogramm "Bcp"](../../tools/bcp-utility.md) nicht unterliegt dieser Einschränkung, verwenden Sie daher für Datendateien, die mehr als 1024 Felder enthalten, die **Bcp** Befehl.  
  
## <a name="performance-considerations"></a>Überlegungen zur Leistung  
 Wenn die Anzahl der in einem einzelnen Batch geleerten Seiten einen internen Schwellenwert überschreitet, könnte ein vollständiger Scan des Pufferpools ausgeführt werden, um die zu leerenden Seiten bei der Durchführung eines Commits für den Batch zu identifizieren. Dieser vollständige Scan kann sich negativ auf die Massenimportleistung auswirken. Die Überschreitung des internen Schwellenwerts ist wahrscheinlich, wenn ein großer Pufferpool mit einem langsamen E/A-Subsystem kombiniert wird. Um Pufferüberläufe auf großen Computern zu vermeiden, verwenden Sie entweder keinen TABLOCK-Hinweis (da dieser die Massenoptimierungen entfernt), oder verwenden Sie eine kleinere Batchgröße (die die Massenoptimierungen beibehält).  
  
 Da Computer unterschiedlich sind, wird empfohlen, verschiedene Batchgrößen mit den geladenen Daten zu testen, um die optimale Vorgehensweise zu bestimmen.  
  
## <a name="security"></a>Security  
  
### <a name="security-account-delegation-impersonation"></a>Delegierung von Sicherheitskonten (Identitätswechsel)  
 Wenn ein Benutzer einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldenamen verwendet, wird das Sicherheitsprofil des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozesskontos verwendet. Ein Anmeldename, für den die SQL Server-Authentifizierung verwendet wird, kann nicht außerhalb des Datenbankmoduls authentifiziert werden. Wenn ein BULK INSERT-Befehl durch einen Anmeldenamen initiiert wird, der die SQL Server-Authentifizierung verwendet, wird die Datenverbindung folglich mithilfe des Sicherheitskontexts des SQL Server-Prozesskontos (dem vom SQL Server-Datenbankmoduldienst verwendeten Konto) hergestellt. Um die Quelldaten lesen zu können, müssen Sie dem vom SQL Server-Datenbankmodul verwendeten Konto Zugriff auf die Quelldaten gewähren. Wenn sich ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Benutzer dagegen mithilfe der Windows-Authentifizierung anmeldet, kann der Benutzer nur diejenigen Dateien lesen, auf die vom Benutzerkonto zugegriffen werden kann. Das gilt unabhängig vom Sicherheitsprofil des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozesses.  
  
 Beim Ausführen der BULK INSERT-Anweisung mit **Sqlcmd** oder **Osql**, von einem Computer Einfügen von Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem zweiten Computer und Angeben einer *Data_file* auf dritten Computer über einen UNC-Pfad möglicherweise Fehler 4861 ausgegeben.  
  
 Verwenden Sie zum Beheben dieses Fehlers [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung, und geben Sie eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung, die das Sicherheitsprofil des verwendet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Prozesskonto, oder konfigurieren Sie Windows so, dass Delegierung von Sicherheitskonten aktiviert. Informationen zum Aktivieren der Delegierung für Benutzerkonten finden Sie in der Windows-Hilfe.  
  
 Weitere Informationen zu diesen und anderen Sicherheitsaspekten bezüglich mithilfe von BULK INSERT finden Sie unter [Importieren von Massendaten durch Verwenden von BULK INSERT oder OPENROWSET &#40; BULK... &#41; &#40; SQLServer &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die Berechtigungen INSERT und ADMINISTER BULK OPERATIONS. In Azure SQL-Datenbank sind INSERT und ADMINISTER Datenbank BULK OPERATIONS-Berechtigungen erforderlich. Darüber hinaus ist die ALTER TABLE-Berechtigung erforderlich, wenn mindestens eine der folgenden Bedingungen zutrifft:  
  
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
>  Aufgrund von wie Textdateien von Microsoft Windows behandelt **(\n** automatisch durch ersetzt ruft **\r\n)**.  
  
### <a name="d-specifying-a-code-page"></a>D. Angeben einer Codepage  
 Im folgenden Beispiel wird gezeigt, wie eine Codepage an.  
  
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
Im folgenden Beispiel wird gezeigt, wie eine CSV-Datei angeben.   
```
BULK INSERT Sales.Invoices
FROM '\\share\invoices\inv-2016-07-25.csv'
WITH (FORMAT = 'CSV'); 
```

### <a name="f-importing-data-from-a-file-in-azure-blob-storage"></a>F. Importieren von Daten aus einer Datei im Azure-Blob-Speicher   
Das folgende Beispiel zeigt, wie zum Laden von Daten aus einer Csv-Datei in einen Azure-Blob-Speicherort, die als externe Datenquelle konfiguriert wurde. Dies erfordert eine datenbankweite Anmeldeinformationen mithilfe einer SAS.    

```sql
BULK INSERT Sales.Invoices
FROM 'inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoices',
     FORMAT = 'CSV'); 
```

Führen Sie für `BULK INSERT` Konfigurieren der Anmeldeinformationen und die externe Datenquelle, einschließlich Beispielen finden Sie unter [Beispiele von Bulk Zugriff auf Daten in Azure Blob-Speicher](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).
  
### <a name="additional-examples"></a>Zusätzliche Beispiele  
 Andere `BULK INSERT` Beispiele in den folgenden Themen:  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [Massenimport und -export von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [bcp (Hilfsprogramm)](../../tools/bcp-utility.md)   
 [Formatdateien zum Importieren oder Exportieren von Daten &#40; SQLServer &#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Vorbereiten von Daten für den Massenexport oder-Import &#40; SQLServer &#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)   
 [Sp_tableoption &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)  
  
  
