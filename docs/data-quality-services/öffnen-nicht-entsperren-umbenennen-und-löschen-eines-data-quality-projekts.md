---
title: "&#214;ffnen, nicht entsperren, umbenennen und L&#246;schen eines Data Quality-Projekts | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dqs.dqproject.opendqproject.f1"
helpviewer_keywords: 
  - "Data Quality-Projekt, löschen"
  - "Data Quality-Projekt, umbenennen"
  - "Data Quality-Projekt, entsperren"
  - "Data Quality-Projekt, öffnen"
ms.assetid: de8a2b04-4673-4beb-b4cf-96a28cdf3a93
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# &#214;ffnen, nicht entsperren, umbenennen und L&#246;schen eines Data Quality-Projekts
  In diesem Thema wird beschrieben, wie ein Data Quality-Projekt mithilfe von [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] verwaltet wird, zum Beispiel das Öffnen, Entsperren, Umbenennen und Löschen eines Data Quality-Projekts.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="LimitationsRestrictions"></a> Einschränkungen  
  
-   Sie können kein gesperrtes Projekt öffnen, das von einem anderen Benutzer erstellt wurde.  
  
-   Sie können kein Data Quality-Projekt entsperren, umbenennen oder löschen, das von einem anderen Benutzer erstellt wurde.  
  
-   Sie können kein gesperrtes Data Quality-Projekt löschen. Zum Löschen müssen Sie es zunächst entsperren.  
  
-   Sie können nur ein Data Quality-Projekt entsperren, das von Ihnen erstellt wurde.  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Sie müssen mindestens ein Data Quality-Projekt verwalten.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die Rolle „dqs_kb_editor“ oder „dqs_kb_operator“ in der Datenbank DQS_MAIN verfügen, um ein Data Quality-Projekt zu verwalten.  
  
##  <a name="Open"></a> Öffnen eines Data Quality-Projekts  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Data Quality-Projekt öffnen**. Der Bildschirm **Projekt öffnen** wird angezeigt.  
  
     Sie können ein unter **Zuletzt verwendetes Data Quality-Projekt** aufgelistetes Data Quality-Projekt auch direkt öffnen, indem Sie darauf klicken.  
  
3.  Wählen Sie auf dem Bildschirm **Projekt öffnen** das zu öffnende Data Quality-Projekt durch Klicken aus, und klicken Sie auf **Weiter**.  
  
4.  Das Data Quality-Projekt wird mit demselben Aktivitätsstatus geöffnet, mit dem es zuletzt geschlossen wurde. Ein Data Quality-Projekt hat die folgenden Status:  
  
    -   Für die **Bereinigung** Aktivität Data Quality-Projekten kann die folgenden Status haben: **Bereinigung - Karte**, **Bereinigung - Bereinigen**, **Bereinigung-Ergebnisse verwalten und anzeigen**, und **Bereinigung-Export**.  
  
    -   Für die **Abgleich** Aktivität Data Quality-Projekten kann die folgenden Status haben: **Abgleich - Zuordnung**, **Abgleich - Übereinstimmung**, **Abgleich-Survivorship**, und **Abgleich-Export**.  
  
##  <a name="Unlock"></a> Entsperren eines Data Quality-Projekts  
 Wenn Sie ein Data Quality-Projekt erstellen, ist es gesperrt, um zu verhindern, dass es von anderen Benutzern verwendet oder geändert wird. Sie müssen das Data Quality-Projekt entsperren, nachdem Sie die Arbeit abgeschlossen haben, wenn Sie möchten, dass andere Benutzer am Data Quality-Projekt arbeiten können. Ein Schlosssymbol wird für gesperrte Projekte angezeigt.  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Data Quality-Projekt öffnen**. Der Bildschirm **Projekt öffnen** wird angezeigt.  
  
3.  In der **Projekt öffnen** Bildschirm mit der rechten Maustaste ein gesperrtes Data Quality-Projekt, das von Ihnen erstellt wurde, und klicken Sie dann auf **Unlock** im Kontextmenü. Ein grünes Häkchen wird für das Projekt angezeigt, das angibt, dass es entsperrt wurde.  
  
##  <a name="Rename"></a> Umbenennen eines Data Quality-Projekts  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Data Quality-Projekt öffnen**. Der Bildschirm **Projekt öffnen** wird angezeigt.  
  
3.  In der **Projekt öffnen** Bildschirm mit der rechten Maustaste ein Data Quality-Projekt, das von Ihnen erstellt wurde, und klicken Sie dann auf **Umbenennen** im Kontextmenü.  
  
4.  Der Name des Data Quality-Projekts kann in der Spalte **Name** bearbeitet werden. Heben Sie einen neuen Namen ein, und drücken Sie die EINGABETASTE.  
  
##  <a name="Delete"></a> Löschen eines Data Quality-Projekts  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Data Quality-Projekt öffnen**. Der Bildschirm **Projekt öffnen** wird angezeigt.  
  
3.  In der **Projekt öffnen** Bildschirm mit der rechten Maustaste ein entsperrtes Data Quality-Projekt, die von Ihnen erstellt wurde, und klicken Sie dann auf **Löschen** im Kontextmenü.  
  
4.  Eine Bestätigungsmeldung wird angezeigt. Klicken Sie auf **Ja**.  
  
  