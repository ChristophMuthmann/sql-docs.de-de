---
title: Zeitpläne verwalten | Microsoft-Dokumentation
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
- sql13.ag.job.manageschedules.f1
ms.assetid: f56c0736-dccc-41d2-afcf-71344aff143a
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 953fbad4ea7ede7a681b52b2e8ea32cf680e7db8
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="manage-schedules"></a>Zeitpläne verwalten
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Ermöglicht Ihnen das Anzeigen und Ändern von Eigenschaften für Auftragszeitpläne des [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents.  
  
## <a name="options"></a>Tastatur  
**Verfügbare Zeitpläne**  
Führt die für diesen Benutzer verfügbaren Zeitpläne auf. Ein Auftrag und ein Zeitplan müssen denselben Besitzer haben. Deshalb enthält die Liste nur Zeitpläne, die dem Besitzer des Auftrags gehören.  
  
**Name**  
Zeigt den Namen des Zeitplans an.  
  
**Enabled**  
Wählen Sie diese Option aus, um den Zeitplan zu aktivieren.  
  
**Beschreibung**  
Beschreibt die Bedingungen, unter denen der Zeitplan den Auftrag ausführt.  
  
**Aufträge im Zeitplan**  
Listet die Auftragsnummern auf, die an den Zeitplan angefügt sind. Wenn Sie auf eine Nummer klicken, zeigen Sie die Eigenschaften des Auftrags an.  
  
**Neu**  
Klicken Sie auf diese Schaltfläche, um einen neuen Zeitplan zu erstellen.  
  
**Delete**  
Klicken Sie auf diese Schaltfläche, um den ausgewählten Zeitplan zu löschen.  
  
**Eigenschaften**  
Klicken Sie auf diese Schaltfläche, um die Eigenschaften des ausgewählten Zeitplans zu ändern.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Anlegen und Zuweisen von Zeitplänen zu Aufträgen](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
  
