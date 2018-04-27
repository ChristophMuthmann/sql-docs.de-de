---
title: SQL Server-Agent-Eigenschaften (Seite Verlauf)|Microsoft-Dokumente
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ag.agent.history.f1
ms.assetid: dc73734c-b3c3-407f-bbd1-8714b4fa47b0
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 92c8938b332ec2b4ad8a1b9dd99c4ce8e420bfe2
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="sql-server-agent-properties-history-page"></a>SQL Server-Agent-Eigenschaften (Seite Verlauf)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Auf dieser Seite können Sie die Einstellungen für die Verwaltung des Verlaufsprotokolls für den [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst anzeigen und bearbeiten.  
  
## <a name="options"></a>Tastatur  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[SQL Server-Agent-Fehlerprotokoll](../../ssms/agent/sql-server-agent-error-log.md)  
  
