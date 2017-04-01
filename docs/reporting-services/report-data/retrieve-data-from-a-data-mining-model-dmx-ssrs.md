---
title: "Abrufen von Daten aus einem Data Mining-Modell (DMX) (SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Abrufen von Berichtsdaten"
  - "Datasets [Reporting Services], mit DMX-Abfragen"
  - "Datasets [Reporting Services], Analysis Services"
  - "Abfragen [Reporting Services], Datamining-Vorhersage"
ms.assetid: d9cd3624-1594-4707-8887-55437dd7e07c
caps.latest.revision: 19
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 19
---
# Abrufen von Daten aus einem Data Mining-Modell (DMX) (SSRS)
  Zur Verwendung von Daten aus einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Data Mining-Modell in Ihrem Bericht müssen Sie eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenquelle und mindestens ein Berichtsdataset definieren. Sie müssen beim Erstellen der Datenquellendefinition eine Verbindungszeichenfolge sowie Anmeldeinformationen angeben, damit Sie von Ihrem Clientcomputer auf die Datenquelle zugreifen können.  
  
 Sie können eine eingebettete Datenquellendefinition für die Verwendung in einem Bericht oder eine freigegebene Datenquellendefinition für die Verwendung durch mehrere Berichte erstellen. Die Verfahren in diesem Thema beschreiben, wie eine eingebettete Datenquelle erstellt wird. Weitere Informationen zu freigegebenen Datenquellen finden Sie unter [Eingebettete und freigegebene Datenverbindungen oder Datenquellen &#40;Berichts-Generator und SSRS&#41;](../Topic/Embedded%20and%20Shared%20Data%20Connections%20or%20Data%20Sources%20\(Report%20Builder%20and%20SSRS\).md) und [Erstellen, Ändern und Löschen von freigegebenen Datenquellen &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md).  
  
 Nachdem Sie eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenquelle erstellt haben, können Sie ein oder mehrere Datasets erstellen. Für jedes Dataset verwenden Sie einen DMX-Abfrage-Designer (Data Mining-Vorhersageabfrage) zur Erstellung einer DMX-Abfrage, die die Feldauflistung angibt. Weitere Informationen finden Sie unter [Analysis Services DMX Query Designer User Interface](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md).  
  
 Nachdem Sie ein Dataset erstellt haben, wird der Name des Datasets im Berichtsdatenbereich als Knoten unter seiner Datenquelle angezeigt.  
  
 Nachdem Sie den Bericht veröffentlicht haben, müssen Sie eventuell die Anmeldeinformationen für die Datenquelle ändern, sodass die Berechtigungen zum Abrufen der Daten beim Ausführen des Berichts auf dem Berichtsserver gültig sind.  
  
### So erstellen Sie eine eingebettete Microsoft SQL Server Analysis Services-Datenquelle  
  
1.  Klicken Sie im Berichtsdatenbereich auf der Symbolleiste auf **Neu**und anschließend auf **Datenquelle**.  
  
2.  Geben Sie im Dialogfeld **Datenquelleneigenschaften** im Textfeld **Name** einen Namen ein, oder übernehmen Sie den Standardnamen.  
  
3.  Überprüfen Sie, ob **Eingebettete Verbindung** aktiviert ist.  
  
4.  Wählen Sie in der Dropdownliste **Typ** die Option **Microsoft SQL Server Analysis Services** aus.  
  
5.  Geben Sie eine Verbindungszeichenfolge an, die für Ihre [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenquelle verwendet werden kann.  
  
     Erfragen Sie bei Ihrem Datenbankadministrator die Verbindungsinformationen und die Anmeldeinformationen, die verwendet werden sollen, um eine Verbindung mit der Datenquelle herzustellen. Die Verbindungszeichenfolge im folgenden Beispiel gibt die [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] -Beispieldatenbank auf dem lokalen Client an.  
  
    ```  
    Data Source=localhost;Initial Catalog=AdventureWorksDW2012  
    ```  
  
6.  Klicken Sie auf **Anmeldeinformationen**.  
  
     Legen Sie die Anmeldeinformationen fest, die für eine Verbindung mit der Datenquelle verwendet werden sollen. Weitere Informationen finden Sie unter [Specify Credential and Connection Information for Report Data Sources](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
    > [!NOTE]  
    >  Um die Datenquellenverbindung zu testen, klicken Sie auf **Bearbeiten**. Klicken Sie im Dialogfeld **Verbindungseigenschaften** auf **Verbindung testen**. Wenn der Test erfolgreich ist, sehen Sie die Informationsmeldung "Der Verbindungstest war erfolgreich". Wenn der Test fehlschlägt, wird eine Warnmeldung mit weiteren Informationen darüber angezeigt, warum der Test nicht erfolgreich war.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Die Datenquelle wird im Berichtsdatenbereich angezeigt.  
  
### So erstellen Sie ein Dataset für eine Microsoft SQL Server Analysis Services-Datenquelle  
  
1.  Klicken Sie im Bereich **Berichtsdaten** mit der rechten Maustaste auf den Namen der Datenquelle, die eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Datenquelle herstellt, und klicken Sie dann auf **Dataset hinzufügen**.  
  
2.  Geben Sie im Dialogfeld **Dataseteigenschaften** im Textfeld **Name** einen Namen ein.  
  
3.  Überprüfen Sie im Textfeld **Datenquelle**, es sich um den Namen einer Datenquelle handelt, die eine Verbindung mit einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenquelle herstellt.  
  
4.  Klicken Sie auf **Abfrage-Designer** , um den grafischen Abfrage-Designer zu öffnen und interaktiv eine Abfrage zu erstellen. Wenn der Abfrage-Designer im MDX-Modus geöffnet wird, klicken Sie auf der Symbolleiste auf **DMX-Befehlstyp** (![Ändern der Anzeige der DMX-Abfragesprache](../../reporting-services/report-data/media/rsqdicon-commandtypedmx.png "Ändern der Anzeige der DMX-Abfragesprache")), um zum Data Mining-Abfrage-Designer zu wechseln. Weitere Informationen finden Sie unter [Analysis Services DMX Query Designer User Interface](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md).  
  
     Um eine vorhandene DMX-Abfrage aus einem anderen Bericht zu importieren, können Sie auch auf **Importieren**klicken und dann zur RDL-Datei mit der DMX-Abfrage navigieren. Das Importieren einer Abfrage aus einer DMX-Datei wird nicht unterstützt.  
  
5.  Nachdem Sie die Abfrage erstellt und ausgeführt haben, um Beispielergebnisse zu sehen, klicken Sie auf **OK**.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Das Dataset und seine Feldauflistung werden im Berichtsdatenbereich unter dem Datenquellenknoten angezeigt.  
  
## Siehe auch  
 [Analysis Services-Verbindungstyp für DMX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)   
 [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Datasetfeld-Auflistung &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  