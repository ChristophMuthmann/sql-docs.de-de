---
title: SQL Server-Agent-Fehlerprotokoll |Microsoft-Dokumente
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- messages [SQL Server], SQL Server Agent
- errors [SQL Server], logs
- SQL Server Agent, errors
ms.assetid: 0b2d6e6e-cd2d-4b8b-9fa2-2bbd2fc0da41
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d1947c39760dc30d22c7b419412288da72fcc9e3
ms.contentlocale: de-de
ms.lasthandoff: 08/18/2017

---
# <a name="sql-server-agent-error-log"></a>SQL Server-Agent-Fehlerprotokoll
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent erstellt ein Fehlerprotokoll, in dem standardmäßig Warnungen und Fehler erfasst werden. Die folgenden Warnungen und Fehler werden im Protokoll angezeigt:  
  
-   Warnmeldungen, die Informationen zu möglichen Problemen bereitstellen, z.B. „Job <\<*job_name*> wurde beim Ausführen gelöscht“.  
  
-   Fehlermeldungen, die in der Regel Eingriff eines Systemadministrators erfordern, z. B. "Mailsitzung kann nicht gestartet werden". Fehlermeldungen können mithilfe von **NET SEND**an bestimmte Benutzer oder Computer gesendet werden.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] verwaltet bis zu neun [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Fehlerprotokolle. Jedes archivierte Fehlerprotokoll verfügt über eine Dateierweiterung, durch die das relative Alter des Protokolls angegeben wird. So gibt z. B. die Erweiterung ".1" das zuletzt archivierte Fehlerprotokoll an, während die Erweiterung ".9" das Fehlerprotokoll kennzeichnet, das zuerst archiviert wurde.  
  
Standardmäßig werden Meldungen zur Ablaufverfolgung nicht in das [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Fehlerprotokoll geschrieben, da das Protokoll dadurch zu schnell aufgefüllt werden könnte. Wenn das Fehlerprotokoll voll ist, sind Ihre Möglichkeiten zur Auswahl und Analyse schwierigerer Fehler eingeschränkt. Da durch das Protokoll die Verarbeitungsmenge für den Server erhöht wird, sollten Sie genau überlegen, welche Vorteile Ihnen das Aufzeichnen der Meldungen zur Ablaufverfolgung im Fehlerprotokoll bietet. Im Allgemeinen ist es am besten, alle Meldungen nur beim Debuggen eines bestimmten Problems aufzuzeichnen.  
  
Beim Beenden des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents können Sie den Speicherort des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Fehlerprotokolls ändern. Leere Fehlerprotokolle können nicht geöffnet werden. Sie können das [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Protokoll jederzeit durchlaufen, ohne den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent anhalten zu müssen.  
  
**So zeigen Sie das SQL Server-Agent-Fehlerprotokoll an**  
  
-   [Fehlerprotokoll des SQL Server-Agents anzeigen &#40;SQL Server Management Studio&#41;](../../ssms/agent/view-sql-server-agent-error-log-sql-server-management-studio.md)  
  
**So benennen Sie ein SQL Server-Agent-Fehlerprotokoll um**  
  
-   [Fehlerprotokoll des SQL Server-Agents umbenennen &#40;SQL Server Management Studio&#41;](../../ssms/agent/rename-a-sql-server-agent-error-log-sql-server-management-studio.md)  
  
**So senden Sie SQL Server-Agent-Fehlermeldungen**  
  
-   [Send SQL Server Agent Error Messages](../../ssms/agent/send-sql-server-agent-error-messages.md)  
  
**So schreiben Sie Meldungen zur Ablaufverfolgung in das SQL Server-Agent-Fehlerprotokoll**  
  
-   [Schreiben von Meldungen zur Ablaufverfolgung in das SQL Server-Agent-Fehlerprotokoll &#40;SQL Server Management Studio&#41;](../../ssms/agent/write-execution-trace-messages-to-sql-server-agent-log-ssms.md)  
  

