---
title: Optimieren der automatischen Verwaltung in einem Unternehmen | Microsoft-Dokumentation
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
helpviewer_keywords:
- performance [SQL Server], automated administration
- tuning automated administration [SQL Server]
- monitoring performance [SQL Server], automated administration
ms.assetid: 671fed35-3859-4b0d-8f38-4dd07436857e
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 952fe37adc74e5ba7312e2ba1afd40ff50f74249
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="tune-automated-administration-across-an-enterprise"></a>Optimieren der automatischen Verwaltung in einem Unternehmen
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Die Multiserververwaltung mit dem Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent nutzt die Selbstoptimierungsfunktionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Deshalb ist unter normalen Bedingungen keine zusätzliche Auftragsoptimierung erforderlich. Die Belastung des Netzwerks nimmt jedoch zu, wenn Sie Aufträge ausführen, Warnungen generieren und Operatoren benachrichtigen. Sie können die automatische Administration für ein Unternehmen optimieren, um den Netzwerkverkehr zu minimieren, der durch diese Aktivitäten verursacht wird.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Überwachen der Leistung des Datenflussmoduls](http://msdn.microsoft.com/en-us/11e17f4e-72ed-44d7-a71d-a68937a78e4c)  
  
