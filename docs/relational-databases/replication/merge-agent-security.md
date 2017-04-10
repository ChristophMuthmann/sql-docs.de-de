---
title: "Sicherheit f&#252;r den Merge-Agent | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.security.MA.f1"
helpviewer_keywords: 
  - "Sicherheit für den Merge-Agent (Dialogfeld)"
ms.assetid: 9b86171a-4381-4b39-869a-cdc161e7cd15
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# Sicherheit f&#252;r den Merge-Agent
  Im Dialogfeld **Sicherheit für den Merge-Agent** können Sie das [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto angeben, unter dem der Merge-Agent ausgeführt wird. Der Merge-Agent wird für Pushabonnements auf dem Verteiler und für Pullabonnements auf dem Abonnenten ausgeführt. Das Windows-Konto wird auch als *Prozesskonto*bezeichnet, da der Agentprozess unter diesem Konto ausgeführt wird. Abhängig davon, wie Sie auf dieses Dialogfeld zugreifen, stehen zusätzliche Optionen zur Verfügung:  
  
-   Wenn Sie das Dialogfeld über den Assistenten für neue Abonnements aufrufen, können Sie auch den Kontext angeben, unter dem der Merge-Agent Verbindungen mit dem Abonnenten (bei Pushabonnements) oder dem Verleger und Verteiler (bei Pullabonnements) herstellt. Die Verbindung kann entweder mithilfe des Windows-Kontos oder unter dem Kontext eines von Ihnen angegebenen [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Kontos hergestellt werden.  
  
-   Wenn das Dialogfeld aus zugegriffen werden kann die **Abonnementeigenschaften** Dialogfeld geben den Kontext, unter dem der Merge-Agent Verbindungen durch Klicken auf die Eigenschaftenschaltfläche (**...**) in der **Verbindung zum Abonnenten** oder **Verlegerverbindung** Zeile des Dialogfelds. Weitere Informationen zum Zugreifen auf die **Abonnementeigenschaften** Dialogfeld finden Sie unter [anzeigen und Push Abonnementeigenschaften](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) und: [anzeigen und ändern Sie Eigenschaften von Pullabonnement](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
 Alle Konten müssen gültig sein, und für jedes Konto muss das richtige Kennwort angegeben sein. Konten und Kennwörter werden erst bei der Ausführung eines Agents überprüft.  
  
## Optionen  
 **Prozesskonto**  
 Geben Sie ein Windows-Konto ein, unter dem der Merge-Agent ausgeführt wird.  
  
-   Bei Pushabonnements muss das Konto folgende Voraussetzungen erfüllen:  
  
    -   Zumindest Mitglied der **Db_owner** -Datenbankrolle in der Verteilungsdatenbank.  
  
    -   Es muss Mitglied der Veröffentlichungszugriffsliste sein.  
  
    -   Die Anmeldung muss mit einem Benutzer in der Veröffentlichungsdatenbank verknüpft sein.  
  
    -   Es muss über Leseberechtigungen für die Momentaufnahmefreigabe verfügen.  
  
-   Bei Pullabonnements müssen Sie das Konto muss zumindest Mitglied der **Db_owner** festen Datenbankrolle in der Abonnementdatenbank.  
  
 Zusätzliche Berechtigungen sind erforderlich, wenn beim Herstellen von Verbindungen die Identität des Prozesskontos angenommen wird. Siehe nachstehende Abschnitte **Verbindung mit dem Verleger und mit dem Verteiler herstellen** und **Verbindung mit dem Abonnenten herstellen** .  
  
 **Process Account** kann bei Pullabonnements für [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]nicht angegeben werden, da der Merge-Agent auf Instanzen von [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
 **Das Kennwort** und **Kennwort bestätigen**  
 In diese Felder geben Sie das Kennwort für das Windows-Konto ein.  
  
 **Verbindung mit dem Verleger und mit dem Verteiler herstellen**  
 Bei Pushabonnements Verbindungen mit dem Verleger und Verteiler immer hergestellt, indem angegebene Konto Identität der **Prozesskonto** Textfeld.  
  
 Bei Pullabonnements müssen Sie auswählen, ob der Merge-Agent die Verbindungen mit dem Verleger und dem Verteiler entweder durch Annahme der Identität des im Textfeld **Prozesskonto** angegebenen Kontos oder mithilfe eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Kontos herstellt. Wenn Sie sich für ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konto entscheiden, müssen Sie einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Benutzernamen und ein Kennwort eingeben.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, dass Sie auswählen, um das Windows-Benutzerkonto zu imitieren, anstatt mit einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Konto.  
  
 Das für die Verbindung verwendete Windows-Konto bzw. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konto muss die folgenden Voraussetzungen erfüllen:  
  
-   Es muss Mitglied der Veröffentlichungszugriffsliste sein.  
  
-   Die Anmeldung muss mit einem Benutzer in der Veröffentlichungsdatenbank verknüpft sein.  
  
-   Die Anmeldung muss mit einem Benutzer in der Verteilungsdatenbank verknüpft sein (der Benutzer kann der Gastbenutzer sein).  
  
-   Es muss über Leseberechtigungen für die Momentaufnahmefreigabe verfügen.  
  
 **Verbindung mit dem Abonnenten herstellen**  
 Für Pullabonnements Verbindungen mit dem Abonnenten immer hergestellt, indem angegebene Konto Identität der **Prozesskonto** Textfeld.  
  
 Bei Pushabonnements müssen Sie auswählen, ob der Merge-Agent die Verbindungen mit dem Verleger und dem Verteiler entweder durch Annahme der Identität des im Textfeld **Prozesskonto** angegebenen Kontos oder mithilfe eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Kontos herstellt. Wenn Sie sich für ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konto entscheiden, müssen Sie einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Benutzernamen und ein Kennwort eingeben.  
  
> [!NOTE]  
>  Es wird empfohlen, kein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konto zu verwenden und stattdessen festzulegen, dass der Agent die Identität des Windows-Kontos annimmt.  
  
 Das Windows-Konto oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die Verbindung mit dem Abonnenten verwendete Konto muss zumindest Mitglied der **Db_owner** festen Datenbankrolle in der Abonnementdatenbank.  
  
## Siehe auch  
 [Verwalten von Anmeldeinformationen und Kennwörtern bei der Replikation](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Sicherheitsmodell des Replikations-Agents](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Replikations-Agents (Übersicht)](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  