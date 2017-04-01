---
title: "Agentsicherheit (Assistent f&#252;r neue Ver&#246;ffentlichung) | Microsoft Docs"
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
  - "sql13.rep.agentsecurity.articles.f1"
ms.assetid: 05ae44df-8e9f-46ea-95f6-972ad109c6c0
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Agentsicherheit (Assistent f&#252;r neue Ver&#246;ffentlichung)
  Die **-Agent-Sicherheit** Seite können Sie die Konten angeben, unter dem die folgenden Agents ausgeführt werden soll, und stellen Verbindungen mit den Computern in einer Replikationstopologie:  
  
-   Der Momentaufnahme-Agent für alle Veröffentlichungen.  
  
-   Der Protokolllese-Agent für alle Transaktionsveröffentlichungen.  
  
-   Der Warteschlangenlese-Agent für Transaktionsveröffentlichungen, die Abonnements mit Aktualisierung gestatten. Die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für diesen Agent-Agent-Auftrag wird erstellt, wenn Sie angegeben haben **Transaktionspublikation mit aktualisierbaren Abonnements** auf die **Veröffentlichungstyp** Seite unabhängig vom Typ der aktualisierbaren Abonnements. Weitere Informationen zu aktualisierbaren Abonnements finden Sie unter [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 Informationen zu Agents und best Practices für die replikationssicherheit erforderlichen Berechtigungen finden Sie unter [Sicherheitsmodell des Replikations-Agent](../../relational-databases/replication/security/replication-agent-security-model.md) und [Replikationssicherheit, bewährte Methoden](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## enthalten  
 **Momentaufnahme-Agent**  
 Wird für alle Veröffentlichungen angezeigt. Klicken Sie auf **Security Settings** die Sicherheitseinstellungen in den **Snapshot-Agent-Sicherheit** Dialogfeld.  
  
 Klicken Sie auf **Hilfe** auf die **Snapshot-Agent-Sicherheit** für Weitere Informationen zu den erforderlichen Berechtigungen für den Snapshot-Agent verwendeten Konten im Dialogfeld.  
  
 **Protokolllese-Agent**  
 Wird für alle Transaktionsveröffentlichungen angezeigt. Klicken Sie auf **Security Settings** die Sicherheitseinstellungen in der **Sicherheit für den Protokolllese-Agent** Dialogfeld.  
  
 Klicken Sie auf **Hilfe** auf die **Sicherheit für den Protokolllese-Agent** für Weitere Informationen zu den erforderlichen Berechtigungen für den Protokolllese-Agent verwendeten Konten im Dialogfeld.  
  
> [!NOTE]  
>  Es gibt einen Protokolllese-Agent für jede Datenbank, die mithilfe der Transaktionsreplikation veröffentlicht wird. Wenn bereits eine Transaktionsveröffentlichung in der Datenbank vorhanden ist, sind die Sicherheitseinstellungen schreibgeschützt. Ändern Sie die Einstellungen in der **Veröffentlichungseigenschaften** (Dialogfeld), Änderungen wirken sich jedoch alle transaktionsveröffentlichungen in der Datenbank.  
  
 **Warteschlangenlese-Agent**  
 Wird für Momentaufnahme- oder Transaktionsveröffentlichungen angezeigt, die aktualisierbare Abonnements zulassen. Klicken Sie auf **Security Settings** die Sicherheitseinstellungen in der **Sicherheit für den Warteschlangenlese-Agent** Dialogfeld. Bei Abschluss dieses Assistenten wird ein Auftrag des Warteschlangenlese-Agents erstellt, unabhängig davon, ob Sie Abonnements mit verzögertem Update über eine Warteschlange erstellen. Wenn Sie keine Abonnements mit verzögertem Update über eine Warteschlange erstellen möchten, können Sie den Auftrag deaktivieren. Mit der rechten Maustaste des Auftrags (mit dem Namen in der Form: *[\< Publisher>]. \< ganze Zahl>*.) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent **Aufträge** Ordner, und klicken Sie dann auf **deaktivieren**.  
  
 Klicken Sie auf **Hilfe** auf die **Sicherheit für den Warteschlangenlese-Agent** für Weitere Informationen zu den erforderlichen Berechtigungen für den Warteschlangenlese-Agent verwendeten Konten im Dialogfeld.  
  
> [!NOTE]  
>  Für jede Verteilungsdatenbank (und alle dazugehörigen Verleger) gibt es einen Warteschlangenlese-Agent. Wenn eine Transaktionsveröffentlichung, die Abonnements mit verzögertem Update über eine Warteschlange gestattet, bereits auf einem der Verleger vorhanden ist, die eine bestimmte Verteilungsdatenbank verwenden, sind die Sicherheitseinstellungen schreibgeschützt. Sie können das Konto, unter dem der Warteschlangenlese-Agent ausgeführt wird und Verbindungen im, Ändern der **Verteilereigenschaften** (Dialogfeld), Änderungen wirken sich jedoch Veröffentlichungen auf allen Verlegern, die die Verteilungsdatenbank verwenden.  
  
## Siehe auch  
 [Erstellen einer Veröffentlichung](../../relational-databases/replication/publish/create-a-publication.md)   
 [Erstellen von aktualisierbaren Abonnements für eine Transaktionsveröffentlichung](https://msdn.microsoft.com/library/mt740635.aspx)   
 [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Verwalten von Anmeldeinformationen und Kennwörtern bei der Replikation](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Replikations-Agents (Übersicht)](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  