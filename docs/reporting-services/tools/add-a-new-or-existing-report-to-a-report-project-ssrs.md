---
title: "Hinzufügen eines neuen oder vorhandenen Berichts zu einem Berichtsprojekt (SSRS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: tools
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: reports [Reporting Services], creating
ms.assetid: 8bc0bb53-ad8a-464d-bb6a-7fea5fa62c5c
caps.latest.revision: "20"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: e29acdb16ec95fa3e2504cef099e26f55b82b792
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="add-a-new-or-existing-report-to-a-report-project-ssrs"></a>Hinzufügen eines neuen oder vorhandenen Berichts zu einem Berichtsprojekt (SSRS)
  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]können Sie einen neuen paginierten [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Bericht hinzufügen, indem Sie den Berichts-Assistenten nutzen oder dem Projekt einen neuen, leeren Bericht hinzufügen. Darüber hinaus können Sie einen vorhandenen Bericht hinzufügen. Nachdem Sie einen Bericht hinzugefügt haben, wird der Name des Berichts im Ordner **Berichte** Ihres Projekts aufgelistet.  
  
> [!NOTE]  
>  Um eine Vorschau eines Berichts mit vorhandenen Datenquellen einzusehen, müssen Sie über die Berechtigung zur Datenquelle von Ihrem Berichtserstellungsclient verfügen. Weitere Informationen finden Sie unter [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen (Berichts-Generator und SSRS)](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
 Nachdem Sie einen Bericht hinzugefügt haben, können Sie Datenquellen und Datasets definieren und ein Berichtslayout entwerfen. Informationen zum Einstieg finden Sie unter [Erstellen eines einfachen Tabellenberichts (SSRS-Tutorial)](../../reporting-services/create-a-basic-table-report-ssrs-tutorial.md) oder [Tables (Report Builder and SSRS) (Tabellen (Berichts-Generator und SSRS))](../../reporting-services/report-design/tables-report-builder-and-ssrs.md).  
  
## <a name="to-add-a-new-report-using-the-report-wizard"></a>So fügen Sie einen neuen Bericht über den Berichts-Assistenten hinzu  
  
1.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Ordner „Berichte“, und klicken Sie dann auf **Neuen Bericht hinzufügen**. Das Dialogfeld **Berichts-Assistent** wird geöffnet.  
  
     Der Assistent führt Sie durch die Erstellung einer Datenquelle, die Erstellung eines Datasets mit einer Abfrage, die Definition von Gruppen, das Festlegen eines Layouts, und die Erstellung des Berichts. Die Schritte umfassen Folgendes:  
  
    -   **Wählen Sie eine Datenquelle aus.** Der erste Schritt beim Erstellen eines Berichts besteht im Definieren einer Datenquelle. Der Berichts-Assistent stellt eine Liste aller freigegebenen Datenquellen in dem Berichtsprojekt bereit und bietet außerdem die Option, eine neue Datenquelle zu erstellen.  
  
    -   **Entwerfen Sie eine Abfrage.** Im nächsten Schritt muss eine Abfrage entworfen werden. Sie können die Zeichenfolge der Abfrage eingeben, diese mithilfe des Abfrage-Designers erstellen oder eine Abfrage aus einem anderen Bericht importieren. Weitere Informationen über den Abfrage-Designer finden Sie unter [Reporting Services Query Designers](http://msdn.microsoft.com/library/07efd3f1-804f-45f7-b62a-3e727a3d9835).  
  
    -   **Wählen Sie einen Berichtstyp aus.** Als Nächstes muss der gewünschte Berichtstyp ausgewählt werden. Sie können zwischen einem tabellarischen Bericht und einem Matrixbericht auswählen. Ein tabellarischer Bericht verfügt über eine feste Anzahl von Spalten. Ein Matrix- oder Kreuztabellenbericht verfügt über eine variable Anzahl von Spalten, die vom Ergebnis der Abfrage abhängt. In einem Kartenbericht werden Analysedaten vor einem geografischen Hintergrund dargestellt.  
  
    -   **Geben Sie einen Namen für den Bericht ein.**  Der letzte Schritt besteht darin, einen Namen für den Bericht anzugeben und die Felder zu überprüfen, die in dem Bericht enthalten sein werden. Nach Abschluss aller Schritte wird der Bericht von Berichts-Designer erstellt und zum Berichtsserverprojekt hinzugefügt.  
  
## <a name="to-add-a-new-blank-report"></a>So fügen Sie einen neuen, leeren Bericht hinzu  
  
1.  Klicken Sie im Menü **Projekt** auf **Neues Element hinzufügen**.  
  
2.  Klicken Sie in **Vorlagen**auf **Bericht**.  
  
3.  Klicken Sie auf **Hinzufügen**.  
  
     Dem Projekt wird ein neuer, leerer Bericht hinzugefügt und auf der Entwurfsoberfläche angezeigt.  
  
## <a name="to-add-an-existing-report"></a>So fügen Sie einen vorhandenen Bericht hinzu  
  
1.  Klicken Sie im Menü **Projekt** auf **Hinzufügen**und dann auf  **Vorhandenes Element hinzufügen**.  
  
2.  Navigieren Sie zum Speicherort der RDL-Datei, markieren Sie die Datei, und klicken Sie dann auf **Hinzufügen**.  
  
     Der Bericht wird dem Projekt im Ordner **Berichte** hinzugefügt. Wenn Sie das Projekt schließen und erneut öffnen, sind die Berichte alphabetisch geordnet.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Reporting Services-Tutorials &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)  
 Haben Sie dazu Fragen? [Besuchen Sie das Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
  
  
