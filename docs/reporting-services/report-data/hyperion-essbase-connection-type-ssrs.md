---
title: Hyperion Essbase-Verbindungstyp (SSRS) | Microsoft-Dokumentation
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
ms.assetid: 108a00b6-799f-4066-b796-da59e95c09fd
caps.latest.revision: "10"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d89029ffc521d08ea3152ca164d3985de4644a32
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="hyperion-essbase-connection-type-ssrs"></a>Hyperion Essbase-Verbindungstyp (SSRS)
  Wenn Sie Daten aus einer externen [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] -Datenquelle in den Bericht einschließen möchten, benötigen Sie ein Dataset, das auf einer Berichtsdatenquelle vom Typ " [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]" basiert. Dieser integrierte Datenquellentyp basiert auf der Datenerweiterung für [!INCLUDE[extEssbase](../../includes/extessbase-md.md)], die es Ihnen ermöglicht, mehrdimensionale Daten aus einer externen [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] -Datenquelle abzurufen.  
  
 Verwenden Sie die Informationen in diesem Thema, um eine Datenquelle zu erstellen. Eine Schritt-für-Schritt-Anleitung finden Sie unter [Hinzufügen und Prüfen einer Datenverbindung &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Verbindungszeichenfolge  
 In der Verbindungszeichenfolge im folgenden Beispiel wird eine [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] -Datenquelle auf einem Server mit Port 13080 und XML für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (XMLA) über das Internet mit SOAP angegeben, um eine Verbindung mit einem Beispielkatalog herzustellen:  
  
```  
Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample  
```  
  
 Weitere Informationen zu Beispielen für Verbindungszeichenfolgen finden Sie unter [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen in Berichts-Generator](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34).  
  
  
##  <a name="Credentials"></a> Anmeldeinformationen  
 Anmeldeinformationen sind erforderlich, um Abfragen auszuführen und den Bericht lokal oder vom Berichtsserver aus in der Vorschau anzuzeigen.  
  
 Nachdem Sie den Bericht veröffentlicht haben, müssen Sie eventuell die Anmeldeinformationen für die Datenquelle ändern, sodass die Berechtigungen zum Abrufen der Daten beim Ausführen des Berichts auf dem Berichtsserver gültig sind.  
  
 Weitere Informationen finden Sie unter [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) und [Angeben von Anmeldeinformationen im Berichts-Generator](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53).  
  
  
##  <a name="Query"></a> Abfragen  
 Zum Angeben einer Abfrage stehen Ihnen folgende Methoden zur Auswahl:  
  
-   Erstellen Sie eine Abfrage interaktiv. Verwenden Sie den grafischen Abfrage-Designer im Entwurfs- oder Abfragemodus, um die Metadaten in der externen Datenquelle zu durchsuchen und eine Abfrage in der MDX-Syntax (Multidimensional Expressions) zu generieren.  
  
    -   **Entwurfsansicht** Ziehen Sie Dimensionen, Elemente, Elementeigenschaften, Measures und KPIs aus dem Metadatenbrowser in den Bereich **Daten** , um eine MDX-Abfrage zu erstellen. Ziehen Sie berechnete Elemente aus dem Bereich „Berechnete Elemente“ in den Datenbereich, um zusätzliche Datasetfelder zu definieren.  
  
    -   **Abfrageansicht** Ziehen Sie Dimensionen, Elemente, Elementeigenschaften, Measures und KPIs aus dem Metadatenbrowser in den Bereich "Abfrage", um eine MDX-Abfrage zu erstellen. Sie können MDX-Text direkt im Abfragebereich bearbeiten. Ziehen Sie berechnete Elemente aus dem Bereich „Berechnete Elemente“ in den Abfragebereich, um zusätzliche Datasetfelder zu definieren.  
  
     Weitere Informationen finden Sie unter [Benutzeroberfläche des Abfrage-Designers von Hyperion Essbase (Berichts-Generator)](http://msdn.microsoft.com/library/d89a6773-dbe5-48e5-bda9-db0e67100696).  
  
-   Importieren Sie eine vorhandene MDX-Abfrage aus einem Bericht. Verwenden Sie die Schaltfläche **Abfrage importieren** , um eine RDL-Datei auszuwählen und eine Abfrage zu importieren. Sie können eine Abfrage aus einem Bericht importieren, der ein eingebettetes, auf einer [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] -Datenquelle beruhendes Dataset enthält. Das direkte Importieren einer MDX-Abfrage aus einer MDX-Datei wird nicht unterstützt.  
  
 Führen Sie die Abfrage zur Entwurfszeit aus, um ein Resultset anzuzeigen. Nachdem Sie die Abfrage erstellt haben, zeigen Sie die aus den Metadaten generierte Datasetfeldauflistung im Berichtsdatenbereich an. Bei der Ausführung des Berichts werden die tatsächlichen Daten aus der externen Datenquelle zurückgegeben.  
  
 Die [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] -Datenverarbeitungserweiterung unterstützt erweiterte Datasetfeldeigenschaften. Bei diesen Eigenschaften handelt es sich um Werte, die in der externen Datenquelle verfügbar sind, aber nicht im Berichtsdatenbereich angezeigt werden. Weitere Informationen finden Sie an späterer Stelle dieses Themas unter [Erweiterte Feldeigenschaften](#Extended) .  
  
  
##  <a name="Parameters"></a> Erstellen Sie im Filterbereich des Abfrage-Designers einen Filter, und markieren Sie ihn als Parameter, um Abfrageparameter einzuschließen. Für jeden Filter wird automatisch ein Dataset erstellt, um die verfügbaren Werte bereitzustellen. Diese Datasets werden standardmäßig nicht im Berichtsdatenbereich angezeigt. Weitere Informationen finden Sie unter [Anzeigen von ausgeblendeten Datasets für Parameterwerte für mehrdimensionale Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/show-hidden-datasets-for-parameter-values-multidimensional-data.md).  
  
 Alle Berichtsparameter sind standardmäßig vom Datentyp **Text**. Die Standardwerte müssen möglicherweise nach dem Erstellen der Berichtsparameter geändert werden. Weitere Informationen finden Sie unter [Berichtsparameter &#40;Berichts-Generator und Berichts-Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)" basiert.  
  
  
##  <a name="Extended"></a> Erweiterte Feldeigenschaften  
 Die [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] -Datenverarbeitungserweiterung unterstützt erweiterte Feldeigenschaften. Erweiterte Feldeigenschaften sind zusätzlich zu **Value** und **IsMissing** verwendete Eigenschaften, die von der Datenverarbeitungserweiterung für ein Datasetfeld definiert werden. Erweiterte Eigenschaften umfassen vordefinierte Eigenschaften und benutzerdefinierte Eigenschaften. Bei vordefinierten Eigenschaften handelt es sich um Eigenschaften, die von mehreren Datenquellen gemeinsam verwendet werden. Benutzerdefinierte Eigenschaften gelten jeweils nur für eine Datenquelle.  
  
 Erweiterte Feldeigenschaften werden im Berichtsdatenbereich nicht als Elemente angezeigt, die in das Berichtslayout gezogen werden können. Ziehen Sie stattdessen das übergeordnete Feld der Eigenschaft in den Bericht, und ändern Sie anschließend die Standardeigenschaft von **Value** in die gewünschte Eigenschaft.  
  
 Der Name einer erweiterten Feldeigenschaft wird in der QuickInfo angezeigt, wenn Sie im Abfrage-Designer den Mauszeiger über ein Feld im Metadatenbereich bewegen. Weitere Informationen zum Abfrage-Designer, den Sie zum Durchsuchen der zugrunde liegenden Daten verwenden können, finden Sie unter [Hyperion Essbase Query Designer User Interface](../../reporting-services/report-data/hyperion-essbase-query-designer-user-interface.md).  
  
> [!NOTE]  
>  Werte sind für erweiterte Feldeigenschaften nur dann vorhanden, wenn sie im MDX-Ausdruck enthalten sind. Diese Werte werden von der Datenquelle bereitgestellt, wenn der Bericht ausgeführt wird und die Daten für seine Datasets abgerufen werden. Sie können anschließend von einem beliebigen Ausdruck aus mithilfe der im folgenden Abschnitt erläuterten Syntax auf diese **Field** -Eigenschaftswerte verweisen. Da diese Felder jedoch vom Datenanbieter abhängen und nicht Bestandteil der Berichtsdefinitionssprache sind, werden an diesen Werten vorgenommene Änderungen nicht mit der Berichtsdefinition gespeichert.  
  
  
### <a name="predefined-field-properties"></a>Vordefinierte Feldeigenschaften  
 Vordefinierte Feldeigenschaften sind Eigenschaften, die in der Regel von mehreren Datenanbietern unterstützt und in der zugrunde liegenden MDX-Abfrage für ein Berichtsdataset angezeigt werden. Beispielsweise ist die MDX-Dimensionseigenschaft MEMBER_UNIQUE_NAME der vordefinierten Berichtsdataset-Feldeigenschaft **UniqueName**zugeordnet. Verwenden Sie den Ausdruck `=Fields!`*\<Feldname>*`.UniqueName`, um den Wert des eindeutigen Namens in ein Textfeld einzuschließen.  
  
 Die folgende Tabelle enthält eine Liste vordefinierter Feldeigenschaften, die Sie für eine [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] -Datenquelle verwenden können.  
  
|**Eigenschaft**|**Typ**|**Beschreibung oder erwarteter Wert**|  
|------------------|--------------|---------------------------------------|  
|**Value**|**Objekt**|Gibt den Datenwert des Felds an.<br /><br /> Bei einer Dimensionseigenschaft wird dies MEMBER_CAPTION zugeordnet. Bei einem Measure wird dies dem Datenwert zugeordnet.|  
|**IsMissing**|**Boolean**|Gibt an, ob das Feld im resultierenden Dataset gefunden wurde.|  
|**FormattedValue**|**String**|Gibt einen formatierten Wert für eine Kennzahl zurück.<br /><br /> Von FORMATTED_VALUE im MDX-Ausdruck zugeordnet.|  
|**BackgroundColor**|**String**|Gibt die Hintergrundfarbe zurück, die in der Datenbank für das Feld definiert ist.<br /><br /> Von BACK_COLOR im MDX-Ausdruck zugeordnet.|  
|**Farbe**|**String**|Gibt die Vordergrundfarbe zurück, die in der Datenbank für das Element definiert ist.<br /><br /> Von FORE_COLOR im MDX-Ausdruck zugeordnet.|  
|**UniqueName**|**String**|Gibt den vollqualifizierten Namen einer Ebene zurück.<br /><br /> Von MEMBER_UNIQUE_NAME im MDX-Ausdruck zugeordnet.|  
  
 Weitere Informationen zur Verwendung von Feldern und Feldeigenschaften in einem Ausdruck finden Sie unter [Integrierte Sammlungen in Ausdrücken &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md).  
  
  
### <a name="custom-properties"></a>Benutzerdefinierte Eigenschaften  
 Benutzerdefinierte Feldeigenschaften sind Eigenschaften, die von einem Datenanbieter unterstützt und in der zugrunde liegenden MDX-Abfrage für ein Berichtsdataset angezeigt werden, jedoch nicht im Bereich "Datasets" des Berichts als Felder unter diesem Dataset aufgeführt werden. Beispielsweise ist **Long Names** eine für eine Dimensionsebene definierte Elementeigenschaft. Verwenden Sie den Ausdruck `=Fields!`*\<FieldName>*`("Long Names")`, um den Wert in ein Textfeld einzuschließen. Bei Feldnamen im Ausdruck wird zwischen Groß-/Kleinschreibung unterschieden.  
  
 Verwenden Sie die folgende Syntax, um in einem Ausdruck auf benutzerdefinierte erweiterte Eigenschaften zu verweisen:  
  
-   *Fields!FieldName("PropertyName")*  
  
 In der folgenden Tabelle werden die benutzerdefinierten Feldeigenschaften angezeigt, die Sie für eine [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] -Datenquelle verwenden können.  
  
|**Eigenschaft**|**Typ**|**Beschreibung oder erwarteter Wert**|  
|------------------|--------------|---------------------------------------|  
|**FORMAT_STRING**|**String**|Bei Definition für ein Measure ist dies der als String-Typ verfügbare **FormattedValue** .|  
  
  
##  <a name="Remarks"></a> Hinweise  
 Nicht alle Berichtsübermittlungsmodi werden von diesem Datenanbieter unterstützt. Die Übermittlung von Berichten über datengesteuerte Abonnements wird für diese Datenverarbeitungserweiterung nicht unterstützt. Weitere Informationen finden Sie unter [Verwenden einer externen Datenquelle für Abonnentendaten &#40;datengesteuertes Abonnement&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md) in der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Dokumentation der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-[Onlinedokumentation](http://go.microsoft.com/fwlink/?linkid=121312).  
  
 Weitere Informationen finden Sie unter [Verwenden von SQL Server 2005 Reporting Services mit Hyperion Essbase](http://go.microsoft.com/fwlink/?LinkId=81970).  
  
  
##  <a name="HowTo"></a> Themen zur Vorgehensweise  
 Dieser Abschnitt enthält schrittweise Anweisungen zum Arbeiten mit Datenverbindungen, Datenquellen und Datasets:  
  
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
 Enthält Informationen zu der von der Datasetabfrage generierten Feldauflistung.  
  
 [Von Reporting Services unterstützte Datenquellen (SSRS)](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) in der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Dokumentation der [Onlinedokumentation](http://go.microsoft.com/fwlink/?linkid=121312) zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Enthält ausführliche Informationen zur Plattform- und Versionsunterstützung für die einzelnen Datenerweiterungen.  
  
 [Verwenden von SQL Server 2005 Reporting Services mit Hyperion Essbase](http://go.microsoft.com/fwlink/?LinkId=81970)  
 Enthält ausführliche Informationen zum Arbeiten mit dieser Datenerweiterung.  
  
  
## <a name="see-also"></a>Siehe auch  
 [Berichtsparameter &#40;Berichts-Generator und Berichts-Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtern, Gruppieren und Sortieren von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
