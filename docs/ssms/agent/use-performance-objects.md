---
title: Verwenden von Leistungsobjekten | Microsoft-Dokumentation
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
helpviewer_keywords:
- SQL Server Agent, monitoring
- SQL Server Agent service, monitoring
- SQL Server Agent service, performance objects
- SQL Server Agent, performance objects
- performance objects [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- performance counters [SQL Server], SQL Server Agent
- counters [SQL Server], SQL Server Agent
ms.assetid: 830b843a-6b2a-4620-a51b-98358e9fc54b
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d5033120057e83f6fd155466a35188be04068ef6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="use-performance-objects"></a>Verwenden von Leistungsobjekten
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent umfasst Leistungsobjekte und -indikatoren zum Überwachen der Leistung des Diensts. Mithilfe dieser Leistungsobjekte können Sie das Windows-Tool Systemmonitor verwenden, um festzustellen, welche Vorgänge vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst im Hintergrund ausgeführt werden. Sie können beispielsweise die Anzahl der aktiven Aufträge feststellen, die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst aktuell ausgeführt werden, um blockierte Aufträge zu identifizieren.  
  
Die Leistungsobjekte und Leistungsindikatoren des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Diensts sind für jede Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] vorhanden, die auf einem Computer installiert ist. Leistungsobjekte sind nach der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] benannt, die jedes Objekt repräsentiert.  
  
Die folgende Tabelle veranschaulicht, wie die Leistungsobjekte des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Diensts benannt werden:  
  
|Instanztyp|Objektname|  
|-----------------|---------------|  
|Default|**SQLAgent:***Objekt*:*Zähler*|  
|Benannt|**SQLAgent$**<br /> ***Instanzname*:***Objekt*:*Zähler*|  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] beinhaltet die folgenden Leistungsobjekte für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent.  
  
|Objektname|Description|  
|---------------|---------------|  
|[SQLAgent:Aufträge](http://msdn.microsoft.com/en-us/225b5e2d-4a78-4178-b2b6-b419df83c4aa)|Leistungsinformationen zu gestarteten Aufträgen, Erfolgsrate und aktuellem Status|  
|[SQLAgent:Auftragsschritte](http://msdn.microsoft.com/en-us/44f9983c-1753-4fe0-8475-973aa2460b3a)|Statusinformationen zu Auftragsschritten|  
|[SQLAgent:Warnungen](http://msdn.microsoft.com/en-us/e5e37f74-ee88-46d0-ad8f-71fd1b1fa64a)|Informationen zur Anzahl der Warnungen und Benachrichtigungen|  
|[SQLAgent:Statistik](http://msdn.microsoft.com/en-us/ebe92bfa-0721-48aa-9ba6-e7904ad265a1)|Allgemeine Leistungsinformationen|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Überwachen und Optimieren der Leistung](http://msdn.microsoft.com/en-us/87f23f03-0f19-4b2e-bfae-efa378f7a0d4)  
[Vorgehensweise: Starten des Systemmonitors (Windows)](http://msdn.microsoft.com/en-us/5e51bb79-5737-470b-9c47-fac330c001c5)  
  
