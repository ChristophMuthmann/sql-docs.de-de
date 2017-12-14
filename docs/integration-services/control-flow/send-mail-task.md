---
title: Mail senden (Task) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sendmailtask.f1
- sql13.dts.designer.sendmailtask.general.f1
- sql13.dts.designer.sendmailtask.mail.f1
helpviewer_keywords:
- mail [Integration Services]
- Send Mail task
- e-mail [Integration Services]
- messages [Integration Services]
- sending messages
ms.assetid: fe0b7cbc-fe8e-4fe2-95b4-2953efff5869
caps.latest.revision: "51"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a810d72817ebdf5a1078e95315adb755a2d42891
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="send-mail-task"></a>Mail senden (Task)
  Der Task 'Mail senden' sendet eine E-Mail. Mithilfe des Tasks 'Mail senden' kann ein Paket Nachrichten senden, wenn Tasks im Paket-Workflow erfolgreich ausgeführt werden oder einen Fehler erzeugen, oder Nachrichten als Antwort auf ein Ereignis senden, das vom Paket zur Laufzeit ausgelöst wird. Beispielsweise kann mit diesem Task ein Datenbankadministrator über das erfolgreiche Ausführen des Tasks Datenbank sichern benachrichtigt werden.  
  
 Es gibt folgende Möglichkeiten, um den Task Mail senden zu konfigurieren:  
  
-   Geben Sie den Nachrichtentext für die E-Mail-Nachricht ein.  
  
-   Geben Sie ein Betreffzeile für die E-Mail-Nachricht ein.  
  
-   Legen Sie die Prioritätsstufe der Nachricht fest. Dieser Task unterstützt drei Prioritätsebenen: normal, niedrig und hoch.  
  
-   Geben Sie in den Zeilen An, Cc und Bcc die Empfänger an. Falls für den Task mehrere Empfänger angegeben sind, werden sie durch Semikolons getrennt.  
  
    > [!NOTE]  
    >  Die Zeilen An, Cc und Bcc sind auf 256 Zeichen in Übereinstimmung mit den Internetstandards begrenzt.  
  
-   Fügen Sie Anlagen hinzu. Falls für den Task mehrere Anlagen angegeben sind, werden sie durch einen senkrechten Strich (|) getrennt.  
  
    > [!NOTE]  
    >  Falls beim Ausführen des Pakets eine Anlagedatei nicht vorhanden ist, wird ein Fehler gemeldet.  
  
-   Geben Sie den zu verwendenden SMTP-Verbindungs-Manager an.  
  
    > [!IMPORTANT]  
    >  Der SMTP-Verbindungs-Manager unterstützt nur die anonyme Authentifizierung und die Windows-Authentifizierung. Er unterstützt keine Standardauthentifizierung.  
  
 Der Nachrichtentext kann eine von Ihnen eingegebene Zeichenfolge sein, eine Verbindung mit einer Datei, die den Text enthält, oder der Name einer Variablen, die den Text enthält. Dieser Task verwendet einen Dateiverbindungs-Manager, um eine Verbindung mit einer Datei herzustellen. Weitere Informationen finden Sie unter [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 Dieser Task verwendet einen SMTP-Verbindungs-Manager, um eine Verbindung mit einem Mailserver herzustellen. Weitere Informationen finden Sie unter [SMTP Connection Manager](../../integration-services/connection-manager/smtp-connection-manager.md).  
  
## <a name="custom-logging-messages-available-on-the-send-mail-task"></a>Verfügbare benutzerdefinierte Meldungen für die Protokollierung für den Task 'Mail senden'  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Task 'Mail senden' aufgelistet. Weitere Informationen finden Sie unter [Integration Services-Protokollierung &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**SendMailTaskBegin**|Zeigt an, dass das Senden einer E-Mail-Nachricht begonnen wurde.|  
|**SendMailTaskEnd**|Zeigt an, dass das Senden einer E-Mail-Nachricht beendet wurde.|  
|**SendMailTaskInfo**|Enthält beschreibende Informationen zum Task.|  
  
## <a name="configuring-the-send-mail-task"></a>Konfigurieren des Tasks Mail senden  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf das folgende Thema, um Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Klicken Sie auf das folgende Thema, um Informationen zum programmgesteuerten Festlegen dieser Eigenschaften anzuzeigen:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.SendMailTask.SendMailTask>  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 Klicken Sie auf [!INCLUDE[ssIS](../../includes/ssis-md.md)] Festlegen der Eigenschaften eines Tasks oder Containers [, um Informationen zum Festlegen dieser Eigenschaften im](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)-Designer zu erhalten.  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   Technischer Artikel [How to send email with delivery notification in C#](http://go.microsoft.com/fwlink/?LinkId=237625)(Gewusst wie: Senden von E-Mails mit Zustellungsbenachrichtigung in C#) auf shareourideas.com  
  
## <a name="send-mail-task-editor-general-page"></a>Editor für den Task 'Mail senden' (Seite Allgemein)
  Auf der Seite **Allgemein** des Dialogfelds **Editor für den Task 'Mail senden'** können Sie einen Namen und eine Beschreibung für den Task 'Mail senden' angeben.  
  
### <a name="options"></a>enthalten  
 **Name**  
 Geben Sie einen eindeutigen Namen für den Task 'Mail senden' an. Dieser Name wird im Tasksymbol als Bezeichnung verwendet.  
  
 **Hinweis** Der Taskname muss innerhalb eines Pakets eindeutig sein.  
  
 **Description**  
 Geben Sie eine Beschreibung des Tasks 'Mail senden' ein.  
  
## <a name="send-mail-task-editor-mail-page"></a>Editor für den Task 'Mail senden' (Seite E-Mail)
  Auf der Seite **E-Mail** im Dialogfeld **Editor für den Task „Mail senden“** können Sie die Empfänger, den Nachrichtentyp und die Priorität einer Nachricht angeben. Sie können der Nachricht auch Dateien anfügen. Bei dem Nachrichtentext kann es sich um eine bereitgestellte Zeichenfolge, eine Dateiverbindung mit einer Datei mit Text oder den Namen einer Variablen mit Text handeln.  
  
### <a name="options"></a>enthalten  
 **SMTPConnection**  
 Wählen Sie in der Liste einen SMTP-Verbindungs-Manager aus, oder klicken Sie auf **\<Neue Verbindung…>**, um einen neuen Verbindungs-Manager zu erstellen.  
  
> [!IMPORTANT]  
>  Der SMTP-Verbindungs-Manager unterstützt nur die anonyme Authentifizierung und die Windows-Authentifizierung. Er unterstützt keine Standardauthentifizierung.  
  
 **Verwandte Themen:** [SMTP-Verbindungs-Manager](../../integration-services/connection-manager/smtp-connection-manager.md)  
  
 **Von**  
 Geben Sie die E-Mail-Adresse des Absenders an.  
  
 **Aktion**  
 Stellen Sie die E-Mail-Adresse der Empfänger bereit. Verwenden Sie als Trennzeichen ein Semikolon.  
  
 **Cc**  
 Geben Sie die E-Mail-Adressen der Personen an, die Kopien der Nachricht erhalten sollen. Verwenden Sie als Trennzeichen ein Semikolon.  
  
 **Bcc**  
 Geben Sie die E-Mail-Adressen der Personen an, die Blindkopien der Nachricht erhalten sollen. Verwenden Sie als Trennzeichen ein Semikolon.  
  
 **Betreff**  
 Geben Sie einen Betreff für die E-Mail-Nachricht an.  
  
 **MessageSourceType**  
 Wählen Sie den Quelltyp der Nachricht aus. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Direct input**|Legen Sie für die Quelle den Nachrichtentext fest. Bei Auswahl dieses Wertes wird die dynamische Option **MessageSource**angezeigt.|  
|**File connection**|Legen Sie für die Quelle die Datei fest, die den Nachrichtentext enthält. Bei Auswahl dieses Wertes wird die dynamische Option **MessageSource**angezeigt.|  
|**Variable**|Legen Sie für die Quelle eine Variable fest, die den Nachrichtentext enthält. Bei Auswahl dieses Wertes wird die dynamische Option **MessageSource**angezeigt.|  
  
 **Priority**  
 Legen Sie die Priorität der Nachricht fest.  
  
 **Attachments**  
 Geben Sie die Dateinamen der Anlagen für die E-Mail-Nachricht an. Verwenden Sie als Trennzeichen das Pipe-Zeichen (|).  
  
> [!NOTE]  
>  Die Zeilen An, Cc und Bcc sind in Übereinstimmung mit Internetstandards auf 256 Zeichen begrenzt.  
  
### <a name="messagesourcetype-dynamic-options"></a>MessageSourceType (dynamische Optionen)  
  
#### <a name="messagesourcetype--direct-input"></a>MessageSourceType = Direct Input  
 **MessageSource**  
 Geben Sie den Nachrichtentext ein, oder klicken Sie auf die Schaltfläche zum Durchsuchen (…), und geben Sie die Nachricht in das Dialogfeld **Nachrichtenquelle** ein.  
  
#### <a name="messagesourcetype--file-connection"></a>MessageSourceType = File connection  
 **MessageSource**  
 Wählen Sie in der Liste einen Dateiverbindungs-Manager aus, oder klicken Sie auf \<**Neue Verbindung...**>, um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="messagesourcetype--variable"></a>MessageSourceType = Variable  
 **MessageSource**  
 Wählen Sie in der Liste eine Variable aus, oder klicken Sie auf \<**Neue Variable…**>, um eine neue Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Hinzufügen von Variablen](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="see-also"></a>Siehe auch  
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)  
  
  
