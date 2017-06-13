---
title: Entwurfsansicht | Microsoft Docs
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rtp.rptdesigner.layoutview.f1
helpviewer_keywords:
- Layout View dialog box
ms.assetid: 6fa378aa-442f-4d2f-beab-02a0fb5cd3ce
caps.latest.revision: 38
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7a3129645fd110b2bddedae0022592a74fb97a9e
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="design-view"></a>Entwurfsansicht
Im [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Berichtsdesigner können Sie mithilfe der Entwurfsansicht Berichtselemente im Bericht anordnen. Die Entwurfsansicht wird auch als Entwurfsoberfläche oder Layoutansicht bezeichnet.  
  ![ssrs_ssdt_preview](../../reporting-services/media/ssrs-ssdt-preview.png)
## <a name="report-design-surface"></a>Berichtsentwurfsoberfläche  
Die Entwurfsoberfläche besteht aus drei Abschnitten: 
+ Hauptteil des Berichts
+ Kopfzeile
+ Fußzeile 

Mithilfe der Toolbox können Sie Elemente auswählen, die in einem dieser drei Abschnitte platziert werden sollen. Verwenden Sie den Berichtsdatenbereich, um Bilder, Parameter, Datenquellen und Datasets, einschließlich Datasetabfragen und Feldlisten, anzuzeigen. Nachdem Sie Berichtselemente zur Entwurfsoberfläche hinzugefügt haben, ziehen Sie Datasetfelder aus dem **Berichtsdatenbereich** in Datenregionen wie eine Tabelle, Matrix oder Liste. Jedes Element in der Berichtsentwurfsoberfläche enthält Eigenschaften, die mithilfe eines Eigenschaftendialogfelds oder des Bereichs Eigenschaften verwaltet werden können.  
  
## <a name="toolbox"></a>Toolbox  
 Die Toolbox listet Datenbereiche und andere Berichtselemente auf, die für den Bericht verfügbar sind. Doppelklicken Sie auf das entsprechende Symbol, oder ziehen Sie das Symbol auf die Entwurfsoberfläche, um Berichtselemente aus der Toolbox hinzuzufügen. Sie können anschließend die Form und die Größe mithilfe der Objekthandles ändern.  
  
## <a name="report-data-pane"></a>Berichtsdatenbereich  
 Zum Anzeigen des Berichtsdatenbereichs klicken Sie im Menü **Ansicht** auf **Berichtsdaten**. Verwenden Sie diesen Bereich zum Definieren von Parametern, Bildern, Datenquellen und Datasets sowie zum Verweisen auf integrierte Felder, wie ReportName. Um ein neues Element hinzuzufügen, klicken Sie auf das Menü **Neu** , und wählen Sie ein Element aus. Um berechnete Felder einem vorhandenen Dataset hinzuzufügen, klicken Sie auf **Dataset**, und wählen Sie im Dialogfeld **Dataseteigenschaften** den Eintrag **Felder**aus. Wählen Sie ein Element aus, und klicken Sie auf **Bearbeiten** , um das Dialogfeld **Eigenschaften** zu öffnen. Sie können auch mit der rechten Maustaste im Berichtsdatenbereich auf Elemente klicken, um Elemente hinzuzufügen oder ihre Eigenschaften zu aktualisieren.  
  
 Ziehen Sie Elemente aus dem Berichtsdatenbereich auf die Datenbereiche und Textfelder auf der Entwurfsoberfläche, um einem Bericht Daten und Bilder hinzuzufügen.  
  
 Weitere Informationen finden Sie unter [Report Data Pane](../../reporting-services/report-data/report-data-pane.md).  
  
## <a name="grouping-pane"></a>Gruppierungsbereich  
 Gruppen werden verwendet, um die Berichtsdaten in einer visuellen Hierarchie zu organisieren und Ergebnisse zu berechnen. Verwenden Sie den Gruppierungsbereich, um die für eine Tabelle, Matrix oder Liste definierten Gruppen anzuzeigen. Standardmäßig werden im Gruppierungsbereich alle Gruppen für den ausgewählten Datenbereich als vereinfachte Liste angezeigt. Der Gruppierungsbereich ist für Diagramm- und Messgerätdatenbereiche deaktiviert.  
  
 Um die Gruppen in Beziehung zueinander zu sehen, schalten Sie den Gruppierungsbereich in den Erweiterten Modus. Dieser Modus zeigt die Hierarchie der Gruppenmitglieder als visuelle Darstellung von Zellen in einem Datenbereich an, die den einzelnen Gruppen entsprechen.  
  
 Weitere Informationen finden Sie unter [Grouping Pane](../../reporting-services/tools/grouping-pane.md).  
  
## <a name="page-header-and-page-footer"></a>Seitenkopf und Seitenfuß  
 Eine Seitenkopf- und Seitenfußzeile verläuft jeweils am oberen bzw. unteren Rand jeder Seite. Kopf- und Fußzeilen können statischen Text, Bilder, Linien, Rechtecke, Rahmen, Hintergrundfarbe und Hintergrundbilder enthalten. Zum Hinzufügen von Berichtselementen zur Kopf- oder Fußzeile klicken Sie mit der rechten Maustaste auf die Entwurfsoberfläche, und wählen Sie den gewünschten Eintrag für die Kopf- oder Fußzeile aus. Der Bereich für Kopf- und Fußzeilen wird auf der Entwurfsoberfläche angezeigt.  
  
## <a name="properties-pane"></a>Eigenschaftenbereich  
 Verwenden Sie den Bereich Eigenschaften, um Eigenschaften für das ausgewählte Berichtselement auf der Entwurfsoberfläche oder die ausgewählte Gruppe im Gruppierungsbereich anzuzeigen. Alternativ können Sie mit der rechten Maustaste auf das ausgewählte Berichtselement oder die Gruppe klicken und anschließend auf **Eigenschaften** klicken, um das entsprechende Dialogfeld **Eigenschaften** für das Berichtselement oder die Gruppe zu öffnen.  
  
## <a name="see-also"></a>Siehe auch  
 [Seitenkopf- und Seitenfußzeilen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [Berichtsentwurfstipps &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-design-tips-report-builder-and-ssrs.md)  
  
  

