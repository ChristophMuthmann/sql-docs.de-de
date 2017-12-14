---
title: Sperren-Ereigniskategorie | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: event-classes
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Locks event category [SQL Server]
- SQL Server event classes, Locks event category
- event classes [SQL Server], Locks event category
- lock escalation [SQL Server], locks event category
ms.assetid: 27d6afa2-7dab-4fe7-a1ad-064b879dc654
caps.latest.revision: "27"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0d055f85d5059f8e374a9e111c5b0286e3907a87
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="locks-event-category"></a>Sperren-Ereigniskategorie
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Verwenden Sie die Ereignisklassen in der **Sperren**-Ereigniskategorie, um die Sperraktivität in einer Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] zu überwachen. Diese Ereignisklassen können Ihnen die Untersuchung von Sperrproblemen erleichtern, die auftreten können, wenn Daten von mehreren Benutzern gleichzeitig gelesen und bearbeitet werden.  
  
 Da das [!INCLUDE[ssDE](../../includes/ssde-md.md)] häufig mehrere Sperren verarbeitet, kann das Erfassen der **Sperren** -Ereignisklassen während einer Ablaufverfolgung einen deutlich höheren Verarbeitungsaufwand zur Folge haben. Außerdem können dabei große Ablaufverfolgungsdateien oder -tabellen entstehen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Beschreibung|  
|-----------|-----------------|  
|[Deadlock Graph (Ereignisklasse)](../../relational-databases/event-classes/deadlock-graph-event-class.md)|Stellt eine XML-Beschreibung eines Deadlocks bereit.|  
|[Lock:Acquired (Ereignisklasse)](../../relational-databases/event-classes/lock-acquired-event-class.md)|Gibt an, dass für eine Ressource, z. B. eine Zeile in einer Tabelle, eine Sperre eingerichtet wurde.|  
|[Lock:Cancel-Ereignisklasse](../../relational-databases/event-classes/lock-cancel-event-class.md)|Verfolgt Sperranforderungen nach, die vor dem Einrichten der Sperre abgebrochen wurden (beispielsweise, um einen Deadlock zu verhindern).|  
|[Lock:Deadlock Chain (Ereignisklasse)](../../relational-databases/event-classes/lock-deadlock-chain-event-class.md)|Überwacht, wann Deadlockbedingungen auftreten und welche Objekte betroffen sind.|  
|[Lock:Deadlock (Ereignisklasse)](../../relational-databases/event-classes/lock-deadlock-event-class.md)|Verfolgt nach, wann eine Transaktion eine Sperre für eine bereits durch eine andere Transaktion gesperrte Ressource angefordert hat, wodurch ein Deadlock auftritt.|  
|[Lock:Escalation-Ereignisklasse](../../relational-databases/event-classes/lock-escalation-event-class.md)|Zeigt an, dass eine differenziertere Sperre in eine gröbere Sperre konvertiert wurde.|  
|[Lock:Released (Ereignisklasse)](../../relational-databases/event-classes/lock-released-event-class.md)|Verfolgt nach, wann eine Sperre aufgehoben wird.|  
|[Lock:Timeout &#40;timeout &#62; 0&#41; Ereignisklasse](../../relational-databases/event-classes/lock-timeout-timeout-0-event-class.md)|Verfolgt nach, wann Sperranforderungen nicht erfüllt werden können, weil eine andere Transaktion eine blockierende Sperre für die angeforderte Ressource aufrechterhält. Dieses Ereignis tritt nur in Situationen auf, in denen der Wert für den Sperrtimeout größer als Null ist.|  
|[Lock:Timeout (Ereignisklasse)](../../relational-databases/event-classes/lock-timeout-event-class.md)|Verfolgt nach, wann Sperranforderungen nicht erfüllt werden können, weil eine andere Transaktion eine blockierende Sperre für die angeforderte Ressource aufrechterhält.|  
  
  
