---
title: "Task &#39;Nachrichtenwarteschlange&#39; (Seite Senden) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.msgqueuetask.send.f1"
helpviewer_keywords: 
  - "Editor für den Task Nachrichtenwarteschlange"
ms.assetid: 565aa079-ac44-4407-8efc-cddab839de30
caps.latest.revision: 37
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 37
---
# Task &#39;Nachrichtenwarteschlange&#39; (Seite Senden)
  Im Dialogfeld **Editor für den Task 'Nachrichtenwarteschlange'** können Sie auf der Seite **Senden** den Task Nachrichtenwarteschlange so konfigurieren, dass Nachrichten von einem [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket gesendet werden.  
  
 Informationen, um sich mit diesem Thema vertraut zu machen, finden Sie unter [Message Queue Task](../../integration-services/control-flow/message-queue-task.md).  
  
## enthalten  
 **UseEncryption**  
 Geben Sie an, ob die Nachricht verschlüsselt werden soll. Der Standardwert ist **False**.  
  
 **EncryptionAlgorithm**  
 Wenn Sie die Verschlüsselung verwenden möchten, müssen Sie den Namen des verwendeten Verschlüsselungsalgorithmus angeben. Für den Task "Nachrichtenwarteschlange" können die Algorithmen RC2 und RC4 verwendet werden. Die Standardeinstellung lautet **RC2**.  
  
> [!NOTE]  
>  Der RC4-Algorithmus wird nur aus Gründen der Abwärtskompatibilität unterstützt. Neues Material kann nur mit RC4 oder RC4_128 verschlüsselt werden, wenn die Datenbank den Kompatibilitätsgrad 90 oder 100 besitzt. (Nicht empfohlen.) Verwenden Sie stattdessen einen neueren Algorithmus, z. B. einen der AES-Algorithmen. In der aktuellen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann mit RC4 oder RC4_128 verschlüsseltes Material in jedem Kompatibilitätsgrad entschlüsselt werden.  
  
> [!IMPORTANT]  
>  Diese Verschlüsselungsalgorithmen werden von der Message Queuing-Technologie (auch bekannt als MSMQ) unterstützt. Diese Verschlüsselungsalgorithmen werden inzwischen im Vergleich zu neueren Algorithmen, die von Message Queuing noch nicht unterstützt werden, beide als kryptografisch schwach betrachtet. Daher sollten Sie Ihren Kryptografiebedarf sorgfältig überdenken, wenn Sie Nachrichten mithilfe des Tasks Nachrichtenwarteschlange senden.  
  
 **MessageType**  
 Wählen Sie den Nachrichtentyp aus. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Data file message**|Die Nachricht wird in einer Datei gespeichert. Bei Auswahl dieses Wertes wird die dynamische Option **DataFileMessage**angezeigt.|  
|**Variable message**|Die Nachricht wird in einer Variable gespeichert. Bei Auswahl dieses Wertes wird die dynamische Option **VariableMessage**angezeigt.|  
|**String message**|Die Nachricht wird im Task 'Nachrichtenwarteschlange' gespeichert. Bei Auswahl dieses Wertes wird die dynamische Option **StringMessage**angezeigt.|  
  
## MessageType (dynamische Optionen)  
  
### MessageType = Data file message  
 **DataFileMessage**  
 Geben Sie den Pfad der Datendatei an, oder klicken Sie auf die Schaltfläche mit den Auslassungspunkten **(…)**, um nach der Datei zu suchen.  
  
### MessageType = Variable message  
 **VariableMessage**  
 Geben Sie die Variablennamen ein, oder klicken Sie auf die Schaltfläche mit den Auslassungspunkten **(…)**, und wählen Sie dann die Variablen aus. Die Variablen werden durch Kommas getrennt.  
  
 **Verwandte Themen:** Variablen auswählen  
  
### MessageType = Zeichenfolgennachricht  
 **StringMessage**  
 Geben Sie die Zeichenfolgennachricht ein, oder klicken Sie auf die Schaltfläche mit den Auslassungspunkten **(…)**, und geben Sie dann im Dialogfeld **Zeichenfolgennachricht eingeben** die Nachricht ein.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor für den Task „Nachrichtenwarteschlange“ &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/message-queue-task-editor-general-page.md)   
 [Editor für den Task „Nachrichtenwarteschlange“ &#40;Seite „Empfangen“&#41;](../../integration-services/control-flow/message-queue-task-editor-receive-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
  