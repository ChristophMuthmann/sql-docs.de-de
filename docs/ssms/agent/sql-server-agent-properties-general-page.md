---
title: SQL Server-Agent-Eigenschaften (Seite Allgemein)|Microsoft-Dokumente
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
- sql13.ag.agent.general.f1
ms.assetid: b51601e9-5454-43c6-bb5e-24eb2ff043c8
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 74935b05168dc6334704027b9fd7913ea25a52d0
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="sql-server-agent-properties-general-page"></a>SQL Server-Agent-Eigenschaften (Seite Allgemein)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Mithilfe dieser Seite können Sie die allgemeinen Eigenschaften des [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienstes anzeigen und ändern.  
  
## <a name="options"></a>Tastatur  
**Dienststatus**  
Zeigt den aktuellen Status des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienstes an.  
  
**SQL Server nach unerwartetem Beenden automatisch neu starten**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent startet [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] neu, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] unerwartet beendet wird.  
  
**SQL Server-Agent nach unerwartetem Beenden automatisch neu starten**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] startet [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent neu, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent unerwartet beendet wird.  
  
**Filename**  
Geben Sie den Dateinamen für das Fehlerprotokoll an.  
  
**...**  
Mit dieser Schaltfläche können Sie nach der Fehlerprotokolldatei suchen.  
  
**Meldungen zur Ablaufverfolgung einschließen**  
Meldungen zur Ablaufverfolgung werden in das Fehlerprotokoll eingeschlossen. Meldungen zur Ablaufverfolgung stellen detaillierte Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Vorgängen bereit. Deshalb benötigt die Protokolldatei mehr Datenträgerspeicherplatz, wenn diese Option ausgewählt ist. Diese Option sollte nur bei der Behandlung eines Problems ausgewählt werden, bei dem der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent eine Rolle spielt.  
  
**OEM-Datei schreiben**  
Speichert die Fehlerprotokolldatei als Nicht-Unicode-Datei. Dadurch wird der für die Protokolldatei erforderliche Datenträgerspeicherplatz reduziert. Meldungen, die Unicode enthalten, können jedoch schwieriger lesbar sein, wenn diese Option aktiviert ist.  
  
**NET SEND-Empfänger**  
Geben Sie den Namen eines Operators ein, der NET SEND-Benachrichtigungen von Meldungen empfängt, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent in die Protokolldatei schreibt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Operatoren](../../ssms/agent/operators.md)  
[SQL Server-Agent-Fehlerprotokoll](../../ssms/agent/sql-server-agent-error-log.md)  
  
