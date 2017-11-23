---
title: CAST und CONVERT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/08/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CAST_TSQL
- CONVERT_TSQL
- CAST
- CONVERT
dev_langs: TSQL
helpviewer_keywords:
- CAST function
- automatic data type conversion
- varbinary data type
- CONVERT function
- data types [SQL Server], converting
- large value data types
- implicit data type conversions
- image data type, converting
- explicit data type conversions [SQL Server]
- binary [SQL Server], converting
- text data type, converting
- date and time [SQL Server], cast and convert
- truncating conversions
- converting data types [SQL Server], conversion functions
- time zones [SQL Server]
- roundtrip conversions
ms.assetid: a87d0850-c670-4720-9ad5-6f5a22343ea8
caps.latest.revision: "136"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: dd3db7627c4190a51db01082138677bc2b6d40d9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="cast-and-convert-transact-sql"></a>CAST und CONVERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Konvertiert einen Ausdruck von einem Datentyp in einen anderen.  
In den folgenden Beispielen werden z. B. dem Eingabedatentyp in zwei andere Datentypen mit anderen Genauigkeitsgraden ändern.
```sql  
SELECT 9.5 AS Original, CAST(9.5 AS int) AS int, 
    CAST(9.5 AS decimal(6,4)) AS decimal;
SELECT 9.5 AS Original, CONVERT(int, 9.5) AS int, 
    CONVERT(decimal(6,4), 9.5) AS decimal;
```  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
|Original   |int    |decimal |  
|----|----|----|  
|9.5 |9 |9.5000 |  

> [!TIP]
> Viele [Beispiele](#BKMK_examples) finden Sie am Ende dieses Themas.  
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
-- Syntax for CAST:  
CAST ( expression AS data_type [ ( length ) ] )  
  
-- Syntax for CONVERT:  
CONVERT ( data_type [ ( length ) ] , expression [ , style ] )  
```  
  
## <a name="arguments"></a>Argumente  
*expression*  
Ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md).
  
*data_type*  
Der Zieldatentyp. Dies schließt **Xml**, **"bigint"**, und **Sql_variant**. Aliasdatentypen können nicht verwendet werden.
  
*length*  
Eine optionale ganze Zahl, die die Länge des Zieldatentyps angibt. Der Standardwert ist 30.
  
*Stil*  
Ist ein Ganzzahlausdruck, der angibt, wie die CONVERT-Funktion übersetzen *Ausdruck*. Wenn style NULL ist, wird NULL zurückgegeben. Der Bereich richtet sich nach *Data_type*. 
  
## <a name="return-types"></a>Rückgabetypen
Gibt *Ausdruck* übersetzt *Data_type*.

## <a name="date-and-time-styles"></a>Datums- und Uhrzeitformate  
Wenn *Ausdruck* ist ein Datentyp Datum oder Uhrzeit *Stil* kann einen der Werte in der folgenden Tabelle gezeigt. Andere Werte werden als 0 verarbeitet. Beginnend mit [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], die einzigen Formate, die unterstützt werden, beim Konvertieren von Datums- und Uhrzeittypen in **"DateTimeOffset"** sind 0 oder 1. Bei allen anderen Konvertierungsformaten wird der Fehler 9809 zurückgegeben.
  
>  [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt das Datumsformat im arabischem Format, indem der kuwaitische Algorithmus verwendet wird.
  
|Ohne Jahrhundert (JJ) (<sup>1</sup>)|Mit Jahrhundert (jjjj)|Standard|Eingabe/Ausgabe (<sup>3</sup>)|  
|---|---|--|---|
|-|**0** oder **100** (<sup>1</sup><sup>2</sup>)|Standard für datetime und smalldatetime|mon tt jjjj hh:miAM (oder PM)|  
|**1**|**101**|USA|1 = mm/tt/jj<br /> 101 = mm/tt/jjjj|  
|**2**|**102**|ANSI|2 = jj.mm.tt<br /> 102 = jjjj.mm.tt|  
|**3**|**103**|Britisch/Französisch|3 = tt/mm/jj<br /> 103 = tt/mm/jjjj|  
|**4**|**104**|Deutsch|4 = tt.mm.jj<br /> 104 = tt.mm.jjjj|  
|**5**|**105**|Italienisch|5 = tt-mm-jj<br /> 105 = tt-mm-jjjj|  
|**6**|**106** <sup>(1)</sup>|-|6 = tt mon jj<br /> 106 = tt mon jjjj|  
|**7**|**107** <sup>(1)</sup>|-|7 = Mon tt, jj<br /> 107 = Mon tt, jjjj|  
|**8**|**108**|-|hh:mi:ss|  
|-|**9** oder **109** (<sup>1</sup><sup>2</sup>)|Standardwert + Millisekunden|mon tt jjjj hh:mi:ss:mmmAM (oder PM)|  
|**10**|**110**|USA|10 = mm-tt-jj<br /> 110 = mm-tt-jjjj|  
|**11**|**111**|JAPAN|11 = jj/mm/tt<br /> 111 = jjjj/mm/tt|  
|**12**|**112**|ISO|12 = jjmmtt<br /> 112 = jjjjmmtt|  
|-|**13** oder **113** (<sup>1</sup><sup>2</sup>)|Europ. Standard + Millisekunden|tt mon jjjj hh:mi:ss:mmm(24h)|  
|**14**|**114**|-|hh:mi:ss:mmm(24h)|  
|-|**20** oder **120** (<sup>2</sup>)|ODBC kanonisch|jjjj-mm-tt hh:mi:ss(24h)|  
|-|**21** oder **121** (<sup>2</sup>)|ODBC kanonisch (mit Millisekunden) Standard für time, date, datetime2 und datetimeoffset|jjjj-mm-tt hh:mi:ss.mmm(24h)|  
|-|**126** (<sup>4</sup>)|ISO8601|jjjj-mm-ttThh:mi:ss.mmm (keine Leerzeichen)<br /> Hinweis: Wenn der Wert für Millisekunden (mmm) 0 ist, wird der Millisekundenwert nicht angezeigt. Beispielsweise wird der Wert '2012-11-07T18:26:20.000' als '2012-11-07T18:26:20' angezeigt.|  
|-|**127**(<sup>6, 7</sup>)|ISO8601 mit Zeitzone (Z).|jjjj-mm-ttThh:mi:ss.mmmZ (keine Leerzeichen)<br /> Hinweis: Wenn der Wert für Millisekunden (mmm) 0 ist, wird der Millisekundenwert nicht angezeigt. Beispielsweise wird der Wert '2012-11-07T18:26:20.000' als '2012-11-07T18:26:20' angezeigt.|  
|-|**130** (<sup>1,</sup><sup>2</sup>)|Hijri (<sup>5</sup>)|tt mon jjjj hh:mi:ss:mmmAM<br /> In diesem Format entspricht "mon" dem vollständigen Monatsnamen in Form einer Hijri-Unicode-Darstellung mit mehreren Token. Dieser Wert wird nicht ordnungsgemäß in einer standardmäßigen US-Installation von SSMS gerendert.|  
|-|**131** (<sup>2</sup>)|Hijri (<sup>5</sup>)|tt/mm/jjjj hh:mi:ss:mmmAM|  
  
<sup>1</sup> diese Formatwerte geben nicht deterministische Ergebnisse zurück. Dazu gehören alle (jj)-Formate (ohne Jahrhundert) und eine Teilmenge der (jjjj)-Formate (mit Jahrhundert).
  
<sup>2</sup> die Standardwerte (*Stil** *0** oder **100**, **9** oder **109**, **13** oder **113**, **20** oder **120**, und **21** oder **121**) Gibt immer das Jahrhundert (JJJJ) zurück.
  
<sup>3</sup> Eingabe beim Konvertieren in **"DateTime"**; Ausgabe bei der Konvertierung in Zeichendaten.
  
<sup>4</sup> für die XML-Verwendung vorgesehen. Für die Konvertierung von **"DateTime"** oder **Smalldatetime** -Daten in Zeichendaten entspricht das Ausgabeformat ist, wie in der obigen Tabelle beschrieben.
  
<sup>5</sup> Hijri ist ein Kalendersystem mit mehreren Variationen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet den kuwaitischen Algorithmus.
  
> [!IMPORTANT]  
>  Standardmäßig verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bei der Interpretation von zweistelligen Jahresangaben 2049 als Umstellungsjahr. Das zweistellige Jahr 49 wird also als 2049 und das zweistellige Jahr 50 als 1950 interpretiert. Viele Clientanwendungen, z. B. jene auf Grundlage der Automatisierungsobjekte, verwenden als Umstellungsjahr 2030. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Stellt die Option two Digit Year cutoff Konfiguration, die das Umstellungsjahr verwendeten ändert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und ermöglicht eine einheitliche Behandlung der Datumsangaben. Die Verwendung von vierstelligen Jahresangaben wird empfohlen.  
  
<sup>6</sup> nur unterstützt, wenn die Umwandlung von Zeichendaten in **"DateTime"** oder **Smalldatetime**. Wenn Zeichendaten, die nur Zeit- oder nur Komponenten umgewandelt werden die **"DateTime"** oder **Smalldatetime** Datentypen, die nicht angegebene Zeitkomponente festgelegt ist 00:00:00.000 und die nicht angegeben Datumskomponente wird auf 1900-01-01 festgelegt.
  
<sup>7</sup>der optionalen Zeitzone Indikator Z, wird verwendet, um die XML-Zuordnung vereinfachen **"DateTime"** Werte mit Zeitzoneninformationen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **"DateTime"** Werte, die ohne Zeitzone . Z ist der Indikator für die Zeitzone UTC-0. Andere Zeitzonen werden durch einen positiven (+) oder negativen (-) Offset (HH:MM) angegeben. Beispiel: `2006-12-12T23:45:12-08:00`
  
Bei der Konvertierung in Zeichendaten aus **Smalldatetime**, die Stile, die Sekunden Millisekunden oder zeigen diesen Stellen Nullen. Sie können unerwünschte Teile in Datumsangaben abschneiden, beim Konvertieren von **"DateTime"** oder **Smalldatetime** Werte mit einer entsprechenden **Char** oder **Varchar** Länge des Datentyps.
  
Beim Konvertieren in **"DateTimeOffset"** von Zeichendaten mit einer Formatvorlage, die eine Uhrzeit enthält, ist ein Zeitzonenoffset an das Ergebnis angehängt.
  
## <a name="float-and-real-styles"></a>float- und Real-Formate
Wenn *Ausdruck* ist **"float"** oder **echte**, *Stil* kann einen der Werte in der folgenden Tabelle gezeigt. Andere Werte werden als 0 verarbeitet.
  
|Wert|Ausgabe|  
|---|---|
|**0** (Standardwert)|Maximal 6 Ziffern. Wird ggf. in der wissenschaftlichen Schreibweise verwendet.|  
|**1**|Immer 8 Ziffern. Wird immer in der wissenschaftlichen Schreibweise verwendet.|  
|**2**|Immer 16 Ziffern. Wird immer in der wissenschaftlichen Schreibweise verwendet.|  
|**3**|Immer 17 Ziffern. Verwenden Sie für die verlustfreie Konvertierung. In diesem Format wird jedes distinct "float" oder den echten Wert garantiert in eine unterschiedliche Zeichenfolge zu konvertieren.<br /> **Gilt für:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], und starten [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].|  
|**126, 128, 129**|Aufgenommen zur Kompatibilität mit Legacykomponenten, in zukünftigen Versionen möglicherweise als veraltet markiert.|  
  
## <a name="money-and-smallmoney-styles"></a>Money und Smallmoney-Formate
Wenn *Ausdruck* ist **Money** oder **Smallmoney**, *Stil* kann einen der Werte in der folgenden Tabelle gezeigt. Andere Werte werden als 0 verarbeitet.
  
|Wert|Ausgabe|  
|---|---|
|**0** (Standardwert)|Links vom Dezimaltrennzeichen werden keine Tausendertrennzeichen eingefügt, rechts vom Dezimaltrennzeichen stehen zwei Ziffern; z. B. 4235,98.|  
|**1**|Links vom Dezimaltrennzeichen werden Tausendertrennzeichen eingefügt, rechts vom Dezimaltrennzeichen stehen zwei Ziffern; z. B. 3.510,92.|  
|**2**|Links vom Dezimaltrennzeichen werden keine Tausendertrennzeichen eingefügt, rechts vom Dezimaltrennzeichen stehen vier Ziffern; z. B. 4235,9819.|  
|**126**|Entspricht Format 2 bei der Konvertierung in char(n) oder varchar(n).|  
  
## <a name="xml-styles"></a>XML-Formate
Wenn *Ausdruck* ist **Xml***, Stil* kann einen der Werte in der folgenden Tabelle gezeigt. Andere Werte werden als 0 verarbeitet.
  
|Wert|Ausgabe|  
|---|---|
|**0** (Standardwert)|Verwenden Sie das Standardanalyseverhalten, bei dem bedeutungslose Leerzeichen verworfen werden und interne DTD-Teilmengen nicht zulässig sind.<br /> **Hinweis:** beim Konvertieren in die **Xml** Datentyp [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht signifikanter Leerraum anders behandelt als in XML 1.0. Weitere Informationen finden Sie unter [erstellen Sie Instanzen der XML-Daten](../../relational-databases/xml/create-instances-of-xml-data.md).|  
|**1**|Bedeutungslose Leerzeichen erhalten. Diese Einstellung legt den Standardwert **XML: Space** Behandlung so verhält wie **XML: space = "preserve"** stattdessen angegeben wurde.|  
|**2**|Begrenzte interne DTD-Teilmengenverarbeitung aktivieren.<br /><br /> Falls aktiviert, kann der Server die folgenden Informationen, die in einer internen DTD-Teilmenge bereitgestellt werden, zur Ausführung von Analysevorgängen ohne Überprüfungscharakter verwenden.<br /> -Standardwerte für Attribute angewendet werden.<br /> – Interne Entitätsverweise werden aufgelöst und erweitert.<br /> -Die DTD-Inhaltsmodell wird auf seine syntaktische Richtigkeit überprüft.<br /> Der Parser ignoriert externe DTD-Teilmengen. Er nimmt auch keine Auswertung der XML-Deklaration, um festzustellen, ob die **eigenständigen** -Attribut festgelegt ist **Ja** oder **keine**, aber stattdessen analysiert die XML-Instanz, als wäre sie eine eigenständige Dokument.|  
|**3**|Bedeutungslose Leerzeichen erhalten und die Verarbeitung begrenzter interner DTD-Teilmengen aktivieren.|  
  
## <a name="binary-styles"></a>Binäre Formate
Wenn *Ausdruck* ist **Binary**, **varbinary**, **char**, oder **varchar**, *Stil* kann einen der Werte in der folgenden Tabelle gezeigt. Bei Formatwerten, die nicht in der Tabelle aufgelistet sind, wird ein Fehler zurückgegeben.
  
|Wert|Ausgabe|  
|---|---|
|**0** (Standardwert)|Übersetzt ASCII-Zeichen in binäre Bytes bzw. binäre Bytes in ASCII-Zeichen. Jedes Zeichen bzw. Byte wird 1:1 konvertiert.<br /> Wenn die *Data_type* ist ein binärer Typ ist, die Zeichen 0 X auf der linken Seite des Ergebnisses hinzugefügt werden.|  
|**1**, **2**|Wenn die *Data_type* ein binärer Typ ist, wird der Ausdruck muss einen Zeichenausdruck sein. Die *Ausdruck* muss einer geraden Anzahl von Hexadezimalziffern zusammengesetzt sein (0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F, a, b, c, d, e, f). Wenn die *Stil* auf 1 festgelegt den Zeichen 0 X muss die ersten beiden Zeichen im Ausdruck. Wenn der Ausdruck eine ungerade Anzahl an Zeichen oder ein ungültiges Zeichen enthält, wird ein Fehler ausgelöst.<br /> Wenn die Länge des konvertierten Ausdrucks größer als die Länge des ist die *Data_type* das Ergebnis rechts abgeschnitten wird.<br /> Fester Länge *Data_types* , sind größer als das konvertierte Ergebnis Nullen rechts des Ergebnisses hinzugefügt wurde.<br /> Wenn data_type ein Zeichentyp ist, muss der Ausdruck ein binärer Ausdruck sein. Jedes Binärzeichen wird in zwei Hexadezimalzeichen konvertiert. Wenn die Länge des konvertierten Ausdrucks größer als die *Data_type* Länge, es rechts abgeschnitten.<br /> Wenn die *Data_type* ist ein Zeichentyp mit fester und die Länge des konvertierten Ergebnisses kleiner als die Länge von der *Data_type*; Leerzeichen rechts neben der konvertierte Ausdruck, um eine noch verwalten hinzugefügt werden die Anzahl von hexadezimalen Ziffern.<br /> Die Zeichen 0 X links neben dem konvertierten Ergebnis für hinzugefügt *Stil* 1.|  
  
## <a name="implicit-conversions"></a>Implizite Konvertierungen
Implizite Konvertierungen sind Konvertierungen, die ohne Angabe der CAST- oder CONVERT-Funktion durchgeführt werden. Explizite Konvertierungen sind Konvertierungen, die die Angabe der CAST- oder CONVERT-Funktion erfordern. In der folgenden Abbildung werden alle expliziten und impliziten Datentypkonvertierungen aufgeführt, die für die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-System bereitgestellten Datentypen zulässig sind. Dazu gehören **Xml**, **"bigint"**, und **Sql_variant**. Es gibt keine implizite Konvertierung bei der Zuweisung vom der **Sql_variant** -Datentyp, aber es die implizite Konvertierung in ist **Sql_variant**.
  
> [!TIP]  
>  Dieses Diagramm ist als herunterladbare PDF-Datei an die [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=35834).  
  
![Datentyp-Konvertierungstabelle](../../t-sql/data-types/media/lrdatahd.png "Datentyp-Konvertierungstabelle")
  
Bei der Konvertierung zwischen **"DateTimeOffset"** und den Zeichentypen **Char**, **Varchar**, **Nchar**, und **Nvarchar**  konvertierte Zeitzone offsetteil muss immer zwei Ziffern für sowohl für HH als auch für MM beispielsweise-08: 00.
  
> [!NOTE]  
>  Da Unicode-Daten immer eine gerade Anzahl von Bytes verwenden, seien Sie bei der Konvertierung **binäre** oder **Varbinary** in oder aus Unicode-Datentypen. Die folgende Konvertierung gibt z. B. nicht den Hexadezimalwert 41, sondern 4100 zurück: `SELECT CAST(CAST(0x41 AS nvarchar) AS varbinary)`.  
  
## <a name="large-value-data-types"></a>Datentypen mit umfangreichen Werten 
Datentypen mit umfangreichen Werten zeigen das gleiche implizite und explizite Konvertierungsverhalten wie ihre kleineren Gegenstücke, insbesondere die **Varchar**, **Nvarchar** und **Varbinary**-Datentypen. Sie sollten jedoch die folgenden Richtlinien beachten:
-   Konvertierung von **Image** auf **varbinary(max)** und umgekehrt ist eine implizite Konvertierung und daher sind Konvertierungen zwischen **Text** und **varchar(max)**, und **Ntext** und **nvarchar(max)**.  
-   Konvertierung von Datentypen mit umfangreichen Werten Typen, z. B. **varchar(max)**in einen entsprechenden kleineren Datentyp, wie z. B. **Varchar**, ist eine implizite Konvertierung, aber abgeschnitten, wenn der große Wert zu groß für die angegebene Länge des kleineren Datentyps.  
-   Konvertierung von **Varchar**, **Nvarchar**, oder **Varbinary** auf ihre entsprechenden Datentypen mit umfangreichen Werten wird implizit ausgeführt.  
-   Konvertierung von der **Sql_variant** -Datentyp, um die Datentypen mit umfangreichen Werten ist eine explizite Konvertierung.  
-   Datentypen mit umfangreichen Werten können nicht konvertiert werden, um die **Sql_variant** -Datentyp.  
  
Weitere Informationen zum Konvertieren von der **Xml** -Datentyp, finden Sie unter [erstellen Sie Instanzen der XML-Daten](../../relational-databases/xml/create-instances-of-xml-data.md).
  
## <a name="xml-data-type"></a>xml-Datentyp
Wenn Sie explizit oder implizit umgewandelt der **Xml** Datentyp eine Zeichenfolge oder binary-Datentyp, den Inhalt der **Xml** Datentyp basierend auf einem Satz von Regeln serialisiert wird. Informationen zu diesen Regeln finden Sie unter [definieren die Serialisierung von XML-Daten](../../relational-databases/xml/define-the-serialization-of-xml-data.md). Informationen zum Konvertieren von anderen Datentypen, die **Xml** -Datentyp, finden Sie unter [erstellen Sie Instanzen der XML-Daten](../../relational-databases/xml/create-instances-of-xml-data.md).
  
## <a name="text-and-image-data-types"></a>Text- und Image-Datentypen
Automatische datentypkonvertierung wird nicht unterstützt, für die **Text** und **Image** -Datentypen. Können Sie explizit konvertieren **Text** Daten, Zeichendaten, und **Image** Daten **binäre** oder **Varbinary**, aber die maximale Länge beträgt 8000 Bytes. Wenn Sie versuchen, eine unzulässige Konvertierung wie z. B. einen Zeichenausdruck konvertieren, der Buchstaben in einem **Int**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird eine Fehlermeldung zurückgegeben.
  
## <a name="output-collation"></a>Ausgabesortierung  
Wenn sowohl die Ausgabe von CAST oder CONVERT als auch die Eingabe eine Zeichenfolge ist, hat die Ausgabe dieselbe Sortierung und Sortierungsbezeichnung wie die Eingabe. Wenn die Eingabe keine Zeichenfolge ist, hat die Ausgabe die Standardsortierung der Datenbank und die Sortierungsbezeichnung coercible-default (Standard erzwingbar). Weitere Informationen finden Sie unter [Rangfolge von Sortierungen &#40; Transact-SQL &#41; ](../../t-sql/statements/collation-precedence-transact-sql.md).
  
Wenn Sie der Ausgabe eine andere Sortierung zuweisen möchten, wenden Sie die COLLATE-Klausel auf den Ergebnisausdruck der CAST- oder CONVERT-Funktion an. Beispiel:
  
`SELECT CAST('abc' AS varchar(5)) COLLATE French_CS_AS`
  
## <a name="truncating-and-rounding-results"></a>Abschneiden und Runden von Ergebnissen
Bei der Konvertierung von Zeichen oder binäre Ausdrücke (**Char**, **Nchar**, **Nvarchar**, **Varchar**, **Binär**, oder **Varbinary**) auf einen Ausdruck, der einen anderen Datentyp, können die Daten abgeschnitten, nur teilweise angezeigt, oder ein Fehler wird zurückgegeben, da das Ergebnis zum Anzeigen zu kurz ist. Konvertierungen in **Char**, **Varchar**, **Nchar**, **Nvarchar**, **binäre**, und  **Varbinary** abgeschnitten werden, mit Ausnahme der in der folgenden Tabelle aufgelisteten Konvertierungen.
  
|Ausgangsdatentyp|Zieldatentyp|Ergebnis|  
|---|---|---|
|**Int**, **"smallint"**, oder **"tinyint"**|**char**|*|  
||**varchar**|*|  
||**nchar**|E|  
||**nvarchar**|E|  
|**Money**, **Smallmoney**, **numerischen**, **decimal**, **"float"**, oder **real**|**char**|E|  
||**varchar**|E|  
||**nchar**|E|  
||**nvarchar**|E|  
  
\*= Ergebnislänge zu kurz angezeigt. E = Error. Es wird ein Fehler zurückgegeben, da die Ergebnislänge zu kurz ist, um angezeigt zu werden.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]garantiert, dass nur reversible Konvertierungen, Konvertierungen, die aus den ursprünglichen Datentyp einen Datentyp zu konvertieren und wieder zurück, die gleichen Werte von Version zu Version erhalten. Im folgenden Beispiel wird eine solche Hin- und Rückkonvertierung veranschaulicht:
  
```sql
DECLARE @myval decimal (5, 2);  
SET @myval = 193.57;  
SELECT CAST(CAST(@myval AS varbinary(20)) AS decimal(10,5));  
-- Or, using CONVERT  
SELECT CONVERT(decimal(10,5), CONVERT(varbinary(20), @myval));  
```  
  
> [!NOTE]  
>  Versuchen Sie nicht zum Erstellen **binäre** Werte und diese dann in einen Datentyp der numerischen Datentypkategorie zu konvertieren. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]garantiert nicht, dass das Ergebnis einer **decimal** oder **numerischen** datentypkonvertierung zu **binäre** identisch zwischen verschiedenen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Im folgenden Beispiel ist der resultierende Ausdruck zu klein, um angezeigt zu werden.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName, SUBSTRING(p.Title, 1, 25) AS Title,
    CAST(e.SickLeaveHours AS char(1)) AS [Sick Leave]  
FROM HumanResources.Employee e JOIN Person.Person p 
    ON e.BusinessEntityID = p.BusinessEntityID  
WHERE NOT e.BusinessEntityID >5;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```   
FirstName   LastName      Title   Sick Leave
---------   ------------- ------- --------`
Ken         Sanchez       NULL   *
Terri       Duffy         NULL   *
Roberto     Tamburello    NULL   *
Rob         Walters       NULL   *
Gail        Erickson      Ms.    *
(5 row(s) affected)  
```
  
Beim Konvertieren von Datentypen mit unterschiedlichen Dezimalstellen wird der Ergebniswert manchmal abgeschnitten und manchmal gerundet. In der folgenden Tabelle wird das Verhaltensmuster veranschaulicht.
  
|Von|Aktion|Verhalten|  
|---|---|---|
|**numeric**|**numeric**|Round|  
|**numeric**|**int**|Abschneiden|  
|**numeric**|**money**|Round|  
|**money**|**int**|Round|  
|**money**|**numeric**|Round|  
|**float**|**int**|Abschneiden|  
|**float**|**numeric**|Round<br /><br /> Konvertierung von **"float"** Werte, die wissenschaftliche für Schreibweise **decimal** oder **numerischen** auf den Werten der Genauigkeit von 17 Stellen beschränkt. Alle Werte mit einer Genauigkeit von mehr als 17 Stellen werden auf Null gerundet.|  
|**float**|**datetime**|Round|  
|**datetime**|**int**|Round|  
  
Beispielsweise können Werte 10.6496 "und"-10.6496 abgeschnitten oder gerundet, während der Konvertierung in **Int** oder **numerischen** Typen:
  
```sql
SELECT  CAST(10.6496 AS int) as trunc1,
         CAST(-10.6496 AS int) as trunc2,
         CAST(10.6496 AS numeric) as round1,
         CAST(-10.6496 AS numeric) as round2;
 ```
Die Ergebnisse der Abfrage werden in der folgenden Tabelle angezeigt:
 
|trunc1|trunc2|round1|round2|
|---|---|---|---|
|10|-10|11|-11|
 
Falls eine Konvertierung von Datentypen vorgenommen wird, bei der der Zieldatentyp weniger Dezimalstellen hat als der Quelldatentyp, wird der Wert abgeschnitten. Das Ergebnis der Konvertierung im folgenden Beispiel ist `$10.3497`:
  
`SELECT CAST(10.3496847 AS money);`
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Gibt eine Fehlermeldung angezeigt, wenn nicht numerische **Char**, **Nchar**, **Varchar**, oder **Nvarchar** Daten konvertiert **Int** , **"float"**, **numerischen**, oder **decimal**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gibt auch einen Fehler, wenn eine leere Zeichenfolge ("") konvertiert **numerischen** oder **decimal**.
  
## <a name="certain-datetime-conversions-are-nondeterministic"></a>Bestimmte Datetime-Konvertierungen sind nicht deterministisch
In der folgenden Tabelle werden die Formate aufgelistet, bei denen die Konvertierung von string in datetime nicht deterministisch ist.
  
|||  
|-|-|  
|Alle Formate unter 100<sup>1</sup>|106|  
|107|109|  
|113|130|  
  
<sup>1</sup> mit Ausnahme der Formate 20 und 21
  
## <a name="supplementary-characters-surrogate-pairs"></a>Ergänzende Zeichen (Ersatzpaare)
Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], bei der Verwendung eines Umwandlungsvorgangs aus ergänzenden Zeichen (SC) Sortierungen **Nchar** oder **Nvarchar** auf eine **Nchar** oder  **Nvarchar** -Typ von geringerer Länge in einem Ersatzzeichenpaar nicht abgeschnitten werden; es vor dem ergänzenden Zeichen abgeschnitten. Im folgenden Codefragment wird `@x` z. B. weggelassen, sodass nur `'ab'` erhalten bleibt. Es ist nicht genügend Platz für das ergänzende Zeichen vorhanden.
  
```sql
DECLARE @x NVARCHAR(10) = 'ab' + NCHAR(0x10000);  
SELECT CAST (@x AS NVARCHAR(3));  
```  
  
Bei SC-Sortierungen entspricht das Verhalten von `CONVERT` dem von `CAST`.
  
## <a name="compatibility-support"></a>Kompatibilitätsunterstützung
In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], das Standardformat für CAST- und CONVERT-Vorgänge auf **Zeit** und **datetime2** Datentypen ist 121, wenn einer der Typen in einem berechneten Spaltenausdruck verwendet wird. Für berechnete Spalten ist das Standardformat 0. Dieses Verhalten wirkt sich auf berechnete Spalten aus, wenn sie erstellt werden und in Abfragen mit automatischer Parametrisierung oder in Einschränkungsdefinitionen verwendet werden.
  
Unter Kompatibilitätsgrad 110 und höher, das Standardformat für CAST- und CONVERT-Vorgänge auf **Zeit** und **datetime2** Datentypen ist immer 121. Basiert die Abfrage auf dem alten Verhalten, verwenden Sie einen Kompatibilitätsgrad unter 110, oder geben Sie in der betroffenen Abfrage explizit das Format 0 an.
  
Ein Upgrade der Datenbank auf Kompatibilitätsgrad 110 und höher ändert keine Benutzerdaten, die auf dem Datenträger gespeichert wurden. Sie müssen diese Daten entsprechend manuell korrigieren. Haben Sie beispielsweise SELECT INFO zum Erstellen einer Tabelle von einer Quelle verwendet, die einen Ausdruck für eine berechnete Spalte (oben beschrieben) beinhaltete, werden die Daten mit dem Format 0 anstelle der Definition der berechneten Spalte an sich gespeichert. Sie müssen diese Daten manuell aktualisieren, um sie an das Format 121 anzupassen.
  
## <a name="BKMK_examples"></a> Beispiele  
  
### <a name="a-using-both-cast-and-convert"></a>A. Verwenden von CAST und CONVERT  
In jedem der Beispiele werden die Namen der Produkte abgerufen, deren Listenpreis mit der Ziffer `3` beginnt. Der `ListPrice`-Wert wird in einen `int`-Wert konvertiert.
  
```sql
-- Use CAST  
USE AdventureWorks2012;  
GO  
SELECT SUBSTRING(Name, 1, 30) AS ProductName, ListPrice  
FROM Production.Product  
WHERE CAST(ListPrice AS int) LIKE '3%';  
GO  
  
-- Use CONVERT.  
USE AdventureWorks2012;  
GO  
SELECT SUBSTRING(Name, 1, 30) AS ProductName, ListPrice  
FROM Production.Product  
WHERE CONVERT(int, ListPrice) LIKE '3%';  
GO  
```  
  
### <a name="b-using-cast-with-arithmetic-operators"></a>B. Verwenden von CAST mit arithmetischen Operatoren  
Im folgenden Beispiel wird eine einzelne Spalte (`Computed`) berechnet. Hierbei wird der Gesamtumsatz des laufenden Jahres (`SalesYTD`) durch den Prozentsatz der Umsatzbeteiligung (`CommissionPCT`) geteilt. Dieses Ergebnis wird in einen `int`-Datentyp konvertiert, nachdem es auf die nächste ganze Zahl gerundet wurde.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT CAST(ROUND(SalesYTD/CommissionPCT, 0) AS int) AS Computed  
FROM Sales.SalesPerson   
WHERE CommissionPCT != 0;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
```  
Computed
------
379753754
346698349
257144242
176493899
281101272
0  
301872549
212623750
298948202
250784119
239246890
101664220
124511336
97688107
(14 row(s) affected)  
```  
  
### <a name="c-using-cast-to-concatenate"></a>C. Verwenden von CAST zur Verkettung  
Im folgende Beispiel werden nicht auf Zeichen basierende Ausdrücke durch Verwenden von CAST verkettet. AdventureWorksDW wird verwendet.
  
```sql
SELECT 'The list price is ' + CAST(ListPrice AS varchar(12)) AS ListPrice  
FROM dbo.DimProduct  
WHERE ListPrice BETWEEN 350.00 AND 400.00;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
ListPrice
------------------------
The list price is 357.06
The list price is 364.09
The list price is 364.09
The list price is 364.09
The list price is 364.09  
```  
  
### <a name="d-using-cast-to-produce-more-readable-text"></a>D. Verwenden von CAST zur Generierung besser lesbaren Texts  
Im folgenden Beispiel wird die Umwandlung in der SELECT-Liste zum Konvertieren der `Name` Spalte eine **char(10)** Spalte. AdventureWorksDW wird verwendet.
  
```sql
SELECT DISTINCT CAST(EnglishProductName AS char(10)) AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE EnglishProductName LIKE 'Long-Sleeve Logo Jersey, M';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Name        UnitPrice
----------  ---------
Long-Sleev  31.2437
Long-Sleev  32.4935
Long-Sleev  49.99  
```  
  
### <a name="e-using-cast-with-the-like-clause"></a>E. Verwenden von CAST mit der LIKE-Klausel  
Im folgenden Beispiel wird die `money`-Spalte `SalesYTD` in eine `int`- und dann in eine `char(20)`-Spalte umgewandelt, damit sie mit der `LIKE`-Klausel verwendet werden kann.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName, s.SalesYTD, s.BusinessEntityID  
FROM Person.Person AS p   
JOIN Sales.SalesPerson AS s   
    ON p.BusinessEntityID = s.BusinessEntityID  
WHERE CAST(CAST(s.SalesYTD AS int) AS char(20)) LIKE '2%';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
FirstName        LastName            SalesYTD         SalesPersonID
---------------- ------------------- ---------------- -------------
Tsvi             Reiter              2811012.7151      279
Syed             Abbas               219088.8836       288
Rachel           Valdez              2241204.0424      289
(3 row(s) affected)  
```
  
### <a name="f-using-convert-or-cast-with-typed-xml"></a>F. Verwenden von CONVERT oder CAST mit typisierter XML  
Im folgenden sind einige Beispiele zur Verwendung in typisiertes XML mithilfe von convert konvertiert die [XML-Datentyp und-Spalten &#40; SQLServer &#41; ](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md).
  
In diesem Beispiel wird eine aus Leerzeichen, Text und Markup bestehende Zeichenfolge in typisierte XML-Daten konvertiert und alle bedeutungslosen Leerzeichen (begrenzender Leerraum zwischen Knoten) entfernt.
  
```sql
CONVERT(XML, '<root><child/></root>')  
```  
  
In diesem Beispiel wird eine ähnliche, aus Leerzeichen, Text und Markup bestehende Zeichenfolge in typisierte XML-Daten konvertiert und alle bedeutungslosen Leerzeichen (begrenzender Leerraum zwischen Knoten) beibehalten.
  
```sql
CONVERT(XML, '<root>          <child/>         </root>', 1)  
```  
  
In diesem Beispiel wird eine aus Leerzeichen, Text und Markup bestehende Zeichenfolge in typisierte XML-Daten umgewandelt:
  
```sql
CAST('<Name><FName>Carol</FName><LName>Elliot</LName></Name>'  AS XML)  
```  
  
Weitere Beispiele finden Sie unter [erstellen Sie Instanzen der XML-Daten](../../relational-databases/xml/create-instances-of-xml-data.md).
  
### <a name="g-using-cast-and-convert-with-datetime-data"></a>G. Verwenden von CAST und CONVERT mit datetime-Daten  
Im folgenden Beispiel werden das aktuelle Datum und die aktuelle Uhrzeit dargestellt. `CAST` wird verwendet, um das aktuelle Datum und die aktuelle Uhrzeit in einen Zeichendatentyp zu ändern. Anschließend wird `CONVERT` verwendet, um das Datum und die Uhrzeit im `ISO 8901`-Format anzuzeigen.
  
```sql
SELECT   
   GETDATE() AS UnconvertedDateTime,  
   CAST(GETDATE() AS nvarchar(30)) AS UsingCast,  
   CONVERT(nvarchar(30), GETDATE(), 126) AS UsingConvertTo_ISO8601  ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedDateTime     UsingCast              UsingConvertTo_ISO8601
----------------------- ---------------------- ------------------------------
2006-04-18 09:58:04.570 Apr 18 2006  9:58AM    2006-04-18T09:58:04.570
(1 row(s) affected)  
```
  
Das folgende Beispiel entspricht in etwa der Umkehrung des vorherigen Beispiels. In dem Beispiel werden ein Datum und eine Uhrzeit als Zeichendaten angezeigt, und `CAST` wird verwendet, um die Zeichendaten in `datetime`-Datentypen zu ändern. Anschließend wird `CONVERT` verwendet, um die Zeichendaten in den `datetime`-Datentyp zu ändern.
  
```sql
SELECT   
   '2006-04-25T15:50:59.997' AS UnconvertedText,  
   CAST('2006-04-25T15:50:59.997' AS datetime) AS UsingCast,  
   CONVERT(datetime, '2006-04-25T15:50:59.997', 126) AS UsingConvertFrom_ISO8601 ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedText         UsingCast               UsingConvertFrom_ISO8601
----------------------- ----------------------- ------------------------
2006-04-25T15:50:59.997 2006-04-25 15:50:59.997 2006-04-25 15:50:59.997
(1 row(s) affected)  
```
  
### <a name="h-using-convert-with-binary-and-character-data"></a>H. Verwenden von CONVERT mit Binär- und Zeichendaten  
Die folgenden Beispiele zeigen die Ergebnisse der Konvertierung von Binär- und Zeichendaten mit verschiedenen Formaten.
  
```sql
--Convert the binary value 0x4E616d65 to a character value.  
SELECT CONVERT(char(8), 0x4E616d65, 0) AS [Style 0, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 0, binary to character
----------------------------
Name  
(1 row(s) affected)  
```
 
Das folgende Beispiel zeigt, wie Stil 1 kann das Ergebnis abgeschnitten wird erzwungen. Das Abschneiden wird durch einschließlich die Zeichen 0 X in das Ergebnis verursacht.  
```sql  
SELECT CONVERT(char(8), 0x4E616d65, 1) AS [Style 1, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 1, binary to character
------------------------------
0x4E616D
(1 row(s) affected)  
```  
 
Das folgende Beispiel zeigt, dass die Formatvorlage 2 nicht das Ergebnis da truncate die Zeichen 0 X nicht im Resultset enthalten sind.  
```sql  
SELECT CONVERT(char(8), 0x4E616d65, 2) AS [Style 2, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 2, binary to character
------------------------------
4E616D65
(1 row(s) affected)  
```
  
Den Zeichenwert "Name" in einen Binärwert konvertiert werden.  
```sql
SELECT CONVERT(binary(8), 'Name', 0) AS [Style 0, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 0, character to binary
----------------------------
0x4E616D6500000000
(1 row(s) affected)  
```
  
```sql
SELECT CONVERT(binary(4), '0x4E616D65', 1) AS [Style 1, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 1, character to binary
---------------------------- 
0x4E616D65
(1 row(s) affected)  
```  

```sql
SELECT CONVERT(binary(4), '4E616D65', 2) AS [Style 2, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 2, character to binary  
----------------------------------  
0x4E616D65
(1 row(s) affected)  
```  
  
### <a name="i-converting-date-and-time-data-types"></a>I. Vergleichen von date- und time-Datentypen  
Das folgende Beispiel zeigt die Konvertierung von date-, time- und datetime-Datentypen.
  
```sql
DECLARE @d1 date, @t1 time, @dt1 datetime;  
SET @d1 = GETDATE();  
SET @t1 = GETDATE();  
SET @dt1 = GETDATE();  
SET @d1 = GETDATE();  
-- When converting date to datetime the minutes portion becomes zero.  
SELECT @d1 AS [date], CAST (@d1 AS datetime) AS [date as datetime];  
-- When converting time to datetime the date portion becomes zero   
-- which converts to January 1, 1900.  
SELECT @t1 AS [time], CAST (@t1 AS datetime) AS [time as datetime];  
-- When converting datetime to date or time non-applicable portion is dropped.  
SELECT @dt1 AS [datetime], CAST (@dt1 AS date) AS [datetime as date], 
   CAST (@dt1 AS time) AS [datetime as time];  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="j-using-cast-and-convert"></a>J. Verwenden von CAST und CONVERT  
In diesem Beispiel ruft den Namen des Produkts für diese Produkte mit einem `3` in die erste Ziffer ihrer Listenpreis und konvertiert ihre `ListPrice` auf **Int**. AdventureWorksDW wird verwendet.
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(ListPrice AS int) LIKE '3%';  
```  
  
Dieses Beispiel zeigt die gleiche Abfragen, die mithilfe von CONVERT anstelle von CAST. AdventureWorksDW wird verwendet.
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CONVERT(int, ListPrice) LIKE '3%';  
```  
  
### <a name="k-using-cast-with-arithmetic-operators"></a>K. Verwenden von CAST mit arithmetischen Operatoren  
Im folgende Beispiel wird eine einzelne Spalte durch Dividieren den Einzelpreis des Produkts berechnet (`UnitPrice`) durch den Prozentsatz des Rabatts (`UnitPriceDiscountPct`). Dieses Ergebnis wird in einen `int`-Datentyp konvertiert, nachdem es auf die nächste ganze Zahl gerundet wurde. AdventureWorksDW wird verwendet.
  
```sql
SELECT ProductKey, UnitPrice,UnitPriceDiscountPct,  
       CAST(ROUND (UnitPrice*UnitPriceDiscountPct,0) AS int) AS DiscountPrice  
FROM dbo.FactResellerSales  
WHERE SalesOrderNumber = 'SO47355'   
      AND UnitPriceDiscountPct > .02;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
ProductKey  UnitPrice  UnitPriceDiscountPct  DiscountPrice
----------  ---------  --------------------  -------------
323         430.6445   0.05                  22
213         18.5043    0.05                  1
456         37.4950    0.10                  4
456         37.4950    0.10                  4
216         18.5043    0.05                  1  
```  
  
### <a name="l-using-cast-with-the-like-clause"></a>L. Verwenden von CAST mit der LIKE-Klausel  
Das folgende Beispiel konvertiert die **Money** Spalte `ListPrice` auf eine **Int** Typ, und klicken Sie dann auf eine **char(20)** geben, sodass sie mit der LIKE-Klausel verwendet werden kann. AdventureWorksDW wird verwendet.
  
```sql
SELECT EnglishProductName AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(CAST(ListPrice AS int) AS char(20)) LIKE '2%';  
```  
  
### <a name="m-using-cast-and-convert-with-datetime-data"></a>M. Verwenden von CAST und CONVERT mit datetime-Daten  
Das folgende Beispiel zeigt das aktuelle Datum und die Uhrzeit, verwendet Umwandlung in das aktuelle Datum und die Uhrzeit in einen Zeichendatentyp zu ändern, und klicken Sie dann mithilfe von CONVERT Datum und Uhrzeit im ISO 8601-Format anzeigen. AdventureWorksDW wird verwendet.
  
```sql
SELECT TOP(1)  
   SYSDATETIME() AS UnconvertedDateTime,  
   CAST(SYSDATETIME() AS nvarchar(30)) AS UsingCast,  
   CONVERT(nvarchar(30), SYSDATETIME(), 126) AS UsingConvertTo_ISO8601  
FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedDateTime     UsingCast                     UsingConvertTo_ISO8601  
---------------------   ---------------------------   ---------------------------  
07/20/2010 1:44:31 PM   2010-07-20 13:44:31.5879025   2010-07-20T13:44:31.5879025  
```  
  
Das folgende Beispiel entspricht in etwa der Umkehrung des vorherigen Beispiels. Das Beispiel zeigt ein Datum und eine Uhrzeit als Zeichendaten, verwendet CAST so ändern Sie die Zeichendaten in der **"DateTime"** -Datentyp und dann verwendet, zu ändern, die Zeichendaten in konvertiert, die **"DateTime"** -Datentyp. AdventureWorksDW wird verwendet.
  
```sql
SELECT TOP(1)   
   '2010-07-25T13:50:38.544' AS UnconvertedText,  
CAST('2010-07-25T13:50:38.544' AS datetime) AS UsingCast,  
   CONVERT(datetime, '2010-07-25T13:50:38.544', 126) AS UsingConvertFrom_ISO8601  
FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedText         UsingCast               UsingConvertFrom_ISO8601
----------------------- ----------------------- ------------------------
2010-07-25T13:50:38.544 07/25/2010 1:50:38 PM   07/25/2010 1:50:38 PM  
```  
  
## <a name="see-also"></a>Siehe auch
[Datentypkonvertierung &#40; Datenbankmodul &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
[Systemfunktionen &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
[Schreiben internationaler Transact-SQL-Anweisungen](../../relational-databases/collations/write-international-transact-sql-statements.md)
  
