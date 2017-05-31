---
title: "Sicherheit für den Verteilungs-Agent (Peer-zu-Peer-Replikation) | Microsoft-Dokumentation"
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
- sql13.rep.p2pwizard.DA.f1
ms.assetid: def6bf26-c640-4caf-ad30-05d1e649541d
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cca409052d10cc153417c1bd984273e1cad4bb9a
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="distribution-agent-security-peer-to-peer-replication"></a>Sicherheit für den Verteilungs-Agent (Peer-zu-Peer-Replikation)
  Mithilfe der Seite **Sicherheit für den Verteilungs-Agent** können Sie die Konten angeben, unter denen der Verteilungs-Agent ausgeführt wird und Verbindungen mit den Computern in einer Peer-zu-Peer-Topologie hergestellt werden. Weitere Informationen zu den für Agents erforderlichen Berechtigungen und zu bewährten Methoden der Replikationssicherheit finden Sie unter [Sicherheitsmodell des Replikations-Agents](../../relational-databases/replication/security/replication-agent-security-model.md) und [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
> [!NOTE]  
>  Wenn der Verteilungs-Agent für ein Abonnement bereits in einer früheren Ausführung dieses Assistenten konfiguriert wurde, können Sie die entsprechenden in diesem Assistenten verwendeten Anmeldeinformationen nicht ändern. Von Ihnen neu angegebene Anmeldeinformationen werden ignoriert. Sie können die Anmeldeinformationen im Dialogfeld **Abonnementeigenschaften** ändern. Weitere Informationen finden Sie unter [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
## <a name="options"></a>enthalten  
 Klicken Sie in der Zeile für jeden Abonnenten auf die Eigenschaftenschaltfläche****(die Schaltfläche mit den drei Punkten), um auf das Dialogfeld **Sicherheit für den Verteilungs-Agent** zuzugreifen. Klicken Sie im geöffneten Dialogfeld **Sicherheit für den Verteilungs-Agent** auf **Hilfe** , um weitere Informationen zu den Berechtigungen zu erhalten, die für die von den Agents verwendeten Konten erforderlich sind.  
  
 Wenn Sie die Einstellungen in einem der beiden Dialogfelder eingegeben haben, werden im Raster die Verbindungsinformationen zu dem Abonnenten angezeigt.  
  
 **Agent für Abonnent**  
 Der Name der einzelnen Peers.  
  
 **Peerdatenbank**  
 Die Datenbank auf dem Peer, der sowohl als Veröffentlichungs- als auch als Abonnementdatenbank dient.  
  
 **Verbindung mit Verteiler**  
 Der Kontext, unter dem die Verbindung mit dem Verteiler hergestellt wird. Lokale Verbindungen werden immer unter dem Kontext des Windows-Kontos hergestellt, das zum Ausführen der Agents verwendet wird. Dieser Assistent erstellt Pushabonnements (die Verbindung mit dem Verteiler ist gleichzeitig die lokale Verbindung), sodass in dem betreffenden Feld immer **Impersonate '\<Domain>\\<Login\>'** oder **Impersonate '\<Computer>\\<Login\>'** angezeigt wird.  
  
 **Verbindung mit Abonnent**  
 Der Kontext, unter dem die Verbindung mit dem Abonnenten hergestellt wird. Die Verbindung kann entweder mithilfe des Kontexts des Windows-Kontos hergestellt werden, unter dem der Agent ausgeführt wird, oder mithilfe des Kontexts einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung. Das Feld zeigt eine der folgenden Angaben: **Use login '\<Login>'**, **Impersonate '\<Domain>\\<Login\>'** oder **Impersonate '\<Computer>\\<Login\>'**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, alle Verbindungen unter dem Kontext des Windows-Kontos herzustellen.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten einer Peer-zu-Peer-Topologie &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Peer-zu-Peer-Transaktionsreplikation](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
