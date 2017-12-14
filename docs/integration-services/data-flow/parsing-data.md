---
title: Analysieren von Daten | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parsing [Integration Services]
- data parsing [Integration Services]
ms.assetid: 8893ea9d-634c-4309-b52c-6337222dcb39
caps.latest.revision: "39"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e7d198fce5bdc57a21083ea063522f73cc9dde22
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="parsing-data"></a>Analysieren von Daten
  Mit Datenflüssen in Paketen werden Daten zwischen heterogenen Datenspeichern extrahiert und geladen, die eine Reihe von standardmäßigen und benutzerdefinierten Datentypen verwenden können. In einem Datenfluss werden mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Quellen Daten extrahiert, Zeichenfolgendaten analysiert und Daten in einen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Datentyp konvertiert. Nachfolgende Transformationen können Daten analysieren, um sie in einen anderen Datentyp zu konvertieren oder um Spaltenkopien mit anderen Datentypen zu erstellen. Mit Ausdrücken in Komponenten können außerdem Argumente und Operanden in andere Datentypen umgewandelt werden. Wenn die Daten in einen Datenspeicher geladen werden, kann schließlich das Ziel die Daten analysieren, um sie in einen vom Ziel verwendeten Datentyp zu konvertieren. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="two-types-of-parsing"></a>Zwei Analysetypen  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] stellt zwei Analysemethoden zum Konvertieren von Daten bereit: schnelle Analyse und Standardanalyse.  
  
-   Die schnelle Analyse besteht aus schnellen, einfachen Analyseroutinen, die keine gebietsschemaspezifischen Datentypkonvertierungen unterstützen, sondern nur die am häufigsten verwendeten Datums- und Zeitformate. 
  
-   Die Standardanalyse enthält viele Analyseroutinen, die alle Datentypkonvertierungen der APIs für die automatische Datentypkonvertierung in Oleaut32.dll und Ole2dsip.dll unterstützen.   
  
## <a name="fast-parse"></a>Fast Parse
Die schnelle Analyse stellt schnelle, einfache Routinen zum Analysieren von Daten bereit. Diese Routinen sind nicht gebietsschemaspezifisch und unterstützen nur eine Teilmenge von Datums-, Uhrzeit- und Ganzzahlformaten.  
  
### <a name="requirements-and-limitations"></a>Anforderungen und Einschränkungen  
 Durch Implementieren der schnellen Analyse ist das Interpretieren von Datum, Uhrzeit und numerischen Daten in gebietsschemaspezifischen Formaten sowie in häufig verwendeten ISO 8601-Basisformaten und erweiterten Formaten über ein Paket nicht möglich. Jedoch trägt dies zur Leistungssteigerung des Pakets bei. Beispielsweise unterstützt die schnelle Analyse nur die gängigsten Datumsformatdarstellungen, wie z. B. YYYYMMDD und YYYY-MM-DD, führt keine gebietsschemaspezifische Analyse durch, erkennt keine Sonderzeichen in Währungsdaten und kann die hexadezimale oder wissenschaftliche Darstellung von ganzen Zahlen nicht konvertieren.  
  
 Die schnelle Analyse ist nur bei Verwenden der Flatfilequelle oder der Transformation für Datenkonvertierung verfügbar. Die Leistungssteigerung kann sehr erheblich sein. Daher sollten Sie nach Möglichkeit die schnelle Analyse in diesen Datenflusskomponenten verwenden.  
  
 Wenn der Datenfluss im Paket eine gebietsschemabezogene Analyse erfordert, wird stattdessen die Standardanalyse empfohlen. So erkennt die schnelle Analyse beispielsweise keine gebietsschemabezogenen Daten mit Dezimalsymbolen wie dem Komma, anderen Datenformaten als dem Jahr-Monat-Datum-Format und Währungssymbolen.  
  
 Abgeschnittene Darstellungen, die mindestens ein Datumsteil implizieren, wie z. B. ein Jahrhundert, ein Jahr oder ein Monat, werden von der schnellen Analyse nicht erkannt. Die schnelle Analyse erkennt z.B. weder das Format**-JJMM**, das ein Jahr und einen Monat in einem implizierten Jahrhundert angibt, noch**--MM**, das einen Monat in einem implizierten Jahr angibt. Bestimmte Darstellungen mit reduzierter Genauigkeit werden jedoch erkannt. Beispielsweise erkennt die schnelle Analyse das Format 'hhmm;', das nur die Stunde und die Minute angibt, sowie '**YYYY**', das nur das Jahr angibt.  
  
 Die schnelle Analyse wird auf Spaltenebene angegeben. In der Flatfilequelle und der Transformation für Datenkonvertierung können Sie die schnelle Analyse für Ausgabespalten festlegen. Eingaben und Ausgaben können gebietsschemabezogene und gebietsschemaneutrale Spalten enthalten.  
 
## <a name="numeric-data-formats-fast-parse"></a>Numerische Datenformate (schnelle Analyse)
Die schnelle Analyse stellt schnelle, einfache und gebietsschemabezogene Routinen zum Analysieren von Daten bereit. Nur bestimmte Formate für integer-Datentypen werden von der schnellen Analyse unterstützt.  
  
### <a name="integer-data-type"></a>Integer-Datentyp
 Die integer-Datentypen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sind DT_I1, DT_UI1, DT_I2, DT_UI2, DT_I4, DT_UI4, DT_I8 und DT_UI8. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Die schnelle Analyse unterstützt die folgenden Formate für integer-Datentypen:  
  
-   Null oder mehr führende und nachfolgende Leerzeichen oder Tabstopps. Beispielsweise ist der Wert "  123  " gültig. Ein Wert, der nur aus Leerzeichen besteht, wird zu Null ausgewertet.  
  
-   Ein führendes Pluszeichen, Minuszeichen oder keines von beiden. Beispielsweise sind die Werte +123, -123 und 123 gültig.  
  
-   Mindestens eine hindu-arabische Ziffer (0-9). Beispielsweise ist der Wert 345 gültig. Ziffern aus anderen Sprachen werden nicht unterstützt.  
  
 Folgende Datenformate werden nicht unterstützt:  
  
-   Sonderzeichen. Beispielsweise wird das Währungszeichen $ nicht unterstützt, und der Wert $20 kann nicht analysiert werden.  
  
-   Leerzeichen, wie z. B. ein Zeilenvorschub, ein Wagenrücklauf und ein geschütztes Leerzeichen. Beispielsweise kann der Wert " 123" nicht analysiert werden.  
  
-   Hexadezimale Darstellungen von ganzen Zahlen. Beispielsweise kann der Wert 2EE nicht analysiert werden.  
  
-   Darstellung von ganzen Zahlen in wissenschaftlicher Schreibweise. Beispielsweise kann der Wert 1E+10 nicht analysiert werden.  
  
 Die folgenden Formate sind Ausgabedatenformate für ganze Zahlen:  
  
-   Ein Minuszeichen für negative Zahlen und kein Zeichen für positive Zahlen.  
  
-   Keine Leerzeichen.  
  
-   Mindestens eine hindu-arabische Ziffer (0-9).  

## <a name="date-and-time-formats-fast-parse"></a>Datums- und Zeitformate (schnelle Analyse)
Die schnelle Analyse stellt schnelle, einfache Routinen zum Analysieren von Daten bereit. Die schnelle Analyse unterstützt die folgenden Formate für Datums- und Zeitdatentypen.  
  
### <a name="date-data-type"></a>Date-Datumstyp 
 Die schnelle Analyse unterstützt die folgenden Zeichenfolgenformate für Datumsdaten:  
  
-   Datumsformate, die führende Leerstellen einschließen. Beispielsweise ist der Wert " 2004- 02-03" gültig.  
  
-   ISO 8601-Formate, wie in der folgenden Tabelle aufgeführt:  
  
    |Format|Description|  
    |------------|-----------------|  
    |YYYYMMDD<br /><br /> YYYY-MM-DD|Basisformate und erweiterte Formate für eine vierstellige Jahresangabe, eine zweistellige Monatsangabe und eine zweistellige Tagesangabe. Beim erweiterten Format werden die Datumsteile durch einen Bindestrich (-) getrennt.|  
    |YYYY-MM|Basisformate und erweiterte Formate mit reduzierter Genauigkeit für eine vierstellige Jahresangabe und eine zweistellige Monatsangabe. Beim erweiterten Format werden die Datumsteile durch einen Bindestrich (-) getrennt.|  
    |YYYY|Das Format mit reduzierter Genauigkeit ist eine vierstellige Jahresangabe.|  
  
 Die schnelle Analyse unterstützt die folgenden Formate für Datumsdaten nicht:  
  
-   Alphabetische Monatswerte. Beispielsweise ist das Datumsformat Oct-31-2003 ungültig.  
  
-   Mehrdeutige Formate wie z. B. DD-MM-YYYY und MM-DD-YYYY. Beispielsweise sind die Datumsangaben 03-04-1995 und 04-03-1995 ungültig.  
  
-   Grundlegende und erweiterte abgeschnittene Formate für ein vierstelliges Kalenderjahr und einen dreistelligen Tag innerhalb eines Jahres: YYYYDDD und YYYY-DDD.  
  
-   Grundlegende und erweiterte Formate für ein vierstelliges Jahr, eine zweistellige Zahl für die Woche des Jahres und eine einstellige Zahl für den Tag der Woche: YYYYWwwD und YYYY-Www-D.  
  
-   Grundlegende und erweiterte abgeschnittene Formate für ein Jahr und eine Wochenangabe, für ein vierstelliges Jahr und eine zweistellige Zahl für die Woche: YYYWww und YYYY-Www.  
  
 Die schnelle Analyse gibt die Daten als DT_DBDATE aus. Datumswerte in abgeschnittenen Formaten werden aufgefüllt. Beispielsweise wird YYYY zu YYYY0101.  
  
 Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
### <a name="time-data-type"></a>Zeitdatentyp
 Die schnelle Analyse unterstützt die folgenden Zeichenfolgenformate für Zeitdaten:  
  
-   Zeitformate, die führende Leerstellen einschließen. Beispielsweise ist der Wert " 10:24" gültig.  
  
-   24-Stunden-Format. Die schnelle Analyse unterstützt die Angabe von AM (Vormittag) und PM (Nachmittag) nicht.  
  
-   ISO 8601-Zeitformate, wie in der folgenden Tabelle aufgeführt:  
  
    |Format|Description|  
    |------------|-----------------|  
    |HHMISS<br /><br /> HH:MI:SS|Basisformate und erweiterte Formate für eine zweistellige Stundenangabe, eine zweistellige Minutenangabe und eine zweistellige Sekundenangabe. Beim erweiterten Format werden die Zeitteile durch einen Doppelpunkt (:) getrennt.|  
    |HHMI<br /><br /> HH:MI|Basisformate und erweiterte abgeschnittene Formate für eine zweistellige Stundenangabe und eine zweistellige Minutenangabe. Beim erweiterten Format werden die Zeitteile durch einen Doppelpunkt (:) getrennt.|  
    |HH|Das abgeschnittene Format für eine zweistellige Stundenangabe.|  
    |00:00:00<br /><br /> 000000<br /><br /> 0000<br /><br /> 00<br /><br /> 240000<br /><br /> 24:00:00<br /><br /> 2400<br /><br /> 24|Das Format für Mitternacht.|  
  
-   Zeitformate, die eine Zeitzone angeben, wie in der folgenden Tabelle aufgeführt:  
  
    |Format|Description|  
    |------------|-----------------|  
    |+HH:MI<br /><br /> +HHMI|Basisformate und erweiterte Formate, die die Anzahl von Stunden und Minuten angeben, die zur koordinierten Weltzeit (UTC) addiert werden, um die lokale Zeit zu ermitteln.|  
    |-HH:MI<br /><br /> -HHMI|Basisformate und erweiterte Formate, die die Anzahl von Stunden und Minuten angeben, die von der koordinierten Weltzeit (UTC) subtrahiert werden, um die lokale Zeit zu ermitteln.|  
    |+HH|Abgeschnittene Formate, die die Anzahl von Stunden angeben, die zur koordinierten Weltzeit (UTC) addiert werden, um die lokale Zeit zu ermitteln.|  
    |-HH|Abgeschnittene Formate, die die Anzahl von Stunden angeben, die von der koordinierten Weltzeit (UTC) subtrahiert werden, um die lokale Zeit zu ermitteln.|  
    |Z|Ein Wert von 0, der angibt, dass die Zeit in UTC dargestellt wird.|  
  
     Die Formate für alle Zeit- und Datums-/Zeitdaten können ein Zeitzonenelement enthalten. Das System ignoriert jedoch den Zeitzonenwert, außer wenn die Daten vom Typ DT_DBTIMESTAMPOFFSET sind. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
     Bei Formaten, die ein Zeitzonenelement enthalten, gibt es kein Leerzeichen zwischen dem Zeitelement und dem Zeitzonenelement, wie das folgende Beispiel zeigt:  
  
     HH:MI:SS[+HH:MI]  
  
     Die Klammern im vorherigen Beispiel geben an, dass der Zeitzonenwert optional ist.  
  
-   Zeitformate, die einen Dezimalbruch enthalten, wie in der folgenden Tabelle aufgeführt:  
  
    |Format|Description|  
    |------------|-----------------|  
    |HH[.nnnnnnn]|n ist ein Wert zwischen 0 und 9999999, der einen Stundenbruchteil darstellt. Die Klammern geben an, dass dieser Wert optional ist.<br /><br /> Beispielsweise steht der Wert 12.750 für 12:45.|  
    |HHMI[.nnnnnnn]<br /><br /> HH:MI[.nnnnnnn]|n ist ein Wert zwischen 0 und 9999999, der einen Minutenbruchteil darstellt. Die Klammern geben an, dass dieser Wert optional ist.<br /><br /> Beispielsweise steht der Wert 1220.500 für 12:20:30.|  
    |HHMISS[.nnnnnnn]<br /><br /> HH:MI:SS[.nnnnnnn]|n ist ein Wert zwischen 0 und 9999999, der einen Sekundenbruchteil darstellt. Die Klammern geben an, dass dieser Wert optional ist.<br /><br /> Beispielsweise steht der Wert 122040.250 für 12:20:40.15.|  
  
    > [!NOTE]  
    >  Als Trennzeichen für den Bruchteilwert kann bei den Zeitformaten der vorherigen Tabelle ein Punkt oder ein Komma verwendet werden.  
  
-   Zeitwerte, die eine Schaltsekunde enthalten, wie in den folgenden Beispielen gezeigt:  
  
     23:59:60[.0000000]  
  
     235960[.0000000]  
  
 Die schnelle Analyse gibt die Zeichenfolgen als DT_DBTIME und DT_DBTIME2 aus. Zeitwerte in abgeschnittenen Formaten werden aufgefüllt. Beispielsweise wird HH:MI als HH:MM:00.000 ausgegeben.  
  
 Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
### <a name="datetime-data-type"></a>Datums-/Zeitdatentyp  
 Die schnelle Analyse unterstützt die folgenden Zeichenfolgenformate für Datums-/Zeitdaten:  
  
-   Zeitformate, die führende Leerstellen enthalten. Beispielsweise ist der Wert "  2003-01-10T203910" gültig.  
  
-   Kombinationen gültiger Datumsformate und gültiger Zeitformate, getrennt durch ein groß geschriebenes T, und gültige Zeitzonenformate, beispielsweise YYYYMMDDT[HHMISS][+HH:MI]. Die Zeit- und Zeitzonenwerte sind nicht erforderlich. Beispielsweise ist "2003-10-14" gültig.  
  
 Die schnelle Analyse unterstützt keine Zeitintervalle. Beispielsweise kann ein Zeitintervall, das durch ein Startdatum und ein Enddatum und eine Zeitangabe im Format YYYYMMDDThhmmss/YYYYMMDDThhmmss identifiziert wird, nicht analysiert werden.  
  
 Die schnelle Analyse gibt die Zeichenfolgen als DT_DATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2 und DT_DBTIMESTAMPOFFSET aus. Datums-/Zeitwerte in abgeschnittenen Formaten werden aufgefüllt. In der folgenden Tabelle werden die Werte aufgeführt, die für fehlende Datums- und Zeitteile hinzugefügt werden.  
  
|Datums-/Zeitteil|Auffüllung|  
|---------------------|-------------|  
|Sekunden|00 hinzufügen.|  
|Minuten|00:00 hinzufügen.|  
|Hour|00:00:00 hinzufügen.|  
|Day|01 für den Tag des Monats hinzufügen.|  
|Month|01 für den Monat des Jahres hinzufügen.|  
  
 Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="enable-fast-parse"></a>Aktivieren der schnellen Analyse
Die Fast Parse-Eigenschaft muss für jede Spalte der Quelle oder Transformation festgelegt werden, die die schnelle Analyse verwendet. Verwenden Sie zum Festlegen der Eigenschaft den Erweiterten Editor der Flatfilequelle und der Transformation für Datenkonvertierung.  
  
1.  Klicken Sie mit der rechten Maustaste auf die Flatfilequelle bzw. die Transformation für Datenkonvertierung, und klicken Sie anschließend auf **Erweiterten Editor anzeigen**.  
  
2.  Klicken Sie im Dialogfeld **Erweiterter Editor** auf die Registerkarte **Eingabe- und Ausgabeeigenschaften** .  
  
3.  Klicken Sie im Bereich **Eingaben und Ausgaben** auf die Spalte, für die die schnelle Analyse aktiviert werden soll.  
  
4.  Erweitern Sie im Eigenschaftenfenster den Knoten **Benutzerdefinierte Eigenschaften** , und legen Sie anschließend die **FastParse** -Eigenschaft auf **True**fest.  
  
5.  Klicken Sie auf **OK**.  

## <a name="standard-parse"></a>Standard Parse
Die Standardanalyse enthält gebietsschemabezogene Analyseroutinen, die alle in Oleaut32.dll und Ole2dsip.dll verfügbaren Datentypkonvertierungen der APIs für die automatische Datentypkonvertierung unterstützen. Die Standardanalyse entspricht den OLE DB-Analyse-APIs.  
  
 Die Standardanalyse stellt die Datentypkonvertierung interner Daten bereit und sollte verwendet werden, wenn das Datenformat nicht von der schnellen Analyse unterstützt wird. Weitere Informationen zur API für die automatische Datentypkonvertierung finden Sie unter "Data Type Conversion APIs" in der [MSDN Library](http://go.microsoft.com/fwlink/?LinkId=79427). 
 
