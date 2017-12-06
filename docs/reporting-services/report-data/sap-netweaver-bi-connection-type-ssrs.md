---
title: SAP NetWeaver BI-Verbindungstyp (SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f985856b-31d5-4e56-844b-8a8ee38da67e
caps.latest.revision: "8"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f3a004db77f5c137742542a729ced6e79c708c43
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="sap-netweaver-bi-connection-type-ssrs"></a>SAP NetWeaver BI-Verbindungstyp (SSRS)
  Wenn Sie Daten aus einer externen SAP NetWeaver® Business Intelligence-Datenquelle in den Bericht einschließen möchten, benötigen Sie ein Dataset, das auf einer Berichtsdatenquelle vom Typ " [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)]" basiert. Dieser integrierte Datenquellentyp basiert auf der Datenerweiterung für den [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework-Datenanbieter 1.0 für [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)].  
  
 Diese Datenerweiterung ermöglicht Ihnen das Abrufen mehrdimensionaler Daten aus InfoCubes, MultiProvidern (virtuelle InfoCubes) und webfähigen Abfragen, die in einer externen [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] -Datenquelle definiert sind.  
  
 Verwenden Sie die Informationen in diesem Thema, um eine Datenquelle zu erstellen. Eine Schritt-für-Schritt-Anleitung finden Sie unter [Hinzufügen und Prüfen einer Datenverbindung &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Verbindungszeichenfolge  
 Erfragen Sie die Verbindungsinformationen und die Anmeldeinformationen zum Herstellen einer Verbindung mit der Datenquelle bei Ihrem Datenbankadministrator. In der Verbindungszeichenfolge im folgenden Beispiel wird eine [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] -Datenquelle auf einem Server mit Port 8000 und XML für Analysis Services (XMLA) über das Internet mit SOAP angegeben:  
  
```  
DataSource=http://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla  
```  
  
 Weitere Beispiele für Verbindungszeichenfolgen finden Sie unter [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen in Berichts-Generator](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34).  
  
  
##  <a name="Credentials"></a> Anmeldeinformationen  
 Anmeldeinformationen sind erforderlich, um Abfragen auszuführen und den Bericht lokal oder vom Berichtsserver aus in der Vorschau anzuzeigen.  
  
 Nachdem Sie den Bericht veröffentlicht haben, müssen Sie eventuell die Anmeldeinformationen für die Datenquelle ändern, sodass die Berechtigungen zum Abrufen der Daten beim Ausführen des Berichts auf dem Berichtsserver gültig sind.  
  
 Weitere Informationen finden Sie unter [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) und [Angeben von Anmeldeinformationen im Berichts-Generator](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53).  
  
  
##  <a name="Query"></a> Abfragen  
 Verwenden Sie den grafischen Abfrage-Designer im Entwurfs- oder Abfragemodus, um eine MDX-Abfrage (Multidimensional Expression) zu erstellen, indem Sie die zugrunde liegenden Datenstrukturen in der Datenquelle durchsuchen. Sie können eine Abfrage aus dem Abfrage-Designer interaktiv zur Laufzeit ausführen, um die Ergebnisse anzuzeigen. Die von Ihnen erstelle Abfrage definiert Felder im Dataset. Die eigentlichen Daten werden zur Laufzeit von der Datenquelle zurückgegeben. Mit dem grafischen Abfrage-Designer können Sie die folgenden Aktionen ausführen:  
  
-   Sie können im Entwurfsmodus Dimensionen, Elemente, Elementeigenschaften und Kennzahlen aus der Datenquelle in den Datenbereich ziehen, um eine MDX-Abfrage (Multidimensional Expression) zu erstellen. Ziehen Sie berechnete Elemente aus dem Bereich "Berechnete Elemente" in den Bereich "Daten", um zusätzliche Datasetfelder zu definieren.  
  
-   Im Abfragemodus können Sie Dimensionen, Elemente, Elementeigenschaften und Kennzahlen in den Abfragebereich ziehen oder MDX-Text direkt in den Abfragebereich eingeben. Ziehen Sie berechnete Elemente aus dem Bereich "Berechnete Elemente" in den Bereich "Daten", um zusätzliche Datasetfelder zu definieren.  
  
 Während Sie Abfragen erstellen, fügt der Abfrage-Designer der MDX-Abfrage automatisch Standardeigenschaften hinzu. Ändern Sie die MDX-Abfrage manuell, wenn Sie andere Eigenschaften als die Standardeigenschaften verwenden möchten.  
  
 Weitere Informationen zum Verwenden dieses Abfrage-Designers finden Sie unter [Benutzeroberfläche des Abfrage-Designers für SAP NetWeaver BI &#40;Berichts-Generator&#41;](http://msdn.microsoft.com/library/8edda06d-1608-498b-bd50-10905e54f6ce).  
  
  
##  <a name="Extended"></a> Erweiterte Feldeigenschaften  
 Die [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] -Datenquelle unterstützt erweiterte Feldeigenschaften. Erweiterte Feldeigenschaften sind zusätzlich zu **Value** und **IsMissing** verwendete Eigenschaften, die von der Datenverarbeitungserweiterung für ein Datasetfeld definiert werden. Erweiterte Eigenschaften umfassen vordefinierte Eigenschaften und benutzerdefinierte Eigenschaften. Bei vordefinierten Eigenschaften handelt es sich um Eigenschaften, die von mehreren Datenquellen gemeinsam verwendet werden. Benutzerdefinierte Eigenschaften gelten jeweils nur für eine Datenquelle.  
  
### <a name="working-with-field-properties"></a>Arbeiten mit Feldeigenschaften  
 Erweiterte Feldeigenschaften werden im Berichtsdatenbereich nicht als Elemente angezeigt, die in das Berichtslayout gezogen werden können. Ziehen Sie stattdessen das übergeordnete Feld der Eigenschaft in den Bericht, und ändern Sie anschließend die Standardeigenschaft von **Value** in die gewünschte Eigenschaft. Wenn der Feldname **Calendar Year/Month Level 01** beispielsweise im MDX-Abfrage-Designer durch Ziehen einer Ebene aus dem Metadatenbereich in den Abfragebereich erstellt wurde, würden Sie in einem Ausdruck mithilfe der folgenden Syntax auf die benutzerdefinierte erweiterte Eigenschaft **Long Name** verweisen:  
  
 `=Fields!Calendar_Year_Month_Level_01("Long Name")`  
  
 Der Name einer erweiterten Feldeigenschaft wird in der QuickInfo angezeigt, wenn Sie mit dem Mauszeiger auf ein Feld im Metadatenbereich zeigen. Weitere Informationen zu den Abfrage-Designern, die Sie zum Durchsuchen der zugrunde liegenden Daten verwenden können, finden Sie unter [SAP NetWeaver BI Query Designer User Interface](../../reporting-services/report-data/sap-netweaver-bi-query-designer-user-interface.md).  
  
> [!NOTE]  
>  Für erweiterte Feldeigenschaften sind nur Werte vorhanden, wenn diese Werte bei der Ausführung des Berichts und beim Abrufen der Daten für die Datasets von der Datenquelle bereitgestellt werden. Sie können anschließend von einem beliebigen Ausdruck aus mithilfe der unten erläuterten Syntax auf diese **Field** -Eigenschaftswerte verweisen. Da diese Felder jedoch vom Datenanbieter abhängen und nicht Bestandteil der Berichtsdefinitionssprache sind, werden an diesen Werten vorgenommene Änderungen nicht mit der Berichtsdefinition gespeichert.  
  
 Verwenden Sie eine der folgenden Syntaxen, um in einem Ausdruck auf vordefinierte erweiterte Eigenschaften zu verweisen.  
  
-   *Fields!FieldName.PropertyName*  
  
-   *Fields!FieldName("PropertyName")*  
  
 Verwenden Sie die folgende Syntax, um in einem Ausdruck auf benutzerdefinierte erweiterte Eigenschaften zu verweisen:  
  
-   *Fields!FieldName("PropertyName")*  
  
  
### <a name="predefined-field-properties"></a>Vordefinierte Feldeigenschaften  
 Die folgende Tabelle enthält eine Liste der vordefinierten Feldeigenschaften, die Sie für eine [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] -Datenquelle verwenden können.  
  
|**Eigenschaft**|**Typ**|**Beschreibung oder erwarteter Wert**|  
|------------------|--------------|---------------------------------------|  
|**Value**|**Objekt**|Gibt den Datenwert des Felds an.|  
|**IsMissing**|**Boolean**|Gibt an, ob das Feld im resultierenden Dataset gefunden wurde.|  
|**FormattedValue**|**String**|Gibt einen formatierten Wert für eine Kennzahl zurück.|  
|**BackgroundColor**|**String**|Gibt die Hintergrundfarbe zurück, die in der Datenbank für das Feld definiert ist.|  
|**Farbe**|**String**|Gibt die Vordergrundfarbe zurück, die in der Datenbank für das Element definiert ist.|  
|**Key**|**Objekt**|Gibt den Schlüssel für eine Ebene zurück.|  
|**LevelNumber**|**Integer**|Gibt bei Über-/Unterordnungshierarchien die Nummer der Ebene oder Dimension zurück.|  
|**ParentUniqueName**|**String**|Gibt bei Über-/Unterordnungshierarchien einen vollqualifizierten Namen der übergeordneten Ebene zurück.|  
|**UniqueName**|**String**|Gibt den vollqualifizierten Namen einer Ebene zurück. Der Wert **UniqueName** für einen Mitarbeiter kann z.B. *[0D_Company].[10D_Department].[11]*lauten.|  
  
 Weitere Informationen zur Verwendung von Feldern und Feldeigenschaften in einem Ausdruck finden Sie unter [Integrierte Sammlungen in Ausdrücken &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md).  
  
  
##  <a name="Remarks"></a> Hinweise  
 Nicht alle Berichtsübermittlungsmodi werden von diesem Datenanbieter unterstützt. Die Übermittlung von Berichten über datengesteuerte Abonnements wird für diese Datenverarbeitungserweiterung nicht unterstützt. Weitere Informationen finden Sie unter [Verwenden einer externen Datenquelle für Abonnentendaten &#40;datengesteuertes Abonnement&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md).  
  
 Weitere Informationen finden Sie im Thema zur [Verwendung von SQL Server 2008 Reporting Services with SAP NetWeaver Business Intelligence](http://go.microsoft.com/fwlink/?LinkId=167352).  
  
  
##  <a name="HowTo"></a> Themen zur Vorgehensweise  
 Dieser Abschnitt enthält schrittweise Anweisungen zum Arbeiten mit Datenverbindungen, Datenquellen und Datasets.  
  
 [Hinzufügen und Prüfen einer Datenverbindung &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Erstellen eines freigegebenen Datasets oder eingebetteten Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Hinzufügen eines Filters zu einem Dataset &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> Verwandte Abschnitte  
 Diese Abschnitte der Dokumentation enthalten umfassende grundlegende Informationen zu Berichtsdaten sowie Informationen zum Definieren, Anpassen und Verwenden der mit Daten zusammenhängenden Teile eines Berichts.  
  
 [Berichtsdatasets &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 Bietet eine Übersicht über den Zugriff auf Daten für den Bericht.  
  
 [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen in Berichts-Generator](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 Enthält Informationen zu Datenverbindungen und Datenquellen.  
  
 [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Enthält Informationen zu eingebetteten und freigegebenen Datasets.  
  
 [Datasetfelder-Sammlung &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 Enthält Informationen zur von der Abfrage generierten Datasetfeldauflistung.  
  
 [Von Reporting Services unterstützte Datenquellen &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  
 Enthält ausführliche Informationen zur Plattform- und Versionsunterstützung für die einzelnen Datenerweiterungen.  
  
  
## <a name="see-also"></a>Siehe auch  
 [Berichtsparameter &#40;Berichts-Generator und Berichts-Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtern, Gruppieren und Sortieren von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
