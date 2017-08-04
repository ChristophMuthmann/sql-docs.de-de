---
title: Task ' Nachrichtenwarteschlange ' (Seite empfangen) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.msgqueuetask.receive.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 7028756d-1dcc-480c-bbcd-e9654f0772a0
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1f51937fa402accf4e18fefdcec5763987241de4
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="message-queue-task-editor-receive-page"></a>Editor für den Task 'Nachrichtenwarteschlange' (Seite Empfangen)
  Auf der Seite **Empfangen** des Dialogfelds **Editor für den Task „Nachrichtenwarteschlange“** können Sie den Task „Nachrichtenwarteschlange“ konfigurieren, um MSMQ-Nachrichten ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing) zu empfangen.  
  
 Informationen, um sich mit diesem Thema vertraut zu machen, finden Sie unter [Message Queue Task](../../integration-services/control-flow/message-queue-task.md).  
  
## <a name="options"></a>enthalten  
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
  
## <a name="messagetype-dynamic-options"></a>MessageType (dynamische Optionen)  
  
### <a name="messagetype--data-file-message"></a>MessageType = Data file message  
 **SaveFileAs**  
 Geben Sie den Pfad der zu verwendenden Datei an, oder klicken Sie auf die Schaltfläche mit den Auslassungspunkten **(...)** , um nach der Datei zu suchen.  
  
 **Overwrite**  
 Geben Sie an, dass die Daten in einer vorhandenen Datei überschrieben werden sollen, wenn der Inhalt einer Datendateinachricht gespeichert wird. Der Standardwert ist **False**.  
  
 **Filter**  
 Geben Sie an, ob auf die Nachricht ein Filter angewendet werden soll. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Kein Filter**|Der Task filtert keine Nachrichten. Wenn Sie diesen Wert auswählen, wird die dynamische Option **IdentifierReadOnly**angezeigt.|  
|**Vom Paket**|Der Task empfängt nur Nachrichten von dem angegebenen Paket. Wenn Sie diesen Wert auswählen, wird die dynamische Option **Identifier**angezeigt.|  
  
### <a name="filter-dynamic-options"></a>Filter (dynamische Optionen)  
  
#### <a name="filter--no-filter"></a>Filter = No filter  
 **IdentifierReadOnly**  
 Diese Option ist schreibgeschützt. Sie kann leer sein oder die GUID eines Pakets enthalten, wenn die Eigenschaft Filter vorher festgelegt wurde.  
  
#### <a name="filter--from-package"></a>Filter = From package  
 **Identifier**  
 Wenn Sie einen Filter anwenden möchten, geben Sie den eindeutigen Bezeichner des Pakets ein, aus dem die Nachrichten empfangen werden können, oder klicken Sie auf die Schaltfläche mit den Auslassungspunkten **(...)** , und geben Sie das Paket an.  
  
 **Verwandte Themen:** [Paket auswählen](../../integration-services/control-flow/select-a-package.md)  
  
### <a name="messagetype--variable-message"></a>MessageType = Variable message  
 **Filter**  
 Geben Sie an, ob auf Nachrichten ein Filter angewendet werden soll. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Kein Filter**|Der Task filtert keine Nachrichten. Wenn Sie diesen Wert auswählen, wird die dynamische Option **IdentifierReadOnly**angezeigt.|  
|**Vom Paket**|Der Task empfängt nur Nachrichten von dem angegebenen Paket. Wenn Sie diesen Wert auswählen, wird die dynamische Option **Identifier**angezeigt.|  
  
 **Variable**  
 Geben Sie den Variablennamen ein, oder klicken Sie auf \< **neue Variable...** > und konfigurieren Sie dann eine neue Variable.  
  
 **Verwandte Themen:** [Variable hinzufügen](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
### <a name="filter-dynamic-options"></a>Filter (dynamische Optionen)  
  
#### <a name="filter--no-filter"></a>Filter = No filter  
 **IdentifierReadOnly**  
 Diese Option ist leer.  
  
#### <a name="filter--from-package"></a>Filter = From package  
 **Identifier**  
 Wenn Sie einen Filter anwenden möchten, geben Sie den eindeutigen Bezeichner des Pakets ein, aus dem die Nachrichten empfangen werden können, oder klicken Sie auf die Schaltfläche mit den Auslassungspunkten **(...)** , und geben Sie das Paket an.  
  
 **Verwandte Themen:** [Paket auswählen](../../integration-services/control-flow/select-a-package.md)  
  
### <a name="messagetype--string-message"></a>MessageType = Zeichenfolgennachricht  
 **Vergleichen**  
 Geben Sie an, ob auf Nachrichten ein Filter angewendet werden soll. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**InclusionThresholdSetting**|Die Nachrichten werden nicht verglichen.|  
|**Genaue Übereinstimmung**|Die Nachrichten müssen genau mit der Zeichenfolge in der Option **CompareString** übereinstimmen.|  
|**Groß-/Kleinschreibung ignorieren**|Die Nachricht muss mit der Zeichenfolge in der Option **CompareString** übereinstimmen, aber beim Vergleichen wird nicht zwischen Groß- und Kleinschreibung unterschieden.|  
|**Mit Inhalt**|Die Nachrichten müssen die Zeichenfolge in der Option **CompareString** enthalten.|  
  
 **CompareString**  
 Geben Sie hier die Zeichenfolge an, mit der die Nachricht verglichen wird, wenn die Option **Vergleichen** nicht auf **Keine**festgelegt ist.  
  
### <a name="messagetype--string-message-to-variable"></a>MessageType = String message to variable  
 **Vergleichen**  
 Geben Sie an, ob auf Nachrichten ein Filter angewendet werden soll. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**InclusionThresholdSetting**|Die Nachrichten werden nicht verglichen.|  
|**Genaue Übereinstimmung**|Die Nachricht muss genau mit der Zeichenfolge in der Option **CompareString** übereinstimmen.|  
|**Groß-/Kleinschreibung ignorieren**|Die Nachricht muss mit der Zeichenfolge in der Option **CompareString** übereinstimmen, aber beim Vergleichen wird nicht zwischen Groß- und Kleinschreibung unterschieden.|  
|**Mit Inhalt**|Die Nachricht muss die Zeichenfolge in der Option **CompareString** enthalten.|  
  
 **CompareString**  
 Geben Sie hier die Zeichenfolge an, mit der die Nachricht verglichen wird, wenn die Option **Vergleichen** nicht auf **Keine**festgelegt ist.  
  
 **Variable**  
 Geben Sie den Namen der Variablen zum Speichern der Nachricht, oder klicken Sie auf \< **neue Variable...** > und konfigurieren Sie dann eine neue Variable.  
  
 **Verwandte Themen:** [Variable hinzufügen](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Meldungsreferenz von Integration Services-Fehler](../../integration-services/integration-services-error-and-message-reference.md)   
 [Task ' Nachrichtenwarteschlange ' &#40; Seite "Allgemein" &#41;](../../integration-services/control-flow/message-queue-task-editor-general-page.md)   
 [Task ' Nachrichtenwarteschlange ' &#40; Senden Sie die Seite "&#41;](../../integration-services/control-flow/message-queue-task-editor-send-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)   
 [Task "Nachrichtenwarteschlange"](../../integration-services/control-flow/message-queue-task.md)  
  
  
