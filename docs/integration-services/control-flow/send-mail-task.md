---
title: Task "Mail" Senden | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sendmailtask.f1
helpviewer_keywords:
- mail [Integration Services]
- Send Mail task
- e-mail [Integration Services]
- messages [Integration Services]
- sending messages
ms.assetid: fe0b7cbc-fe8e-4fe2-95b4-2953efff5869
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: fd6f7a19c1b553ee06013a4a24fbbf26a759a6cd
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

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
  
 Klicken Sie auf eines der folgenden Themen, um Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Editor für den Task „Mail senden“ &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/send-mail-task-editor-general-page.md)  
  
-   [Editor für den Task „Mail senden“ &#40;Seite „E-Mail“&#41;](../../integration-services/control-flow/send-mail-task-editor-mail-page.md)  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Klicken Sie auf das folgende Thema, um Informationen zum programmgesteuerten Festlegen dieser Eigenschaften anzuzeigen:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.SendMailTask.SendMailTask>  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 Klicken Sie auf [!INCLUDE[ssIS](../../includes/ssis-md.md)] Festlegen der Eigenschaften eines Tasks oder Containers [, um Informationen zum Festlegen dieser Eigenschaften im](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)-Designer zu erhalten.  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   Technischer Artikel [How to send email with delivery notification in C#](http://go.microsoft.com/fwlink/?LinkId=237625)(Gewusst wie: Senden von E-Mails mit Zustellungsbenachrichtigung in C#) auf shareourideas.com  
  
## <a name="see-also"></a>Siehe auch  
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)  
  
  
