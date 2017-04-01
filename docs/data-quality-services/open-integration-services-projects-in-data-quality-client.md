---
title: "&#214;ffnen von Integration Services-Projekten im Data Quality-Client | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a8bad2f1-8fb0-4d14-a978-11a5720e62d6
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# &#214;ffnen von Integration Services-Projekten im Data Quality-Client
  Die Bereinigung der DQs-Komponente in Integration Services können Sie ein bereinigungsprojekt im Batch-Modus ausführen. Manchmal möchten Sie allerdings die Bereinigungsergebnisse vielleicht in einem Integration Services-Paket überprüfen, wie Sie auch die Bereinigungsergebnisse auf der Registerkarte **Ergebnisse verwalten und anzeigen** einer Bereinigungsaktivität in einem Data Quality-Projekt in DQS überprüfen können. DQS ermöglicht es Ihnen, Integration Services-Projekte nur in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] wie ein beliebiges anderes Data Quality-Projekt im Bildschirm **Projekt öffnen** zu öffnen und eine interaktive Bereinigung der Bereinigungsergebnisse in einem Integration Services-Projekt durchzuführen.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="LimitationsRestrictions"></a> Einschränkungen  
  
-   Nur abgeschlossene Integration Services-Projekte sind im Bildschirm **Projekt öffnen** in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]verfügbar. Fehlgeschlagene und aktuell ausgeführte Projekte sind im Bildschirm **Projekt öffnen** nicht verfügbar.  
  
-   Integration Services-Projekten zu öffnen, in der interaktiven Bereinigungsphase (**Ergebnisse verwalten und anzeigen** Registerkarte) in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Sie können nicht auf die Registerkarte **Bereinigen** oder **Struktur** wechseln. Sie können nur zur Registerkarte **Exportieren** wechseln, indem Sie auf **Weiter**klicken.  
  
-   Sie können ein gesperrtes Integration Services-Projekt nicht aus [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]löschen. Zum Löschen müssen Sie es zunächst entsperren.  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Sie müssen das Ausführen eines Integration Services-Projekts, das ein Paket mit einer DQS-Bereinigungskomponente enthält, erfolgreich abgeschlossen haben, um es in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]anzuzeigen und zu öffnen.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen die Rolle „dqs_kb_editor“ oder „dqs_kb_operator“ in der Datenbank DQS_MAIN haben, um ein Integration Services-Projekt zu öffnen.  
  
  
##  <a name="Open"></a> Öffnen eines Integration Services-Projekts  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Data Quality-Projekt öffnen**. Der Bildschirm **Projekt öffnen** wird angezeigt.  
  
3.  Im Bildschirm **Projekt öffnen** können Sie ein Integration Services-Projekt auf eine der folgenden Weisen identifizieren:  
  
    1.  **Projektname**: Integrationsservices-Projekte werden mithilfe der folgenden namensterminologie aufgelistet: "Package.DQS Cleansing_*\< Datum>**\< Zeit>*_ {GUID}." Bei jeder erfolgreichen Ausführung des gleichen Pakets in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]wird ein neues Projekt auf dem Bildschirm **Projekt öffnen** aufgelistet.  
  
    2.  **Projekttyp**: Integration Services-Projekte haben **SSIS** als Projekttyp im Bildschirm **Projekt öffnen** .  
  
     Wählen Sie ein Projekt aus, und klicken Sie auf **Weiter**.  
  
4.  Integration Services-Projekt wird geöffnet, in der interaktiven Bereinigungsphase (**Ergebnisse verwalten und anzeigen** Registerkarte). Sie können eine interaktive Bereinigung für die Daten im Integration Services-Projekt ausführen. Ausführliche Informationen zu den **Verwalten und Anzeigen der Ergebnisse** finden Sie unter [interaktive Bereinigungsphase](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Interactive) in [Bereinigen von Daten mithilfe von DQS &#40; intern &#41; Knowledge](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md).  
  
5.  Klicken Sie auf **Weiter** , um zur Registerkarte **Exportieren** zu wechseln, wo Sie die verarbeiteten Daten in eine neue Tabelle in der SQL Server-Datenbank, eine CSV-Datei oder eine Excel-Datei exportieren können. Ausführliche Informationen zu den **exportieren** finden Sie unter [Exportphase](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Export) in [Bereinigen von Daten mithilfe von DQS &#40; intern &#41; Knowledge](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)  
  
6.  Klicken Sie nach dem Exportieren der Daten auf **Fertig stellen** , um das Integration Services-Projekt zu schließen.  

  
## Siehe auch  
 [DQS-Bereinigungstransformation](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)   
 [SQL Server Integration Services (SSIS)-Projekte](https://msdn.microsoft.com/library/ms138028.aspx)  
  
  