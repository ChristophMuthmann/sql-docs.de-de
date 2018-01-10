---
title: "Datentypen in Ausdrücken (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 94fdf921-270c-4c12-87b3-46b1cc98fae5
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: e8f9aac801e823f364070fc2b3ce2e6b4b015f78
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="data-types-in-expressions-report-builder-and-ssrs"></a>Datentypen in Ausdrücken (Berichts-Generator und SSRS)
  Datentypen stellen verschiedene Arten von Daten dar, die auf diese Weise effizient gespeichert und verarbeitet werden können. Zu den gängigen Datentypen gehören Text (auch String oder Zeichenfolge genannt), Zahlen mit oder ohne Dezimalstellen, Datum und Uhrzeit sowie Bilder. Werte in einem Bericht müssen dem RDL-Datentyp (Report Definition Language) entsprechen. Sie können einen Wert beliebig formatieren, wenn Sie ihn in einem Bericht anzeigen. So kann ein Feld, das eine Währung darstellt, als Gleitkommazahl in der Berichtsdefinition gespeichert, jedoch je nach gewählter Formatierungseigenschaft in verschiedenen Formaten angezeigt werden.  
  
 Weitere Informationen zu Anzeigeformaten finden Sie unter [Formatieren von Berichtselementen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-report-items-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-definition-language-rdl-data-types-and-common-language-runtime-clr-data-types"></a>RDL-Datentypen (Report Definition Language) und CLR-Datentypen (Common Language Runtime)  
 Werte, die in einer RDL-Datei angegeben werden, müssen dem RDL-Datentyp entsprechen. Wenn der Bericht kompiliert und verarbeitet wird, werden RDL-Datentypen in CLR-Datentypen konvertiert. In der folgenden Tabelle wird die Konvertierung angezeigt, die als Standardeinstellung markiert ist:  
  
|RDL-Typ|CLR-Typen|  
|--------------|---------------|  
|Zeichenfolge|Standard: String<br /><br /> Chart, GUID, Timespan|  
|Boolean|Standard: Boolesch|  
|Integer|Standard: Int64<br /><br /> Int16, Int32, Uint16, Uint64, Byte, Sbyte|  
|datetime|Standard: DateTime<br /><br /> DateTimeOffset|  
|Float|Standard: Double<br /><br /> Single, Decimal|  
|Binär (Binary)|Standard: Byte[]|  
|Variant|Beliebiger Wert von oben außer Byte []|  
|VariantArray|Array von Variant|  
|Serializable|Variant oder Typen, die mit Serializable markiert sind oder ISerializable implementieren.|  
  
## <a name="understanding-data-types-and-writing-expressions"></a>Grundlegendes zu Datentypen und zum Schreiben von Ausdrücken  
 Es ist wichtig, dass Sie mit Datentypen vertraut sind, wenn Sie Ausdrücke zum Vergleichen oder Kombinieren von Werten schreiben, zum Beispiel, wenn Sie Gruppierungs- oder Filterausdrücke definieren oder Aggregate berechnen. Vergleiche und Berechnungen können nur mit Elementen des gleichen Datentyps durchgeführt werden. Wenn die Datentypen nicht übereinstimmen, müssen sie explizit in den Berichtselementen durch einen Ausdruck konvertiert werden.  
  
 In den folgenden Situationen müssen Sie möglicherweise Daten in einen anderen Datentyp konvertieren:  
  
-   Vergleichen des Werts eines Berichtsparameters mit einem Datentyp mit einem Datasetfeld eines anderen Datentyps  
  
-   Schreiben von Filterausdrücken, die Werte mit unterschiedlichen Datentypen vergleichen  
  
-   Schreiben von Sortierungsausdrücken, die Felder mit unterschiedlichen Datentypen kombinieren  
  
-   Schreiben von Gruppierungsausdrücken, die Felder mit unterschiedlichen Datentypen kombinieren  
  
-   Konvertieren eines aus der Datenquelle abgerufenen Werts von einem Datentyp in einen anderen Datentyp  
  
## <a name="determining-the-data-type-of-report-data"></a>Ermitteln des Datentyps von Berichtsdaten  
 Zum Ermitteln des Datentyps von Berichtselementen können Sie einen Ausdruck schreiben, der den Datentyp zurückgibt. Wenn Sie beispielsweise den Datentyp des Felds `MyField`anzeigen möchten, fügen Sie einer Tabellenzelle den folgenden Ausdruck hinzu: `=Fields!MyField.Value.GetType().ToString()`. Das Ergebnis zeigt den CLR-Datentyp an, der `MyField`darstellt, zum Beispiel **System.String** oder **System.DateTime**.  
  
## <a name="converting-dataset-fields-to-a-different-data-type"></a>Konvertieren von Datasetfeldern in einen anderen Datentyp  
 Sie können auch Datasetfelder konvertieren, bevor sie in einem Bericht verwendet werden. Im Folgenden werden Methoden beschrieben, mit denen Sie ein vorhandenes Datasetfeld konvertieren können:  
  
-   Ändern Sie die Datasetabfrage so, dass ein neues Abfragefeld mit den konvertierten Daten hinzugefügt wird. Bei relationalen oder mehrdimensionalen Datenquellen werden in diesem Fall Datenquellenressourcen zum Durchführen der Konvertierung verwendet.  
  
-   Erstellen Sie ein berechnetes, auf einem bestehenden Berichtsdatasetfeld basierendes Feld, indem Sie einen Ausdruck schreiben, durch den alle Daten in einer Resultsetspalte in eine neue Spalte mit einem anderen Datentyp konvertiert werden. So wird beispielsweise durch den folgenden Ausdruck das Feld Year von einer Ganzzahl in eine Zeichenfolge konvertiert: `=CStr(Fields!Year.Value)`. Weitere Informationen finden Sie unter [Hinzufügen, Bearbeiten und Aktualisieren von Feldern im Berichtsdatenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).  
  
-   Überprüfen Sie, ob die verwendete Datenverarbeitungserweiterung Metadaten zum Abrufen von vorformatierten Daten enthält. So enthält beispielsweise eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -MDX-Abfrage die erweiterte Eigenschaft FORMATTED_VALUE für Cube-Werte, die bereits während der Verarbeitung des Cubes formatiert wurden. Weitere Informationen finden Sie unter [Erweiterte Feldeigenschaften für eine Analysis Services-Datenbank (SSRS)](../../reporting-services/report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md).  
  
## <a name="understanding-parameter-data-types"></a>Parameterdatentypen  
 Berichtsparameter müssen einen der folgenden Datentypen aufweisen: Boolesch (Boolean), Datum/Zeit (DateTime), Ganzzahl (Integer), Gleitkomma (Float) oder Text (String). Wenn eine Datasetabfrage Abfrageparameter enthält, werden automatisch Berichtsparameter erstellt und mit den Abfrageparametern verknüpft. Der Standarddatentyp für einen Berichtsparameter lautet String. Wenn Sie den Standarddatentyp eines Berichtsparameters ändern möchten, wählen Sie im Dialogfeld **Berichtsparametereigenschaften** auf der Seite **Allgemein** in der Dropdownliste **Datentyp** den gewünschten Wert aus.  
  
> [!NOTE]  
>  Berichtsparameter mit einem DateTime-Datentyp unterstützen keine Millisekunden. Sie können zwar einen Parameter erstellen, der auf Werten mit Millisekunden basiert, in der Dropdownliste mit den verfügbaren Werten kann jedoch kein Wert ausgewählt werden, der Datums- oder Zeitwerte mit Millisekunden enthält.  
  
## <a name="writing-expressions-that-convert-data-types-or-extract-parts-of-data"></a>Schreiben von Ausdrücken zum Konvertieren von Datentypen oder Extrahieren von Datenteilen  
 Wenn Sie Text und Datasetfelder mit dem Verkettungsoperator (&) kombinieren, stellt die Common Language Runtime (CLR) im Allgemeinen Standardformate bereit. Falls Sie ein Datasetfeld oder einen Parameter explizit in einen bestimmten Datentyp konvertieren müssen, müssen die Daten mit einer CLR-Methode oder einer Funktion der Visual Basic-Laufzeit konvertiert werden.  
  
 Die folgende Tabelle enthält Beispiele zum Konvertieren von Datentypen.  
  
|Art der Konvertierung|Beispiel|  
|------------------------|-------------|  
|DateTime zu String|`=CStr(Fields!Date.Value)`|  
|String zu DateTime|`=DateTime.Parse(Fields!DateTimeinStringFormat.Value)`|  
|String zu DateTimeOffset|`=DateTimeOffset.Parse(Fields!DateTimeOffsetinStringFormat.Value)`|  
|Extrahieren des Jahrs|`=Year(Fields!TimeinStringFormat.Value)`<br /><br /> `-- or --`<br /><br /> `=Year(Fields!TimeinDateTimeFormat.Value)`|  
|Boolean zu Integer|`=CInt(Parameters!BooleanField.Value)`<br /><br /> -1 ist True und 0 ist False.|  
|Boolean zu Integer|`=System.Convert.ToInt32(Fields!BooleanFormat.Value)`<br /><br /> 1 ist True und 0 ist False.|  
|Nur der Datums-/Uhrzeitanteil (DateTime) des DateTimeOffset-Werts|`=Fields!MyDatetimeOffset.Value.DateTime`|  
|Nur der Zeitverschiebungsanteil (Offset) des DateTimeOffset-Werts|`=Fields!MyDatetimeOffset.Value.Offset`|  
  
 Mit der Formatierungsfunktion können Sie zudem das Anzeigeformat des Werts steuern. Weitere Informationen finden Sie unter [Funktionen (Visual Basic)](http://go.microsoft.com/fwlink/?linkid=111483).  
  
## <a name="advanced-examples"></a>Komplexere Beispiele  
 Wenn Sie eine Datenquelle mit einem Datenanbieter verbinden, der nicht die Konvertierung aller Datentypen in der Datenquelle unterstützt, wird standardmäßig für alle nicht unterstützten Datentypen der Datentyp String verwendet. In den folgenden Beispielen finden Sie Lösungen für bestimmte Datentypen, die als Zeichenfolge (String) zurückgegeben werden.  
  
### <a name="concatenating-a-string-and-a-clr-datetimeoffset-data-type"></a>Verketten eines String-Datentyps und eines CLR-DateTimeOffset-Datentyps  
 Die CLR stellt für die meisten Datentypen eine Standardkonvertierung bereit, sodass Sie Werte mit unterschiedlichen Datentypen mithilfe des &-Operators in einer Zeichenfolge verketten können. Der folgende Ausdruck verkettet zum Beispiel den Text „The date and time are:“ mit einem StartDate-Datasetfeld, bei dem es sich um einen <xref:System.DateTime> -Wert handelt: `="The date and time are: " & Fields!StartDate.Value`.  
  
 Bei einigen Datentypen müssen Sie eventuell die ToString-Funktion verwenden. Der folgende Ausdruck zeigt das gleiche Beispiel mit dem CLR-Datentyp <xref:System.DateTimeOffset>, der das Datum, die Uhrzeit sowie eine Zeitzonenverschiebung relativ zur UTC-Zeitzone beinhaltet: `="The time is: " & Fields!StartDate.Value.ToString()`.  
  
### <a name="converting-a-string-data-type-to-a-clr-datetime-data-type"></a>Konvertieren eines String-Datentyps in einen CLR-DateTime-Datentyp  
 Falls eine Datenverarbeitungserweiterung nicht alle in einer Datenquelle definierten Datentypen unterstützt, werden die Daten eventuell als Text abgerufen. Beispiel: Der Datentypwert **datetimeoffset(7)** wird möglicherweise als String-Datentyp abgerufen. Für Perth in Australien würde der Zeichenfolgenwert für den 1. Juli 2008, 6:05:07.9999999 in etwa wie folgt aussehen:  
  
 `2008-07-01 06:05:07.9999999 +08:00`  
  
 Dieses Beispiel zeigt das Datum (1. Juli 2008), gefolgt von der Uhrzeit mit 7-stelliger Präzision (6:05:07.9999999), gefolgt von der UTC-Zeitzonenverschiebung in Stunden und Minuten (plus 8 Stunden, 0 Minuten). In den folgenden Beispielen befindet sich dieser Wert im **String** -Feld `MyDateTime.Value`.  
  
 Sie können diese Daten mit einer der folgenden Methoden in einen oder mehrere CLR-Werte konvertieren:  
  
-   Verwenden Sie in einem Textfeld einen Ausdruck, um Teile der Zeichenfolge zu extrahieren. Zum Beispiel:  
  
    -   Mit dem folgenden Ausdruck wird der Stundenwert der UTC-Zeitzonenverschiebung extrahiert und in Minuten konvertiert: `=CInt(Fields!MyDateTime.Value.Substring(Fields!MyDateTime.Value.Length-5,2)) * 60`  
  
         Das Ergebnis ist `480`.  
  
    -   Mit dem folgenden Ausdruck wird die Zeichenfolge in einen Datums- und Uhrzeitwert konvertiert: `=DateTime.Parse(Fields!MyDateTime.Value)`  
  
         Falls die Zeichenfolge `MyDateTime.Value` eine UTC-Zeitverschiebung aufweist, passt die Funktion `DateTime.Parse` zunächst die UTC-Zeitverschiebung an (7:00 - [`+08:00`] zur UTC-Zeit 23:00 in der vorherigen Nacht). Anschließend wendet die Funktion `DateTime.Parse` die UTC-Zeitverschiebung des lokalen Berichtsservers an und passt die Zeit ggf. noch einmal an die Sommerzeit an. So ist zum Beispiel in Redmond, Washington/USA die lokale Zeitverschiebung, angepasst an die Sommerzeit, `[-07:00]`, das heißt 7 Stunden früher als 23:00. Daraus ergibt sich der folgende **DateTime** -Wert: `2007-07-06 04:07:07 PM` (6. Juli 2007, 16:07).  
  
 Weitere Informationen zum Konvertieren von Zeichenfolgen in **DateTime** -Datentypen finden Sie unter [Verarbeiten von Zeichenfolgen für Datum und Uhrzeit](http://go.microsoft.com/fwlink/?LinkId=89703), [Formatieren von Datum und Uhrzeit für eine bestimmte Kultur](http://go.microsoft.com/fwlink/?LinkId=89704)und [Choosing Between DateTime, DateTimeOffsetund TimeZoneInfo](http://go.microsoft.com/fwlink/?linkid=110652) auf der MSDN-Website.  
  
-   Fügen Sie ein neues berechnetes Feld dem Berichtsdataset hinzu, das einen Ausdruck verwendet, mit dem Teile der Zeichenfolge extrahiert werden. Weitere Informationen finden Sie unter [Hinzufügen, Bearbeiten und Aktualisieren von Feldern im Berichtsdatenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).  
  
-   Ändern Sie die Berichtsdatasetabfrage so, dass mit [!INCLUDE[tsql](../../includes/tsql-md.md)] -Funktionen die Datums- und Uhrzeitwerte unabhängig voneinander abgerufen und separate Spalten erstellt werden. Im folgenden Beispiel wird gezeigt, wie Sie mit der Funktion **DatePart** eine Spalte für das Jahr und eine Spalte für die in Minuten konvertierte UTC-Zeitzone hinzufügen können:  
  
     `SELECT`  
  
     `MyDateTime,`  
  
     `DATEPART(year, MyDateTime) AS Year,`  
  
     `DATEPART(tz, MyDateTime) AS OffsetinMinutes`  
  
     `FROM MyDates`  
  
     Das Resultset hat drei Spalten. Die erste Spalte enthält Datum und Uhrzeit, die zweite das Jahr und die dritte die UTC-Zeitverschiebung in Minuten. Die folgende Zeile enthält Beispieldaten:  
  
     `2008-07-01 06:05:07             2008                   480`  
  
 Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbanktypen finden Sie unter [Datentypen (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md) und [Datums- und Uhrzeitdatentypen und zugehörige Funktionen (Transact-SQL)](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md) in der [SQL Server-Onlinedokumentation](http://go.microsoft.com/fwlink/?linkid=120955).  
  
 Weitere Informationen zu den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datentypen fin derden Sie unter [Datentypen in der Analysis Services](../../analysis-services/multidimensional-models/olap-physical/data-types-in-analysis-services.md) in der [SQL Server Books Onlin dere](http://go.microsoft.com/fwlink/?linkid=120955).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Formatieren von Berichtselementen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-report-items-report-builder-and-ssrs.md)  
  
  
