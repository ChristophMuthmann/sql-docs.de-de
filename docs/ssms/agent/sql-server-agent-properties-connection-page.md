---
title: SQL Server-Agent-Eigenschaften (Seite Verbindung)| Microsoft-Dokumente
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- sql13.ag.agent.connection.f1
ms.assetid: d6a677ff-60ad-47ba-a0cb-df4193b165e0
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: da48136d6755097c5f266ea13af2354524be5a38
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2018
---
# <a name="sql-server-agent-properties-connection-page"></a>SQL Server-Agent-Eigenschaften (Seite Verbindung)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Mithilfe dieser Seite können Sie die Einstellungen für die Verbindung zwischen dem [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]anzeigen und ändern.  
  
## <a name="options"></a>Tastatur  
**Aliasname für den lokalen Hostserver**  
Gibt den Aliasnamen an, der beim Verbinden zur lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]verwendet wird. Wenn Sie die Standardoptionen der Verbindung für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent nicht verwenden können, definieren Sie einen Alias für die Instanz, und geben Sie den Aliasnamen hier an.  
  
**Windows-Authentifizierung verwenden**  
Legt die [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows-Authentifizierung als die Authentifizierungsmethode fest, die für die Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Instanz verwendet wird. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent wird als das Konto verbunden, als das der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst ausgeführt wird.  
  
**SQL Server-Authentifizierung verwenden**  
Legt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Authentifizierung als die Authentifizierungsmethode fest, die für die Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Instanz verwendet wird.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Authentifizierung wird aus Gründen der Abwärtskompatibilität bereitgestellt. Aus Sicherheitsgründen sollte möglichst die Windows-Authentifizierung verwendet werden.  
  
**Anmeldename**  
Gibt den Anmeldenamen an, der für die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]verwendet wird.  
  
**Kennwort**  
Gibt das Kennwort an, das für die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]verwendet wird.  
  
