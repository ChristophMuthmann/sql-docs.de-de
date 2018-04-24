---
title: MSSQL_ENG014010 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG014010 error
ms.assetid: 6ea84f2f-e7a2-4028-9ea9-af0d2eba660e
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3e2fa6c35c326711a5dc7b3fb6842f946b506977
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqleng014010"></a>MSSQL_ENG014010
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|14010|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Der Server '%1!s!' ist nicht als Abonnementserver definiert.|  
  
## <a name="explanation"></a>Erklärung  
 Die Replikation erwartet, dass alle Server in einer Topologie mithilfe des Computernamens mit einem optionalen Instanznamen (bei Clusterinstanzen mithilfe des virtuellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Servernamens mit dem optionalen Instanznamen) registriert werden. Damit die Replikation ordnungsgemäß funktioniert, muss der von `SELECT @@SERVERNAME` für jeden Server in der Topologie zurückgegebene Wert mit dem Computernamen bzw. dem virtuellen Servernamen mit dem optionalen Instanznamen übereinstimmen.  
  
 Die Replikation wird nicht unterstützt, wenn Sie eine der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen über die IP-Adresse oder den vollqualifizierten Domänennamen registriert haben. Dieser Fehler kann ausgelöst werden, wenn beim Konfigurieren der Replikation eine der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen über die IP-Adresse oder den vollqualifizierten Domänennamen in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] registriert ist.  
  
## <a name="user-action"></a>Benutzeraktion  
 Überprüfen Sie, dass alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen der Topologie ordnungsgemäß registriert sind. Wenn der Netzwerkname des Computers und der Name der SQL Server-Instanz nicht identisch sind, gehen Sie wie folgt vor:  
  
-   Fügen Sie den SQL Server-Instanznamen als gültigen Netzwerknamen hinzu. Eine Möglichkeit, einen alternativen Netzwerknamen festzulegen, besteht darin, diesen Namen der lokalen Hostdatei hinzuzufügen. Die lokale Hostdatei befindet sich standardmäßig in WINDOWS\system32\drivers\etc oder WINNT\system32\drivers\etc. Weitere Informationen finden Sie in der Windows-Dokumentation.  
  
     Wenn der Computername z. B. comp1 ist und die IP-Adresse des Computers 10.193.17.129 lautet und wenn der Instanzname inst1/instname ist, ist der Hostdatei der folgende Eintrag hinzuzufügen:  
  
     10.193.17.129 inst1  
  
-   Entfernen Sie die Replikation, registrieren Sie einzelne [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen, und stellen Sie dann die Replikation wieder her. Wenn der @@SERVERNAME-Wert für eine nicht in einem Cluster befindliche Instanz falsch ist, führen Sie die folgenden Schritte aus:  
  
    ```  
    sp_dropserver '<old_name>', 'droplogins'  
    go  
    sp_addserver '<new_name>', 'local'  
    go  
    ```  
  
     Nachdem Sie die gespeicherte Prozedur [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)ausgeführt haben, müssen Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienst neu starten, damit die Änderung an @@SERVERNAME wirksam wird.  
  
     Wenn der @@SERVERNAME-Wert für eine in einem Cluster befindliche Instanz falsch ist, müssen Sie mithilfe der Clusterverwaltung den Namen ändern. Weitere Informationen finden Sie unter [Always On-Failoverclusterinstanzen &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)unterstützt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [@@SERVERNAME &#40;Transact-SQL&#41;](../../t-sql/functions/servername-transact-sql.md)   
 [Fehler- und Ereignisreferenz &#40;Replikation&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
