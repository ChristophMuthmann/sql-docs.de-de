---
title: Eigenschaften des SQL Server-Agents (Registerkarte Auftragssystem)|Microsoft-Dokumente
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ag.agent.job.f1
ms.assetid: e171d13e-1302-4f0e-88be-67d656aec8d3
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4d98026d219c3cfc834b96b0d7b5a402622df1be
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-agent-properties-job-system-page"></a>Eigenschaften des SQL Server-Agents (Registerkarte Auftragssystem)
Auf dieser Seite können Sie anzeigen und ändern, wie Aufträge vom [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent-Dienst verwaltet werden.  
  
## <a name="options"></a>enthalten  
**Timeoutintervall beim Herunterfahren (in Sekunden)**  
Gibt an, wie viele Sekunden der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent vor dem Herunterfahren auf den Abschluss von Aufträgen abwartet. Wenn der Auftrag noch nach dem angegebenen Intervall ausgeführt wird, wird das Beenden des Auftrags vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent erzwungen.  
  
**Nichtadministrator-Proxykonto verwenden**  
Legt ein Nichtadministrator-Proxykonto für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent fest. [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] und höhere Versionen unterstützen mehrere Proxys. Diese Option betrifft daher nur die Verwaltung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Versionen vor [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
**Benutzername**  
Geben Sie den Namen des Benutzers für das Nichtadministrator-Proxykonto ein. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] unterstützt mehrere Proxys. Diese Option betrifft daher nur die Verwaltung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Versionen vor [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
**Kennwort**  
Geben Sie das Kennwort des Benutzers für das Nichtadministrator-Proxykonto ein. [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] und höhere Versionen unterstützen mehrere Proxys. Diese Option betrifft daher nur die Verwaltung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Versionen vor [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)].  
  
**Domäne**  
Geben Sie die Domäne des Benutzers für das Nichtadministrator-Proxykonto ein. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] unterstützt mehrere Proxys. Diese Option betrifft daher nur die Verwaltung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Versionen vor [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
## <a name="see-also"></a>Siehe auch  
[Implementieren von Aufträgen](../../ssms/agent/implement-jobs.md)  
  

