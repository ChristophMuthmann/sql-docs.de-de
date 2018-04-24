---
title: Eintragen eines Zielservers bei einem Masterserver | Microsoft-Dokumentation
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
- enlisting target servers [SQL Server]
- SQL Server Agent jobs, target servers
- master servers [SQL Server], enlisting target servers
- SQL Server Agent jobs, master servers
- target servers [SQL Server], enlisting
ms.assetid: 7633adb5-d140-4e58-a8f2-5b4b50c2f95b
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 63173c03617d5d7c3198bc8c29e9b5d7f78ee5f7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="enlist-a-target-server-to-a-master-server"></a>Eintragen eines Zielservers bei einem Masterserver
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In diesem Thema wird die Vorgehensweise zum Hinzufügen eines Zielservers zu einer Multiserververwaltungskonfiguration beschrieben. Führen Sie die folgenden Schritte auf dem Masterserver aus. Die Schritte können in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)]oder SQL Server Management Objects (SMO) ausgeführt werden.  
  
Informationen zu den Auswirkungen des für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst verwendeten Windows-Kontos auf eine Multiserverumgebung finden Sie unter [Erstellen einer Multiserverumgebung](../../ssms/agent/create-a-multiserver-environment.md).  
  
Die vollständige SSL-Verschlüsselung (Secure Sockets Layer) und die Zertifikatüberprüfung sind für Verbindungen zwischen Masterservern und Zielservern standardmäßig aktiviert. Weitere Informationen finden Sie unter [Festlegen von Verschlüsselungsoptionen auf Zielservern](../../ssms/agent/set-encryption-options-on-target-servers.md).  
  
**In diesem Thema**  
  
-   **Eintragen eines Zielservers mit:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="SSMSProcedure"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-enlist-a-target-server"></a>So tragen Sie einen Zielserver ein  
  
1.  Erweitern Sie im **Objekt-Explorer**einen Server, der als Masterserver konfiguriert ist.  
  
2.  Klicken Sie mit der rechten Maustaste auf **SQL Server-Agent**, zeigen Sie auf **Multiserveradministration**, und klicken Sie dann auf **Zielserver hinzufügen**.  
  
3.  Schließen Sie den Zielservererstellungs-Assistenten ab, in dem Sie durch den Prozess geleitet werden.  
  
## <a name="TsqlProcedure"></a>Verwenden von Transact-SQL  
  
#### <a name="to-enlist-a-target-server"></a>So tragen Sie einen Zielserver ein  
  
1.  Verwenden Sie die gespeicherte Prozedur **sp_msx_enlist** .  Weitere Informationen finden Sie unter [sp_msx_enlist (Transact-SQL)](http://msdn.microsoft.com/en-us/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Automatisierte Verwaltung in einem Unternehmen](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  
