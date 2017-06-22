---
title: "Dialogfeld „Erweiterte Bearbeitung (Bedingung)“ | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/12/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.dmf.condition.advancededit.f1
ms.assetid: a0bbe501-78c5-45ad-9087-965d04855663
caps.latest.revision: 44
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 553e8aece3969407a818d98cf69c20bf922d3601
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="advanced-edit-condition-dialog-box"></a>Dialogfeld 'Erweiterte Bearbeitung (Bedingung)'
  Verwenden Sie das Dialogfeld **Erweiterte Bearbeitung**, um komplexe Ausdrücke für Bedingungen der richtlinienbasierten Verwaltung zu erstellen.  
  
## <a name="options"></a>Optionen  
 **Zellenwert**  
 Zeigt die Funktion oder den Ausdruck an, die bzw. der als Zellenwert verwendet wird, wenn Sie ihn erstellen. Wenn Sie auf **OK**klicken, wird der Zellenwert in der Zelle **Feld** oder **Wert** im Bedingungsausdrucksfeld des Dialogfelds **Neue Bedingung erstellen** oder **Bedingung öffnen** auf der Seite **Allgemein** angezeigt.  
  
 **Funktionen und Eigenschaften**  
 Zeigt die verfügbaren Funktionen und Eigenschaften an.  
  
 **Details**  
 Zeigt die Informationen über die Funktionen und Eigenschaften in folgendem Format an: Funktionssignatur, Funktionsbeschreibung, Rückgabewert und Beispiel.  
  
## <a name="syntax"></a>Syntax  
 Gültige Ausdrücke müssen in folgendem Format vorliegen:  
  
 `{property | function | constant}`  
  
 `{operator}`  
  
 `{property | function | constant}`  
  
## <a name="examples"></a>Beispiele  
 Einige Beispiele für gültige Ausdrücke sind:  
  
-   *Eigenschaft1*> 5  
  
-   *Eigenschaft1*=*Eigenschaft2*  
  
-   Add(5, Multiply(.2,*Eigenschaft1*))<*Eigenschaft2*  
  
-   *Irgendein_Text* IN *Eigenschaft1*  
  
-   *Eigenschaft1*< Fn(*Eigenschaft2*)  
  
-   BitwiseAnd(*Eigenschaft1*,*Eigenschaft2*)= 0  
  
## <a name="additional-function-information"></a>Zusätzliche Funktionsinformationen  
 Die folgenden Abschnitte enthalten zusätzliche Informationen über die Funktionen, die Sie verwenden können, um komplexe Ausdrücke für richtlinienbasierte Verwaltungsbedingungen zu erstellen.  
  
> **WICHTIG!** Für die Funktionen, mit denen Sie richtlinienbasierte Verwaltungsbedingungen erstellen können, wird nicht immer die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Syntax verwendet. Stellen Sie sicher, dass Sie die Beispielsyntax befolgen. Wenn Sie beispielsweise die Funktionen **DateAdd** oder **DatePart** verwenden, müssen Sie das *datepart* -Argument in einfache Anführungszeichen einschließen.  
  
|Funktion|Signatur|Beschreibung|Argumente|Rückgabewert|Beispiel|  
|--------------|---------------|-----------------|---------------|------------------|-------------|  
|**Add()**|Numeric Add (Numeric *Ausdruck1*, Numeric *Ausdruck2*)|Addition zweier Zahlen.|*Ausdruck1* und *Ausdruck2* : Jeder gültige Ausdruck eines beliebigen Datentyps der numerischen Kategorie, mit Ausnahme des Datentyps **bit** . Kann eine Konstante, Eigenschaft oder Funktion sein, die einen numerischen Typ zurückgibt.|Gibt den Datentyp des Arguments zurück, das in der Rangfolge höher eingestuft ist.|`Add(Property1, 5)`|  
|**Array()**|Array Array (VarArgs *Ausdruck*)|Erstellt ein Array aus einer Liste von Werten. Kann mit Aggregatfunktionen, wie z. B. Sum() und Count(), verwendet werden.|*Ausdruck* : Ein Ausdruck, der in ein Array konvertiert wird.|Das Array.|`Array(2,3,4,5,6)`|  
|**Avg()**|Numeric Avg (*VarArgs*)|Gibt den Mittelwert der Werte in der Argumentliste zurück.|*VarArgs* : Eine Liste der Variant-Ausdrücke der genauen numerischen oder ungefähren numerischen Datentypkategorie, mit Ausnahme des **bit** -Datentyps.|Der Rückgabetyp wird durch den Typ des ausgewerteten Ergebnisses des Ausdrucks bestimmt.<br /><br /> Wenn das Ausdrucksergebnis einen Datentyp der Kategorien **integer**, **decimal**, **money** oder **smallmoney**, **float** und **real** aufweist, lauten die Rückgabetypen **int**, **decimal**, **money**bzw. **float**.|`Avg(1.0, 2.0, 3.0, 4.0, 5.0)` gibt in diesem Beispiel `3.0` zurück.|  
|**BitwiseAnd()**|Numeric BitwiseAnd (Numeric *Ausdruck1*, Numeric *Ausdruck2*)|Führt eine bitweise logische AND-Operation zwischen zwei ganzzahligen Werten aus.|*Ausdruck1* und *Ausdruck2* : Jeder gültige Ausdruck eines der Datentypen der Datentypkategorie „integer“.|Gibt den Wert der Datentypkategorie „Integer“ zurück.|`BitwiseAnd(Property1, Property2)`|  
|**BitwiseOr()**|Numeric BitwiseOr (Numeric *Ausdruck1*, Numeric *Ausdruck2*)|Führt eine bitweise logische OR-Operation zwischen zwei angegebenen Integer-Werten durch.|*Ausdruck1* und *Ausdruck2* : Jeder gültige Ausdruck eines der Datentypen der Datentypkategorie „integer“.|Gibt den Wert der Datentypkategorie „Integer“ zurück.|`BitwiseOr(Property1, Property2)`|  
|**Concatenate()**|String Concatenate (String *Zeichenfolge1*, String *Zeichenfolge2*)|Verkettet zwei Zeichenfolgen.|*Zeichenfolge1* und *Zeichenfolge2* : Dies sind die beiden Zeichenfolgen, die Sie verketten möchten. Dabei kann es sich um jede gültige Zeichenfolge ungleich NULL handeln.|Die verkettete Zeichenfolge mit *Zeichenfolge1* gefolgt von *Zeichenfolge2*.|`Concatenate("Hello", " World` `")` gibt „`Hello World`“ zurück.|  
|**Count()**|Numeric Count (*VarArgs*)|Gibt die Anzahl von Elementen in der Argumentliste zurück.|*VarArgs* : Ist ein Ausdruck eines beliebigen Typs mit Ausnahme von **text**, **image**und **ntext**.|Gibt den Wert der Datentypkategorie „Integer“ zurück.|`Count(1.0, 2.0, 3.0, 4.0, 5.0)` gibt in diesem Beispiel `5` zurück.|  
|**DateAdd()**|DateTime DateAdd (String *datepart*, Numeric *Zahl*, DateTime *Datum*)|Gibt einen neuen **datetime** -Wert zurück, der auf dem Hinzufügen eines Intervalls zum angegebenen Datum basiert.|*datepart* : Der Parameter, der angibt, für welchen Teil des Datums ein neuer Wert zurückgegeben werden soll. Einige der unterstützten Typen sind year (yy, yyyy), month (mm, m) und dayofyear (dy, y). Weitere Informationen finden Sie unter [DATEADD &#40;Transact-SQL&#41;](../../t-sql/functions/dateadd-transact-sql.md).<br /><br /> *Zahl*: Der Wert, der zum Inkrementieren von *datepart* verwendet wird.<br /><br /> *Datum* : Ein Ausdruck, der einen **datetime** -Wert oder eine Zeichenfolge in einem Datumsformat zurückgibt.|Ist der neue **datetime** -Wert, der auf dem Hinzufügen eines Intervalls zum angegebenen Datum basiert.|**Example:** `DateAdd('day', 21, DateTime('2007-08-06 14:21:50'))` returns `'2007-08-27 14:21:50'` in this example.<br /><br /> Im Folgenden sind die *dateparts* und Abkürzungen aufgeführt, die von dieser Funktion unterstützt werden:<br /><br /> **year**: yy, yyyy<br /><br /> **month**: mm, m<br /><br /> **dayofyear**: dy, y<br /><br /> **day**: dd, d<br /><br /> **week**: wk, ww<br /><br /> **weekday**: dw, w<br /><br /> **hour**: hh<br /><br /> **minute**: mi, n<br /><br /> **second**: ss, s<br /><br /> **millisecond**: ms|  
|**DatePart()**|Numeric DatePart (String *datepart*, DateTime *Datum*)|Gibt eine ganze Zahl zurück, die den angegebenen *datepart* -Wert des angegebenen Datums darstellt.|*datepart* : Der Parameter, der angibt, welche Datumsteil zurückgegeben werden soll. Einige der unterstützten Typen sind year(yy, yyyy), month(mm, m) und dayofyear (dy, y). Weitere Informationen finden Sie unter [DATEPART &#40;Transact-SQL&#41;](../../t-sql/functions/datepart-transact-sql.md).<br /><br /> *Datum*: Ein Ausdruck, der einen **datetime**-Wert oder eine Zeichenfolge in einem Datumsformat zurückgibt.|Gibt einen Wert der Datentypkategorie „integer“ zurück, der den angegebenen *datepart* -Wert des angegebenen Datums darstellt.|`DatePart('month', DateTime('2007-08-06 14:21:50.620'))` gibt in diesem Beispiel `8` zurück.|  
|**DateTime()**|DateTime DateTime (String *dateString*)|Erstellt einen datetime-Wert aus einer Zeichenfolge.|*dateString* : Der datetime-Wert als Zeichenfolge.|Gibt einen aus der Eingabezeichenfolge erstellten datetime-Wert zurück.|`DateTime('3/12/2006')`|  
|**Divide()**|Numeric Divide (Numeric *Ausdruck_Dividend*, Numeric *Ausdruck_Divisor*)|Dividiert eine Zahl durch eine andere.|*Ausdruck_Dividend* : Der numerische Ausdruck, der geteilt werden soll. Der Dividend kann jeder gültige Ausdruck jedes Datentyps der numerischen Datentypkategorie sein, mit Ausnahme des **datetime** -Datentyps.<br /><br /> *Ausdruck_Divisor* : Der numerische Ausdruck, durch den der Dividend geteilt werden soll. Der Divisor kann jeder gültige Ausdruck jedes Datentyps der numerischen Datentypkategorie sein, mit Ausnahme des **datetime** -Datentyps.|Gibt den Datentyp des Arguments zurück, das in der Rangfolge höher eingestuft ist.|**Beispiel** `Divide(Property1, 2)`<br /><br /> Hinweis: Dies ist ein doppelter Vorgang. Um einen Vergleich mit ganzzahligen Werten vorzunehmen, müssen Sie die Ergebnisse mit `Round()`kombinieren. Beispiel: `Round(Divide(10, 3), 0) = 3`|  
|**Enum()**|Numeric Enum (String *enumTypeName*, String *enumValueName*)|Erstellt einen Enumerationswert aus einer Zeichenfolge.|*enumTypName* : Der Name des enum-Typs.<br /><br /> *enumWertName* : Der Wert der Enumeration.|Gibt den Enumerationswert als numerischen Wert zurück.|`Enum('CompatibilityLevel','Version100')`|  
|**Escape()**|String Escape (String *ZuErsetzendeZeichenfolge*, String *ZeichenfolgeFürEscape*, String *EscapeZeichenfolge*)|Versieht eine Teilzeichenfolge der Eingabezeichenfolge mit einer bestimmten Escapezeichenfolge.|*ZuErsetzendeZeichenfolge* : Die Eingabezeichenfolge.<br /><br /> *ZeichenfolgeFürEscape* : Eine Teilzeichenfolge von *ZuErsetzendeZeichenfolge*. Dies ist die Zeichenfolge, vor der Sie eine Escapezeichenfolge hinzufügen möchten.<br /><br /> *EscapeZeichenfolge* : Die Escapezeichenfolge, die Sie vor jeder Instanz von *ZeichenfolgeFürEscape*hinzufügen müssen.|Gibt einen geänderten *ZuErsetzendeZeichenfolge* -Wert zurück, in dem *EscapeZeichenfolge* jeder Instanz von *ZeichenfolgeFürEscape*vorangestellt ist.|`Escape("Hello", "l", "[")` gibt „`He[l[lo`“ zurück.|  
|**ExecuteSQL()**|Variant ExecuteSQL (String *Rückgabetyp*, String *sqlAbfrage*)|Führt die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfrage auf dem Zielserver aus.<br /><br /> Weitere Informationen zu ExecuteSql() finden Sie unter [ExecuteSql()-Funktion](http://blogs.msdn.com/b/sqlpbm/archive/2008/07/03/executesql.aspx).|*Rückgabetyp* : Gibt den Rückgabetyp der durch die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung zurückgegebenen Daten an. Die gültigen Literale für *Rückgabetyp* sind **Numeric**, **String**, **Bool**, **DateTime**, **Array**und **Guid**.<br /><br /> *sqlAbfrage* : Die Zeichenfolge, die die auszuführende Abfrage enthält.||`ExecuteSQL ('Numeric', 'SELECT COUNT(*) FROM msdb.dbo.sysjobs') <> 0`<br /><br /> Führt eine Transact-SQL-Skalarwertabfrage für eine Zielinstanz von SQL Server aus. In einer `SELECT` -Anweisung kann nur eine Spalte angegeben werden. Zusätzliche Spalten nach der ersten Spalte werden ignoriert. Die resultierende Abfrage sollte nur eine Zeile zurückgeben. Zusätzliche Zeilen nach der ersten Zeile werden ignoriert. Wenn die Abfrage eine leere Menge zurückgibt, wird der für `ExecuteSQL` erstellte Bedingungsausdruck zu false ausgewertet. `ExecuteSql` unterstützt die Auswertungsmodi **Bedarfsgesteuert** und **Nach Zeitplan** .<br /><br /> -`@@ObjectName`:<br />                      Entspricht dem Namensfeld in [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md). Die Variable wird durch den Namen des aktuellen Objekts ersetzt.<br /><br /> -`@@SchemaName`Entspricht dem Namensfeld in [sys.schemas](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md). Die Variable wird durch den Namen des Schemas für das aktuelle Objekt ersetzt, sofern zutreffend.<br /><br /> Hinweis: Kennzeichnen Sie das einfache Anführungszeichen mit einem weiteren einfachen Anführungszeichen, um ein einfaches Anführungszeichen in eine ExecuteSQL-Anweisung aufzunehmen. Um beispielsweise einen Verweis auf einen Benutzer mit dem Namen O'Brian einzuschließen, geben Sie O"Brian ein.|  
|**ExecuteWQL()**|Variant ExecuteWQL (string *Rückgabetyp* , string *Namespace*, string *wql*)|Führt das WQL-Skript für den bereitgestellten Namespace aus. Die Select-Anweisung kann nur eine Rückgabespalte enthalten. Wenn mehr als eine Spalte bereitgestellt wird, wird ein Fehler ausgelöst.|*Rückgabetyp* Gibt den Rückgabetyp der durch die WQL-Abfrage zurückgegebenen Daten an. Die gültigen Literale sind **Numeric**, **String**, **Bool**, **DateTime**, **Array**und **Guid**.<br /><br /> *Namespace* : Der WMI-Namespace, in dem die Abfrage ausgeführt wird.<br /><br /> *wql* : Die Zeichenfolge, die die auszuführende WQL-Abfrage enthält.||`ExecuteWQL('Numeric', 'root\CIMV2', 'select NumberOfProcessors from win32_ComputerSystem') <> 0`|  
|**False()**|Bool False()|Gibt den booleschen Wert FALSE zurück.|Keine|Gibt den booleschen Wert FALSE zurück.|`IsDatabaseMailEnabled = False()`|  
|**GetDate()**|DateTime GetDate()|Gibt das Systemdatum zurück.|Keine|Gibt das Systemdatum als datetime-Wert zurück.|`@DateLastModified = GetDate()`|  
|**Guid()**|Guid Guid(String *guidZeichenfolge*)|Gibt eine GUID aus einer Zeichenfolge zurück.|*guidZeichenfolge* : Die Zeichenfolgendarstellung der zu erstellenden GUID.|Gibt die GUID zurück, die aus der Zeichenfolge erstellt wurde.|`Guid('12340000-0000-3455-0000-000000000454')`|  
|**IsNull()**|Variant IsNull (Variant *Prüfausdruck*, Variant *Ersatzwert*)|Der Wert von *Prüfausdruck* wird zurückgegeben, wenn der Wert nicht NULL ist. Andernfalls wird *Ersatzwert* zurückgegeben. Sind die Typen unterschiedlich, wird *Ersatzwert* implizit in den Typ von *Prüfausdruck*konvertiert.|*Prüfausdruck* : Der Ausdruck, der auf NULL überprüft werden soll. *Prüfausdruck* kann ein beliebiger von der richtlinienbasierten Verwaltung unterstützter Typ sein: Numeric, String, Bool, DateTime, Array und Guid.<br /><br /> *Ersatzwert* : Der Ausdruck, der zurückgegeben werden soll, wenn *Prüfausdruck* NULL ist. *Ersatzwert* muss einen Typ aufweisen, der implizit in den Typ von *Prüfausdruck*konvertiert wird.|Der Rückgabetyp entspricht dem Typ von *Prüfausdruck* , wenn *Prüfausdruck* nicht NULL ist, andernfalls wird der Typ von *Ersatzwert* zurückgegeben.||  
|**Len()**|Numeric Len (*Zeichenfolgenausdruck*)|Gibt die Anzahl von Zeichen des angegebenen Zeichenfolgenausdrucks zurück, jedoch ohne nachfolgende Leerzeichen.|*Zeichenfolgenausdruck* : Der auszuwertende Zeichenfolgenausdruck.|Gibt den Wert der Datentypkategorie „Integer“ zurück.|`Len('Hello')` gibt in diesem Beispiel `5` zurück.|  
|**Lower()**|String Lower (String*_Ausdruck*)|Gibt die Zeichenfolge zurück, nachdem alle Großbuchstaben in Kleinbuchstaben konvertiert wurden.|*Ausdruck* : Der Quellzeichenfolgen-Ausdruck.|Gibt eine Zeichenfolge zurück, die den Quellzeichenfolgen-Ausdruck darstellt, nachdem alle Großbuchstaben in Kleinbuchstaben konvertiert wurden.|`Len('HeLlO')` gibt in diesem Beispiel `'hello'` zurück.|  
|**Mod()**|Numeric Mod (Numeric *Ausdruck_Dividend*, Numeric *Ausdruck_Divisor*)|Stellt den ganzzahligen Rest einer Division des ersten numerischen Ausdrucks durch den zweiten numerischen Ausdruck bereit.|*Ausdruck_Dividend* : Der numerische Ausdruck, der geteilt werden soll. *Ausdruck_Dividend* muss ein gültiger Ausdruck eines Datentyps aus den Datentypkategorien für ganze Zahlen oder numerische Werte sein.<br /><br /> *Ausdruck_Divisor* : Der numerische Ausdruck, durch den der Dividend geteilt werden soll. *Ausdruck_Divisor* muss ein gültiger Ausdruck eines Datentyps aus den Datentypkategorien für ganze Zahlen oder numerische Werte sein.|Gibt den Wert der Datentypkategorie „Integer“ zurück.|`Mod(Property1, 3)`|  
|**Multiply()**|Numeric Multiply (Numeric *Ausdruck1*, Numeric *Ausdruck2*)|Multipliziert zwei Ausdrücke.|*Ausdruck1* und *Ausdruck2* : Jeder gültige Ausdruck eines beliebigen Datentyps der numerischen Kategorie, mit Ausnahme des Datentyps **datetime** .|Gibt den Datentyp des Arguments zurück, das in der Rangfolge höher eingestuft ist.|`Multiply(Property1, .20)`|  
|**Power()**|Numeric Power (Numeric *Numerischer_Ausdruck*, Numeric *Ausdruck_Potenz*)|Gibt den Wert des angegebenen Ausdrucks in der angegebenen Potenz zurück.|*Numerischer_Ausdruck* : Ein Ausdruck der genauen numerischen oder ungefähren numerischen Datentypkategorie, mit Ausnahme des bit-Datentyps.<br /><br /> *Ausdruck_Potenz* : Die Potenz, in die *Numerischer_Ausdruck*erhoben werden soll. *Ausdruck_Potenz* kann ein Ausdruck der genauen numerischen oder ungefähren numerischen Datentypkategorie sein, mit Ausnahme des **bit** -Datentyps.|Der Rückgabetyp entspricht dem Typ von *Numerischer_Ausdruck*.|`Power(Property1, 3)`|  
|**Round()**|Numeric Round (Numeric *Ausdruck*, Numeric *Ausdruck_Genauigkeit*)|Gibt einen numerischen Ausdruck zurück, der auf die angegebene Länge oder Genauigkeit gerundet wurde.|*Ausdruck* : Ein Ausdruck der genauen numerischen oder ungefähren numerischen Datentypkategorie, mit Ausnahme des **bit** -Datentyps.<br /><br /> *Ausdruck_Genauigkeit* : Die Genauigkeit, auf die der Ausdruck gerundet werden soll. Wenn *Ausdruck_Genauigkeit* eine positive Zahl ist, wird *Numerischer_Ausdruck* auf die Anzahl der durch „length“ angegebenen Dezimalstellen gerundet. Wenn *Ausdruck_Genauigkeit* eine negative Zahl ist, wird *Numerischer_Ausdruck* auf der linken Seite des Dezimaltrennzeichens gerundet, wie durch *Ausdruck_Genauigkeit*angegeben.|Gibt denselben Typ wie *Numerischer Ausdruck*zurück.|`Round(5.333, 0)`|  
|**String()**|String String (Variant*_Ausdruck*)|Konvertiert einen Variant-Wert in eine Zeichenfolge.|*Ausdruck* : Der Variant-Ausdruck, der zu einer Zeichenfolge konvertiert werden soll.|Gibt den Zeichenfolgenwert des Variant-Ausdrucks zurück.|`String(4)`|  
|**Sum()**|Numeric Sum (*VarArgs*)|Gibt die Summe aller Werte in der Argumentliste zurück. Sum kann mit numerischen Werten verwendet werden.|*VarArgs*: Eine Liste der Variant-Ausdrücke der genauen numerischen oder ungefähren numerischen Datentypkategorie, mit Ausnahme des **bit** -Datentyps.|Gibt die Summe aller Ausdruckswerte im genauesten Ausdrucksdatentyp zurück.<br /><br /> Wenn das Ausdrucksergebnis einen Datentyp der Kategorien **integer**, **numeric**, **money** oder **smallmoney**, **float** und **real** aufweist, lauten die Rückgabetypen **int**, **numeric**, **money**bzw. **float**;.|`Sum(1.0, 2.0, 3.0, 4.0, 5.0)` gibt in diesem Beispiel `15` zurück.|  
|**True()**|Bool TRUE()|Gibt den booleschen Wert TRUE zurück.||Gibt den booleschen Wert TRUE zurück.|`IsDatabaseMailEnabled = True()`|  
|**Upper()**|String Upper (String*_Ausdruck*)|Gibt die Zeichenfolge zurück, nachdem alle Kleinbuchstaben in Großbuchstaben konvertiert wurden.|*Ausdruck* : Der Quellzeichenfolgen-Ausdruck.|Gibt eine Zeichenfolge zurück, die den Quellzeichenfolgen-Ausdruck darstellt, nachdem alle Kleinbuchstaben in Großbuchstaben konvertiert wurden.|`Upper('HeLlO')` gibt in diesem Beispiel `'HELLO'` zurück.|  
  
## <a name="see-also"></a>Siehe auch  
 [Dialogfeld 'Neue Bedingung erstellen' oder 'Bedingung öffnen', Seite 'Allgemein'](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-general-page.md)   
 [Verwalten von Servern mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  

