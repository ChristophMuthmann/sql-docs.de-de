---
title: "Öffnen von Integration Services-Projekten im Data Quality-Client | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a8bad2f1-8fb0-4d14-a978-11a5720e62d6
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cfdebd7cafbdd2918ca69972b81c9a2f87933de1
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="open-integration-services-projects-in-data-quality-client"></a>Öffnen von Integration Services-Projekten im Data Quality-Client
  Die Komponente zur DQS-Bereinigung in Integration Services ermöglicht Ihnen das Ausführen eines Bereinigungsprojekts im Batchmodus. Manchmal möchten Sie allerdings die Bereinigungsergebnisse vielleicht in einem Integration Services-Paket überprüfen, wie Sie auch die Bereinigungsergebnisse auf der Registerkarte **Ergebnisse verwalten und anzeigen** einer Bereinigungsaktivität in einem Data Quality-Projekt in DQS überprüfen können. DQS ermöglicht es Ihnen, Integration Services-Projekte nur in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] wie ein beliebiges anderes Data Quality-Projekt im Bildschirm **Projekt öffnen** zu öffnen und eine interaktive Bereinigung der Bereinigungsergebnisse in einem Integration Services-Projekt durchzuführen.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="LimitationsRestrictions"></a> Einschränkungen  
  
-   Nur abgeschlossene Integration Services-Projekte sind im Bildschirm **Projekt öffnen** in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]verfügbar. Fehlgeschlagene und aktuell ausgeführte Projekte sind im Bildschirm **Projekt öffnen** nicht verfügbar.  
  
-   Integration Services-Projekte werden in der interaktiven Bereinigungsphase in (Registerkarte**Ergebnisse verwalten und anzeigen** ) in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]geöffnet. Sie können nicht auf die Registerkarte **Bereinigen** oder **Struktur** wechseln. Sie können nur zur Registerkarte **Exportieren** wechseln, indem Sie auf **Weiter**klicken.  
  
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
  
    1.  **Projektname**: Die Auflistung von Integration Services-Projekten erfolgt anhand der folgenden Namensterminologie: „Package.DQS Cleansing_*\<DATE>**\<TIME>*_{GUID}“. Bei jeder erfolgreichen Ausführung des gleichen Pakets in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]wird ein neues Projekt auf dem Bildschirm **Projekt öffnen** aufgelistet.  
  
    2.  **Projekttyp**: Integration Services-Projekte haben **SSIS** als Projekttyp im Bildschirm **Projekt öffnen** .  
  
     Wählen Sie ein Projekt aus, und klicken Sie auf **Weiter**.  
  
4.  Das Integration Services-Projekt wird in der interaktiven Bereinigungsphase (Registerkarte**Ergebnisse verwalten und anzeigen** ) geöffnet. Sie können eine interaktive Bereinigung für die Daten im Integration Services-Projekt ausführen. Ausführliche Informationen zur Registerkarte **Ergebnisse verwalten und anzeigen** finden Sie unter [Interaktive Bereinigungsphase](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Interactive) in [Bereinigen von Daten mit &#40;internem&#41; DQS-Wissen](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md).  
  
5.  Klicken Sie auf **Weiter** , um zur Registerkarte **Exportieren** zu wechseln, wo Sie die verarbeiteten Daten in eine neue Tabelle in der SQL Server-Datenbank, eine CSV-Datei oder eine Excel-Datei exportieren können. Ausführliche Informationen zur Registerkarte **Exportieren** finden Sie unter [Exportphase](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Export) in [Bereinigen von Daten mit &#40;internem&#41; DQS-Wissen](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md).  
  
6.  Klicken Sie nach dem Exportieren der Daten auf **Fertig stellen** , um das Integration Services-Projekt zu schließen.  

  
## <a name="see-also"></a>Siehe auch  
 [DQS-Bereinigungstransformation](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)   
 [Integration Services-Projekte (SSIS)](https://msdn.microsoft.com/library/ms138028.aspx)  
  
  
