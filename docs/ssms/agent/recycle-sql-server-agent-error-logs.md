---
title: Fehlerprotokolle des SQL Server-Agents wiederverwenden | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
caps.latest.revision: "3"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: da85bcd6f835dd5b8c3cd2595c2d0e0222a1aefe
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="recycle-sql-server-agent-error-logs"></a>Fehlerprotokolle des SQL Server-Agents wiederverwenden
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Mithilfe dieser Seite können Sie die Fehlerprotokolle des [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agents wiederverwenden. Beim Wiederverwenden des Protokolls werden das aktuelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Fehlerprotokoll geschlossen und ein neues Fehlerprotokoll ohne Neustart des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienstes gestartet. Beachten Sie, dass der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent die letzten neun Fehlerprotokolle speichert. Wenn bereits neun Fehlerprotokolle vorhanden sind, führt das Wiederverwenden des Fehlerprotokolls dazu, dass der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent das älteste Fehlerprotokoll entfernt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[SQL Server-Agent-Fehlerprotokoll](../../ssms/agent/sql-server-agent-error-log.md)  
  
