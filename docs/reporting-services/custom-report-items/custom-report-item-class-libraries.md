---
title: "Klassenbibliotheken für benutzerdefinierten Berichts Element | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom report items, RDL
- RDL [Reporting Services], custom report items
ms.assetid: f18c5d8f-1d6b-4f0b-8657-c14896c2ce0d
caps.latest.revision: 27
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: f216228c01e835e88cd9d4c7d7d4190648a386db
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="custom-report-item-class-libraries"></a>Klassenbibliotheken für ein benutzerdefiniertes Berichtselement
  Benutzerdefinierte Berichtselemente verwenden Klassen aus der **Microsoft.ReportDesigner** Namespace. Die Klassen, die zum Implementieren eines benutzerdefinierten Berichtselements verwendet werden, können in zwei Hauptkategorien gruppiert werden: eindeutige Klassen zur Unterstützung der Infrastruktur eines benutzerdefinierten Berichtselements und verwaltete Wrapperklassen, die die Funktionalität von relevanten RDL-Elementen (Report Definition Language) kapseln. Ein Codebeispiel für die Verwendung dieser Klassen finden Sie unter [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="custom-report-item-infrastructure-classes"></a>Infrastrukturklassen eines benutzerdefinierten Berichtselements  
 Die folgenden Klassen werden zum Implementieren eines benutzerdefinierten Berichtselements verwendet.  
  
> [!NOTE]  
>  Die nachfolgenden Tabellen stellen keine vollständige Liste dar. Sie enthalten nur die am häufigsten verwendeten Eigenschaften und Methoden für jede Klasse.  
  
### <a name="microsoftreportdesignercustomreportitemdesigner"></a>Microsoft.ReportDesigner.CustomReportItemDesigner  
 Dies ist die Hauptklasse eines benutzerdefinierten Berichtselements. Die Hauptklasse der Implementierung eines benutzerdefinierten Berichtselements muss von dieser Klasse erben.  
  
#### <a name="public-properties"></a>Öffentliche Eigenschaften  
  
|||  
|-|-|  
|**Name**|Der Name des benutzerdefinierten Berichtselements.|  
|**Typ**|Der Typ des benutzerdefinierten Berichtselements.|  
|**Die CustomData-Funktion**|Ein <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData>-Objekt, das die während der Entwurfszeit angegebenen Dateneigenschaften für ein benutzerdefiniertes Berichtselement kapselt.|  
|**CustomProperties**|Eine Auflistung benutzerdefinierter Eigenschaften für das benutzerdefinierte Berichtselement.|  
|**Höhe**|Die Höhe der Steuerung für ein benutzerdefiniertes Berichtselement.|  
|**Breite**|Die Breite der Steuerung für ein benutzerdefiniertes Berichtselement.|  
|**Bericht**|Ein Container für die Eigenschaften auf Berichtsebene, z. B. die Liste der Datasets in dem Bericht.|  
|**AltReportItem**|Das alternative Berichtselementobjekt, das verwendet werden muss, wenn die Laufzeitsteuerung für das benutzerdefinierte Berichtselement nicht unterstützt wird.|  
|**Style**|Die Stileigenschaften für das benutzerdefinierte Berichtselement.|  
|**Zusatzelement (adornment)**|Ein Gestaltungsfenster für die interaktive Bearbeitung der Steuerung.|  
|**Website**|Die **ISite** der Komponente.|  
|**Dann DesignerVerbCollection**|Ein Array der benutzerdefinierten Verben für das Kontextmenü der Steuerung.|  
  
#### <a name="public-methods"></a>Öffentliche Methoden  
  
|||  
|-|-|  
|**BeginEdit**|Aktiviert die interaktive Bearbeitung der Steuerung.|  
|**DoDefaultAction**|Wird als Reaktion auf das Doppelklicken oder Drücken der EINGABETASTE auf der Steuerung aufgerufen.|  
|**EndEdit**|Deaktiviert die interaktive Bearbeitung der Steuerung.|  
|**GetService**|Gibt ein Objekt zurück, das einen Dienst darstellt.|  
|**InitializeNewComponent aus**|Wird aufgerufen, wenn ein neues benutzerdefiniertes Berichtselement erstellt wird.|  
|**Für ungültig zu erklären**|Zeichnet die gesamte Oberfläche der Steuerung neu.|  
|**OnDragEnter**<br /><br /> **OnDragDrop**|Wird aufgerufen, wenn ein Objekt auf die Steuerung gezogen wird.|  
|**OnPaint**|Wird aufgerufen, als Antwort auf die **Paint** Ereignis.|  
  
### <a name="microsoftreportdesignercustomreportitemattribute"></a>Microsoft.ReportDesigner.CustomReportItemAttribute  
 Dieses Attribut wird zur Identifizierung des Typs des benutzerdefinierten Berichtselements verwendet. Der Name muss den Wert des übereinstimmen der \< **Namen**>-Attribut des der **ReportItem** Element in der Konfigurationsdatei für den Berichts-Designer.  
  
#### <a name="public-methods"></a>Öffentliche Methoden  
  
|||  
|-|-|  
|**CustomReportItemAttribute**|Erstellt das CustomReportItemAttribute-Objekt.|  
  
### <a name="microsoftreportdesignerlocalizednameattribute"></a>Microsoft.ReportDesigner.LocalizedNameAttribute  
 Dieses Attribut wird zum Festlegen des Anzeigenamens für den Designer des benutzerdefinierten Berichtselements verwendet.  
  
#### <a name="public-methods"></a>Öffentliche Methoden  
  
|||  
|-|-|  
|**LocalizedNameAttribute**|Erstellt das LocalizedNameAttribute-Objekt.|  
  
### <a name="microsoftreportdesigneradornment"></a>Microsoft.ReportDesigner.Adornment  
 Die **Randsteuerelement** Klasse wird von der Entwurfszeitkomponente Element einer benutzerdefinierten Bericht verwendet, um Bereiche außerhalb des hauptrechtecks der Entwurfsoberfläche bereitzustellen. Diese Bereiche behandeln Benutzeroberflächenereignisse wie Mausklicks und Drag und Drop-Vorgänge.  
  
#### <a name="public-methods"></a>Öffentliche Methoden  
  
|||  
|-|-|  
|**OnShow**|Wird aufgerufen, wenn die **Randsteuerelement** aktiviert ist.|  
|**OnHide**|Wird aufgerufen, wenn die **Randsteuerelement** deaktiviert ist.|  
|**Paint**|Wird aufgerufen, als Antwort auf die **Paint** Ereignis.|  
|**OnDragEnter**<br /><br /> **OnDragOver**<br /><br /> **OnDragLeave**<br /><br /> **OnDragDrop**|Wird aufgerufen, wenn ein Objekt, in gezogen wird der **Randsteuerelement**.|  
  
### <a name="microsoftreportdesigneradornerservice"></a>Microsoft.ReportDesigner.AdornerService  
 Diese Klasse wird verwendet, um eine Auflistung von anzeigediensten, die durch das benutzerdefinierte Berichtselement verwendet werden, um Unterstützung zu bieten **Randsteuerelement** Objekte für die Entwurfszeitkomponente Element einer benutzerdefinierten Bericht.  
  
#### <a name="public-properties"></a>Öffentliche Eigenschaften  
  
|||  
|-|-|  
|**AdornerWindowBounds**|Die Begrenzungen des Gestaltungsfensters.|  
|**AdornerWindowRegion**|Der Bereich des Gestaltungsfensters.|  
|**AdornerWindowGraphics**|Ein Grafikontext für das Gestaltungsfenster.|  
  
#### <a name="public-methods"></a>Öffentliche Methoden  
  
|||  
|-|-|  
|**ComponentRectInDesignerFrame**|Gibt die Begrenzungen der Komponente zurück, die in Designerrahmenkoordinaten umgewandelt wurden.|  
|**InvalidateAdorner**|Führt dazu, dass das Gestaltungsfenster ungültig wird.|  
|**PointToAdorner**|Gibt einen Punkt in Bildschirmkoordinaten zurück, der in Gestaltungsfensterkoordinaten umgewandelt wurde.|  
  
### <a name="microsoftreportdesignerexpressioneditor"></a>Microsoft.ReportDesigner.ExpressionEditor  
 Diese Klasse kann von der Entwurfszeitsteuerung eines benutzerdefinierten Berichtselements verwendet werden, um den Ausdrucks-Editor aufzurufen.  
  
#### <a name="public-methods"></a>Öffentliche Methoden  
  
|||  
|-|-|  
|**EditValue**|Ruft den mit dem angegebenen Objektwert initialisierten Ausdrucks-Editor auf.|  
  
### <a name="microsoftreportdesignerifieldsdataobject"></a>Microsoft.ReportDesigner.IFieldsDataObject  
 Diese Klasse ist eine Auflistung von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Feldern und wird zum Unterstützen von Drag und Drop-Vorgängen in der Entwurfsumgebung verwendet. Erbt von **IReportItemDataObject**.  
  
#### <a name="public-properties"></a>Öffentliche Eigenschaften  
  
|||  
|-|-|  
|**DataSetName**|Der Name des Datasets mit den Feldern, die abgelegt werden soll.|  
|**Felder**|Die Auflistung von Feldern (**Microsoft.ReportDesigner.Field**) gelöscht werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Report Definition Language &#40; SSRS &#41;](../../reporting-services/reports/report-definition-language-ssrs.md)   
 [Erstellen ein benutzerdefiniertes Element-Laufzeitkomponente](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [Erstellen einer benutzerdefinierten Bericht Element zur Entwurfszeit-Komponente](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)  
  
  
