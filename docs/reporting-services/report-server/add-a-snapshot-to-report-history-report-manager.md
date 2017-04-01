---
title: "Hinzuf&#252;gen einer Momentaufnahme zum Berichtsverlauf (Berichts-Manager) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Berichtsverlauf [Reporting Services], Hinzufügen von Momentaufnahmen"
  - "Verlaufsdaten [Reporting Services]"
  - "Momentaufnahmen [Reporting Services], Hinzufügen von Berichtsmomentaufnahmen"
  - "Hinzufügen von Momentaufnahmen zum Berichtsverlauf"
  - "Berichtsmomentaufnahmen [Reporting Services], hinzufügen"
ms.assetid: 3aafb183-789e-46ac-966c-881dc549b31d
caps.latest.revision: 35
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 35
---
# Hinzuf&#252;gen einer Momentaufnahme zum Berichtsverlauf (Berichts-Manager)
  Der Berichtsverlauf stellt eine Auflistung von Berichtsmomentaufnahmen dar, die Sie im Laufe der Zeit erstellen. Ein Berichtsmomentaufnahme ist ein Bericht, der Layoutinformationen und Abfrageergebnisse enthält, die zu einem bestimmten Zeitpunkt abgerufen wurden. Während für bedarfsgesteuerte Berichte aktuelle Abfrageergebnisse abgerufen werden, wenn Sie den Bericht auswählen, werden Berichtsmomentaufnahmen anhand eines Zeitplans verarbeitet und anschließend auf einem Berichtsserver gespeichert. Wenn Sie eine Berichtsmomentaufnahme zum Anzeigen auswählen, ruft der Berichtsserver den gespeicherten Bericht aus der Berichtsserver-Datenbank ab und zeigt die Daten und das Layout an, die zum Zeitpunkt der Momentaufnahmeerstellung für den Bericht aktuell waren.  
  
 Berichtsmomentaufnahmen werden in keinem speziellen Renderingformat gespeichert. Stattdessen werden Berichtsmomentaufnahmen erst dann in einem endgültigen Anzeigeformat (wie HTML) gerendert, wenn sie von einem Benutzer oder einer Anwendung angefordert werden. Durch das verzögerte Rendering wird eine Momentaufnahme portabel. Der Bericht kann jeweils im richtigen Format für das anfordernde Gerät oder den anfordernden Webbrowser gerendert werden.  
  
### So fügen Sie dem Berichtsverlauf manuell Momentaufnahmen hinzu  
  
1.  Navigieren Sie im Berichts-Manager zur Seite **Inhalt**, und zeigen Sie auf das Element, dessen Verlauf angezeigt werden soll, und klicken Sie auf den Dropdownpfeil.  
  
2.  Klicken Sie im Dropdownmenü auf **Berichtsverlauf anzeigen**.  
  
3.  Klicken Sie auf **Neue Momentaufnahme**. In der Spalte **Ausführungszeitpunkt** wird eine neue Momentaufnahme erstellt.  
  
    > [!NOTE]  
    >  Dazu muss der Berichtsverlauf vom Administrator auf **Verlauf kann manuell erstellt werden**konfiguriert sein. Weitere Informationen finden Sie unter [Einschränken des Berichtsverlaufs &#40;Berichts-Manager&#41;](../../reporting-services/reports/limit-report-history-report-manager.md).  
  
4.  Klicken Sie auf **Anwenden**.  
  
### So fügen Sie dem Berichtsverlauf automatisch alle Momentaufnahmen hinzu  
  
1.  Für einen Bericht, der bereits für die Ausführung als Berichtsausführungs-Momentaufnahme konfiguriert ist, können Sie zusätzliche Eigenschaften festlegen, um bei jeder Aktualisierung der Momentaufnahme eine Kopie der Momentaufnahme im Berichtsverlauf zu speichern.  
  
2.  Navigieren Sie im Berichts-Manager zur Seite **Inhalt**, zeigen Sie auf das Element, dessen Verlauf angezeigt werden soll, und klicken Sie auf den Dropdownpfeil.  
  
3.  Klicken Sie im Dropdownmenü auf **Verwalten**.  
  
4.  Klicken Sie auf **Momentaufnahmeoptionen**.  
  
5.  Aktivieren Sie das Kontrollkästchen **Alle Berichtsausführungs-Momentaufnahmen im Verlauf speichern**.  
  
6.  Klicken Sie auf **Anwenden**.  
  
### So fügen Sie basierend auf einem Zeitplan automatisch Momentaufnahmen zum Berichtsverlauf hinzu  
  
1.  Navigieren Sie im Berichts-Manager zur Seite **Inhalt**, und zeigen Sie auf das Element, dessen Verlauf angezeigt werden soll, und klicken Sie auf den Dropdownpfeil.  
  
2.  Klicken Sie im Dropdownmenü auf **Verwalten**.  
  
3.  Klicken Sie auf **Momentaufnahmeoptionen**.  
  
4.  Aktivieren Sie das Kontrollkästchen für **Folgenden Zeitplan verwenden, um dem Berichtsverlauf Momentaufnahmen hinzuzufügen**. Führen Sie eine der folgenden Aktionen aus:  
  
    -   Wählen Sie **Berichtsspezifischer Zeitplan** aus. Geben Sie die Zeitplandetails ein, wählen Sie Start- und Enddatum für den Zeitplan aus, und klicken Sie dann auf **OK**.  
  
    -   Wählen Sie **Freigegebener Zeitplan**aus. Wählen Sie aus der Liste den gewünschten Zeitplan aus.  
  
5.  Klicken Sie auf **Anwenden**.  
  
## Siehe auch  
 [Konfigurieren von Ausführungseigenschaften für einen Bericht &#40;Berichts-Manager&#41;](../../reporting-services/reports/configure-execution-properties-for-a-report-report-manager.md)   
 [Öffnen und Schließen eines Berichts &#40;Berichts-Manager&#41;](../../reporting-services/reports/open-and-close-a-report-report-manager.md)   
 [Einschränken des Berichtsverlaufs &#40;Berichts-Manager&#41;](../../reporting-services/reports/limit-report-history-report-manager.md)   
 [Zeitpläne](../../reporting-services/subscriptions/schedules.md)   
 [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md)  
  
  