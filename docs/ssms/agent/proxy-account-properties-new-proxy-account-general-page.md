---
title: 'Proxyeigenschaften: Neues Proxykonto (Seite „Allgemein“) | Microsoft-Dokumentation'
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
- sql13.ag.proxy.general.f1
ms.assetid: 5cd81265-bf59-413b-8397-150ddc70d0c7
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bfe2ff4e8cc614386634a2b80afcee82df2dcf18
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2018
---
# <a name="proxy-account-properties---new-proxy-account-general-page"></a>Proxyeigenschaften – Neues Proxykonto (Seite „Allgemein“)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Mithilfe dieser Seite können Sie die Eigenschaften für ein Proxykonto für den [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent anzeigen und ändern.  
  
## <a name="options"></a>Tastatur  
**Proxyname**  
Geben Sie den Namen des Proxys ein.  
  
**Anmeldeinformationsname**  
Geben Sie den Namen der Anmeldeinformationen für den Proxy ein.  
  
> [!NOTE]  
> Der eingegebene Anmeldeinformationsname muss der Name von vorhandenen Anmeldeinformationen sein. Informationen zum Erstellen von Anmeldeinformationen finden Sie unter [Vorgehensweise: Erstellen eines Proxykontos (SQL Server Management Studio)](http://msdn.microsoft.com/en-us/c1e77e91-2a69-40d9-b8b3-97cffc710586)  
  
**...**  
Öffnet das Dialogfeld **Anmeldeinformationen auswählen** .  
  
**Beschreibung**  
Geben Sie die Beschreibung für den Proxy ein.  
  
**Folgenden Subsystemen gegenüber aktiv**  
Wählen Sie die Subsysteme aus, auf die das Proxykonto zugreifen kann.  
  
**Auftragsschritte erneut zuweisen an**  
Wählen Sie den Proxy aus, dem die Auftragsschritte neu zugewiesen werden sollen. Die Liste ist aktiviert, wenn Sie den Zugriff auf ein Subsystem aufheben, auf das der Proxy vorher zugreifen konnte.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Erstellen eines Proxys für den SQL Server-Agent](../../ssms/agent/create-a-sql-server-agent-proxy.md)  
  
