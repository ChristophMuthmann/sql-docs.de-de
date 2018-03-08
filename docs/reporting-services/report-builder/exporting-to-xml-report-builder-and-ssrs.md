---
title: Exportieren nach XML (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-builder
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 11d72068-2d97-495e-948f-12d1e8c1957d
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d87aa313c0bec7dccfd97feaf3e1771633d773ea
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="exporting-to-xml-report-builder-and-ssrs"></a>Exportieren nach XML (Berichts-Generator und SSRS)
  Die XML-Renderingerweiterung gibt einen paginierten Bericht im XML-Format zurück. Das Schema der Bericht-XML-Ausgabe hängt vom jeweiligen Bericht ab und enthält nur Daten. Layoutinformationen werden von der XML-Renderingerweiterung nicht gerendert, und die Paginierung wird nicht beibehalten. Der von dieser Erweiterung generierte XML-Code kann in eine Datenbank importiert, als XML-Datennachricht verwendet oder an eine benutzerdefinierte Anwendung gesendet werden.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="ReportItems"></a> Berichtselemente  
 In der folgenden Tabelle wird beschrieben, wie Berichtselemente gerendert werden.  
  
|Element|Renderingverhalten|  
|----------|------------------------|  
|Bericht|Wird als Element der obersten Ebene des XML-Dokuments gerendert.|  
|Datenbereiche|Wird als Element innerhalb des Elements für den Container gerendert. Datenbereiche beinhalten Tabellen, Matrizen und Listen, in denen Daten in Text- und Diagrammform angezeigt werden, sowie Datenbalken, Sparklines, Messgeräte und Indikatoren für die visuelle Darstellung von Daten.|  
|Gruppen- und Detailabschnitte|Jede Instanz wird als Element innerhalb des Elements für den Container gerendert.|  
|Textfeld|Wird als Attribut oder Element innerhalb des Containers gerendert.|  
|Rechteck|Wird als Element innerhalb des Containers gerendert.|  
|Matrixspaltengruppen|Werden als Elemente innerhalb von Zeilengruppen gerendert.|  
|Karte|Wird als Element innerhalb des Elements für den Container gerendert. Kartenebenen sind untergeordnete Elemente der Karte, und jede Kartenebene umfasst Elemente für die zugehörigen Kartenelemente und Kartenelementattribute.|  
|Diagramm|Wird als Element innerhalb des Elements für den Container gerendert. Reihen sind untergeordnete Elemente des Diagramms, und Kategorien sind untergeordnete Elemente einer Reihe. Alle Diagrammbezeichnungen für jeden Diagrammwert werden gerendert. Bezeichnungen und Werte sind als Attribute eingeschlossen.|  
|Datenbalken|Wird ähnlich einem Diagramm als Element innerhalb des Elements für den Container gerendert. Ein Datenbalken enthält normalerweise keine Hierarchien oder Bezeichnungen, sondern nur Werte.|  
|Sparkline|Wird ähnlich einem Diagramm als Element innerhalb des Elements für den Container gerendert. Eine Sparkline enthält normalerweise keine Hierarchien oder Bezeichnungen, sondern nur Werte.|  
|Messgerät|Wird als Element innerhalb des Elements für den Container gerendert. Es wird ein einzelnes Element mit dem Minimal- und Maximalwert der Skala, dem Start- und Endwert des Bereichs und dem Wert des Zeigers als Attribute gerendert.|  
|Indikator|Wird ähnlich einem Messgerät als Element innerhalb des Elements für den Container gerendert. Wird als einzelnes Element mit dem Namen des aktiven Zustands, den verfügbaren Zuständen und dem Datenwert als Attribute gerendert.|  
  
 Für Berichte, die mit der XML-Renderingerweiterung gerendert werden, sind außerdem folgende Regeln zu beachten:  
  
-   XML-Elemente und -Attribute werden in der Reihenfolge gerendert, in der sie in der Berichtsdefinition angezeigt werden.  
  
-   Die Paginierung wird ignoriert.  
  
-   Kopf- und Fußzeilen werden nicht gerendert.  
  
-   Ausgeblendete Elemente, die nicht durch Umschalten sichtbar gemacht werden können, werden nicht gerendert. Sichtbare Elemente und ausgeblendete Elemente, die durch Umschalten sichtbar gemacht werden können, werden gerendert.  
  
-   **Images, lines, and custom report items** werden ignoriert.  
  
  
##  <a name="DataTypes"></a> Datentypen  
 Dem Textfeldelement oder -attribut wird basierend auf den im Textfeld angezeigten Werten ein XSD-Datentyp zugewiesen.  
  
|Wert aller Textfeldelemente|Zugewiesener Datentyp|  
|--------------------------------|---------------------------|  
|**Int16**, **Int32**, **Int64**, **UInt16**, **UInt32**, **UInt64**, **Byte**, **SByte**|**xsd:integer**|  
|**Decimal** (oder **Decimal** und jeder integer- oder BYTE-Datentyp)|**xsd:decimal**|  
|**Float** (oder **Decimal** und jeder integer- oder BYTE-Datentyp)|**xsd:float**|  
|**Double** (oder **Decimal** und jeder integer- oder BYTE-Datentyp)|**xsd:double**|  
|**DateTime oder DateTimeOffset**|**xsd:dateTime**|  
|**Zeit**|**xsd:string**|  
|**Boolean**|**xsd:boolean**|  
|**String**, **Char**|**xsd:string**|  
|Andere|**xsd:string**|  
  
  
##  <a name="XMLSpecificRenderingRules"></a> XML-spezifische Renderingregeln  
 In den folgenden Abschnitten wird beschrieben, wie die XML-Renderingerweiterungen die Elemente innerhalb des Berichts interpretieren.  
  
### <a name="report-body"></a>Hauptteil des Berichts  
 Ein Bericht wird als Stammelement des XML-Dokuments gerendert. Der Name des Elements wird von der im Bereich Eigenschaften festgelegten DataElementName-Eigenschaft abgeleitet.  
  
 XML-Namespacedefinitionen und Schemareferenzattribute sind ebenfalls im Berichtselement enthalten. Variablen werden fett formatiert:  
  
 <**Bericht** xmlns="**Schemaname**" xmlns:xsi= http://www.w3.org/2001/XMLSchema-instance" xsi:**Schemaspeicherort**="**SchemanameBerichtURL**&amp;rc%3aSchema=true" Name="BerichtName">  
  
 Die Werte für die Variablen lauten wie folgt:  
  
|Name|value|  
|----------|-----------|  
|Bericht|Report.DataElementName|  
|ReportURL|URL-codierte absolute URL zum Bericht auf dem Server.|  
|SchemaName|Report.SchemaName. Wenn NULL, dann Report.Name. Wenn Report.Name verwendet wird, wird es zuerst mit XmlConvert.EncodeLocalName codiert.|  
|ReportName|Der Berichtsname.|  
  
### <a name="text-boxes"></a>Textfelder  
 Textfelder werden als Elemente oder Attribute der DataElementStyle-RDL-Eigenschaft entsprechend gerendert. Der Name des Elements oder Attributs wird von der TextBox.DataElementName-RDL-Eigenschaft abgeleitet.  
  
### <a name="charts-data-bars-and-sparklines"></a>Diagramme, Datenbalken und Sparklines  
 Diagramme, Datenbalken und Sparklines werden in XML gerendert. Die Daten sind strukturiert.  
  
### <a name="gauges-and-indicators"></a>Messgeräte und Indikatoren  
 Messgeräte und Indikatoren werden in XML gerendert. Die Daten sind strukturiert.  
  
### <a name="subreports"></a>Unterberichte  
 Ein Unterbericht wird als ein Element gerendert. Der Name des Elements wird von der DataElementName-RDL-Eigenschaft abgeleitet. Die Einstellung der TextBoxesAsElements-Eigenschaft des Berichts überschreibt die Einstellung des Unterberichts. Namespace- und XSLT-Attribute werden nicht zum Unterberichtselement hinzugefügt.  
  
### <a name="rectangles"></a>Rechtecke  
 Ein Rechteck wird als ein Element gerendert. Der Name des Elements wird von der DataElementName-RDL-Eigenschaft abgeleitet.  
  
### <a name="custom-report-items"></a>Custom Report Items  
 CustomReportItems (CRI) sind für die Renderingerweiterung nicht sichtbar. Wenn ein benutzerdefiniertes Berichtselement im Bericht vorhanden ist, rendert die Renderingerweiterung dieses als konventionelles Berichtselement.  
  
### <a name="images"></a>Bilder  
 Bilder werden nicht gerendert.  
  
### <a name="lines"></a>Linien  
 Linien werden nicht gerendert.  
  
  
### <a name="tables-matrices-and-lists"></a>Tabellen, Matrizen und Listen  
 Tabellen, Matrizen und Listen werden als Element gerendert. Der Name des Elements wird von der Tablix-RDL-Eigenschaft DataElementName abgeleitet.  
  
#### <a name="rows-and-columns"></a>Zeilen und Spalten  
 Spalten werden innerhalb der Zeilen gerendert.  
  
#### <a name="tablix-corner"></a>Tablix-Ecke  
 Die Ecke wird nicht gerendert. Nur der Inhalt der Ecke wird gerendert.  
  
#### <a name="tablix-cells"></a>Tablix-Zellen  
 Tablix-Zellen werden als Elemente gerendert. Der Name des Elements wird von der DataElementName-RDL-Eigenschaft der Zelle abgeleitet.  
  
#### <a name="automatic-subtotals"></a>Automatische Teilergebnisse  
 Automatische Tablix-Teilergebnisse werden nicht gerendert.  
  
#### <a name="row-and-column-items-that-do-not-repeat-with-a-group"></a>Zeilen- und Spaltenelemente, die sich nicht mit einer Gruppe wiederholen  
 Elemente, die sich nicht mit einer Gruppe wiederholen, wie Bezeichnungen, Teilergebnisse und Gesamtergebnisse, werden als Elemente gerendert. Der Name des Elements wird von der TablixMember-RDL-Eigenschaft DataElementName abgeleitet.  
  
 Die RDL-Eigenschaft TablixMember.DataElementOutput steuert, ob ein nicht wiederholtes Element gerendert wird.  
  
 Wenn die DataElementName-Eigenschaft des Tablix-Elements nicht angegeben ist, wird ein Name für das nicht wiederholte Element in folgender Form dynamisch generiert:  
  
 ReiheX: Für nicht wiederholte Zeilen, wobei X ein nullbasierter Zeilenindex innerhalb des aktuellen übergeordneten Elements ist.  
  
 SpalteY: Für nicht wiederholte Spalten, wobei Y ein nullbasierter Spaltenindex innerhalb des aktuellen übergeordneten Elements ist.  
  
 Eine nicht wiederholte Kopfzeile wird als untergeordnetes Element der Zeile oder Spalte gerendert, die nicht mit einer Gruppe wiederholt wird.  
  
 Wenn ein nicht wiederholtes Element über keine entsprechenden Tablix-Zellen verfügt, wird es nicht gerendert. Dies ist möglicherweise der Fall, wenn sich eine Tablix-Zelle über mehr als eine Spalte erstreckt.  
  
#### <a name="rows-and-columns-that-repeat-with-a-group"></a>Zeilen und Spalten, die sich mit einer Gruppe wiederholen  
 Zeilen und Spalten, die sich innerhalb einer Gruppe wiederholen, werden nach den Regeln Tablix.DataElementOutput gerendert. Der Name des Elements wird von der DataElementName-Eigenschaft abgeleitet.  
  
 Jeder eindeutige Wert innerhalb einer Gruppe wird als untergeordnetes Element der Gruppe gerendert. Der Name des Elements wird von der Group.DataElementName-Eigenschaft abgeleitet.  
  
 Wenn der DataElementOutput-Eigenschaftswert „Output“ lautet, wird die Kopfzeile eines wiederholten Elements als untergeordnetes Element des Detailelements gerendert.  
  
  
##  <a name="CustomFormatsXSLTransformations"></a> Benutzerdefinierte Formate und XSL-Transformationen  
 Von der XML-Renderingerweiterung erstellte XML-Dateien können mithilfe von XSL-Transformationen (XSLT) in beinahe jedes Format transformiert werden. Mit dieser Funktion können Daten in Formaten erstellt werden, die von den vorhandenen Renderingerweiterungen nicht unterstützt werden. Bevor Sie eine eigene Renderingerweiterung erstellen, sollten Sie die Verwendung der XML-Renderingerweiterung und von XSLT in Betracht ziehen.  
  
  
##  <a name="DuplicateName"></a> Doppelte Namen  
 Wenn doppelte Datenelementnamen innerhalb des gleichen Bereichs vorhanden sind, zeigt der Renderer eine Fehlermeldung an.  
  
  
##  <a name="XSLTTransformations"></a> XSLT-Transformationen  
 Der XML-Renderer kann eine serverseitige XSLT-Transformation für die ursprünglichen XML-Daten übernehmen. Wenn eine XSLT-Transformation übernommen wird, gibt der Renderer den transformierten Inhalt statt der ursprünglichen XML-Daten aus. Die Transformation tritt auf dem Server, nicht auf dem Client auf.  
  
 Die XSLT-Transformation, die für die Ausgabe übernommen werden soll, wird entweder in der Berichtsdefinitionsdatei mithilfe der DataTransform-Eigenschaft des Berichts oder mithilfe des *DeviceInfo* -XSLT-Parameters definiert. Wenn beide Werte festgelegt werden, tritt die Transformation bei jeder Verwendung des XML-Renderers auf. Wenn Abonnements verwendet werden, muss die XSLT-Transformation in der DataTransform-RDL-Eigenschaft definiert werden.  
  
 Ist eine XSLT-Datei sowohl in der DataTransform-Definitionseigenschaft als auch der Geräteinformationseinstellung angegeben, tritt die in DataTransform angegebene XSLT-Transformation zuerst auf. Anschließend findet die von den Geräteinformationseinstellungen festgelegte XSLT-Transformation statt.  
  
  
###  <a name="DeviceInfo"></a> Geräteinformationseinstellungen  
 Sie können einige Standardeinstellungen für diesen Renderer ändern, indem Sie die Geräteinformationseinstellungen ändern. Dazu gehören:  
  
-   Eine auf die XML-Ausgabe anzuwendende Transformation (XSLT).  
  
-   Den MIME-Typ des XML-Dokuments.  
  
-   Ob Formatzeichenfolgen auf Daten angewendet werden sollen.  
  
-   Ob die XML-Ausgabe eingezogen werden soll.  
  
-   Ob der XML-Schemaname einbezogen werden soll.  
  
-   Die Codierung für das XML-Dokument.  
  
-   Die Dateierweiterung des XML-Dokuments.  
  
 Weitere Informationen finden Sie unter [XML Device Information Settings](../../reporting-services/xml-device-information-settings.md).  
  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Paginierung in Reporting Services &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Renderingverhalten (Berichts-Generator und SSRS)](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Interaktive Funktionalität für verschiedene Berichtsrenderingerweiterungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Rendern von Berichtselementen (Berichts-Generator und SSRS)](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
