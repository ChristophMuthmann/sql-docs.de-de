---
title: CREATE EXTERNAL FILE FORMAT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 2/20/2018
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL FILE FORMAT
- CREATE_EXTERNAL_FILE_FORMAT
dev_langs:
- TSQL
helpviewer_keywords:
- External
- External, file format
- PolyBase, external file format
ms.assetid: abd5ec8c-1a0e-4d38-a374-8ce3401bc60c
caps.latest.revision: 25
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 790c3bdce51c2359a9cc34aad4a51b4b2f199fd1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-external-file-format-transact-sql"></a>CREATE EXTERNAL FILE FORMAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Erstellt ein Objekt im externen Dateiformat und definiert dabei externe Daten, die in Hadoop, Azure Blob Storage oder Azure Data Lake Store gespeichert sind. Das Erstellen eines externen Dateiformats ist eine Voraussetzung für die Erstellung einer externen Tabelle. Durch das Erstellen eines externen Dateiformats geben Sie das tatsächliche Layout der Daten an, auf die von einer externen Tabelle verwiesen wird.  
  
 PolyBase unterstützt die folgenden Dateiformate:
  
-   Durch Trennzeichen getrennter Text  
  
-   Hive RCFile  
  
-   Hive ORC
  
-   Parquet  
  
Informationen zur Erstellung einer externen Tabelle finden Sie unter [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md).
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax
  
```
-- Create an external file format for PARQUET files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = PARQUET  
     [ , DATA_COMPRESSION = {  
        'org.apache.hadoop.io.compress.SnappyCodec'  
      | 'org.apache.hadoop.io.compress.GzipCodec'      }  
    ]);  
  
--Create an external file format for ORC files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = ORC  
     [ , DATA_COMPRESSION = {  
        'org.apache.hadoop.io.compress.SnappyCodec'  
      | 'org.apache.hadoop.io.compress.DefaultCodec'      }  
    ]);  
  
--Create an external file format for RCFILE.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = {  
        'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'  
      | 'org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe'  
    }  
    [ , DATA_COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec' ]);  
  
--Create an external file format for DELIMITED TEXT files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT  
    [ , FORMAT_OPTIONS ( <format_options> [ ,...n  ] ) ]  
    [ , DATA_COMPRESSION = {  
           'org.apache.hadoop.io.compress.GzipCodec'  
         | 'org.apache.hadoop.io.compress.DefaultCodec'  
        }  
     ]);  
  
<format_options> ::=  
{  
    FIELD_TERMINATOR = field_terminator  
    | STRING_DELIMITER = string_delimiter 
    | First_Row = integer -- ONLY AVAILABLE SQL DW
    | DATE_FORMAT = datetime_format  
    | USE_TYPE_DEFAULT = { TRUE | FALSE } 
    | Encoding = {'UTF8' | 'UTF16'} 
}  
```  
  
## <a name="arguments"></a>Argumente  
 *file_format_name*  
 Gibt einen Namen für das externe Dateiformat an.
  
 FORMAT_TYPE = [ PARQUET | ORC | RCFILE | PARQUET] Gibt das Format der externen Daten an.
  
   -   PARQUET Gibt ein Parquet-Format an.
  
   -   ORC  
   Gibt ein ORC-Format (ORC = Optimized Row Columnar) an. Für diese Option ist auf dem externen Hadoop-Cluster Hive Version 0.11 oder höher erforderlich. In Hadoop bietet das ORC-Dateiformat eine bessere Komprimierung und Leistung als das RCFILE-Dateiformat.

   -   RCFILE (in Kombination mit SERDE_METHOD = *SERDE_method*) Gibt ein RcFile-Format (RcFile = Record Columnar file) an. Für diese Option müssen Sie eine Hive Serializer- und Hive Deserializer-Methode (SerDe) angeben. Diese Anforderung ist auch gegeben, wenn Sie in Hadoop Hive/HiveQL zum Abfragen von RC-Dateien verwenden. Beachten Sie, dass bei der SerDe-Methode die Groß-/Kleinschreibung beachtet werden muss.

   Beispiele für die Angabe von RCFile mit den zwei von PolyBase unterstützten SerDe-Methoden.

    -   FORMAT_TYPE = RCFILE, SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'

    -   FORMAT_TYPE = RCFILE, SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe'

   -   DELIMITEDTEXT Gibt ein Textformat mit Spaltentrennzeichen (auch als Feldabschlusszeichen bekannt) an.
  
 FIELD_TERMINATOR = *field_terminator*  
Gilt nur für durch Trennzeichen getrennte Textdateien. Das Feldabschlusszeichen gibt mindestens ein Zeichen an, welches das Ende der einzelnen Felder (Spalten) in der durch Trennzeichen getrennten Textdatei markiert. Als Standardzeichen wird der senkrechte Strich „|“ verwendet. Für eine garantierte Unterstützung wird empfohlen, mehrere ASCII-Zeichen zu verwenden.
  
  
 Beispiele:  
  
-   FIELD_TERMINATOR = '|'  
  
-   FIELD_TERMINATOR = ' '  
  
-   FIELD_TERMINATOR = ꞌ\tꞌ  
  
-   FIELD_TERMINATOR = '~|~'  
  
 STRING_DELIMITER = *string_delimiter*  
Gibt das Feldabschlusszeichen für Daten der Typzeichenfolge in der durch Trennzeichen getrennten Textdatei an. Das Zeichenfolgen-Trennzeichen umfasst mindestens ein Zeichen und ist in einfache Anführungszeichen gesetzt. Der Standardwert ist die leere Zeichenfolge „“. Für eine garantierte Unterstützung wird empfohlen, mehrere ASCII-Zeichen zu verwenden.
 
  
 Beispiele:  

-   STRING_DELIMITER = '"'

-   STRING_DELIMITER = '0x22' -- Double quote hex
  
-   STRING_DELIMITER = '*'  
  
-   STRING_DELIMITER = ꞌ,ꞌ  
  
-   STRING_DELIMITER = '0x7E0x7E'  -- Zwei Tilden (z.B. ~~)
 
 FIRST_ROW = *First_row_int*  
Gibt die Zeilenzahl an, die während eines PolyBase-Ladevorgangs in allen Dateien zuerst gelesen wird. Dieser Parameter kann Werte von 1 bis 15 umfassen. Wenn der Wert auf 2 festgelegt ist, wird die erste Zeile in jeder Datei (Kopfzeile) beim Laden der Daten übersprungen. Zeilen werden basierend auf dem Vorhandensein von Zeilenabschlusszeichen (/ r/n, r, /n) übersprungen. Wenn diese Option für den Export verwendet wird, werden Zeilen zu den Daten hinzugefügt, um sicherzustellen, dass die Datei ohne Datenverlust gelesen werden kann. Wenn der Wert auf >2 festgelegt wird, enthält die erste exportierte Zeile die Spaltennamen der externen Tabelle.

 DATE\_FORMAT = *datetime_format*  
Gibt ein benutzerdefiniertes Format für alle Datums- und Zeitdaten an, die in einer durch Trennzeichen getrennten Textdatei angezeigt werden könnten. Wenn die Quelldatei Standardformate für datetime verwendet, ist diese Option nicht erforderlich. Pro Datei ist nur ein benutzerdefiniertes datetime-Format zulässig. Sie können pro Datei nicht mehrere benutzerdefinierte datetime-Formate angeben. Sie können jedoch mehrere datetime-Formate verwenden, wenn es sich bei den einzelnen Formaten um die Standardformate der entsprechenden zugehörigen Datentypen in der externen Tabellendefinition handelt.

PolyBase verwendet das benutzerdefinierte Datumsformat nur für den Import der Daten. Es verwendet das benutzerdefinierte Format nicht für das Schreiben von Daten in eine externe Datei.

 Wenn DATE_FORMAT nicht angegeben ist oder eine leere Zeichenfolge ist, verwendet PolyBase folgende Standardformate:
  
-   DateTime: „JJJJ-MM-TT HH:mm:ss“  
  
-   SmallDateTime: „JJJJ-MM-TT HH:mm“  
  
-   Date: „JJJJ-MM-TT“  
  
-   DateTime2: „JJJJ-MM-TT HH:mm:ss“  
  
-   DateTimeOffset: „JJJJ-MM-TT HH:mm:ss“  
  
-   Time: „HH:mm:ss“  
  
In der folgenden Tabelle finden Sie **Beispiele für Datumsformate**:
  
Hinweise zur Tabelle:  
  
-   Jahr, Monat und Tag können verschiedene Formate und Reihenfolgen aufweisen. Die Tabelle enthält nur das Format **JMT**. Ein Monat kann eine oder zwei Ziffern oder drei Zeichen umfassen. Ein Tag kann eine oder zwei Ziffern umfassen. Ein Jahr kann zwei oder vier Ziffern umfassen.
  
-   Millisekunden (fffffff) sind nicht erforderlich.
  
-   Die Angabe von AM oder PM (tt) ist nicht erforderlich. Der Standardwert ist AM.
  
|Datumstyp|Beispiel|Description|  
|---------------|-------------|-----------------|  
|datetime|DATE_FORMAT = 'JJJJ-MM-TT HH:mm:ss.fff'|Neben dem Jahr, dem Monat und dem Tag umfasst dieses Datumsformat 00 bis 24 Stunden, 00 bis 59 Minuten, 00 bis 59 Sekunden und 3 Ziffern für Millisekunden.|  
|datetime|DATE_FORMAT = 'JJJJ-MM-TT hh:mm:ss.ffftt'|Neben dem Jahr, dem Monat und dem Tag umfasst dieses Datumsformat 00 bis 12 Stunden, 00 bis 59 Minuten, 00 bis 59 Sekunden, 3 Ziffern für Millisekunden und AM bzw. am oder PM bzw. pm. |  
|SmallDateTime|DATE_FORMAT = 'JJJJ-MM-TT HH:mm'|Neben dem Jahr, dem Monat und dem Tag umfasst dieses Datumsformat 00 bis 23 Stunden, 00 bis 59 Minuten.|  
|SmallDateTime|DATE_FORMAT = 'JJJJ-MM-TT hh:mmtt'|Neben dem Jahr, dem Monat und dem Tag umfasst dieses Datumsformat 00 bis 11 Stunden, 00 bis 59 Minuten, keine Sekunden und AM bzw. am und PM bzw. pm.|  
|date|DATE_FORMAT = 'JJJJ-MM-TT'|Jahr, Monat und Tag. Es ist kein Zeitelement enthalten.|  
|date|DATE_FORMAT = 'JJJJ-MMM-TT'|Jahr, Monat und Tag. Wenn der Monat mit 3 Ms angegeben ist, steht der Eingabewert für eine der folgenden Zeichenfolgen: Jan, Feb, Mrz, Apr, Mai, Jun, Jul, Aug, Sep, Okt, Nov oder Dez.|  
|datetime2|DATE_FORMAT = 'JJJJ-MM-TT HH:mm:ss.fffffff'|Neben dem Jahr, dem Monat und dem Tag umfasst dieses Datumsformat 00 bis 23 Stunden, 00 bis 59 Minuten, 00 bis 59 Sekunden und 7 Ziffern für Millisekunden.|  
|datetime2|DATE_FORMAT = 'JJJJ-MM-TT hh:mm:ss.ffffffftt'|Neben dem Jahr, dem Monat und dem Tag umfasst dieses Datumsformat 00 bis 11 Stunden, 00 bis 59 Minuten, 00 bis 59 Sekunden, 7 Ziffern für Millisekunden und AM bzw. am oder PM bzw. pm.|  
|DateTimeOffset|DATE_FORMAT = 'JJJJ-MM-TT HH:mm:ss.fffffff zzz'|Neben dem Jahr, dem Monat und dem Tag umfasst dieses Datumsformat 00 bis 23 Stunden, 00 bis 59 Minuten, 00 bis 59 Sekunden, 7 Ziffern für Millisekunden und den Offsetwert für die Zeitzone, den Sie als `{+&#124;-}HH:ss` in die Eingabedatei eingefügt haben. Da die Uhrzeit in Los Angeles beispielsweise ohne Umschaltung der Sommer-/Winterzeit 8 hinter UTC liegt, gibt der Wert -08:00 in der Eingabedatei die Zeitzone für Los Angeles an.|  
|DateTimeOffset|DATE_FORMAT = 'JJJJ-MM-TT hh:mm:ss.ffffffftt zzz'|Neben dem Jahr, dem Monat und dem Tag umfasst dieses Datumsformat 00 bis 11 Stunden, 00 bis 59 Minuten, 00 bis 59 Sekunden, 7 Ziffern für Millisekunden, (AM bzw. am oder PM bzw. pm) und den Offsetwert für die Zeitzone. Eine Beschreibung finden Sie in der vorherigen Zeile.|  
|Uhrzeit|DATE_FORMAT = 'HH:mm:ss'|Es ist kein Datumswert vorhanden, nur 00 bis 23 Stunden, 00 bis 59 Minuten und 00 bis 59 Sekunden.|  
  
 Alle unterstützten Datumsformate:
  
|DATETIME|smalldatetime|date|datetime2|datetimeoffset|  
|--------------|-------------------|----------|---------------|--------------------|  
|[M[M]]M-[T]T-[JJ]JJ HH:mm:ss[.fff]|[M[M]]M-[T]T-[JJ]JJ HH:mm[:00]|[M[M]]M-[T]T-[JJ]JJ|[M[M]]M-[T]T-[JJ]JJ HH:mm:ss[.fffffff]|[M[M]]M-[T]T-[JJ]JJ HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[T]T-[JJ]JJ hh:mm:ss[.fff][tt]|[M[M]]M-[T]T-[JJ]JJ hh:mm[:00][tt]||[M[M]]M-[T]T-[JJ]JJ hh:mm:ss[.fffffff][tt]|[M[M]]M-[T]T-[JJ]JJ hh:mm:ss[.fffffff][tt] zzz|  
|[M[M]]M-[JJ]JJ-[T]T HH:mm:ss[.fff]|[M[M]]M-[JJ]JJ-[T]T HH:mm[:00]|[M[M]]M-[JJ]JJ-[T]T|[M[M]]M-[JJ]JJ-[T]T HH:mm:ss[.fffffff]|[M[M]]M-[JJ]JJ-[T]T HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[JJ]JJ-[T]T hh:mm:ss[.fff][tt]|[M[M]]M-[JJ]JJ-[T]T hh:mm[:00][tt]||[M[M]]M-[JJ]JJ-[T]T hh:mm:ss[.fffffff][tt]|[M[M]]M-[JJ]JJ-[T]T hh:mm:ss[.fffffff][tt] zzz|  
|[JJ]JJ-[M[M]]M-[T]T HH:mm:ss[.fff]|[JJ]JJ-[M[M]]M-[T]T HH:mm[:00]|[JJ]JJ-[M[M]]M-[T]T|[JJ]JJ-[M[M]]M-[T]T HH:mm:ss[.fffffff]|[JJ]JJ-[M[M]]M-[T]T HH:mm:ss[.fffffff] zzz|  
|[JJ]JJ-[M[M]]M-[T]T hh:mm:ss[.fff][tt]|[JJ]JJ-[M[M]]M-[T]T hh:mm[:00][tt]||[JJ]JJ-[M[M]]M-[T]T hh:mm:ss[.fffffff][tt]|[JJ]JJ-[M[M]]M-[T]T hh:mm:ss[.fffffff][tt] zzz|  
|[JJ]JJ-[T]T-[M[M]]M HH:mm:ss[.fff]|[JJ]JJ-[T]T-[M[M]]M HH:mm[:00]|[JJ]JJ-[T]T-[M[M]]M|[JJ]JJ-[T]T-[M[M]]M HH:mm:ss[.fffffff]|[JJ]JJ-[T]T-[M[M]]M HH:mm:ss[.fffffff] zzz|  
|[JJ]JJ-[T]T-[M[M]]M hh:mm:ss[.fff][tt]|[JJ]JJ-[T]T-[M[M]]M hh:mm[:00][tt]||[JJ]JJ-[T]T-[M[M]]M hh:mm:ss[.fffffff][tt]|[JJ]JJ-[T]T-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
|[T]T-[M[M]]M-[JJ]JJ HH:mm:ss[.fff]|[T]T-[M[M]]M-[JJ]JJ HH:mm[:00]|[T]T-[M[M]]M-[JJ]JJ|[T]T-[M[M]]M-[JJ]JJ :mm:ss[.fffffff]|[T]T-[M[M]]M-[JJ]JJ HH:mm:ss[.fffffff] zzz|  
|[T]T-[M[M]]M-[JJ]JJ hh:mm:ss[.fff][tt]|[T]T-[M[M]]M-[JJ]JJ hh:mm[:00][tt]||[T]T-[M[M]]M-[JJ]JJ hh:mm:ss[.fffffff][tt]|[T]T-[M[M]]M-[JJ]JJ hh:mm:ss[.fffffff][tt] zzz|  
|[T]T-[JJ]JJ-[M[M]]M HH:mm:ss[.fff]|[T]T-[JJ]JJ-[M[M]]M HH:mm[:00]|[T]T-[JJ]JJ-[M[M]]M|[T]T-[JJ]JJ-[M[M]]M HH:mm:ss[.fffffff]|[T]T-[JJ]JJ-[M[M]]M HH:mm:ss[.fffffff] zzz|  
|[T]T-[JJ]JJ-[M[M]]M hh:mm:ss[.fff][tt]|[T]T-[JJ]JJ-[M[M]]M hh:mm[:00][tt]||[T]T-[JJ]JJ-[M[M]]M hh:mm:ss[.fffffff][tt]|[T]T-[JJ]JJ-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
  
 Details:  
  
-   Sie können „–“, „/“ oder „'.'“ verwenden, um Werte für Monat, Tag und Jahr zu trennen. Der Einfachheit halber wird in die Tabelle nur das Trennzeichen „–“ verwendet.
  
-   Geben Sie mindestens drei Zeichen an, wenn der Monat in Textform angegeben werden soll. Monate mit einem oder zwei Zeichen werden als Zahlen interpretiert.
  
-   Verwenden Sie das Symbol „:“, um Zeitwerte zu trennen.
  
-   Buchstaben in eckigen Klammern sind optional.
  
-   Die Buchstaben „tt“ kennzeichnen [AM|PM|am|pm]. AM ist die Standardeinstellung. Wenn „tt“ angegeben ist, muss der Wert für die Stunde (hh) in einem Bereich von 0 bis 12 liegen.
  
-   Die Buchstaben „zzz“ kennzeichnen den Offsetwert für die Zeitzone für die aktuelle Zeitzone des Systems im Format {+|-}HH:ss].
  
 USE_TYPE_DEFAULT = { TRUE | **FALSE** }  
 Gibt an, wie fehlende Werte in durch Trennzeichen getrennten Textdateien behandelt werden sollen, wenn PolyBase Daten aus der Textdatei abruft.
  
 TRUE  
 Speichern Sie beim Abrufen von Daten aus der Textdatei jeden fehlenden Wert, indem Sie den Standardwert für den Datentyp der entsprechenden Spalte in der externen Tabellendefinition verwenden. Ersetzen Sie einen fehlenden Wert beispielsweise durch:  
  
-   0, wenn die Spalte als numerische Spalte definiert ist.
  
-   Leere Zeichenfolge „“, wenn die Spalte eine Zeichenfolgenspalte ist.
  
-   1900-01-01, wenn die Spalte eine Datumsspalte ist.
  
 FALSE  
 Speichern Sie alle fehlenden Werte als NULL-Werte. Alle NULL-Werte, die durch Verwendung des Worts NULL in der durch Trennzeichen getrennten Textdatei gespeichert werden, werden als Zeichenfolge „NULL“ importiert.
  
   Encoding = {'UTF8' | 'UTF16'}  
 In Azure SQL Data Warehouse kann PolyBase UTF8- und UTF16-LE-codierte, durch Trennzeichen getrennte Textdateien lesen. In SQL Server und PDW unterstützt PolyBase nicht das Lesen UTF16-codierter Dateien.
  
 DATA_COMPRESSION = *data_compression_method*  
 Gibt die Datenkomprimierungsmethode für die externen Daten an. Wenn DATA_COMPRESSION nicht angegeben ist, stellen dekomprimierte Daten den Standard dar.
 GZip-komprimierte Dateien müssen die Dateierweiterung „.gz“ aufweisen, damit sie ordnungsgemäß funktionieren.
 
 Der Formattyp DELIMITEDTEXT unterstützt folgende Komprimierungsmethoden:
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'

 Der Formattyp RCFILE unterstützt folgende Komprimierungsmethode:
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'
  
 Der FORC-Dateiformattyp unterstützt folgende Komprimierungsmethode:
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'
  
 Der PARQUET-Dateiformattyp unterstützt folgende Komprimierungsmethoden:
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'
  
## <a name="permissions"></a>Berechtigungen  
 Macht eine ALTER ANY EXTERNAL FILE FORMAT-Berechtigung erforderlich.
  
## <a name="general-remarks"></a>Allgemeine Hinweise
 Das externe Dateiformat ist in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] datenbankweit gültig. Es ist in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] serverweit gültig.  
  
 Sämtliche Formatoptionen sind optional und gelten nur für durch Trennzeichen getrennte Textdateien.  
  
 Wenn die Daten in einem der komprimierten Formate gespeichert werden, dekomprimiert PolyBase die Daten zunächst, bevor es die Datensätze zurückgibt.
  
## <a name="limitations-and-restrictions"></a>Einschränkungen
  
 Das Zeilentrennzeichen in durch Trennzeichen getrennten Textdateien muss von dem LineRecordReader von Hadoop unterstützt werden. Es muss „\r“, „\n“ oder „\r\n“ lauten. Diese Trennzeichen sind nicht durch Benutzer konfigurierbar.
  
 Die Kombinationen der unterstützten SerDe-Methoden mit RCFiles und die unterstützten Datenkomprimierungsmethoden werden oben in diesem Artikel aufgeführt. Nicht alle Kombinationen werden unterstützt.
  
 Die maximale Anzahl der gleichzeitigen PolyBase-Abfragen beläuft sich auf 32. Wenn 32 gleichzeitige Abfragen ausgeführt werden, kann jede Abfrage maximal 33.000 Dateien vom Speicherort für externe Dateien lesen. Der Stammordner und die einzelnen Unterordner zählen auch als Datei. Wenn der Grad der Parallelität unter 32 liegt, kann der Speicherort für externe Dateien mehr als 33.000 Dateien enthalten.
  
 Aufgrund der Begrenzung in Bezug auf die Anzahl der Dateien in der externen Tabelle wird empfohlen, weniger als 30.000 Dateien in den Stamm- und Unterordnern des Speicherorts für externe Dateien zu speichern. Darüber hinaus wird empfohlen, die Anzahl der Unterordner unter dem Stammverzeichnis gering zu halten. Wenn auf zu viele Dateien verwiesen wird, kann eine Out-of-Memory-Ausnahme von Java Virtual Machine auftreten.
  
  Beim Exportieren von Daten nach Hadoop oder Azure Blob Storage über PolyBase werden nur die Daten exportiert, nicht die Spaltennamen (Metadaten), wie im CREATE EXTERNAL TABLE-Befehl definiert.

## <a name="locking"></a>Sperren  
 Akzeptiert eine gemeinsame Sperre für das EXTERNAL FILE FORMAT-Objekt.
  
## <a name="performance"></a>Leistung
 Die Verwendung komprimierter Dateien ist immer mit dem Konflikt verbunden, ob weniger Daten zwischen der externen Datenquelle und SQL Server übertragen werden sollen oder ob die CPU-Auslastung zum Komprimieren und Dekomprimieren der Daten erhöht werden soll.
  
 GZip-komprimierte Textdateien können nicht aufgeteilt werden. Es wird empfohlen, zur Verbesserung der Leistung von GZip-komprimierten Textdateien mehrere Dateien zu generieren, die alle in demselben Verzeichnis innerhalb der externen Datenquelle gespeichert sind. Die Dateistruktur ermöglicht PolyBase das schnellere Lesen und Dekomprimieren der Daten, indem mehrere Reader- und Dekomprimierungsprozesse verwendet werden. Die ideale Anzahl der komprimierten Dateien ist die maximale Anzahl der Datenreaderprozesse pro Computeknoten. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] beträgt die maximale Anzahl der Datenreaderprozesse im aktuellen Release 8 pro Knoten. In [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] variiert die maximale Anzahl der Datenreaderprozesse pro Knoten je nach SLO. Weitere Einzelheiten finden Sie unter [Azure SQL Data Warehouse loading patterns and strategies](https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies/) (Azure SQL Data Warehouse – Auslastungsmuster und Strategien).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-create-a-delimitedtext-external-file-format"></a>A. Erstellen eines externen DELIMITEDTEXT-Dateiformats  
 In diesem Beispiel wird für eine durch Trennzeichen getrennte Textdatei ein externes Dateiformat mit dem Namen *textdelimited1* erstellt. Die für FORMAT\_OPTIONS aufgeführten Optionen geben an, dass die Felder in der Datei durch einen senkrechten Strich „|“ voneinander getrennt werden sollten. Die Textdatei wird auch mit dem GZip-Codec komprimiert. Wenn DATA\_COMPRESSION nicht angegeben ist, wird die Textdatei dekomprimiert.
  
 Bei einer durch Trennzeichen getrennten Textdatei kann als Datenkomprimierungsmethode entweder der Standard-Codec „org.apache.hadoop.io.compress.DefaultCodec“ oder der GZip-Codec „org.apache.hadoop.io.compress.GzipCodec“ angewendet werden.
  
```  
CREATE EXTERNAL FILE FORMAT textdelimited1  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT,  
    FORMAT_OPTIONS (  
        FIELD_TERMINATOR = '|',  
        DATE_FORMAT = 'MM/dd/yyyy' ),  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
);  
```  
  
### <a name="b-create-an-rcfile-external-file-format"></a>B. Erstellen eines externen RCFile-Dateiformats  
 In diesem Beispiel wird für eine RCFile ein externes Dateiformat erstellt, das die Serialisierungs-/Deserialisierungsmethode „org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe“ verwendet. Zudem wird angegeben, dass der Standard-Codec für die Datenkomprimierungsmethode verwendet werden soll. Wenn DATA_COMPRESSION nicht angegeben ist, ist keine Komprimierung der Standard.
  
```  
CREATE EXTERNAL FILE FORMAT rcfile1  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe',  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'  
);  
```  
  
### <a name="c-create-an-orc-external-file-format"></a>C. Erstellen eines externen ORC-Dateiformats  
 In diesem Beispiel wird für eine ORC-Datei ein externes Dateiformat erstellt, das die Daten mit der Datenkomprimierungsmethode „org.apache.io.compress.SnappyCodec“ komprimiert. Wenn DATA_COMPRESSION nicht angegeben ist, ist keine Komprimierung der Standard.
  
```  
CREATE EXTERNAL FILE FORMAT orcfile1  
WITH (  
    FORMAT_TYPE = ORC,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
  
### <a name="d-create-a-parquet-external-file-format"></a>D. Erstellen eines externen PARQUET-Dateiformats  
 In diesem Beispiel wird für eine PARQUET-Datei ein externes Dateiformat erstellt, das die Daten mit der Datenkomprimierungsmethode „org.apache.io.compress.SnappyCodec“ komprimiert. Wenn DATA_COMPRESSION nicht angegeben ist, ist keine Komprimierung der Standard.  
  
```  
CREATE EXTERNAL FILE FORMAT parquetfile1  
WITH (  
    FORMAT_TYPE = PARQUET,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
### <a name="e-create-a-delimited-text-file-skipping-header-row-azure-sql-dw-only"></a>E. Erstellen einer durch Trennzeichen getrennten Textdatei, wobei die Kopfzeile übersprungen wird (nur bei Azure SQL DW)
 In diesem Beispiel wird für eine CSV-Datei mit einer einzelnen Kopfzeile ein externes Dateiformat erstellt. 
  
```  
CREATE EXTERNAL FILE FORMAT skipHeader_CSV
WITH (FORMAT_TYPE = DELIMITEDTEXT,
      FORMAT_OPTIONS(
          FIELD_TERMINATOR = ',',
          STRING_DELIMITER = '"',
          FIRST_ROW = 2, 
          USE_TYPE_DEFAULT = True)
)
```   

## <a name="see-also"></a>Weitere Informationen finden Sie unter
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE EXTERNAL TABLE AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [CREATE TABLE AS SELECT &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [sys.external_file_formats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)  
