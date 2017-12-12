---
title: "Warnungseigenschaften – Neue Warnung (Seite „Optionen“)"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.alert.options.f1
ms.assetid: 6e4f41aa-832d-46ba-b6b5-cf1d3b15d33f
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3b38c477c53d988045a01b07a999629459c7560b
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="alert-properties---new-alert-options-page"></a>Warnungseigenschaften – Neue Warnung (Seite „Optionen“)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Verwenden Sie diese Seite, um Optionen für [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent-Warnungen anzuzeigen und zu ändern.  
  
## <a name="options"></a>enthalten  
**E-Mail**  
Schließt Fehlertext des Ereignisses ggf. in E-Mail-Benachrichtigungen ein.  
  
**Pager**  
Schließt Fehlertext des Ereignisses ggf. in Pagerbenachrichtigungen ein.  
  
**NET SEND**  
Schließt Fehlertext des Ereignisses ggf. in NET SEND-Benachrichtigungen ein.  
  
**Zusätzlich zu sendende Warnbenachrichtigung**  
Geben Sie hier zusätzlichen Text ein, der in die Benachrichtigungsmeldungen aufgenommen werden soll.  
  
**Antwortverzögerung**  
Geben Sie eine Verzögerung für das wiederholte Auftreten des Ereignisses an. Einige Ereignisse können innerhalb einer kurzen Zeitspanne häufig auftreten. In diesem Fall könnte es sinnvoll sein, zwar über das Auftreten des Ereignisses informiert zu werden, nicht aber für jedes Auftreten eine Meldung zu erhalten. Mithilfe dieser Option können Sie einen Timeoutwert angeben. Durch die Angabe einer Verzögerung nach der Warnungsantwort auf ein Ereignis wartet der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent die angegebene Verzögerungszeit ab, bevor eine weitere Antwort zurückgegeben wird, unabhängig davon, ob das Ereignis in der Zwischenzeit wieder auftritt.  
  
**Minuten**  
Geben Sie eine Verzögerung in Minuten an. Wenn bei jedem Auftreten des Ereignisses geantwortet werden soll, geben Sie 0 Minuten und 0 Sekunden an.  
  
**Sekunden**  
Geben Sie eine Verzögerung in Sekunden an. Wenn bei jedem Auftreten des Ereignisses geantwortet werden soll, geben Sie 0 Minuten und 0 Sekunden an.  
  
## <a name="see-also"></a>Siehe auch  
[Warnungen](../../ssms/agent/alerts.md)  
  
