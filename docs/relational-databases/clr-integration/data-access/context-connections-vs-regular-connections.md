---
title: "Reguläre im Vergleich zu Kontextverbindungen | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
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
ms.assetid: a1dead02-be88-4b16-8cb2-db1284856764
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6b15a8e2c830c0f8e367aa9b2efc60a6911ee25e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="context-connections-vs-regular-connections"></a>Kontext-Verbindungen im Vergleich zu Reguläre Verbindungen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Wenn Sie eine Verbindung mit einem Remoteserver herstellen, verwenden Sie stets reguläre Verbindungen anstelle von kontextverbindungen. Wenn Sie eine Verbindung mit dem Server herstellen müssen, auf dem die gespeicherte Prozedur oder Funktion ausgeführt wird, verwenden Sie in den meisten Fällen Kontextverbindungen. Dies hat Vorteile, etwa das Ausführen im gleichen Transaktionsbereich, ohne dass eine erneute Authentifizierung erforderlich ist.  
  
 Darüber hinaus führt das Verwenden der Kontextverbindung in der Regel zu einer höheren Leistung und geringeren Ressourcenverwendung. Die Kontextverbindung ist eine Verbindung, die nur innerhalb von Prozessen verwendet wird. Sie kann den Server "direkt" kontaktieren, indem sie das Netzwerkprotokoll und die Transportebenen umgeht, um Transact-SQL-Anweisungen zu senden und Ergebnisse zu empfangen. Der Authentifizierungsprozess wird ebenfalls umgangen. Die folgende Abbildung zeigt die primären Komponenten von der **SqlClient** verwalteten Anbieter als auch wie die verschiedenen Komponenten miteinander interagieren, wenn eine reguläre Verbindung verwenden und mithilfe der kontextverbindung.  
  
 ![Codepfade einer Kontext-und einer regulären Verbindung. ] (../../../relational-databases/clr-integration/data-access/media/clrintdataaccess.gif "Codepfade einer Kontext-und einer regulären Verbindung.")  
  
 Die Kontextverbindung folgt einem kürzeren Codepfad und schließt weniger Komponenten ein, sodass Sie mit schnelleren Anforderungen und Ergebnissen an den Server und vom Server rechnen können als bei einer regulären Verbindung. Die Abfrageausführungszeit auf dem Server ist bei Kontext- und reguläre Verbindungen die gleiche.  
  
 In einigen Fällen müssen Sie möglicherweise eine separate reguläre Verbindung mit dem gleichen Server herstellen. Es gibt z. B. bestimmte Einschränkungen bei der Verwendung der kontextverbindung, die in beschriebenen [Einschränkungen hinsichtlich regulärer Verbindungen und Kontextverbindungen](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Kontextverbindung](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
