---
title: Erstellen eines EXTERNEN DATEIFORMATS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL FILE FORMAT
- CREATE_EXTERNAL_FILE_FORMAT
dev_langs: TSQL
helpviewer_keywords:
- External
- External, file format
- PolyBase, external file format
ms.assetid: abd5ec8c-1a0e-4d38-a374-8ce3401bc60c
caps.latest.revision: "25"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6db9730d5e0905d464a57151365a9413f61a86eb
ms.sourcegitcommit: 16347f3f5ed110b5ce4cc47e6ac52b880eba9f5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="create-external-file-format-transact-sql"></a>Erstellen eines EXTERNEN DATEIFORMATS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Erstellt eine PolyBase externe-Dateiformatdefinition für externe Daten in Hadoop oder Azure Blob-Speicher mit Azure Data Lake-Speicher gespeichert. Erstellen ein externes Dateiformat ist eine Voraussetzung zum Erstellen einer externen PolyBase-Tabelle. Durch das Erstellen eines externen Dateiformats, geben Sie das tatsächliche Layout der Daten von einer externen Tabelle verwiesen wird.  
  
 PolyBase unterstützt die folgenden Dateiformate:  
  
-   Durch Trennzeichen getrennten text  
  
-   Hive-RCFile  
  
-   Hive-ORC.  
  
-   Parquet  
  
 Um eine externe Tabelle zu erstellen, finden Sie unter [CREATE EXTERNAL TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-table-transact-sql.md).  
  
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
    | DATE_FORMAT = datetime_format  
    | USE_TYPE_DEFAULT = { TRUE | FALSE } 
    | Encoding = {'UTF8' | 'UTF16'} 
}  
```  
  
## <a name="arguments"></a>Argumente  
 *file_format_name*  
 Gibt einen Namen für das externe Dateiformat an.  
  
 FORMAT_TYPE  
 Gibt das Format der externen Daten.  
  
 PARQUET  
 Gibt ein Parquet-Format.  
  
 ORC.  
 Gibt ein Format optimiert Zeile Einspaltig (ORC). Diese Option erfordert Hive 0,11 oder höher auf dem externen Hadoop-Cluster. Hadoop bietet das Dateiformat ORC eine bessere Leistung als das Dateiformat RCFILE und Komprimierung.  
  
 RCFILE (in Kombination mit SERDE_METHOD = *SERDE_method*)  
 Gibt einen Datensatz Einspaltig Dateiformat (RcFile). Diese Option müssen Sie eine Hive-Serialisierungsprogramm, das Deserialisierungsprogramm (SerDe)-Methode angeben. Diese Anforderung ist identisch, wenn Sie in Hadoop Hive/HiveQL, zum Abfragen der RC-Dateien verwenden. Beachten Sie, dass die SerDe-Methode für Groß-/Kleinschreibung beachtet wird.  
  
 Beispiele zur Angabe von RCFile mit zwei SerDe-Methoden, die PolyBase unterstützt.  
  
-   FORMAT_TYPE = RCFILE SERDE_METHOD = "org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe"  
  
-   FORMAT_TYPE = RCFILE SERDE_METHOD = "org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe"  
  
 DELIMITEDTEXT  
 Gibt ein Textformat mit Spaltentrennzeichen, so genannte Feldabschlusszeichen an.  
  
 Feldabschlusszeichen = *Feldabschlusszeichen*  
 Gilt nur für durch Trennzeichen getrennten Textdateien. Dies gibt einen oder mehrere Zeichen, die das Ende jedes Feld (Spalte) markieren in der Datei mit Texttrennzeichen an. Die Standardeinstellung ist der Pipe-Zeichen ꞌ auf | ꞌ auf. Garantierte Supportzwecken empfiehlt es sich um eine oder mehrere ASCII-Zeichen verwendet.
  
  
 Beispiele:  
  
-   FELDABSCHLUSSZEICHEN = "|"  
  
-   FELDABSCHLUSSZEICHEN = ""  
  
-   Feldabschlusszeichen = ꞌ\tꞌ  
  
-   FELDABSCHLUSSZEICHEN = "~ | ~"  
  
 STRING_DELIMITER = *String_delimiter*  
 Gibt das Feldabschlusszeichen für Daten vom Typzeichenfolge in der Datei mit Texttrennzeichen an. Die Zeichenfolgen-Trennzeichen für ein oder mehrere Zeichen lang ist und mit einfachen Anführungszeichen eingeschlossen ist. Der Standardwert ist eine leere Zeichenfolge "". Garantierte Supportzwecken empfiehlt es sich um eine oder mehrere ASCII-Zeichen verwendet.
 
  
 Beispiele:  

-   STRING_DELIMITER = "" "

-   STRING_DELIMITER = "0 x 22" – doppelte Anführungszeichen Hex
  
-   STRING_DELIMITER = "*"  
  
-   STRING_DELIMITER = Ꞌ AUF, Ꞌ AUF  
  
-   STRING_DELIMITER = 0x7E0x7E – zwei Tildas (z. B. ~ ~)
  
 DATE_FORMAT = *Datetime_format*  
 Gibt ein benutzerdefiniertes Format für alle Datums- und Zeitdaten, die in einer durch Trennzeichen getrennte Textdatei angezeigt werden. Wenn die Quelldatei "DateTime" Standardformate verwendet wird, ist diese Option nicht erforderlich. Pro Datei ist nur eine benutzerdefinierte Datetime-Format zulässig. Sie können nicht mehrere benutzerdefinierte Datetime-Formate pro Datei angeben. Allerdings können Sie mehrere Datetime-Formate verwenden, ist jeweils das Standardformat für den jeweiligen Datentyp in der externen Tabellendefinition.
 
 
PolyBase verwendet nur die benutzerdefinierten Datumsformat für das Importieren von Daten. Das benutzerdefinierte Format wird nicht zum Schreiben von Daten in eine externe Datei verwendet.

 Wenn DATE_FORMAT nicht angegeben oder ist eine leere Zeichenfolge, wird PolyBase die folgenden Standardformate verwenden:  
  
-   "DateTime": "Yyyy-MM-TT HH: mm:"  
  
-   SmallDateTime: "Yyyy-MM-TT HH: mm"  
  
-   Datum: "Yyyy-MM-TT"  
  
-   DateTime2: "Yyyy-MM-TT HH: mm:"  
  
-   "DateTimeOffset": "Yyyy-MM-TT HH: mm:"  
  
-   Zeit: "hh"  
  
 **Beispiel für Datums-und Uhrzeitformate** in der folgenden Tabelle sind.  
  
 Hinweise zur Tabelle:  
  
-   Jahr, Monat und Tag können eine Vielzahl von Formaten und Aufträge haben. Die Tabelle zeigt nur Ymd. Monat kann Ziffern von 1 oder 2 oder 3 Zeichen hat. Tag kann 1 oder 2 Ziffern haben. Jahr kann 2 oder 4 Ziffern aufweisen.  
  
-   Millisekunden (Fffffff) ist nicht erforderlich.  
  
-   Am, pm (Tt) nicht erforderlich ist. Der Standardwert ist Uhr.  
  
|Date-Typ|Beispiel|Description|  
|---------------|-------------|-----------------|  
|DateTime|DATE_FORMAT = "JJJJ-MM-TT ss.fff"|Zusätzlich zu den Year, Month und Day, umfasst dies 00 bis 24 Stunden, 00-59 Minuten, 00-59 Sekunden und 3 Ziffern für Millisekunden.|  
|DateTime|DATE_FORMAT = "JJJJ-MM-tt hh:mm:ss.ffftt"|Zusätzlich zu den Jahr, Monat und Tag, schließt dies 00-12 Stunden, 00-59 Minuten, 00-59 Sekunden und 3 Ziffern für Millisekunden und Uhr am, PM oder pm.|  
|SmallDateTime|DATE_FORMAT = "JJJJ-MM-TT HH: mm"|Zusätzlich zu den Year, Month und Day, schließt dies 00-23 Stunden, 00-59 Minuten.|  
|SmallDateTime|DATE_FORMAT = "JJJJ-MM-tt Hh:mmtt"|Neben dem Jahr, Monat und Tag, schließt dies 00-11 Stunden 00-59 Minuten, keine Sekunden und Uhr, am, PM oder pm.|  
|Datum|DATE_FORMAT = "JJJJ-MM-TT"|Jahr, Monat und Tag. Keine Time-Element ist enthalten.|  
|Datum|DATE_FORMAT = "JJJJ-MMM-TT"|Jahr, Monat und Tag. Wenn Monat mit 3 M angegeben wird, ist der Wert mindestens eine der Zeichenfolgen Januar, Februar, Mrz, Apr, Mai, Jun, Jul, Aug, Sep, Okt, Nov oder Dec.|  
|datetime2|DATE_FORMAT = "JJJJ-MM-TT HH:mm:ss.fffffff"|Zusätzlich zu den Year, Month und Day, schließt dies 00-23 Stunden, 00-59 Minuten, 00-59 Sekunden und 7 Ziffern für Millisekunden.|  
|datetime2|DATE_FORMAT = "JJJJ-MM-tt hh:mm:ss.ffffffftt"|Neben dem Jahr, Monat und Tag, schließt dies 00-11 Stunden 00-59 Minuten, 00-59 Sekunden, 7 Ziffern für Millisekunden und Uhr, bin, Uhr oder pm.|  
|DateTimeOffset|DATE_FORMAT = "JJJJ-MM-TT HH:mm:ss.fffffff Zzz"|Zusätzlich zu den Year, Month und Day, schließt dies 00-23 Stunden, 00-59 Minuten, 00-59 Sekunden und 7 Ziffern für Millisekunden und den Zeitzonenunterschied, die Sie in der Eingabedatei als verwendet {+ &#124;-} HH:ss. Einsparungen ist z. B. seit Los Angeles ohne Sommerzeit 8 Stunden nach UTC, ein Wert von-08: 00 als Uhrzeit in der Eingabedatei gibt die Zeitzone für Los Angeles an.|  
|DateTimeOffset|DATE_FORMAT = "JJJJ-MM-tt hh:mm:ss.ffffffftt Zzz"|Neben dem Jahr, Monat und Tag, schließt dies 00-11 Stunden 00-59 Minuten, 00-59 Sekunden 7 Ziffern für Millisekunden (Uhr, am, PM oder pm) und den Zeitzonenunterschied. Finden Sie in der Beschreibung in der vorherigen Zeile.|  
|Uhrzeit|DATE_FORMAT = "Hh"|Es ist kein Datumswert, 00-23 Stunden, 00-59 Minuten und 00-59 Sekunden.|  
  
 Alle unterstützten Datums-und Uhrzeitformate:  
  
|datetime|smalldatetime|Datum|datetime2|datetimeoffset|  
|--------------|-------------------|----------|---------------|--------------------|  
|[M [M]] M-[d] d-[Yy] Yy hh: mm: [ss.fff]|[M [M]] M-[d] d-[Yy] Yy hh: mm [: 00]|[M [M]] M-[d] d-[Yy] yy|[M [M]] M-[d] d-[Yy] Yy hh: mm: [.fffffff]|[M [M]] M-[d] d-[Yy] Yy hh: mm: [.fffffff] zzz|  
|[M [M]] M-[d] d-[Yy] Yy hh: mm: [ss.fff] [Tt]|[M [M]] M-[d] d-[Yy] Yy hh: mm [: 00] [Tt]||[M [M]] M-[d] d-[Yy] Yy hh: mm: [.fffffff] [Tt]|[M [M]] M-[d] d-[Yy] Yy hh: mm: [.fffffff] [Tt] Zzz|  
|[M [M]] M [Yy] Yy-[d]-d hh: mm: [ss.fff]|[M [M]] M [Yy] Yy-[d]-d hh: mm [: 00]|[M [M]] M [Yy] Yy-[d]-d|[M [M]] M [Yy] Yy-[d]-d ss [.fffffff]|[M [M]] M [Yy] Yy-[d]-d Zzz ss [.fffffff]|  
|[M [M]] M-[Yy] Yy-[d] d hh: mm: [ss.fff] [Tt]|[M [M]] M-[Yy] Yy-[d] d hh: mm [: 00] [Tt]||[M [M]] M-[Yy] Yy-[d] d ss [.fffffff] [Tt]|[M [M]] M-[Yy] Yy-[d] d ss [.fffffff] [Tt] Zzz|  
|[Yy] Yy [M [M]] M-[d]-d hh: mm: [ss.fff]|[Yy] Yy [M [M]] M-[d]-d hh: mm [: 00]|[Yy] Yy [M [M]] M-[d]-d|[Yy] Yy [M [M]] M-[d]-d ss [.fffffff]|[Yy] Yy-[M [M]] d ss [.fffffff] Zzz M-[d]|  
|[Yy] Yy-[M [M]] M-[d] d hh: mm: [ss.fff] [Tt]|[Yy] Yy-[M [M]] M-[d] d hh: mm [: 00] [Tt]||[Yy] Yy-[M [M]] M-[d] d ss [.fffffff] [Tt]|[Yy] Yy-[M [M]] M-[d] d ss [.fffffff] [Tt] Zzz|  
|[Yy] Yy-[d] d-[M [M]] M hh: mm: [ss.fff]|[Yy] Yy-[d] d-[M [M]] M hh: mm [: 00]|[Yy] Yy - d [d]-[M [M]] M|[Yy] Yy-[d] d-[M [M]] M ss [.fffffff]|[Yy] Yy-[d] M ss [.fffffff] Zzz d-[M [M]]|  
|[Yy] Yy-[d] d-[M [M]] M hh: mm: [ss.fff] [Tt]|[Yy] Yy-[d] d-[M [M]] M hh: mm [: 00] [Tt]||[Yy] Yy-[d] d-[M [M]] M ss [.fffffff] [Tt]|[Yy] Yy-[d] d-[M [M]] M ss [.fffffff] [Tt] Zzz|  
|[d] d-[M [M]] M-[Yy] Yy hh: mm: [ss.fff]|[d] d-[M [M]] M-[Yy] Yy hh: mm [: 00]|[d] d-[M [M]] M-[Yy] yy|[d] d-[M [M]] M-[Yy] Yy hh: mm: [.fffffff]|[d] d-[M [M]] M-[Yy] Yy hh: mm: [.fffffff] zzz|  
|[d] d-[M [M]] M-[Yy] Yy hh: mm: [ss.fff] [Tt]|[d] d-[M [M]] M-[Yy] Yy hh: mm [: 00] [Tt]||[d] d-[M [M]] M-[Yy] Yy hh: mm: [.fffffff] [Tt]|[d] d-[M [M]] M-[Yy] Yy hh: mm: [.fffffff] [Tt] Zzz|  
|[d] d-[Yy] Yy-[M [M]] M hh: mm: [ss.fff]|[d] d-[Yy] Yy-[M [M]] M hh: mm [: 00]|[d] d-[Yy] Yy-[M [M]] M|[d] d-[Yy] Yy-[M [M]] M ss [.fffffff]|[d] d-[Yy] Yy-[M [M]] M ss [.fffffff] zzz|  
|[d] d-[Yy] Yy-[M [M]] M hh: mm: [ss.fff] [Tt]|[d] d-[Yy] Yy-[M [M]] M hh: mm [: 00] [Tt]||[d] d-[Yy] Yy-[M [M]] M ss [.fffffff] [Tt]|[d] d-[Yy] Yy-[M [M]] M ss [.fffffff] [Tt] Zzz|  
  
 Details:  
  
-   Um Werte für Monat, Tag und Jahr zu trennen, können Sie '–', '/' oder '. '. Der Einfachheit halber wird in die Tabelle nur das Trennzeichen ":" verwendet.  
  
-   Zum Angeben der Monat als Text, verwenden drei oder mehr Zeichen. Monate mit 1 oder 2 Zeichen werden als Zahl interpretiert.  
  
-   Verwenden Sie zum Trennen der Time-Werten die ': ' Symbol.  
  
-   Buchstaben, die in eckige Klammern eingeschlossen sind optional.  
  
-   Legen Sie die Buchstaben "Tt" [AM | PM | am | pm]. Uhr ist die Standardeinstellung. Wenn "Tt" angegeben wird, muss ein Wert für die Stunde (Hh) im Bereich von 0 bis 12 sein.  
  
-   Die Buchstaben "Zzz" Festlegen des Zeitzonenoffsets für das System aktuelle Zeitzone im Format {+ |-} HH:ss].  
  
 USE_TYPE_DEFAULT = {TRUE | **"FALSE"** }  
 Gibt an, wie fehlende Werte in einer durch Trennzeichen getrennten Textdateien behandelt wird, wenn PolyBase Daten aus der Textdatei abruft.  
  
 TRUE  
 Beim Abrufen von Daten aus der Textdatei speichern Sie jeden fehlenden Wert durch die Verwendung des Standardwerts für den Datentyp der entsprechenden Spalte in der externen Tabellendefinition. Ersetzen Sie z. B. einen fehlenden Wert mit ein:  
  
-   0, wenn die Spalte als eine numerische Spalte definiert ist.  
  
-   Leere Zeichenfolge "" Wenn die Spalte eine Spalte mit Zeichenfolgen ist.  
  
-   1900-01-01 ist die Spalte eine Datumsspalte.  
  
 FALSE  
 Speichern Sie alle fehlenden Werte als NULL. Alle Nullwerte, die gespeichert werden, verwenden das Wort NULL in die durch Tabstopps getrennte Textdatei importiert werden als die Zeichenfolge 'NULL'.  
  
   Codierung = {'UTF8' | 'UTF16'}   
 In Azure SQL Data Warehouse kann PolyBase gelesen UTF8- und UTF16-LE-codierte Textdateien mit Trennzeichen. In SQL Server und PDW PolyBase unterstützt keine lesen UTF16-Format codierte Dateien.
  
 DATA_COMPRESSION = *Data_compression_method*  
 Gibt die datenkomprimierungsmethode für die externen Daten. Wenn DATA_COMPRESSION nicht angegeben wird, ist die Standardeinstellung von nicht komprimierten Daten.  
 Damit Sie richtig funktioniert, benötigen Gzip-komprimierten Dateien die Dateierweiterung ".gz".
 
 Der Formattyp DELIMITEDTEXT unterstützt diese Komprimierungsmethoden:  
  
-   DATA COMPRESSION = "org.apache.hadoop.io.compress.DefaultCodec"  
  
-   DATA COMPRESSION = "org.apache.hadoop.io.compress.GzipCodec"  

 Der Formattyp rcfile unterstützt diese Komprimierungsmethode:  
  
-   DATA COMPRESSION = "org.apache.hadoop.io.compress.DefaultCodec"  
  
 Formattyp ORC unterstützt diese Komprimierungsmethoden:  
  
-   DATA COMPRESSION = "org.apache.hadoop.io.compress.DefaultCodec"  
  
-   DATA COMPRESSION = "org.apache.hadoop.io.compress.SnappyCodec"  
  
 Formattyp PARQUET unterstützt diese Komprimierungsmethoden:  
  
-   DATA COMPRESSION = "org.apache.hadoop.io.compress.GzipCodec"  
  
-   DATA COMPRESSION = "org.apache.hadoop.io.compress.SnappyCodec"  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Berechtigung ALTER ANY EXTERNAL FILE FORMAT.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Das externe Dateiformat ist im Datenbankbereich [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Es ist im Serverbereich [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 Die Formatoptionen sind optional und gelten nur für durch Trennzeichen getrennten Textdateien.  
  
 Wenn die Daten in einem komprimierten Format gespeichert werden, wird PolyBase zuerst Dekomprimieren der Daten vor der Rückgabe der Datensätze.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen   
  
 Das Zeilentrennzeichen in getrennte Textdateien unterstützt werden muss von Hadoop LineRecordReader also muss er entweder "\r", "\n" oder "\r\n". Dies sind keine Benutzer konfigurierbar.  
  
 Die Kombinationen von unterstützten SerDe-Methoden mit RCFiles und die unterstützten Daten Komprimierungsverfahren, werden zuvor in diesem Artikel aufgeführt. Nicht alle Kombinationen werden unterstützt.  
  
 Die maximale Anzahl gleichzeitiger PolyBase-Abfragen ist 32. Wenn es sich bei 32 gleichzeitige Abfragen ausgeführt werden, kann jede Abfrage maximal 33.000 Dateien vom Speicherort externen lesen. Der Stammordner, und jeder Unterordner werden auch als eine Datei gewertet. Wenn der Grad an Parallelität höchstens 32 ist, kann der Speicherort der externen Datei mehr als 33.000 Dateien enthalten.  
  
 Aufgrund der Einschränkung in Bezug auf die Anzahl der Dateien in der externen Tabelle wird empfohlen, weniger als 30.000 Dateien in die Stamm- und Unterordner der Speicherort der externen Datei zu speichern. Darüber hinaus wird empfohlen, lassen die Anzahl der Unterordner unter dem Stammverzeichnis auf einer kleinen Anzahl. Eine Java Virtual Machine Out-of-Memory-Ausnahme kann auftreten, wenn zu viele Dateien verwiesen werden.  
  
## <a name="locking"></a>Sperren  
 Akzeptiert eine gemeinsame Sperre für das externe DATEIFORMAT-Objekt.  
  
## <a name="performance"></a>Leistung  
 Immer mithilfe von komprimierten Dateien im Lieferumfang der Kompromiss zwischen weniger Daten zwischen der externen Datenquelle und die SQL Server beim Erhöhen der CPU-Auslastung zum Komprimieren und Dekomprimieren die Daten übertragen.  
  
 Textdateien Gzip komprimiert sind nicht teilbar. Es wird empfohlen, zum Verbessern der Leistung für Gzip komprimierte Textdateien generiert mehrere Dateien, die alle im selben Verzeichnis in der externen Datenquelle gespeichert sind. Dadurch wird zum Lesen und Dekomprimieren die Daten schneller mehrere Reader und -dekomprimierung Prozesse mit PolyBase. Die ideale Anzahl von komprimierten Dateien ist die maximale Anzahl von Data Reader Prozessen pro Compute-Knoten. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], die maximale Anzahl von Data Reader-Prozesse ist 8 pro Knoten in der aktuellen Version. In [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], die maximale Anzahl von Data Reader Prozessen pro Knoten variiert je nach SLO. Finden Sie unter [Azure SQL Data Warehouse Laden von Mustern und Strategien](https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies/) Details.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-create-a-delimitedtext-external-file-format"></a>A. Erstellen Sie ein externes Dateiformat DELIMITEDTEXT  
 In diesem Beispiel wird ein externes Dateiformat mit dem Namen *textdelimited1* für eine Datei mit Texttrennzeichen. Die FORMAT_OPTIONS Geben Sie die Felder in der Datei durch einen senkrechten Strich getrennt werden ' |'. Die Textdatei wird mit dem Gzip-Codec auch komprimiert. Wenn DATA_COMPRESSION nicht angegeben ist, wird die Textdatei dekomprimiert.  
  
 Für eine durch Tabstopps getrennte Textdatei die datenkomprimierungsmethode oder sein. der Standardwert Codec, "org.apache.hadoop.io.compress.DefaultCodec", dem Gzip-Codec "org.apache.hadoop.io.compress.GzipCodec".  
  
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
  
### <a name="b-create-an-rcfile-external-file-format"></a>B. Erstellen Sie ein externes Dateiformat RCFile  
 Dieses Beispiel erstellt ein externes Dateiformat für eine RCFile, die die Serialisierung/Deserialisierung Methode org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe verwendet. Außerdem angegeben, um die Standard-Codec für die datenkomprimierungsmethode zu verwenden. Wenn DATA_COMPRESSION nicht angegeben ist, wird standardmäßig keine Komprimierung.  
  
```  
CREATE EXTERNAL FILE FORMAT rcfile1  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe',  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'  
);  
```  
  
### <a name="c-create-an-orc-external-file-format"></a>C. Erstellen Sie ein externes Dateiformat ORC.  
 Dieses Beispiel erstellt ein externes Dateiformat für eine ORC-Datei, die die Daten mit der org.apache.io.compress.SnappyCodec datenkomprimierungsmethode komprimiert. Wenn DATA_COMPRESSION nicht angegeben ist, wird standardmäßig keine Komprimierung.  
  
```  
CREATE EXTERNAL FILE FORMAT orcfile1  
WITH (  
    FORMAT_TYPE = ORC,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
  
### <a name="d-create-a-parquet-external-file-format"></a>D. Erstellen Sie ein externes Dateiformat PARQUET  
 Dieses Beispiel erstellt ein externes Dateiformat für eine Parquet-Datei, die die Daten mit der org.apache.io.compress.SnappyCodec datenkomprimierungsmethode komprimiert. Wenn DATA_COMPRESSION nicht angegeben ist, wird standardmäßig keine Komprimierung.  
  
```  
CREATE EXTERNAL FILE FORMAT parquetfile1  
WITH (  
    FORMAT_TYPE = PARQUET,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [Erstellen Sie die externe Tabelle AS SELECT &#40; Transact-SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [Erstellen Sie die Tabelle als SELECT &#40; Azure SQL Datawarehouse &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [sys.external_file_formats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)  
  
  
