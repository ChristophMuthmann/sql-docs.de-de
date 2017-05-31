---
title: SQL Server-Agent-Eigenschaften (Seite Verlauf)|Microsoft-Dokumente
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
- sql13.ag.agent.history.f1
ms.assetid: dc73734c-b3c3-407f-bbd1-8714b4fa47b0
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 51839ab3d459e2350c582810fe003fc5086de3eb
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-agent-properties-history-page"></a>SQL Server-Agent-Eigenschaften (Seite Verlauf)
Auf dieser Seite können Sie die Einstellungen für die Verwaltung des Verlaufsprotokolls für den [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst anzeigen und bearbeiten.  
  
## <a name="options"></a>enthalten  
**Größe des Auftragsverlaufsprotokolls beschränken**  
Legt die Grenzen für die Menge der Auftragsverlaufsinformationen fest, die im Protokoll des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents verbleiben.  
  
**Maximale Länge des Auftragsverlaufsprotokolls (in Zeilen)**  
Legt die maximale Anzahl der Zeilen fest, die der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent beibehält. Wenn das Protokoll diese Anzahl von Zeilen überschreitet, werden die ältesten Zeilen vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent entfernt, sobald neue Zeilen eingetragen werden.  
  
**Maximale Zeilenanzahl pro Auftrag in Auftragsverlauf**  
Legt die maximale Anzahl von Zeilen fest, die der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent pro Auftrag beibehält. Wenn der Verlauf eines bestimmten Auftrags diese Anzahl von Zeilen überschreitet, werden die ältesten Zeilen vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent entfernt, sobald neue Zeilen eingetragen werden.  
  
**Agentverlauf entfernen**  
Gibt an, dass der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent Einträge entfernt, die länger als eine bestimmte Zeitspanne im Protokoll vorhanden sind. Dies ist eine einmalige Ausführung zum Löschen des Verlaufs. Wenn ein erneut auftretender Auftrag benötigt wird, erstellen und planen Sie einen Wartungsplan mit einem Cleanupauftrag.  
  
**Älter als**  
Legt die Zeitspanne fest, für die der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent die Einträge beibehält.  
  
## <a name="see-also"></a>Siehe auch  
[SQL Server-Agent-Fehlerprotokoll](../../ssms/agent/sql-server-agent-error-log.md)  
  

