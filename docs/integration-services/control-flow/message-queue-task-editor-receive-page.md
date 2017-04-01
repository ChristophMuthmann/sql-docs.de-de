---
title: "Editor f&#252;r den Task &#39;Nachrichtenwarteschlange&#39; (Seite Empfangen) | Microsoft Docs"
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
  - "sql13.dts.designer.msgqueuetask.receive.f1"
helpviewer_keywords: 
  - "Editor für den Task Nachrichtenwarteschlange"
ms.assetid: 7028756d-1dcc-480c-bbcd-e9654f0772a0
caps.latest.revision: 29
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 29
---
# Editor f&#252;r den Task &#39;Nachrichtenwarteschlange&#39; (Seite Empfangen)
  Auf der Seite **Empfangen** des Dialogfelds **Editor für den Task „Nachrichtenwarteschlange“** können Sie den Task „Nachrichtenwarteschlange“ konfigurieren, um MSMQ-Nachrichten ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing) zu empfangen.  
  
 Informationen, um sich mit diesem Thema vertraut zu machen, finden Sie unter [Message Queue Task](../../integration-services/control-flow/message-queue-task.md).  
  
## enthalten  
 **RemoveFromMessageQueue**  
 Geben Sie an, ob die Nachricht aus der Warteschlange entfernt werden soll, nachdem sie empfangen wurde. Standardmäßig ist dieser Wert auf **False**festgelegt.  
  
 **ErrorIfMessageTimeOut**  
 Geben Sie an, ob der Task fehlschlägt und eine Fehlermeldung angezeigt wird, wenn die Zeit für die Nachricht überschritten wird. Der Standardwert ist **False**.  
  
 **TimeoutAfter**  
 Wenn eine Fehlermeldung beim Fehlschlagen des Tasks angezeigt werden soll, geben Sie hier die Wartezeit vor dem Anzeigen der Timeoutmeldung in Sekunden an.  
  
 **MessageType**  
 Wählen Sie den Nachrichtentyp aus. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Data file message**|Die Nachricht wird in einer Datei gespeichert. Bei Auswahl dieses Wertes wird die dynamische Option **DataFileMessage**angezeigt.|  
|**Variable message**|Die Nachricht wird in einer Variable gespeichert. Bei Auswahl dieses Wertes wird die dynamische Option **VariableMessage**angezeigt.|  
|**String message**|Die Nachricht wird im Task 'Nachrichtenwarteschlange' gespeichert. Bei Auswahl dieses Wertes wird die dynamische Option **StringMessage**angezeigt.|  
|**String message to variable**|Die Nachricht wurde in einer Variablen gespeichert.<br /><br /> Bei Auswahl dieses Wertes wird die dynamische Option **StringMessage**angezeigt.|  
  
## MessageType (dynamische Optionen)  
  
### MessageType = Data file message  
 **SaveFileAs**  
 Geben Sie den Pfad der zu verwendenden Datei an, oder klicken Sie auf die Schaltfläche mit den Auslassungspunkten **(...)**, um nach der Datei zu suchen.  
  
 **Overwrite**  
 Geben Sie an, dass die Daten in einer vorhandenen Datei überschrieben werden sollen, wenn der Inhalt einer Datendateinachricht gespeichert wird. Der Standardwert ist **False**.  
  
 **Filter**  
 Geben Sie an, ob auf die Nachricht ein Filter angewendet werden soll. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Kein Filter**|Der Task filtert keine Nachrichten. Wenn Sie diesen Wert auswählen, wird die dynamische Option **IdentifierReadOnly**angezeigt.|  
|**Vom Paket**|Der Task empfängt nur Nachrichten von dem angegebenen Paket. Wenn Sie diesen Wert auswählen, wird die dynamische Option **Identifier**angezeigt.|  
  
### Filter (dynamische Optionen)  
  
#### Filter = No filter  
 **IdentifierReadOnly**  
 Diese Option ist schreibgeschützt. Sie kann leer sein oder die GUID eines Pakets enthalten, wenn die Eigenschaft Filter vorher festgelegt wurde.  
  
#### Filter = From package  
 **Bezeichner**  
 Wenn Sie einen Filter anwenden möchten, geben Sie den eindeutigen Bezeichner des Pakets ein, aus dem die Nachrichten empfangen werden können, oder klicken Sie auf die Schaltfläche mit den Auslassungspunkten **(...)**, und geben Sie das Paket an.  
  
 **Verwandte Themen:** [Paket auswählen](../../integration-services/control-flow/select-a-package.md)  
  
### MessageType = Variable message  
 **Filter**  
 Geben Sie an, ob auf Nachrichten ein Filter angewendet werden soll. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Kein Filter**|Der Task filtert keine Nachrichten. Wenn Sie diesen Wert auswählen, wird die dynamische Option **IdentifierReadOnly**angezeigt.|  
|**Vom Paket**|Der Task empfängt nur Nachrichten von dem angegebenen Paket. Wenn Sie diesen Wert auswählen, wird die dynamische Option **Identifier**angezeigt.|  
  
 **Variable**  
 Geben Sie den Variablennamen an, oder klicken Sie auf \<**Neue Variable…**>, und konfigurieren Sie anschließend eine neue Variable.  
  
 **Verwandte Themen:** [Variable hinzufügen](../Topic/Add%20Variable.md)  
  
### Filter (dynamische Optionen)  
  
#### Filter = No filter  
 **IdentifierReadOnly**  
 Diese Option ist leer.  
  
#### Filter = From package  
 **Bezeichner**  
 Wenn Sie einen Filter anwenden möchten, geben Sie den eindeutigen Bezeichner des Pakets ein, aus dem die Nachrichten empfangen werden können, oder klicken Sie auf die Schaltfläche mit den Auslassungspunkten **(...)**, und geben Sie das Paket an.  
  
 **Verwandte Themen:** [Paket auswählen](../../integration-services/control-flow/select-a-package.md)  
  
### MessageType = Zeichenfolgennachricht  
 **Vergleichen**  
 Geben Sie an, ob auf Nachrichten ein Filter angewendet werden soll. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**InclusionThresholdSetting**|Die Nachrichten werden nicht verglichen.|  
|**Genaue Übereinstimmung**|Die Nachrichten müssen genau mit der Zeichenfolge in der Option **CompareString** übereinstimmen.|  
|**Groß-/Kleinschreibung ignorieren**|Die Nachricht muss mit der Zeichenfolge in der Option **CompareString** übereinstimmen, aber beim Vergleichen wird nicht zwischen Groß- und Kleinschreibung unterschieden.|  
|**Mit Inhalt**|Die Nachrichten müssen die Zeichenfolge in der Option **CompareString** enthalten.|  
  
 **CompareString**  
 Geben Sie hier die Zeichenfolge an, mit der die Nachricht verglichen wird, wenn die Option **Vergleichen** nicht auf **Keine** festgelegt ist.  
  
### MessageType = String message to variable  
 **Vergleichen**  
 Geben Sie an, ob auf Nachrichten ein Filter angewendet werden soll. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**InclusionThresholdSetting**|Die Nachrichten werden nicht verglichen.|  
|**Genaue Übereinstimmung**|Die Nachricht muss genau mit der Zeichenfolge in der Option **CompareString** übereinstimmen.|  
|**Groß-/Kleinschreibung ignorieren**|Die Nachricht muss mit der Zeichenfolge in der Option **CompareString** übereinstimmen, aber beim Vergleichen wird nicht zwischen Groß- und Kleinschreibung unterschieden.|  
|**Mit Inhalt**|Die Nachricht muss die Zeichenfolge in der Option **CompareString** enthalten.|  
  
 **CompareString**  
 Geben Sie hier die Zeichenfolge an, mit der die Nachricht verglichen wird, wenn die Option **Vergleichen** nicht auf **Keine** festgelegt ist.  
  
 **Variable**  
 Geben Sie den Namen der Variablen zum Speichern der Nachricht ein, oder klicken Sie auf \<**Neue Variable…**>, und konfigurieren Sie anschließend eine neue Variable.  
  
 **Verwandte Themen:** [Variable hinzufügen](../Topic/Add%20Variable.md)  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor für den Task „Nachrichtenwarteschlange“ &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/message-queue-task-editor-general-page.md)   
 [Editor für den Task „Nachrichtenwarteschlange“ &#40;Seite „Senden“&#41;](../../integration-services/control-flow/message-queue-task-editor-send-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)   
 [Nachrichtenwarteschlange (Task)](../../integration-services/control-flow/message-queue-task.md)  
  
  