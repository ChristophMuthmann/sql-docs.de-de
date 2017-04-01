---
title: "Anmeldename f&#252;r aktualisierbare Abonnements | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.updatablesubscriptionslogin.f1"
ms.assetid: 301ea227-0455-40ba-9009-d38f8676b325
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# Anmeldename f&#252;r aktualisierbare Abonnements
  Für sofortige Aktualisierung, sofern Sie **replizieren** auf die **aktualisierbare Abonnements** Seite dieses Assistenten müssen Sie ein Konto angeben, mit dem Abonnenten, unter denen Verbindungen mit dem Verleger hergestellt werden. 
  
 Verbindungen werden von den Triggern verwendet, die auf dem Abonnenten auslösen und Änderungen an den Verleger weitergegeben. Dieses Konto ist erforderlich, auch wenn Sie **in die Warteschlange ändert und Commit baldmöglichst ausführen** auf die **aktualisierbare Abonnements** Seite. Assistenten für neue Abonnements standardmäßig konfiguriert Aktualisieren über eine Warteschlange mit der Möglichkeit, zur sofortigen Aktualisierung zu wechseln.  
  
> **WICHTIG!** Das Konto angegeben, für die Verbindung nur sollte Berechtigung zum Einfügen, aktualisieren und Löschen von Daten auf die Ansichten, die die Replikation in der Veröffentlichungsdatenbank erstellt. Es sollten keine weiteren Berechtigungen erhalten. Erteilen von Berechtigungen für Sichten in der Publikationsdatenbank mit dem Namen in der Form **Syncobj_***\< HexadecimalNumber>* für das Konto, das Sie auf den einzelnen Abonnenten konfiguriert.  
  
 Für den Typ der Verbindung gibt es drei Optionen:  
  
-   Ein vordefinierter Verbindungsserver oder Remoteserver.  
  
-   Ein durch die Replikation erstellter Verbindungsserver. Die Verbindung wird mit den Anmeldeinformationen hergestellt, die Sie im Assistenten angeben.  
  
-   Ein durch die Replikation erstellter Verbindungsserver. Die Verbindung wird mit den Anmeldeinformationen des Benutzers hergestellt, der die Änderung auf dem Abonnenten vornimmt.  
  
 Die ersten beiden Optionen können im Assistenten angegeben werden. Die letzte Option kann nur angegeben werden mit [Sp_link_publication &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md); Geben Sie den Wert **1** für den Parameter **@security_mode**.  
  
## enthalten  
 **Erstellen Sie einen Verbindungsserver, der die Verbindung mithilfe des folgenden Anmeldenamens für die SQL Server-Authentifizierung herstellt:**  
 Die Replikation erstellt einen Verbindungsserver mithilfe der Anmeldeinformationen in der **Anmeldung** und **Kennwort** Felder.  
  
 **Anmeldename**  
 Geben Sie einen [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung, die nur die in diesem Thema beschriebenen Berechtigungen aufweist.  
  
 **Kennwort**  
 Geben Sie ein sicheres Kennwort für die Anmeldung, die im angegebenen **Anmeldung**.  
    
 **Vordefinierten Verbindungsserver oder Remoteserver verwenden**  
 Bei dieser Option ist ein bereits von Ihnen definierter Verbindungsserver oder Remoteserver erforderlich. Weitere Informationen finden Sie unter [Verbindungsserver &#40; Datenbankmodul &#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md) und [Remoteserver](../../database-engine/configure-windows/remote-servers.md). Stellen Sie sicher, dass der für den Verbindungsserver oder Remoteserver verwendete Anmeldename ein sicheres Kennwort sowie ausschließlich die in diesem Thema beschriebenen Berechtigungen aufweist.  
  
## Siehe auch  
 [Erstellen von aktualisierbaren Abonnements für eine Transaktionsveröffentlichung](https://msdn.microsoft.com/library/ms152769.aspx)   
 [Anzeigen und Ändern von Replikationssicherheitseinstellungen](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Aktualisierbare Abonnements für die Transaktionsreplikation](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  