---
title: "Ändern des Proxykontos für den Hilfsprogramm-Sammlungssatz auf einer verwalteten Instanz von SQL Server | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ff37ba8b-a08c-4109-b6e2-5748c995a52c
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5345501c146c5d48d8d7f8cd5fd06f4fc9dfc749
ms.lasthandoff: 04/11/2017

---
# <a name="change-proxy-account-for-utility-collection-on--managed-sql-server"></a>Ändern des Proxykontos für den Hilfsprogramm-Sammlungssatz auf einer verwalteten Instanz von SQL Server
  In diesem Thema wird beschrieben, wie Sie das Proxykonto für den Hilfsprogramm-Sammlungssatz auf einer verwalteten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ändern können.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-change-the-proxy-account-for-the-utility-collection-set-on-a-managed-instance-of-sql-server"></a>So ändern Sie das Proxykonto für den Hilfsprogramm-Sammlungssatz auf einer verwalteten Instanz von SQL Server  
  
1.  Entfernen Sie die verwaltete Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aus dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm.  
  
    -   Klicken Sie im **Hilfsprogramm-Explorer** in SSMS auf den Knoten **Verwaltete Instanzen** .  
  
    -   Klicken Sie in der Listenansicht **Hilfsprogramm-Explorer** mit der rechten Maustaste auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanznamen, und wählen Sie **Verwaltete Instanz entfernen**aus. Weitere Informationen finden Sie unter [Vorgehensweise: Entfernen einer Instanz von SQL Server aus dem SQL Server-Hilfsprogramm](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md).  
  
2.  Registrieren Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erneut im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm.  
  
    -   Klicken Sie im **Hilfsprogramm-Explorer** in SSMS mit der rechten Maustaste auf den Knoten **Verwaltete Instanzen** , und wählen Sie **Verwaltete Instanz hinzufügen**aus.  
  
    -   Befolgen Sie die Eingabeaufforderungen zum Abschließen des Assistenten, indem Sie das neue Proxykonto angeben.  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Problembehandlung beim SQL Server-Hilfsprogramm](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  
