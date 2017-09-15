---
title: Datei "Schema.ini" (Text-Datei-Treiber) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- schema.ini file [ODBC]
- text file driver [ODBC], schema.ini file
ms.assetid: 0c4625c4-c730-4984-b430-9051b7bc0451
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 709df0de2e0191c0f03026afdad7b8e9b8480cae
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="schemaini-file-text-file-driver"></a>Datei "Schema.ini" (Text-Datei-Treiber)
Wenn der Text-Treiber verwendet wird, wird das Format der Textdatei mit einer Schema-Informationsdatei bestimmt. Die Schemadatei für die Informationen ist immer mit dem Namen "Schema.ini" und im selben Verzeichnis wie die Textdatenquelle immer beibehalten. Die Schemadatei für die Informationen enthält die IISAM mit Informationen über das allgemeine Format der Datei, den Spaltennamen und Datentypinformationen und mehrere andere Datenmerkmale. Datei "Schema.ini" ist immer erforderlich, für den Zugriff auf Daten fester Länge. Sie sollten die Datei "Schema.ini" verwenden, wenn Ihre Texttabelle enthält, DateTime, Währung oder Dezimaldaten oder jedes Mal, wenn Sie mehr Kontrolle über die Behandlung der Daten in der Tabelle werden soll.  
  
> [!NOTE]  
>  Aus der Registrierung und nicht von "Schema.ini" Text-ISAM Anfangswerte abgerufen. Das gleiche Standard-Dateiformat gilt für alle neuen Datentabellen von Text. Alle Dateien, die von der CREATE TABLE-Anweisung erstellt wurden, erben die gleichen Format Standardwerte, die festgelegt werden, durch Auswählen der Datei Formatierung von Werten in der **Textformat definieren** Dialogfeld mit \<Standardwert > in der ausgewähltwurde** Tabellen** Liste. Wenn die Werte in der Registrierung von den Werten in Schema.ini unterscheiden zu können, werden die Werte in der Registrierung durch die Werte aus "Schema.ini" überschrieben.  
  
## <a name="understanding-schemaini-files"></a>Grundlegendes zu Schema.ini-Dateien  
 Schema.ini-Dateien bieten Schemainformationen zu den Datensätzen in einer Textdatei. Jeder Eintrag Schema.ini gibt einen von fünf Eigenschaften der Tabelle:  
  
-   Den Namen der Textdatei  
  
-   Das Dateiformat  
  
-   Die Feldnamen, Breite und Typen  
  
-   Der Zeichensatz  
  
-   Spezielle Konvertierung von Datentypen  
  
 Den folgenden Abschnitten werden diese Eigenschaften.  
  
## <a name="specifying-the-file-name"></a>Namen der Datei angeben  
 Der erste Eintrag in Schema.ini ist immer der Name der Quelltextdatei in eckige Klammern eingeschlossen. Das folgende Beispiel veranschaulicht den Eintrag für die Datei "Sample.txt":  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>Das Dateiformat angeben  
 Die **Format** -Option in Schema.ini gibt das Format der Textdatei an. Der Text-IISAM können das Format automatisch die meisten Zeichen getrennte Dateien gelesen werden. Sie können jedem beliebigen einzelnes Zeichen als Trennzeichen in der Datei außer einem doppelten Anführungszeichen (") verwenden. Die **Format** in Schema.ini überschreibt die Einstellung in der Windows-Registrierung Datei. Die folgende Tabelle enthält die gültigen Werte für die **Format** Option.  
  
|Formatbezeichner|Tabellenformat|"Schema.ini" Format-Anweisung|  
|----------------------|------------------|---------------------------------|  
|**Tabstopp-getrennt**|Felder in der Datei werden durch Registerkarten getrennt.|Format = TabDelimited|  
|**Als Trennzeichen für CSV**|Felder in der Datei werden durch Kommas (mit kommagetrennten Werten) getrennt.|Format = CSVDelimited|  
|**Als Trennzeichen für benutzerdefinierte**|Felder in der Datei werden von einem Zeichen getrennt, die Sie auswählen, geben Sie in das Dialogfeld. Alle außer das doppelte Anführungszeichen (") sind zulässig, einschließlich leer.|Format = mit Trennzeichen (*benutzerdefinierte Zeichen*)<br /><br /> -oder-<br /><br /> Ohne Trennzeichen angegeben werden:<br /><br /> Format = mit Trennzeichen)|  
|**Fester Länge**|Felder in der Datei sind eine feste Länge.|Format = FixedLength|  
  
## <a name="specifying-the-fields"></a>Die Felder angeben  
 Sie können die Feldnamen in einer Zeichen getrennte Textdatei auf zwei Arten angeben:  
  
-   Die Feldnamen in der ersten Zeile der Tabelle enthalten, und legen Sie **ColNameHeader** zu **"true".**  
  
-   Geben Sie jede Spalte nach Anzahl und festzulegen Sie der Spalte Name und Datentyp.  
  
 Sie müssen jede Spalte nach Anzahl angeben und Festlegen der Spaltenname, Datentyp und Breite für Dateien mit fester Länge.  
  
> [!NOTE]  
>  Die **ColNameHeader** Schema.ini Außerkraftsetzungen Festlegen der **FirstRowHasNames** in der Windows-Registrierung Datei festlegen.  
  
 Die Datentypen der Felder können auch ermittelt werden. Verwenden der **MaxScanRows** Option, um anzugeben, wie viele Zeilen gescannt werden sollen, wenn die Spaltentypen bestimmt. Wenn Sie festlegen, **MaxScanRows** 0 ist, wird die gesamte Datei überprüft. Die **MaxScanRows** in Schema.ini überschreibt die Einstellung in der Windows-Registrierung Datei.  
  
 Der folgende Eintrag gibt an, dass Microsoft Jet die Daten in der ersten Zeile der Tabelle verwenden sollten, um Feldnamen zu bestimmen, und untersuchen Sie die gesamte Datei, um zu bestimmen, die Daten sollten Typen verwendet:  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 Die nächste Eintrag kennzeichnet Felder in einer Tabelle mit der Nummer der Spalte (**Col***n*) Option, die für Zeichen getrennte Dateien optional und für Dateien mit fester Länge, die erforderlich ist. Das Beispiel zeigt die Schema.ini Einträge für zwei Felder, einem 10-stelligen "customernumber" besitzen Textfeld und eine 30 Zeichen CustomerName Textfeld:  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 Die Syntax der **Col** * n * ist:  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>Hinweise  
 Die folgende Tabelle beschreibt die einzelnen Bestandteile der **Col** * n * Eintrag.  
  
|Parameter|Description|  
|---------------|-----------------|  
|*Spaltenname*|Der Textname der Spalte. Wenn der Spaltenname Leerzeichen enthält, müssen Sie ihn in doppelte Anführungszeichen setzen.|  
|*type*|Datentypen sind wie folgt aus:<br /><br /> **Microsoft Jet-Datentypen**<br /><br /> bit<br /><br /> Byte<br /><br /> Short<br /><br /> Long<br /><br /> Währung<br /><br /> Single<br /><br /> Double<br /><br /> DateTime<br /><br /> Text<br /><br /> Memo<br /><br /> **ODBC-Datentypen** Char (identisch mit Text)<br /><br /> "Float" (identisch mit Double)<br /><br /> Ganze Zahl (identisch mit Short)<br /><br /> LongChar (identisch mit Memo)<br /><br /> Datum *Datumsformat*|  
|**Breite**|Der Wert des Literals `Width`. Gibt an, dass die folgende Anzahl legt die Breite der Spalte fest (optional für Zeichen getrennte Dateien; für Dateien mit fester Länge erforderlich).|  
|*#*|Der ganzzahlige Wert, der die Breite der Spalte bestimmt (erforderlich, wenn **Breite** angegeben ist).|  
  
## <a name="selecting-a-character-set"></a>Auswählen eines Zeichensatzes  
 Sie können auswählen, aus zwei Zeichen: ANSI- und OEM. Die **CharacterSet** in Schema.ini überschreibt die Einstellung in der Windows-Registrierung Datei. Das folgende Beispiel zeigt den Schema.ini-Eintrag, der den Zeichensatz in ANSI festlegt:  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>Angeben von Datenformaten-Typ und Konvertierungen  
 Die Datei Schema.ini enthält mehrere Optionen, die Sie verwenden können, um anzugeben, wie Daten konvertiert oder angezeigt werden. Die folgende Tabelle enthält jede dieser Optionen.  
  
|Option|Description|  
|------------|-----------------|  
|**DateTimeFormat**|Kann auf eine Formatzeichenfolge festgelegt werden, die Datums- und Uhrzeitangaben angibt. Dieser Eintrag sollte angegeben werden, wenn alle Datum/Uhrzeit-Felder in den Import-/Export mit dem gleichen Format behandelt werden. Alle Microsoft Jet-Formate außer Uhr und Uhr. werden unterstützt. Ist keine Formatzeichenfolge, werden die Optionen für das kurze Datum Windows-Systemsteuerung der Bild und die Uhrzeit verwendet.|  
|**DecimalSymbol**|Kann auf jedem beliebigen einzelnen Zeichen festgelegt werden, die verwendet wird, um die ganze Zahl von der Bruchteil einer Zahl zu trennen.|  
|**NumberDigits**|Gibt die Anzahl von Dezimalstellen in der Bruchteil einer Zahl an.|  
|**NumberLeadingZeros**|Gibt an, ob ein decimal-Wert kleiner als 1 und mehr als – 1 führende Nullen enthalten soll. Dieser Wert kann entweder "false" (ohne führenden Nullen) oder "true".|  
|**CurrencySymbol**|Gibt an, das Währungssymbol ein, das für die Currency-Werte in der Textdatei verwendet werden kann. Beispiele sind das Dollarzeichen ($) und Data Mining.|  
|**CurrencyPosFormat**|Kann auf eine der folgenden Werte festgelegt werden:<br /><br /> -Currency Symbol-Präfix und keine Trennung ($1)<br />-Currency Symbol Suffix mit keine Trennung (1$)<br />-Currency Symbol Präfix mit einem Zeichen getrenntem ($ 1)<br />-Currency Symbol Suffix mit einem Zeichen getrenntem (1 $)|  
|**CurrencyDigits**|Gibt die Anzahl von Ziffern für den Bruchteil der einen Währungswert.|  
|**CurrencyNegFormat**|Folgende Werte sind möglich:<br /><br /> -   ($1)<br />-   –$1<br />-   $–1<br />-   $1–<br />-   (1$)<br />-   –1$<br />-   1–$<br />-   1$–<br />-   –1 $<br />-   –$ 1<br />-   1 $–<br />-   $ 1–<br />-   $ –1<br />-   1– $<br />-   ($ 1)<br />-   (1 $)<br /><br /> Dieses Beispiel zeigt das Dollarzeichen, aber Sie sollten mit dem entsprechenden ersetzen **CurrencySymbol** Wert in der aktuellen Anwendung.|  
|**CurrencyThousandSymbol**|Gibt an, das Einzelzeichen-Symbol, das zur Trennung von Währungswerten in der Textdatei von Tausenden verwendet werden kann.|  
|**CurrencyDecimalSymbol**|Kann auf jedem beliebigen einzelnen Zeichen festgelegt werden, die verwendet wird, um die gesamte von den Bruchteil der einen Währungswert zu trennen.|  
  
> [!NOTE]  
>  Wenn Sie einen Eintrag weglassen, wird der Standardwert in der Windows-Systemsteuerung verwendet.
