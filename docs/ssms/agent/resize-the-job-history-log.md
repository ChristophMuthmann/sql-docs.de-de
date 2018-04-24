---
title: Ändern der Größe des Auftragsverlaufsprotokolls | Microsoft-Dokumentation
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
- jobs [SQL Server Agent], history
- resizing job history log
- size [SQL Server], job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: ddee1ce8-9d1b-4017-9894-bf7256aed95d
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3a6ee894c216ce27c5919675e6b1ae38a60e1e44
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="resize-the-job-history-log"></a>Resize the Job History Log
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In diesem Thema wird beschrieben, wie Sie Größenbeschränkungen für Agent-Auftragsverlaufsprotokolle in [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] festlegen.
  
-   **Vorbereitungen:**  
  
    [Security](#Security)  
  
-   **So legen Sie Größenbeschränkungen für den Auftragsverlauf fest mit**  
  
    [SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Security"></a>Security  
Ausführliche Informationen finden Sie unter [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Verwenden von SQL Server Management Studio  
  
*So ändern Sie die Größe des Auftragsverlaufsprotokolls basierend auf der Basisgröße:*
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]her, und erweitern Sie dann diese Instanz.  
  
2.  Klicken Sie mit der rechten Maustaste auf **SQL Server-Agent**, und klicken Sie anschließend auf **Eigenschaften**.  
  
3.  Wählen Sie die Seite **Verlauf** aus und bestätigen Sie dann, dass **Größe des Auftragsverlaufsprotokolls beschränken**aktiviert ist.  
  
4.  Geben Sie im Feld **Maximale Länge des Auftragsverlaufsprotokolls** die Anzahl von Zeilen ein, die maximal für das Auftragsverlaufsprotokoll zulässig sind.  
  
5.  Geben Sie im Feld **Maximale Zeilenanzahl pro Auftrag in Auftragsverlauf** die Anzahl von Zeilen ein, die maximal für das Auftragsverlaufsprotokoll eines Auftrags zulässig sind.  
  
**So ändern Sie die Größe des Auftragsverlaufsprotokolls basierend auf der Zeit:**
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung zu einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]her, und erweitern Sie dann diese Instanz.  
  
2.  Klicken Sie mit der rechten Maustaste auf **SQL Server-Agent**, und klicken Sie anschließend auf **Eigenschaften**.  
  
3.  Wählen Sie die Seite **Verlauf** aus, und klicken Sie dann auf **Agentverlauf automatisch entfernen**.  
  
4.  Wählen Sie die entsprechende Anzahl der **Tage**, **Wochen** oder **Monate** aus.  
  
