---
title: Analysis Services MDX Query Designer User Interface | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10012"
- sql13.rtp.rptdesigner.dataview.asquerydesigner.f1
helpviewer_keywords:
- MDX [Reporting Services], creating datasets
- query designers [Reporting Services]
ms.assetid: d9c7c0b3-fce4-4a65-b679-408273e6a925
caps.latest.revision: 38
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7f8838c9793cfc4a8e38bea3f0f27e702dd27e4d
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="analysis-services-mdx-query-designer-user-interface"></a>Benutzeroberfläche des MDX-Abfrage-Designers für Analysis Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] stellt grafische Abfrage-Designer zum Erstellen von MDX-Abfragen (Multidimensional Expressions) und DMX-Abfragen (Data Mining Expressions) für eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenquelle bereit. In diesem Thema wird der MDX-Abfrage-Designer beschrieben. Weitere Informationen zum DMX-Abfrage-Designer finden Sie unter [Analysis Services-Verbindungstyp für DMX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md).  
  
 Der grafische MDX-Abfrage-Designer verfügt über zwei Modi: Entwurfsmodus und Abfragemodus. Jeder Modus stellt einen Metadatenbereich bereit, in dem Sie Elemente aus den ausgewählten Cubes ziehen können, um eine MDX-Abfrage zu erstellen, die beim Verarbeiten des Berichts Daten abruft.  
  
> [!IMPORTANT]  
>  Benutzer greifen auf Datenquellen zu, wenn sie Abfragen erstellen und ausführen. Sie sollten minimale Berechtigungen für die Datenquellen gewähren, z. B. nur Leseberechtigungen.  
  
> [!NOTE]  
>  Das Importieren einer MDX-Abfrage aus einer Datei wird nicht unterstützt.  
  
## <a name="graphical-mdx-query-designer-in-design-mode"></a>Grafischer MDX-Abfrage-Designer im Entwurfsmodus  
 Wenn Sie eine MDX-Abfrage für ein Berichtsdataset bearbeiten, wird der grafische MDX-Abfrage-Designer im Entwurfsmodus geöffnet.  
  
 In der folgenden Abbildung werden die Bereiche für den Entwurfsmodus bezeichnet.  
  
 ![Analysis Services-MDX-Abfrage-Designer, der Designansicht](../../reporting-services/report-data/media/rsqd-dsawas-mdx-designmode.gif "Analysis Services-MDX-Abfrage-Designer, Entwurfsansicht")  
  
 In der folgenden Tabelle sind die Bereiche in diesem Modus aufgeführt.  
  
|Bereich|Funktion|  
|----------|--------------|  
|Cube auswählen (Schaltfläche**...**)|Zeigt den aktuell ausgewählten Cube an.|  
|Metadaten (Bereich)|Zeigt eine hierarchische Liste von Measures, KPIs (Key Performance Indicators) und Dimensionen an, die für den ausgewählten Cube definiert sind.|  
|Berechnete Elemente (Bereich)|Zeigt die aktuell definierten berechneten Elemente an, die für eine Verwendung in der Abfrage verfügbar sind.|  
|Filter (Bereich)|Wird zum Auswählen von Dimensionen und zugehörigen Hierarchien verwendet, um Daten an der Quelle zu filtern und die an den Bericht zurückgegebenen Daten zu beschränken.|  
|Daten (Bereich)|Zeigt die Spaltenüberschriften für das Resultset an, während Sie Elemente aus dem Metadatenbereich und dem Bereich für berechnete Elemente ziehen. Aktualisiert automatisch das Resultset, wenn die Schaltfläche **Automatisch ausführen** ausgewählt wird. .|  
  
 Sie können Dimensionen, Measures und KPIs aus dem Metadatenbereich sowie berechnete Elemente aus dem Bereich für berechnete Elemente in den Datenbereich ziehen. Im Filterbereich können Sie Dimensionen und zugehörige Hierarchien auswählen sowie Filterausdrücke festlegen, um die für eine Abfrage zur Verfügung stehenden Daten zu beschränken. Wenn die **AutoExecute** (![Automatisches Ausführen der Abfrage](../../reporting-services/report-data/media/rsqdicon-autoexecute.gif "Automatisches Ausführen der Abfrage")) auf der Symbolleiste auf die Umschaltfläche ausgewählt ist, wird der Abfrage-Designer ausgeführt wird, die Abfrage jedes Mal, dass Sie ein Metadatenobjekt im Datenbereich ablegen. Sie können manuell ausführen, die Abfrage mithilfe der **ausführen** (![führen Sie die Abfrage](../../reporting-services/report-data/media/rsqdicon-run.gif "führen Sie die Abfrage")) auf der Symbolleiste.  
  
 Wenn Sie in diesem Modus eine MDX-Abfrage erstellen, werden die folgenden zusätzlichen Eigenschaften automatisch in die Abfrage eingeschlossen:  
  
 **Elementeigenschaften** MEMBER_CAPTION, MEMBER_UNIQUE_NAME  
  
 **Zelleigenschaften** VALUE, BACK_COLOR, FORE_COLOR, FORMATTED_VALUE, FORMAT_STRING, FONT_NAME, FONT_SIZE, FONT_FLAGS  
  
 Um eigene zusätzliche Eigenschaften anzugeben, müssen Sie die MDX-Abfrage im Abfragemodus manuell bearbeiten.  
  
### <a name="graphical-mdx-query-designer-toolbar-in-design-mode"></a>Symbolleiste des grafischen MDX-Abfrage-Designers im Entwurfsmodus  
 Die Symbolleiste des Abfrage-Designers stellt Schaltflächen bereit, die Ihnen beim Entwurf von MDX-Abfragen mit der grafischen Oberfläche helfen. In der folgenden Tabelle sind die Schaltflächen und ihre Funktionen aufgeführt.  
  
|Schaltfläche|Description|  
|------------|-----------------|  
|**Als Text bearbeiten**|Nicht aktiviert für diesen Datenquellentyp.|  
|**Importieren**|Importieren einer vorhandenen Abfrage aus einer Berichtsdefinitionsdatei (.rdl) im Dateisystem. Weitere Informationen finden Sie unter [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Ändern Sie in MDX-Abfragesicht](../../reporting-services/report-data/media/rsqdicon-commandtypemdx.gif "ändern Sie in MDX-Abfragesicht")|Wechselt zum MDX-Befehlstyp.|  
|![Ändern Sie in der Ansicht "Abfragesprache" DMX](../../reporting-services/report-data/media/rsqdicon-commandtypedmx.gif "ändern Sie in der Ansicht "Abfragesprache" DMX")|Wechselt zum DMX-Befehlstyp.|  
|![Aktualisieren der Ergebnisdaten](../../reporting-services/report-data/media/rsqdicon-refresh.gif "Aktualisieren der Ergebnisdaten")|Aktualisieren von Metadaten aus der Datenquelle.|  
|![Add calculated member](../../reporting-services/report-data/media/rsqdicon-addcalculatedmember.gif "Add calculated member")|Zeigt das Dialogfeld **Generator für berechnete Elemente** an.|  
|![Zum ein-/ausschalten für leere Zellen anzeigen](../../reporting-services/report-data/media/rsqdicon-showemptycells.gif "zum ein-/ausschalten für leere Zellen anzeigen")|Schaltet zwischen dem Anzeigen und Nichtanzeigen von leeren Zellen im Datenbereich um. (Dies entspricht dem Verwenden der NON EMPTY-Klausel in MDX.)|  
|![Automatisches Ausführen der Abfrage](../../reporting-services/report-data/media/rsqdicon-autoexecute.gif "Automatisches Ausführen der Abfrage")|Bei jeder Änderung wird die Abfrage automatisch ausgeführt, und das Ergebnis wird angezeigt. Die Ergebnisse werden im Datenbereich angezeigt.|  
|![Aggregationen Schaltfläche "anzeigen"](../../reporting-services/report-data/media/rsqdicon-showaggregations.gif "Schaltfläche anzeigen, Aggregationen")|Zeigt Aggregationen im Datenbereich an.|  
|![Löschen](../../reporting-services/report-data/media/rsqdicon-delete.gif "Löschen")|Löschen der ausgewählten Spalte im Datenbereich aus der Abfrage.|  
|![Symbol für das Dialogfeld Abfrageparameter](../../reporting-services/report-data/media/iconqueryparameter.gif "Symbol für die Abfrageparameter (Dialogfeld)")|Anzeigen des Dialogfelds **Abfrageparameter** . Bei der Angabe von Werten für einen Abfrageparameter wird automatisch ein Berichtsparameter mit demselben Namen erstellt. Der Wert des Abfrageparameters wird auf einen Ausdruck festgelegt, der auf den Berichtsparameter verweist.|  
|![Vorbereiten der Abfrageschaltfläche](../../reporting-services/report-data/media/rsqdicon-preparequery.gif "Schaltfläche Abfrage vorbereiten")|Bereitet die Abfrage vor.|  
|![Führen Sie die Abfrage](../../reporting-services/report-data/media/rsqdicon-run.gif "führen Sie die Abfrage")|Führt die Abfrage aus und zeigt die Ergebnisse im Datenbereich an.|  
|![Abbrechen der Abfrage](../../reporting-services/report-data/media/rsqdicon-cancel.gif "Abbrechen der Abfrage")|Abbrechen der Abfrage.|  
|![Wechseln Sie in den Entwurfsmodus](../../reporting-services/media/rsqdicon-designmode.gif "in den Entwurfsmodus wechseln")|Umschalten zwischen Entwurfsmodus und Abfragemodus.|  
  
## <a name="graphical-mdx-query-designer-in-query-mode"></a>Grafischer MDX-Abfrage-Designer im Abfragemodus  
 Wenn Sie vom grafischen Abfrage-Designer in den **Abfragemodus** wechseln möchten, klicken Sie auf der Symbolleiste auf die Schaltfläche **Entwurfsmodus** .  
  
 In der folgenden Abbildung sind die Bereiche für den Abfragemodus veranschaulicht.  
  
 ![Analysis Services MDX-Abfrage-Designer, Abfrageansicht](../../reporting-services/report-data/media/rsqd-dsawas-mdx-querymode.gif "Analysis Services MDX-Abfrage-Designer, Abfrageansicht")  
  
 In der folgenden Tabelle sind die Bereiche in diesem Modus aufgeführt.  
  
|Bereich|Funktion|  
|----------|--------------|  
|Cube auswählen (Schaltfläche**...**)|Zeigt den aktuell ausgewählten Cube an.|  
|Metadaten/Funktionen/Vorlagen (Bereich)|Zeigt eine hierarchische Liste von Measures, KPIs und Dimensionen an, die für den ausgewählten Cube definiert sind.|  
|Abfragebereich|Zeigt den Abfragetext an.|  
|Ergebnisbereich|Zeigt die Ergebnisse des Ausführens der Abfrage an.|  
  
 Im Metadatenbereich werden Registerkarten für **Metadaten**, **Funktionen**und **Vorlagen**angezeigt. Auf der Registerkarte **Metadaten** können Sie Dimensionen, Hierarchien, KPIs und Measures in den MDX-Abfragebereich ziehen. Auf der Registerkarte **Funktionen** können Sie Funktionen in den MDX-Abfragebereich ziehen. Auf der Registerkarte **Vorlagen** können Sie dem MDX-Abfragebereich MDX-Vorlagen hinzufügen. Wenn Sie die Abfrage ausführen, werden im Ergebnisbereich die Ergebnisse für die MDX-Abfrage angezeigt.  
  
 Sie können die im Entwurfsmodus erstellte Standard-MDX-Abfrage um zusätzliche Elementeigenschaften und Zelleigenschaften erweitern. Wenn Sie die Abfrage ausführen, werden diese Werte nicht im Resultset angezeigt. Sie werden jedoch an [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] zurückgegeben, und Sie können diese Werte in einem Bericht verwenden. Weitere Informationen finden Sie unter [Erweiterte Feldeigenschaften für eine Analysis Services-Datenbank &#40;SSRS&#41;](../../reporting-services/report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md).  
  
### <a name="graphical-query-designer-toolbar-in-query-mode"></a>Symbolleiste für den grafischen Abfrage-Designer im Abfragemodus  
 Die Symbolleiste des Abfrage-Designers stellt Schaltflächen bereit, die Ihnen beim Entwurf von MDX-Abfragen mit der grafischen Oberfläche helfen.  
  
 Die Schaltflächen der Symbolleiste sind im Entwurfs- und Abfragemodus identisch, aber die folgenden Schaltflächen sind für den Abfragemodus nicht aktiviert:  
  
-   **Als Text bearbeiten**  
  
-   **Berechnetes Element hinzufügen** (![Add calculated member](../../reporting-services/report-data/media/rsqdicon-addcalculatedmember.gif "Add calculated member"))  
  
-   **Leere Zellen anzeigen** (![zum ein-/ausschalten für leere Zellen anzeigen](../../reporting-services/report-data/media/rsqdicon-showemptycells.gif "zum ein-/ausschalten für leere Zellen anzeigen"))  
  
-   **AutoExecute** (![Automatisches Ausführen der Abfrage](../../reporting-services/report-data/media/rsqdicon-autoexecute.gif "Automatisches Ausführen der Abfrage"))  
  
-   **Zeigt Aggregationen** (![anzeigen, Aggregationen Schaltfläche](../../reporting-services/report-data/media/rsqdicon-showaggregations.gif "anzeigen, Aggregationen Schaltfläche"))  
  
## <a name="see-also"></a>Siehe auch  
 [Definieren von Parametern im MDX-Abfrage-Designer für Analysis Services &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/define-parameters-in-the-mdx-query-designer-for-analysis-services.md)   
 [Erstellen eines freigegebenen Datasets oder eingebetteten Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Analysis Services-Verbindungstyp für DMX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)   
 [RSReportDesigner-Konfigurationsdatei](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)   
 [Analysis Services-Verbindungstyp für MDX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)  
  
  
