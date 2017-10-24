---
title: FORMAT_STRING-Inhalt (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- formats [Analysis Services], string values
- VALUE property
- formats [Analysis Services], numeric values
- FORMATTED_VALUE property
- FORMAT_STRING contents
ms.assetid: c354c938-0328-4b8e-adc5-3b52fd2a7152
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 95d4624aab2e35b3e7ec34963aa33c3af8434eb5
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-cell-properties---formatstring-contents"></a>MDX-Cell Properties - FORMAT_STRING-Inhalt
  Die **FORMAT_STRING** -Zelleigenschaft formatiert die **VALUE** -Zelleigenschaft, indem sie den Wert für die **FORMATTED_VALUE** -Zelleigenschaft erstellt. Die **FORMAT_STRING** -Zelleigenschaft behandelt sowohl Zeichenfolgenwerte als auch numerische Rohdaten, indem sie einen Formatausdruck auf den Wert anwendet, um einen formatierten Wert für die **FORMATTED_VALUE** -Zelleigenschaft zurückzugeben. Die folgenden Tabellen geben die Syntax und die Formatierungszeichen detailliert an, mit denen Zeichenfolgenwerte und numerische Werte behandelt werden.  
  
## <a name="string-values"></a>Zeichenfolgenwerte  
 Ein Formatausdruck für Zeichenfolgen kann aus einem Abschnitt oder aus zwei durch ein Semikolon (;) getrennten Abschnitten bestehen.  
  
|Verwendung|Ergebnis|  
|-----------|------------|  
|Ein Abschnitt|Das Format gilt für alle Zeichenfolgenwerte.|  
|Zwei Abschnitte|Der erste Abschnitt gilt für Zeichenfolgendaten, der zweite Abschnitt für NULL-Werte und leere Zeichenfolgen ("").|  
  
 Die in der folgenden Tabelle beschriebenen Zeichen können in der Formatzeichenfolge für Zeichenfolgen verwendet werden.  
  
|Zeichen|Description|  
|---------------|-----------------|  
|@|Entspricht einem Zeichenplatzhalter, der ein Zeichen oder ein Leerzeichen anzeigt. Steht in der Zeichenfolge ein Zeichen an der Position, an der die Formatzeichenfolge ein @-Zeichen enthält, zeigt die formatierte Zeichenfolge das Zeichen an. Andernfalls zeigt die formatierte Zeichenfolge an dieser Position ein Leerzeichen an. Platzhalter werden von rechts nach links aufgefüllt, es sei denn, die Formatzeichenfolge enthält ein Ausrufezeichen (!).|  
|&|Entspricht einem Zeichenplatzhalter, der ein Zeichen oder nichts anzeigt. Wenn die Zeichenfolge ein Zeichen an der Position des kaufmännischen Und-Zeichens (&) enthält, wird das Zeichen von der formatierten Zeichenfolge angezeigt. Andernfalls zeigt die formatierte Zeichenfolge nichts an. Platzhalter werden von rechts nach links aufgefüllt, es sei denn, die Formatzeichenfolge enthält ein Ausrufezeichen (!).|  
|\<|Erzwingt Kleinbuchstaben. Die formatierte Zeichenfolge zeigt alle Zeichen als Kleinbuchstaben an.|  
|>|Erzwingt Großbuchstaben. Die formatierte Zeichenfolge zeigt alle Zeichen als Großbuchstaben an.|  
|!|Erzwingt das Auffüllen von Platzhaltern von links nach rechts. (Standardmäßig werden Platzhalter von rechts nach links aufgefüllt.)|  
  
## <a name="numeric-values"></a>Numerische Werte  
 Ein benutzerdefinierter Formatausdruck für Zahlen kann ein bis vier Abschnitte enthalten, die durch ein Semikolon (;) getrennt sind. Falls das Formatargument eines der benannten numerischen Formate enthält, ist nur ein Abschnitt zulässig.  
  
|Verwendung|Ergebnis|  
|-----------|------------|  
|Ein Abschnitt|Der Formatausdruck gilt für alle Werte.|  
|Zwei Abschnitte|Der erste Abschnitt gilt für positive Werte und Nullen, der zweite Abschnitt gilt für negative Werte.|  
|Drei Abschnitte|Der erste Abschnitt gilt für positive Werte, der zweite Abschnitt für negative Werte und der dritte Abschnitt für Nullen.|  
|Vier Abschnitte|Der erste Abschnitt gilt für positive Werte, der zweite Abschnitt für negative Werte, der dritte Abschnitt für Nullen und der vierte Abschnitt für NULL-Werte.|  
  
 Das folgende Beispiel hat zwei Abschnitte. Der erste Abschnitt definiert das Format für positive Werte und Nullen, und der zweite Abschnitt definiert das Format für negative Werte.  
  
```  
"$#,##0;($#,##0)"  
```  
  
 Wenn Sie zwei Semikolons ohne etwas dazwischen einfügen, wird der fehlende Abschnitt entsprechend dem Format des positiven Wertes ausgegeben. Das folgende Format zeigt positive und negative Werte mit dem Format im ersten Abschnitt an und zeigt "Zero" an, wenn der Wert null ist:  
  
```  
"$#,##0;;\Z\e\r\o"  
```  
  
 In der folgenden Tabelle sind die Zeichen aufgeführt, die in der Formatzeichenfolge für numerische Formate enthalten sein können.  
  
|Zeichen|Description|  
|---------------|-----------------|  
|InclusionThresholdSetting|Zeigt die Zahl ohne jegliche Formatierung an.|  
|**0**|Entspricht einem Ziffernplatzhalter, der eine Ziffer oder eine Null (0) anzeigt.<br /><br /> Wenn die Zahl an der Stelle, an der in der Formatzeichenfolge die Null vorkommt, eine Ziffer enthält, zeigt der formatierte Wert die Ziffer an. Andernfalls zeigt der formatierte Wert an dieser Position eine Null an.<br /><br /> Hat die Zahl weniger Ziffern als der Formatausdruck Nullen (auf beiden Seiten des Dezimaltrennzeichens), zeigt der formatierte Wert führende oder nachfolgende Nullen an.<br /><br /> Hat die Zahl rechts vom Dezimaltrennzeichen mehr Ziffern, als im Formatausdruck rechts vom Dezimaltrennzeichen Nullen vorkommen, wird der formatierte Wert auf so viele Dezimalstellen gerundet, wie Nullen vorhanden sind.<br /><br /> Hat die Zahl links vom Dezimaltrennzeichen mehr Ziffern, als im Formatausdruck links vom Dezimaltrennzeichen Nullen vorkommen, werden die zusätzlichen Ziffern im formatierten Wert unverändert angezeigt.|  
|**#**|Entspricht einem Ziffernplatzhalter, der eine Ziffer oder nichts anzeigt.<br /><br /> Hat der Ausdruck eine Ziffer an der Stelle, an der in der Formatzeichenfolge das Nummernzeichen (**#**) vorkommt, zeigt der formatierte Wert die Ziffer an. Andernfalls zeigt der formatierte Wert an dieser Position nichts an.<br /><br /> Der Platzhalter Nummernzeichen (**#**) führt zum gleichen Ergebnis wie der Ziffernplatzhalter null (**0**), mit dem einzigen Unterschied, dass keine führenden und nachfolgenden Nullen angezeigt werden, wenn die Zahl ebenso viele oder weniger Ziffern hat, wie **#** -Zeichen in der Formatzeichenfolge auf beiden Seiten des Dezimaltrennzeichens vorhanden sind.|  
|**.**|Entspricht einem Dezimaltrennzeichen, das festlegt, wie viele Ziffern links und rechts vom Dezimaltrennzeichen angezeigt werden.<br /><br /> Wenn der Formatausdruck links vom Punkt (**#**.**) nur Nummernzeichen (**) enthält, beginnen Zahlen, die kleiner sind als 1, mit dem Dezimaltrennzeichen. Sollen Bruchzahlen mit einer führenden Null angezeigt werden, verwenden Sie 0 als ersten Ziffernplatzhalter links vom Dezimaltrennzeichen.<br /><br /> Welches Zeichen tatsächlich als Dezimaltrennzeichen in der formatierten Ausgabe verwendet wird, hängt von dem Zahlenformat ab, das vom Computersystem erkannt wird.<br /><br /> Hinweis: In manchen Gebietsschemas wird ein Komma als Dezimaltrennzeichen verwendet.|  
|**%**|Entspricht einem Prozentwertplatzhalter. Der Ausdruck wird mit 100 multipliziert. Das Prozentzeichen (**%**) wird an der Position eingefügt, an der der Prozentsatz in der Formatzeichenfolge angezeigt wird.|  
|**,**|Entspricht einem Tausendertrennzeichen, das in einer Zahl, die vier oder mehr Stellen links vom Dezimaltrennzeichen hat, die Tausender von den Hundertern trennt.<br /><br /> Die standardmäßige Verwendung des Tausendertrennzeichens wird angegeben, wenn das Format ein Tausendertrennzeichen enthält, das in Ziffernplatzhaltern (**0** oder **#**) eingeschlossen ist.<br /><br /> Zwei benachbarte Tausendertrennzeichen oder ein Tausendertrennzeichen direkt links vom Dezimaltrennzeichen (unabhängig davon, ob ein Dezimaltrennzeichen angegeben ist oder nicht) bedeuten Folgendes: "Die Zahl durch Division durch 1000 skalieren, gegebenenfalls mit Rundung". Sie können z.B. die Formatzeichenfolge „**##0**,,“ verwenden, um 100 Millionen als 100 darzustellen. Zahlen, die kleiner als 1 Million sind, werden als 0 dargestellt. Zwei benachbarte Tausendertrennzeichen in jeder anderen Position als direkt links vom Dezimaltrennzeichen werden so behandelt, als würden sie die Verwendung eines Tausendertrennzeichens angeben.<br /><br /> Welches Zeichen tatsächlich als Tausendertrennzeichen in der formatierten Ausgabe verwendet wird, hängt von dem Zahlenformat ab, das vom Computersystem erkannt wird.<br /><br /> Hinweis: In manchen Gebietsschemas wird der Punkt als Tausendertrennzeichen verwendet.|  
|**:**|Entspricht einem Zeittrennzeichen, das Stunden, Minuten und Sekunden trennt, wenn Zeitwerte formatiert werden.<br /><br /> Hinweis: In manchen Gebietsschemas werden unter Umständen andere Zeichen als Zeittrennzeichen verwendet.<br /><br /> Welches Zeichen tatsächlich als Zeittrennzeichen in der formatierten Ausgabe verwendet wird, hängt von den Systemeinstellungen des Computers ab.|  
|**/**|Entspricht einem Datumstrennzeichen, das den Tag, den Monat und das Jahr trennt, wenn Datumswerte formatiert werden.<br /><br /> Welches Zeichen tatsächlich als Datumstrennzeichen in der formatierten Ausgabe verwendet wird, hängt von den Systemeinstellungen des Computers ab.<br /><br /> Hinweis: In manchen Gebietsschemas werden unter Umständen andere Zeichen als Datumstrennzeichen verwendet.|  
|**E- E+ e- e+**|Entspricht dem wissenschaftlichen Format.<br /><br /> Wenn der Formatausdruck mindestens einen Ziffernplatzhalter (**0** oder **#**) rechts von **E-**, **E+**, **e-**oder **e+**enthält, wird der formatierte Wert im wissenschaftlichen Format angezeigt, und E oder e wird zwischen der Zahl und dem Exponenten der Zahl eingefügt. Die Anzahl der Ziffernplatzhalter auf der rechten Seite bestimmt die Anzahl der Ziffern im Exponenten. Verwenden Sie **E-** oder **e-** , um vor negativen Exponenten ein Minuszeichen einzufügen. Verwenden Sie **E+** oder **e+** , um vor negativen Exponenten ein Minuszeichen und vor positiven Exponenten ein Pluszeichen einzufügen.|  
|**- + $ ( )**|Zeigt ein Literalzeichen an.<br /><br /> Wenn Sie keines der hier aufgelisteten Zeichen, sondern ein anderes Zeichen anzeigen möchten, setzen Sie einen umgekehrten Schrägstrich (**\\**) vor das Zeichen oder schließen das Zeichen in doppelte Anführungszeichen (**" "**) ein.|  
|**\\**|Zeigt das nächste Zeichen in der Formatzeichenfolge an.<br /><br /> Soll ein Zeichen, das eine spezielle Bedeutung hat, als Literalzeichen angezeigt werden, setzen Sie einen umgekehrten Schrägstrich (**\\**) vor das Zeichen. Der umgekehrte Schrägstrich wird nicht angezeigt. Das Verwenden des umgekehrten Schrägstrichs ist gleichbedeutend mit dem Einschließen des nächsten Zeichens in doppelte Anführungszeichen. Um einen umgekehrten Schrägstrich anzuzeigen, verwenden Sie zwei umgekehrte Schrägstriche (**\\\\**). Folgende Zeichen gehören zu den Zeichen, die nicht als Literalzeichen angezeigt werden können:<br /><br /> <br /><br /> Die Zeichen zum Formatieren von Datums- und Zeitangaben:**a**, **c**, **d**, **h**, **m**, **n**, **p**, **q**, **s**, **t**, **w**, **y**, **/**und **:**<br /><br /> Die Zeichen zum Formatieren von Zahlen:**#**, **0**, **%**, **E**, **e**, **Komma**und **Punkt**<br /><br /> Die Zeichen zum Formatieren von Zeichenfolgen:**@**, **&**, **\<**, **>**und **!**|  
|**"ABC"**|Zeigt die Zeichenfolge innerhalb der doppelten Anführungszeichen (**" "**) an.<br /><br /> Um aus Code heraus eine Zeichenfolge in ein Format einzuschließen, schließen Sie den Text mithilfe von Chr(**34**) ein. (Der Zeichencode für ein doppeltes Anführungszeichen ist **34**.)|  
  
### <a name="named-numeric-formats"></a>Benannte numerische Formate  
 Die folgende Tabelle enthält eine Übersicht über die vordefinierten numerischen Formate:  
  
|Formatname|Description|  
|-----------------|-----------------|  
|`General Number`|Zeigt die Zahl ohne Tausendertrennzeichen an.|  
|`Currency`|Zeigt ggf. die Zahl mit einem Tausendertrennzeichen an. Zeigt zwei Ziffern rechts vom Dezimaltrennzeichen an. Die Ausgabe hängt vom verwendeten Systemgebietsschema ab.|  
|`Fixed`|Zeigt mindestens eine Ziffer links und zwei Ziffern rechts vom Dezimaltrennzeichen an.|  
|`Standard`|Zeigt die Zahl mit Tausendertrennzeichen und mindestens einer Ziffer links sowie zwei Ziffern rechts vom Dezimaltrennzeichen an.|  
|`Percent`|Zeigt die mit 100 multiplizierte Zahl mit einem rechts anschließenden Prozentzeichen (%) an. Zeigt immer zwei Ziffern rechts vom Dezimaltrennzeichen an.|  
|`Scientific`|Verwendet standardmäßige wissenschaftliche Notation.|  
|`Yes/No`|Zeigt No an, wenn die Zahl 0 lautet. Andernfalls wird Yes angezeigt.|  
|`True/False`|Zeigt False an, wenn die Zahl 0 lautet. Andernfalls wird True angezeigt.|  
|`On/Off`|Zeigt Off an, wenn die Zahl 0 lautet. Andernfalls wird On angezeigt.|  
  
## <a name="date-values"></a>Datumswerte  
 Die folgende Tabelle identifiziert die Zeichen, die in der Formatzeichenfolge für Datums-/Zeitformate verwendet werden können.  
  
|Zeichen|Description|  
|---------------|-----------------|  
|**:**|Entspricht einem Zeittrennzeichen, das Stunden, Minuten und Sekunden trennt, wenn Zeitwerte formatiert werden.<br /><br /> Welches Zeichen tatsächlich als Zeittrennzeichen in der formatierten Ausgabe verwendet wird, hängt von den Systemeinstellungen des Computers ab.<br /><br /> Hinweis: In manchen Gebietsschemas werden unter Umständen andere Zeichen als Zeittrennzeichen verwendet.|  
|**/**|Entspricht einem Datumstrennzeichen, das den Tag, den Monat und das Jahr trennt, wenn Datumswerte formatiert werden.<br /><br /> Welches Zeichen tatsächlich als Datumstrennzeichen in der formatierten Ausgabe verwendet wird, hängt von den Systemeinstellungen des Computers ab.<br /><br /> Hinweis: In einigen Gebietsschemas werden unter Umständen andere Zeichen als Datumstrennzeichen verwendet.|  
|**C**|Zeigt das Datum als **ddddd** und die Zeit als **ttttt**an, in dieser Reihenfolge.<br /><br /> Zeigt nur Datumsinformationen an, wenn die Datumsseriennummer keine Nachkommastellen enthält. Zeigt nur Zeitinformationen an, wenn kein ganzzahliger Teil vorhanden ist.|  
|**d**|Zeigt den Tag als Zahl ohne führende Null an (1-31).|  
|**dd**|Zeigt den Tag als Zahl mit einer führenden Null an (01-31).|  
|**ddd**|Zeigt den Tag als Abkürzung an (So-Sa).|  
|**dddd**|Zeigt den Tag mit vollem Namen an (Sonntag-Samstag).|  
|**ddddd**|Zeigt das Datum als vollständiges Datum (einschließlich Tag, Monat und Jahr) an, formatiert entsprechend der Systemeinstellung für das kurze Datumsformat.<br /><br /> In Microsoft Windows lautet das standardmäßige kurze Datumsformat **dd.mm.yy**.|  
|**dddddd**|Zeigt eine Datumsseriennummer als vollständiges Datum (einschließlich Tag, Monat und Jahr) an, das entsprechend dem langen Datumsformat formatiert ist, auf das das Computersystem festgelegt ist.<br /><br /> In Windows ist das standardmäßige lange Datumsformat **dddd, d. mmmm yyyy**.|  
|**w**|Zeigt den Wochentag als Zahl an (1 für Sonntag bis 7 für Samstag).|  
|**ww**|Zeigt die Woche des Jahres als Zahl an (1–54).|  
|**m**|Zeigt den Monat als Zahl ohne führende Null an (1-12).<br /><br /> Wenn **m** direkt auf **h** oder **hh**folgt, wird nicht der Monat, sondern die Minute angezeigt.|  
|**mm**|Zeigt den Monat als Zahl mit einer führenden Null an (01–12).<br /><br /> Wenn **m** direkt auf **h** oder **hh**folgt, wird nicht der Monat, sondern die Minute angezeigt.|  
|**mmm**|Zeigt den Monat als Abkürzung an (Jan-Dez).|  
|**mmmm**|Zeigt den Monat als vollständigen Monatsnamen an (Januar-Dezember).|  
|**q**|Zeigt das Quartal des Jahres als Zahl an (1-4).|  
|**y**|Zeigt den Tag des Jahres als Zahl an (1-366).|  
|**yy**|Zeigt das Jahr als zweistellige Zahl an (00-99).|  
|**yyyy**|Zeigt das Jahr als vierstellige Zahl an (100-9999).|  
|**h**|Zeigt die Stunde als Zahl ohne führende Nullen an (0-23).|  
|**hh**|Zeigt die Stunde als Zahl mit führenden Nullen an (00-23).|  
|**n**|Zeigt die Minute als Zahl ohne führende Nullen an (0-59).|  
|**nn**|Zeigt die Minute als Zahl mit führenden Nullen an (00-59).|  
|**s**|Zeigt die Sekunde als Zahl ohne führende Nullen an (0-59).|  
|**ss**|Zeigt die Sekunde als Zahl mit führenden Nullen an (00-59).|  
|**t t t t t**|Zeigt eine Zeit als vollständige Zeit (einschließlich Stunde, Minute und Sekunde) an, wobei die Zeit mit dem Zeittrennzeichen formatiert ist, das durch das Zeitformat definiert ist, das vom Computersystem erkannt wird.<br /><br /> Eine führende Null wird angezeigt, wenn die entsprechende Option ausgewählt und die Uhrzeit früher als 10:00 Uhr (z. B. 09:59) ist. Dies gilt im 12-Stunden-Format für A.M. und P.M.<br /><br /> Das Standardzeitformat in Windows ist **hh:mm:ss**.|  
|**AM/PM**|Zeigt die Großbuchstaben **AM** hinter jeder Stunde ab Mitternacht bis Mittag und die Großbuchstaben **PM** hinter jeder Stunde ab Mittag bis Mitternacht an.<br /><br /> Hinweis: Verwendet ein 12-Stunden-Format.|  
|**am/pm**|Zeigt die Kleinbuchstaben **am** hinter jeder Stunde ab Mitternacht bis Mittag und die Kleinbuchstaben **pm** hinter jeder Stunde ab Mittag bis Mitternacht an.<br /><br /> Hinweis: Verwendet ein 12-Stunden-Format.|  
|**A/P**|Zeigt den Großbuchstaben **A** hinter jeder Stunde ab Mitternacht bis Mittag und den Großbuchstaben **P** hinter jeder Stunde ab Mittag bis Mitternacht an.<br /><br /> Hinweis: Verwendet ein 12-Stunden-Format.|  
|**a/p**|Zeigt den Kleinbuchstaben **a** hinter jeder Stunde ab Mitternacht bis Mittag und den Kleinbuchstaben **p** hinter jeder Stunde ab Mittag bis Mitternacht an.<br /><br /> Hinweis: Verwendet ein 12-Stunden-Format.|  
|**AMPM**|Zeigt entsprechend den Einstellungen des Computersystems das Zeichenfolgenliteral für vormittags (AM) hinter jeder Stunde ab Mitternacht bis Mittag und das Zeichenfolgenliteral für nachmittags (PM) hinter jeder Stunde ab Mittag bis Mitternacht an.<br /><br /> **AMPM** kann in Großbuchstaben oder in Kleinbuchstaben angegeben sein, während die Groß-/Kleinschreibung der angezeigten Zeichenfolge mit der Definition der Zeichenfolge in den Systemeinstellungen des Computers übereinstimmt.<br /><br /> Das Standardformat in Windows ist **AM/PM**.<br /><br /> Hinweis: Verwendet ein 12-Stunden-Format.|  
  
### <a name="named-date-formats"></a>Benannte Datumsformate  
 Die folgende Tabelle enthält eine Übersicht über die vordefinierten Datums- und Zeitformate:  
  
|Formatname|Description|  
|-----------------|-----------------|  
|`General Date`|Zeigt ein Datum und/oder eine Uhrzeit an. Zeigt für reelle Zahlen ein Datum und eine Uhrzeit an (z. B. 4/3/93 05:34 PM). Wenn es keinen Bruchteil gibt, wird nur ein Datum angezeigt (z. B. 4/3/93). Wenn es keinen ganzzahligen Teil gibt, wird nur eine Zeit angezeigt (z. B. 05:34 PM). Das Format der Datumsanzeige wird von den Systemeinstellungen bestimmt.|  
|`Long Date`|Zeigt ein Datum entsprechend dem langen Datumsformat Ihres Systems an.|  
|`Medium Date`|Zeigt ein Datum an, das dem mittleren Datumsformat für die Sprachversion der Hostanwendung entspricht.|  
|`Short Date`|Zeigt ein Datum entsprechend dem kurzen Datumsformat Ihres Systems an.|  
|`Long Time`|Zeigt eine Uhrzeit entsprechend dem langen Zeitformat Ihres Systems an. Dabei werden Stunden, Minuten und Sekunden angezeigt.|  
|`Medium Time`|Zeigt eine Uhrzeit im 12-Stunden-Format mit Stunden und Minuten sowie AM/PM-Unterscheidung an.|  
|`Short Time`|Zeigt eine Uhrzeit im 24-Stunden-Format an (z. B. 17:45).|  
  
## <a name="see-also"></a>Siehe auch  
 [LANGUAGE und FORMAT_STRING für FORMATTED_VALUE](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-formatted-value-property.md)   
 [Verwenden von Zelleigenschaften &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties.md)   
 [Erstellen und Verwenden von Eigenschaftswerten &#40; MDX &#41;](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)   
 [Grundlegendes zu MDX-Abfragen &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  

