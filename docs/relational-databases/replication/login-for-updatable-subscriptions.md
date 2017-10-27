---
title: "Anmeldename für aktualisierbare Abonnements | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/25/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.newsubwizard.updatablesubscriptionslogin.f1
ms.assetid: 301ea227-0455-40ba-9009-d38f8676b325
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 8ec5dd80718de624c3e45ac81eceedc7dfaed2ad
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="login-for-updatable-subscriptions"></a>Anmeldename für aktualisierbare Abonnements
  Wenn Sie im Assistenten auf der Seite **Aktualisierbare Abonnements** die Option **Replizieren** ausgewählt haben, müssen Sie mit dem Abonnenten ein Konto angeben, unter dem die Verbindungen mit dem Verleger für das sofortige Update hergestellt werden. 
  
 Die Verbindungen werden durch die Trigger verwendet, die auf dem Abonnenten ausgelöst werden und die Änderungen zum Verleger weitergeben. Dieses Konto ist erforderlich, auch wenn Sie **Änderungen in die Warteschlange einreihen und Commit baldmöglichst ausführen** auf der Seite **Aktualisierbare Abonnements** ausgewählt haben. Der Assistent für neue Abonnements konfiguriert standardmäßig verzögerte Updates über eine Warteschlange mit der Möglichkeit, zur sofortigen Aktualisierung zu wechseln.  
  
> **WICHTIG!** Dem für die Verbindung angegebenen Konto sollten nur die Berechtigung zum Einfügen, Aktualisieren und Löschen der Daten in den durch die Replikation in der Veröffentlichungsdatenbank erstellten Sichten erteilt werden. Darüber hinaus sollte das Konto über keine weiteren Berechtigungen verfügen. Erteilen Sie dem von Ihnen auf den einzelnen Abonnenten konfigurierten Konto Berechtigungen für Sichten in der Veröffentlichungsdatenbank, deren Namen das Format **syncobj_***\<HexadecimalNumber>* aufweisen.  
  
 Für den Typ der Verbindung gibt es drei Optionen:  
  
-   Ein vordefinierter Verbindungsserver oder Remoteserver.  
  
-   Ein durch die Replikation erstellter Verbindungsserver. Die Verbindung wird mit den Anmeldeinformationen hergestellt, die Sie im Assistenten angeben.  
  
-   Ein durch die Replikation erstellter Verbindungsserver. Die Verbindung wird mit den Anmeldeinformationen des Benutzers hergestellt, der die Änderung auf dem Abonnenten vornimmt.  
  
 Die ersten beiden Optionen können im Assistenten angegeben werden. Die letzte Option kann nur mithilfe von [sp_link_publication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) angegeben werden. Geben Sie für den Parameter **@security_mode** den Wert **1** an.  
  
## <a name="options"></a>enthalten  
 **Erstellen Sie einen Verbindungsserver, der die Verbindung mithilfe des folgenden Anmeldenamens für die SQL Server-Authentifizierung herstellt:**  
 Durch die Replikation wird ein Verbindungsserver mithilfe der in den Feldern **Anmeldename** und **Kennwort** angegebenen Anmeldeinformationen erstellt.  
  
 **Anmeldename**  
 Geben Sie einen [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldenamen ein, der nur die in diesem Thema beschriebenen Berechtigungen aufweist.  
  
 **Kennwort**  
 Geben Sie ein sicheres Kennwort für den in **Anmeldename**angegebenen Anmeldenamen ein.  
    
 **Vordefinierten Verbindungsserver oder Remoteserver verwenden**  
 Bei dieser Option ist ein bereits von Ihnen definierter Verbindungsserver oder Remoteserver erforderlich. Weitere Informationen finden Sie unter [Verbindungsserver &#40;Datenbankmodul&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md) und [Remoteserver](../../database-engine/configure-windows/remote-servers.md). Stellen Sie sicher, dass der für den Verbindungsserver oder Remoteserver verwendete Anmeldename ein sicheres Kennwort sowie ausschließlich die in diesem Thema beschriebenen Berechtigungen aufweist.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von aktualisierbaren Abonnements für eine Transaktionsveröffentlichung](publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [Anzeigen und Ändern von Replikationssicherheitseinstellungen](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Aktualisierbare Abonnements für die Transaktionsreplikation](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  

