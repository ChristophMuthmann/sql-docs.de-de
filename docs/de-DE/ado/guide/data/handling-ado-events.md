---
title: Behandlung von Ereignissen für ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO]
- ADO, events
- event handlers [ADO]
ms.assetid: e9003457-0762-48b3-942f-0820266b158f
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b84df66d25c4e1ccda2330ccb1b0d02ff89dc20c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="handling-ado-events"></a>Behandlung von Ereignissen für ADO
Das ADO-Ereignismodell unterstützt bestimmte synchrone und asynchrone ADO-Vorgänge, die Zertifikate ausstellen *Ereignisse*, oder Benachrichtigungen, die vor dem Vorgang gestartet oder abgeschlossen ist. Ein Ereignis ist tatsächlich ein Aufruf an eine Ereignishandler-Routine, die Sie in der Anwendung zu definieren.  
  
 Wenn Sie für die Gruppe von Ereignissen Handlerfunktionen oder Prozeduren, die vor dem Starten der Vorgang auftreten angeben, können Sie überprüfen oder ändern die Parameter, die um den Vorgang übergeben wurden. Da er noch nicht ausgeführt wurde, können Sie brechen Sie den Vorgang oder abgeschlossen werden kann.  
  
 Die Ereignisse, die nach Abschluss eines Vorgangs auftreten sind besonders wichtig, wenn Sie ADO asynchron verwenden. Z. B. eine Anwendung, die einen asynchronen startet [Recordset.Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) Vorgang wird benachrichtigt, durch eine Ausführung ausgelöste Ereignis, wenn die Operation abgeschlossen ist.  
  
 Fügt ein gewisser Aufwand für die Anwendung mithilfe von ADO-Ereignismodell, jedoch bietet weitaus mehr Flexibilität als andere Methoden zum Umgang mit asynchronen Vorgängen, z. B. Überwachung der [Zustand](../../../ado/reference/ado-api/state-property-ado.md) Eigenschaft eines Objekts mit einer Schleife.  
  
> [!NOTE]
>  Um Ereignisse zu behandeln, ADO-Meldungsverteilschleife oder muss in einem Singlethread-Apartment (STA)-Modell verwendet werden. ADO-Ereignisse werden intern von Fenster zum Erstellen einer ausgeblendeten behandelt. ADO sendet Nachrichten an dieses Fenster, wenn Ereignisse ausgelöst werden müssen. Dies geschieht, um sicherzustellen, dass Ereignisse an den Thread gesendet werden, die aufgerufen **IConnectionPoint:: Advise** auf dem Verbindungspunkt. Diese Architektur kann Probleme verursachen, wenn der Thread, der die Benachrichtigung erhalten sollen, nicht fenstermeldungen pump. Potenzielle Probleme umfassen ADO-Ereignisse, die nicht zugestellt werden, auf den Thread und globale Fenster Broadcasts ein Timeout eintritt und das gesamte System möglicherweise verlangsamen, da die ausgeblendete Windows keine Nachrichten verarbeiten. STA-Threads verfügen typischerweise über eine Meldungsverteilschleife, die ausgeführt werden, damit dieses Problem selbst nicht auf STA-Threads manifest. MTA-Threads müssen jedoch in der Regel ein Nachrichtensystem keine damit das Problem selbst in der Regel auf MTA-Threads manifest.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [ADO-Ereignishandler – Zusammenfassung](../../../ado/guide/data/ado-event-handler-summary.md)  
  
-   [Typen von Ereignissen](../../../ado/guide/data/types-of-events.md)  
  
-   [Ereignisparameter](../../../ado/guide/data/event-parameters.md)  
  
-   [Zusammenwirken der Ereignishandler](../../../ado/guide/data/how-event-handlers-work-together.md)  
  
-   [ADO-Ereignisinstanziierung nach Sprache](../../../ado/guide/data/ado-event-instantiation-by-language.md)  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-Ereignis-Handler-Zusammenfassung](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO-Ereignisinstanziierung nach Sprache](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [ADO-Ereignisse](../../../ado/reference/ado-api/ado-events.md)   
 [Ereignisparameter](../../../ado/guide/data/event-parameters.md)   
 [Typen von Ereignissen](../../../ado/guide/data/types-of-events.md)
