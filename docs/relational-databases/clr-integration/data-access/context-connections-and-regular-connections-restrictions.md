---
title: "Einschränkungen hinsichtlich regulärer Verbindungen und Kontextverbindungen | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: 0c6fe4cb-d846-40b5-8884-35a9c770f5e8
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2294c9ce526f1c91c48139aea21a72b1cbab9515
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="context-connections-and-regular-connections---restrictions"></a>Kontextverbindungen und reguläre Verbindungen - Einschränkungen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]In diesem Thema wird erläutert, die Einschränkungen im Zusammenhang mit der Ausführung von Code in der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Prozess durch kontextverbindungen und reguläre Verbindungen.  
  
## <a name="restrictions-on-context-connections"></a>Einschränkungen für Kontextverbindungen  
 Berücksichtigen Sie bei der Anwendungsentwicklung die folgenden Einschränkungen, die für Kontextverbindungen gelten:  
  
-   Zu einem bestimmten Zeitpunkt kann in einer gegebenen Verbindung nur eine Kontextverbindung bestehen. Wenn in verschiedenen Verbindungen mehrere Anweisungen gleichzeitig ausgeführt werden, kann jede dieser Verbindungen eine eigene Kontextverbindung erhalten. Die Einschränkung wirkt sich nicht auf gleichzeitige Anforderungen verschiedener Verbindungen aus, sondern sie gilt nur für eine gegebene Anforderung für eine gegebene Verbindung.  
  
-   MARS (Multiple Active Result Set) wird in einer Kontextverbindung nicht unterstützt.  
  
-   Die **SqlBulkCopy** -Klasse funktioniert in Kontextverbindungen nicht.  
  
-   Die Batchverarbeitung von Updates wird in Kontextverbindungen nicht unterstützt  
  
-   **SqlNotificationRequest** kann nicht mit Befehlen verwendet werden, die für eine Kontextverbindung ausgeführt werden.  
  
-   Befehle, die für die Kontextverbindung ausgeführt werden, können nicht abgebrochen werden. Die **SqlCommand.Cancel** -Methode ignoriert die Anforderung stillschweigend.  
  
-   Wenn "context connection=true" verwendet wird, können keine anderen Schlüsselwörter in Verbindungszeichenfolgen angegeben werden.  
  
-   Die **SqlConnection.DataSource** Eigenschaft gibt null, wenn die Verbindungszeichenfolge für die **SqlConnection** ist "kontextverbindung = True", anstelle des Namens der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Die Festlegung der **SqlCommand.CommandTimeout** -Eigenschaft hat keine Auswirkungen, wenn der Befehl für eine Kontextverbindung ausgeführt wird.  
  
## <a name="restrictions-on-regular-connections"></a>Einschränkungen für reguläre Verbindungen  
 Berücksichtigen Sie bei der Anwendungsentwicklung die folgenden Einschränkungen, die für reguläre Verbindungen gelten:  
  
-   Die asynchrone Befehlsausführung mit internen Servern wird nicht unterstützt. Wenn in der Verbindungszeichenfolge eines Befehls "async=true" angegeben wird, dann führt die Ausführung des Befehls dazu, dass die **System.NotSupportedException** -Ausnahme ausgelöst wird. Die folgende Meldung wird angezeigt: "Die asynchrone Verarbeitung wird bei einer Ausführung im Rahmen des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Prozesses nicht unterstützt".  
  
-   Das**SqlDependency** -Objekt wird nicht unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
 [Kontextverbindung](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
