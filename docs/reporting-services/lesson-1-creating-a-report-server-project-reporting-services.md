---
title: 'Lektion 1: Erstellen eines Berichtsserverprojekts (Reporting Services) | Microsoft-Dokumentation'
ms.custom: 
ms.date: 11/30/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
caps.latest.revision: "57"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Active
ms.openlocfilehash: ce02663b3fd39c18e692b56473afb302788c5605
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="lesson-1-creating-a-report-server-project-reporting-services"></a>Lektion 1: Erstellen eines Berichtsserverprojekts (Reporting Services)

 > Inhalt im Zusammenhang mit früheren Versionen von SQL Server finden Sie unter [Lektion 1: Erstellen eines Berichtsserverprojekts (Reporting Services)](https://msdn.microsoft.com/en-US/library/ms167559(SQL.120).aspx).

In dieser Lektion erstellen Sie in Visual Studio ein *Berichtsserverprojekt* und eine *Berichtsdefinitionsdatei (.rdl)* in [!INCLUDE[ssBIDevStudio_md](../includes/ssbidevstudio-md.md)] . 

Zum Erstellen eines Berichts mit [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]benötigen Sie zunächst ein Berichtsserverprojekt, in dem Sie Ihre Berichtsdefinitionsdatei (.rdl) und alle anderen Ressourcendateien speichern können, die für Ihren Bericht erforderlich sind. 

In den folgenden Lektionen definieren Sie eine Datenquelle für Ihren Bericht, ein Dataset sowie das Berichtslayout. Beim Ausführen des Berichts werden die Daten abgerufen und mit dem Layout kombiniert und anschließend auf dem Bildschirm gerendert. Dort können Sie sie exportieren, drucken und speichern.  
  
  
  
## <a name="to-create-a-report-server-project"></a>So erstellen Sie ein Berichtsserverprojekt  
  
1.  Öffnen Sie [!INCLUDE[ssBIDevStudio_md](../includes/ssbidevstudio-md.md)].  
  
2.  Klicken Sie im Menü **Datei** auf **Neu** > **Projekt**.  

    ![ssrs-ssdt-file-01-new-project](../reporting-services/media/ssrs-ssdt-file-01-new-project.png)
  
3.  Klicken Sie unter **Installiert** > **Vorlagen** > **Business Intelligence**auf **Reporting Services**.

    ![ssrs-ssdt-01-new-rs-project](../reporting-services/media/ssrs-ssdt-01-new-rs-project.png)

5. Klicken Sie auf **Berichtsserverprojekt** ![ssrs_ssdt_report_server_project](../reporting-services/media/ssrs-ssdt-report-server-project.png). 

   >**Hinweis**: Wenn die Optionen **Business Intelligence** oder **Berichtsserverprojekt** nicht angezeigt werden, müssen Sie SSDT mit den Business Intelligence-Vorlagen aktualisieren. Weitere Informationen finden Sie unter [Herunterladen von SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md).  
  
5.  Geben Sie im Feld **Name**den Namen **Tutorial**ein.  

    Standardmäßig wird es in Ihrem Ordner Visual Studio 2015\Projects in einem neuen Verzeichnis erstellt.
    
    ![ssrs-ssdt-01-solution-location](../reporting-services/media/ssrs-ssdt-01-solution-location.png)
  
6.  Klicken Sie auf **OK** , um das Projekt zu erstellen.  
  
    Das Projekt für das Tutorial wird rechts im Projektmappen-Explorer angezeigt.  
  
## <a name="to-create-a-new-report-definition-file"></a>So erstellen Sie eine neue Berichtsdefinitionsdatei  
  
1.  Klicken Sie mit der rechten Maustaste im **Projektmappen-Explorer** auf **Berichte** > **Hinzufügen** > **Neues Element**. 

    >**Tipp**: Wenn der **Projektmappen-Explorer** nicht geöffnet ist, klicken Sie im Menü **Ansicht** auf **Projektmappen-Explorer**. 

    ![ssrs_ssdt_Bericht_hinzufügen](../reporting-services/media/ssrs-ssdt-add-report.png)
  
2.  Klicken Sie im Fenster **Neues Element hinzufügen** auf **Bericht** ![ssrs_ssdt_report](../reporting-services/media/ssrs-ssdt-report.png).  
  
3.  Geben Sie in **Name** **Sales Orders.rdl** ein, und klicken Sie auf **Hinzufügen**.  
  
    Der Berichts-Designer wird geöffnet, und in der Entwurfsansicht wird die neue RDL-Datei angezeigt.  
    
    ![ssrs-ssdt-01-new-report-designer](../reporting-services/media/ssrs-ssdt-01-new-report-designer.png)
  
     Der Berichts-Designer ist eine [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Komponente, die in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]ausgeführt wird. Er weist zwei Ansichten auf: **Entwurf** und **Vorschau**. Klicken Sie auf die einzelnen Registerkarten, um zwischen den Ansichten zu wechseln.  
  
    Die Daten werden im **Berichtsdatenbereich** definiert. In der Ansicht **Entwurf** wird das Berichtslayout definiert. Sie können den Bericht ausführen, und in der Ansicht **Vorschau** können Sie eine Vorschau des Berichts anzeigen.  
  
## <a name="next-lesson"></a>Nächste Lektion  
Sie haben das Berichtsprojekt Tutorial erfolgreich erstellt und dem Berichtsprojekt eine Berichtsdefinitionsdatei (*.rdl) hinzugefügt. Als Nächstes geben Sie eine Datenquelle an, die für den Bericht verwendet werden soll. Weitere Informationen finden Sie unter [Lektion 2: Angeben von Verbindungsinformationen (Reporting Services)](../reporting-services/lesson-2-specifying-connection-information-reporting-services.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Erstellen eines einfachen Tabellenberichts &#40;SSRS-Tutorial&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  

