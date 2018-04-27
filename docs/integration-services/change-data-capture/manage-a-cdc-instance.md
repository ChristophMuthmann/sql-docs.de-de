---
title: Verwalten einer CDC-Instanz | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: change-data-capture
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- manIns
ms.assetid: cfed22c8-c666-40ca-9e73-24d93e85ba92
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8840756a2036b5c2a62d2aa456773a46167a51fe
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="manage-a-cdc-instance"></a>Verwalten einer CDC-Instanz
  Sie können die CDC Designer Console zum Anzeigen von Informationen zu den erstellten Instanzen und zum Verwalten des Betriebs der Instanzen verwenden.  
  
 Klicken Sie im linken Bereich auf den Namen einer Instanz, um die Informationen zur Instanz anzuzeigen.  
  
> [!NOTE]  
>  Wenn Sie im linken Bereich einen Dienst auswählen, wird die Liste der verfügbaren Instanzen auch im mittleren Bereich der CDC Designer Console angezeigt. Wenn Sie eine der Instanzen in diesem Abschnitt auswählen, können Sie die Tasks im rechten Bereich ausführen. Sie können jedoch nicht die Informationen auf den Registerkarten mit den Eigenschaften anzeigen.  
  
## <a name="what-you-can-do-when-you-display-the-cdc-instance-information"></a>Optionen beim Anzeigen der Informationen zur CDC-Instanz  
 Die folgenden Aktionen werden im rechten Bereich ausgeführt:  
  
 **Start**  
 Klicken Sie auf **Start** , um die Aufzeichnung der Änderungen für die ausgewählte CDC-Instanz zu starten.  
  
 **Beenden**  
 Klicken Sie auf **Beenden** , um die Aufzeichnung für die ausgewählte CDC-Instanz zu beenden. Wenn Sie die CDC-Instanz beenden, gehen die Änderungen, die bis zu diesem Punkt aufgezeichnet wurden, nicht verloren und werden übermittelt, wenn die CDC-Instanz fortgesetzt wird.  
  
 **Zurücksetzen**  
 Klicken Sie auf **Zurücksetzen** , um die CDC-Instanz auf ihren ursprünglichen (leeren) Zustand zurückzusetzen. Diese Option ist verfügbar, wenn die CDC-Instanz beendet wurde. Alle Änderungen in den Änderungstabellen und der interne Status der CDC-Instanz werden gelöscht. Wenn die CDC-Instanz später dann gestartet wird, beginnt die Änderungsaufzeichnung ab diesem Zeitpunkt und schließt nur Transaktionen ein, die nach dem Starten der CDC-Instanz gestartet wurden.  
  
 Klicken Sie im Bestätigungsdialogfeld auf **OK** , um zu bestätigen, dass Sie die CDC-Instanz zurücksetzen und die in die Änderungstabellen geschriebenen Änderungen löschen möchten.  
  
 **Delete**  
 Klicken Sie auf **Löschen** , um die CDC-Instanz dauerhaft zu löschen. Diese Option ist nur verfügbar, wenn die CDC-Instanz beendet wurde.  
  
 Klicken Sie im Bestätigungsdialogfeld auf **OK** , um zu bestätigen, dass Sie die CDC-Instanz löschen möchten.  
  
 **Oracle Logging Script**  
 Klicken Sie auf diesen Link, um das Dialogfeld Oracle Logging Script mit dem ergänzenden Oracle-Protokollierungsskript anzuzeigen. Informationen zu den Schritten, die Sie in diesem Dialogfeld ausführen können, finden Sie unter [Oracle Supplemental Logging Script](../../integration-services/change-data-capture/oracle-supplemental-logging-script.md).  
  
> [!NOTE]  
>  Wenn Sie die ergänzenden Protokollierungsskripts ausführen, wird das Dialogfeld Oracle Credentials for Running Script geöffnet, in dem Sie einen gültigen Oracle-Benutzernamen und das dazugehörige Kennwort angeben können. Informationen zum Bereitstellen der richtigen Oracle-Anmeldeinformationen finden Sie unter [Oracle Credentials for Running Script](../../integration-services/change-data-capture/oracle-credentials-for-running-script.md).  
  
 **CDC Instance Deployment Script**  
 Klicken Sie auf diesen Link, um das Dialogfeld CDC Instance Deployment Script zu öffnen, in dem das Bereitstellungsskript für die CDC-Instanz angezeigt wird. Informationen zu diesem Dialogfeld finden Sie unter [CDC Instance Deployment Script](../../integration-services/change-data-capture/cdc-instance-deployment-script.md).  
  
 **Eigenschaften**  
 Klicken Sie auf diesen Link, um den Eigenschaften-Editor zu öffnen. Sie bearbeiten die CDC-Instanzkonfiguration mithilfe des Eigenschaften-Editors. Weitere Informationen zum Bearbeiten der Eigenschaften für eine CDC-Instanz finden Sie unter [Edit Instance Properties](../../integration-services/change-data-capture/edit-instance-properties.md).  
  
 **Viewer-Registerkarten**  
  
 Die folgenden Viewer-Registerkarten sind verfügbar, wenn Sie Informationen für die CDC-Instanz anzeigen. Die Informationen auf diesen Registerkarten sind schreibgeschützt.  
  
 **Status**  
 Diese Registerkarte enthält Informationen und Statistiken zum aktuellen Status der CDC-Instanz. Sie liefert die folgenden Informationen.  
  
-   **Status**: Ein Symbol, das den aktuellen Status für die CDC-Instanz angibt. Die Status sind unten beschrieben.  
  
    |||  
    |-|-|  
    |![Fehler](../../integration-services/change-data-capture/media/error.gif "Fehler")|**Fehler**: Die Oracle CDC-Instanz wird nicht ausgeführt, da ein nicht wiederholbarer Fehler aufgetreten ist. Die folgenden Unterstatus sind verfügbar:<br /><br /> **Misconfigured**: Es ist ein Konfigurationsfehler aufgetreten, der einen manuellen Eingriff erfordert.<br /><br /> **Kennwort erforderlich**: Für die Oracle CDC-Instanz wurde kein Kennwort festgelegt, oder das Kennwort ist nicht gültig.<br /><br /> **Unerwartet**: Alle anderen nicht behebbaren Fehler.|  
    |![OK](../../integration-services/change-data-capture/media/okay.gif "OK")|**Wird ausgeführt:** Die CDC-Instanz wird ausgeführt und verarbeitet Änderungsdatensätze. Die folgenden Unterstatus sind verfügbar:<br /><br /> **Im Leerlauf**: Alle Änderungsdatensätze wurden verarbeitet und in den Zieländerungstabellen gespeichert. Es sind keine aktiven Transaktionen mehr vorhanden.<br /><br /> **Processing**: Es werden Änderungsdatensätze verarbeitet, die noch nicht in die Änderungstabellen geschrieben wurden.|  
    |![Beenden](../../integration-services/change-data-capture/media/stop.gif "Beenden")|**Beendet**: Die CDC-Instanz wird nicht ausgeführt. Der Status Beendet gibt an, dass die CDC-Instanz auf normale Weise beendet wurde.|  
    |![Angehalten](../../integration-services/change-data-capture/media/paused.gif "Angehalten")|**Angehalten**: Die CDC-Instanz wird ausgeführt, aber die Verarbeitung wurde aufgrund eines wiederholbaren Fehlers angehalten. Die folgenden Unterstatus sind verfügbar:<br /><br /> **Getrennt**: Die Verbindung zur Oracle-Quelldatenbank kann nicht hergestellt werden. Die Verarbeitung wird fortgesetzt, nachdem die Verbindung wiederhergestellt wurde.<br /><br /> **Speicher**: Der Speicher ist voll. Die Verarbeitung wird fortgesetzt, wenn zusätzlicher Speicher verfügbar wird.<br /><br /> **Logger**: Die Protokollierung ist mit Oracle verbunden, kann aber die Oracle-Transaktionsprotokolle aufgrund eines vorübergehenden Problems nicht lesen, weil z. B. ein erforderliches Transaktionsprotokoll nicht verfügbar ist.|  
  
-   **Detailed Status**: Der aktuelle Unterstatus.  
  
-   **Status Message**: Weitere Informationen zum aktuellen Status.  
  
-   **Zeitstempel**: Die Uhrzeit im UTC-Format, zu der der CDC-Status zuletzt aus der Statustabelle gelesen wurde.  
  
-   **Currently Processing**: In diesem Abschnitt können Sie die folgenden Informationen überwachen.  
  
    -   **Last transaction timestamp**: Die Ortszeit der letzten in die Änderungstabellen geschriebenen Transaktion.  
  
    -   **Last change timestamp**: Die Ortszeit der letzten Änderung, die für die Oracle CDC-Instanz in den Transaktionsprotokollen der Oracle-Quelldatenbank sichtbar ist. Hierbei werden Informationen zur aktuellen Latenzzeit der CDC-Instanz beim Lesen des Oracle-Transaktionsprotokolls bereitgestellt.  
  
    -   **Transaction log head CN:** Die letzte Änderungsnummer (CN), die aus dem Oracle-Transaktionsprotokoll gelesen wurde.  
  
    -   **Transaction log tail CN**: Die Änderungsnummer zur Wiederherstellung oder zum Neustarten der CDC-Instanz. Die Oracle CDC-Instanz greift auf diese Position zurück, falls ein Neustart durchgeführt wird oder ein anderer Fehler auftritt (einschließlich Clusterfailover).  
  
    -   **Current CN:** Die letzte Änderungsnummer (SCN) in der Oracle-Quelldatenbank (nicht das Transaktionsprotokoll).  
  
    -   **Aktive Transaktionen:** Die aktuelle Anzahl von Oracle-Quelltransaktionen, die von der Oracle CDC-Instanz verarbeitet werden und für die noch keine Entscheidung getroffen wurde (Commit/Rollback).  
  
    -   **Bereitgestellte Transaktionen:** Die aktuelle Anzahl von Oracle-Quelltransaktionen, die für die Tabelle [cdc.xdbcdc_staged_transactions](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_staged_transactions) bereitgestellt werden.  
  
-   **Indikatoren**: In diesem Abschnitt können Sie die folgenden Informationen überwachen.  
  
    -   **Completed transactions**: Die Anzahl der Transaktionen, die seit der letzten Zurücksetzung der CDC-Instanz abgeschlossen wurden. Dies schließt keine Transaktionen ein, die keine relevanten Tabellen enthalten.  
  
    -   **Written changes**: Die Anzahl der Änderungen, die in die SQL Server-Änderungstabellen geschrieben werden.  
  
 **Oracle**  
 Zeigt Informationen zur CDC-Instanz und zu ihrer Verbindung mit der Oracle-Datenbank an. Diese Registerkarte ist schreibgeschützt. Klicken Sie zum Bearbeiten dieser Eigenschaften im linken Bereich mit der rechten Maustaste auf die Instanz, und wählen Sie **Eigenschaften** aus, oder klicken Sie im rechten Bereich auf **Eigenschaften**, um das Dialogfeld mit den „Eigenschaften von \<Instanz>“ zu öffnen.  
  
 Informationen zu diesen Eigenschaften und zu deren Bearbeitung finden Sie unter [Edit the Oracle Database Properties](../../integration-services/change-data-capture/edit-the-oracle-database-properties.md).  
  
 **Tabellen**  
 Zeigt Informationen zu den in der CDC-Instanz enthaltenen Tabellen an. Spalteninformationen sind ebenfalls verfügbar. Diese Registerkarte ist schreibgeschützt. Klicken Sie zum Bearbeiten dieser Eigenschaften im linken Bereich mit der rechten Maustaste auf die Instanz, und wählen Sie **Eigenschaften** aus, oder klicken Sie im rechten Bereich auf **Eigenschaften**, um das Dialogfeld mit den „Eigenschaften von \<Instanz>“ zu öffnen.  
  
 Informationen zu diesen Eigenschaften und zu deren Bearbeitung finden Sie unter [Edit Tables](../../integration-services/change-data-capture/edit-tables.md).  
  
 **Erweitert:**  
 Zeigt die erweiterten Eigenschaften für die CDC-Instanz und die Eigenschaftswerte an. Diese Registerkarte ist schreibgeschützt. Klicken Sie zum Bearbeiten dieser Eigenschaften im linken Bereich mit der rechten Maustaste auf die Instanz, und wählen Sie **Eigenschaften** aus, oder klicken Sie im rechten Bereich auf **Eigenschaften**, um das Dialogfeld mit den „Eigenschaften von \<Instanz>“ zu öffnen.  
  
 Informationen zu diesen Eigenschaften und zu deren Bearbeitung finden Sie unter [Edit the Advanced Properties](../../integration-services/change-data-capture/edit-the-advanced-properties.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen der Instanz für die SQL Server-Änderungsdatenbank](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Anzeigen der CDC-Instanzeigenschaften](../../integration-services/change-data-capture/how-to-view-the-cdc-instance-properties.md)   
 [Bearbeiten der CDC-Instanzeigenschaften](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [Verwenden des Assistenten für neue Instanzen](../../integration-services/change-data-capture/use-the-new-instance-wizard.md)  
  
  
