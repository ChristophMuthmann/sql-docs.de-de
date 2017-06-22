---
title: "Sicherheit für den Protokolllese-Agent (Peer-zu-Peer-Replikation) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.p2pwizard.LRA.f1
ms.assetid: 6575e2a8-16bb-449c-bdca-4a4202d0972f
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7b670e48c6859dfaad38b9383fb3e2056fa47994
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="log-reader-agent-security-peer-to-peer-replication"></a>Sicherheit für den Protokolllese-Agent (Peer-zu-Peer-Replikation)
  Mithilfe der Seite **Sicherheit für den Protokolllese-Agent** können Sie Konten angeben, unter denen der Protokolllese-Agent auf jedem Peer ausgeführt wird und die Verbindungen hergestellt werden. Weitere Informationen zu den für Agents erforderlichen Berechtigungen und zu bewährten Methoden der Replikationssicherheit finden Sie unter [Sicherheitsmodell des Replikations-Agents](../../relational-databases/replication/security/replication-agent-security-model.md) und [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
> [!NOTE]  
>  Es gibt einen Protokolllese-Agent für jede Datenbank, die mithilfe der Transaktionsreplikation veröffentlicht wird. Wenn der Protokolllese-Agent für eine Datenbank bereits konfiguriert wurde (entweder für eine Veröffentlichung bei einer vorherigen Ausführung dieses Assistenten oder für eine andere Transaktionsveröffentlichung in derselben Datenbank), können Sie die bestehenden Anmeldeinformationen mit diesem Assistenten nicht ändern. Von Ihnen neu angegebene Anmeldeinformationen werden ignoriert. Sie können die Anmeldeinformationen im Dialogfeld **Veröffentlichungseigenschaften** ändern. Weitere Informationen finden Sie unter [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
## <a name="options"></a>enthalten  
 Klicken Sie in der Zeile für jeden Peer auf die Eigenschaftenschaltfläche****(die Schaltfläche mit den drei Punkten), um auf das Dialogfeld **Sicherheit für den Protokolllese-Agent** zuzugreifen. Klicken Sie im geöffneten Dialogfeld **Sicherheit für den Protokolllese-Agent** auf **Hilfe** , um weitere Informationen zu den Berechtigungen zu erhalten, die für die von den Agents verwendeten Konten erforderlich sind.  
  
 Wenn Sie die Einstellungen im Dialogfeld eingegeben haben, werden im Raster die Verbindungsinformationen zu dem Abonnenten angezeigt.  
  
 **Agents für Verleger**  
 Der Name jeder Peerserverinstanz.  
  
 **Peerdatenbank**  
 Die Datenbank, die auf jedem Peer als Veröffentlichungs- und Abonnementdatenbank dient.  
  
 **Verbindung mit Verteiler**  
 Der Kontext, unter dem die Verbindung mit dem Verteiler hergestellt wird. Die lokale Verbindung mit dem Verteiler wird immer mithilfe des Kontexts des [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Windows-Kontos hergestellt, unter dem der Agent ausgeführt wird. In diesem Feld wird daher immer **Identität von „\<Domain>\\<Login\>“ annehmen** oder **Identität von „\<Computer>\\<Login\>“ annehmen** angezeigt.  
  
 **Verbindung mit dem Verleger**  
 Der Kontext, unter dem die Verbindung mit dem Verleger hergestellt wird. Die Verbindung mit dem Verleger kann mithilfe einer [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung oder mithilfe des Windows-Kontos, unter dem der Agent ausgeführt wird, hergestellt werden. Das Feld zeigt eine der folgenden Angaben: **Anmeldung „\<Login>“ verwenden**, **Identität von „\<Domain>\\<Login\>“annehmen** oder **Identität von „\<Computer>\\<Login\>“annehmen**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, alle Verbindungen unter dem Kontext des Windows-Kontos herzustellen.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten einer Peer-zu-Peer-Topologie &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Peer-zu-Peer-Transaktionsreplikation](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
