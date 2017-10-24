---
title: Typen von Ereignissen | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- EventComplete event [ADO]
- events [ADO], types
- Will events [ADO]
- complete events [ADO]
- WillEvent event [ADO]
ms.assetid: f3327ea0-635a-43d4-bd78-c1674f62f1a2
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 502c77b55eb0e3a60497fa10bf9fe8c8a412dc4d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="types-of-events"></a>Typen von Ereignissen
Es gibt zwei grundlegende Arten von Ereignissen. "Werden Ereignisse" die aufgerufen werden, bevor ein Vorgang gestartet wird, in der Regel in ihren Namen enthalten "Wird" – z. B. **WillChangeRecordset** oder **WillConnect**. Ereignisse, die aufgerufen werden, nachdem ein Ereignis in der Regel abgeschlossen wurde "Vollständig" in ihren Namen enthalten, z. B. **RecordChangeComplete** oder **ConnectComplete**. Ausnahmen vorhanden sind – z. B. **InfoMessage** –, aber diese erfolgen, wenn der zugeordnete Vorgang abgeschlossen wurde.  
  
## <a name="will-events"></a>Ereignisse  
 Ereignishandler wird aufgerufen, bevor der Vorgang gestartet wird Ihnen die Möglichkeit zum Untersuchen bieten oder ändern Sie die Vorgangsparameter, und brechen Sie den Vorgang oder abgeschlossen werden kann. Diese Routinen Ereignishandler in der Regel haben Namen im Format * *wird*Ereignis***.  
  
## <a name="complete-events"></a>Ereignisse durch Abschluss  
 Ereignishandler wird aufgerufen, nachdem ein Vorgang abgeschlossen ist, können die Anwendung benachrichtigt, die eine Operation abgeschlossen wurde. Ein solcher Ereignishandler wird auch benachrichtigt, wenn ein Ereignishandler wird Bricht einen ausstehenden Vorgang ab. Diese Routinen Ereignishandler in der Regel haben Namen im Format ** *Ereignis*Complete**.  
  
 Wird und vollständige Ereignisse werden in der Regel paarweise verwendet.  
  
## <a name="other-events"></a>Andere Ereignisse  
 Die anderen Ereignishandler – d. h. die Ereignisse, deren Namen nicht im Format sind * *wird*Ereignis*** oder ** *Ereignis*Complete** – nur aufgerufen werden nach Abschluss eines Vorgangs. Diese Ereignisse sind **trennen**, **EndOfRecordset**, und **InfoMessage**.  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-Ereignis-Handler-Zusammenfassung](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO-Ereignisinstanziierung nach Sprache](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Ereignisparameter](../../../ado/guide/data/event-parameters.md)   
 [Zusammenwirken der Ereignishandler](../../../ado/guide/data/how-event-handlers-work-together.md)

