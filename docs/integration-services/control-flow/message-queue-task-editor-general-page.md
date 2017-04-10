---
title: "Editor f&#252;r den Task &#39;Nachrichtenwarteschlange&#39; (Seite Allgemein) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.msgqueuetask.general.f1"
helpviewer_keywords: 
  - "Editor für den Task Nachrichtenwarteschlange"
ms.assetid: 09368b18-37a5-4321-a173-7cfe5d42d2a2
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 25
---
# Editor f&#252;r den Task &#39;Nachrichtenwarteschlange&#39; (Seite Allgemein)
  Auf der Seite **Allgemein** des Dialogfelds **Editor für den Task „Nachrichtenwarteschlange“** können Sie den Task „Nachrichtenwarteschlange“ benennen und beschreiben, das Nachrichtenformat angeben und kennzeichnen, ob vom Task Nachrichten gesendet oder empfangen werden.  
  
 Informationen, um sich mit diesem Thema vertraut zu machen, finden Sie unter [Message Queue Task](../../integration-services/control-flow/message-queue-task.md).  
  
## enthalten  
 **Name**  
 Geben Sie einen eindeutigen Namen für den Task Nachrichtenwarteschlange an. Dieser Name wird im Tasksymbol als Bezeichnung verwendet.  
  
> [!NOTE]  
>  Tasknamen müssen innerhalb eines Pakets eindeutig sein.  
  
 **Description**  
 Geben Sie eine Beschreibung des Tasks Nachrichtenwarteschlange ein.  
  
 **Use2000Format**  
 Geben Sie an, ob das 2000-Format von Message Queuing (auch bekannt als MSMQ) verwendet werden soll. Der Standardwert ist **False**.  
  
 **MSMQConnection**  
 Wählen Sie einen vorhandenen MSMQ-Verbindungs-Manager aus, oder klicken Sie auf \<**Neue Verbindung…**>, um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [MSMQ Connection Manager](../../integration-services/connection-manager/msmq-connection-manager.md), [MSMQ Connection Manager Editor](../../integration-services/connection-manager/msmq-connection-manager-editor.md)  
  
 **MessageBox**  
 Geben Sie an, ob Nachrichten vom Task Nachrichtenwarteschlange gesendet oder empfangen werden. Wenn Sie **Nachricht senden** auswählen, wird im linken Bereich des Dialogfelds die Seite Senden angezeigt; wenn Sie **Nachricht empfangen** auswählen, wird die Seite Empfangen aufgelistet. Standardmäßig ist dieser Wert auf **Nachricht senden** festgelegt.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor für den Task „Nachrichtenwarteschlange“ &#40;Seite „Empfangen“&#41;](../../integration-services/control-flow/message-queue-task-editor-receive-page.md)   
 [Editor für den Task „Nachrichtenwarteschlange“ &#40;Seite „Senden“&#41;](../../integration-services/control-flow/message-queue-task-editor-send-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
  