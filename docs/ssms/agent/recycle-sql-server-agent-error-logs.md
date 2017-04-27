---
title: Fehlerprotokolle des SQL Server-Agents wiederverwenden | Microsoft-Dokumentation
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
- sql13.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6b3b79686cbc194eda76fd1f4873d81c26d8d31c
ms.lasthandoff: 04/11/2017

---
# <a name="recycle-sql-server-agent-error-logs"></a>Fehlerprotokolle des SQL Server-Agents wiederverwenden
Mithilfe dieser Seite können Sie die Fehlerprotokolle des [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents wiederverwenden. Beim Wiederverwenden des Protokolls werden das aktuelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Fehlerprotokoll geschlossen und ein neues Fehlerprotokoll ohne Neustart des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienstes gestartet. Beachten Sie, dass der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent die letzten neun Fehlerprotokolle speichert. Wenn bereits neun Fehlerprotokolle vorhanden sind, führt das Wiederverwenden des Fehlerprotokolls dazu, dass der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent das älteste Fehlerprotokoll entfernt.  
  
## <a name="see-also"></a>Siehe auch  
[SQL Server-Agent-Fehlerprotokoll](../../ssms/agent/sql-server-agent-error-log.md)  
  

