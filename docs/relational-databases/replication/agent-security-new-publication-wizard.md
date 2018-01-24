---
title: "Agentsicherheit (Assistent für neue Veröffentlichung) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.agentsecurity.articles.f1
ms.assetid: 05ae44df-8e9f-46ea-95f6-972ad109c6c0
caps.latest.revision: "23"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 29e770bf4a90282f2ba0d5a1cd6ad7662a83c897
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="agent-security-new-publication-wizard"></a>Agentsicherheit (Assistent für neue Veröffentlichung)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Auf der **Agentsicherheit**-Seite können Sie die Konten angeben, unter denen die folgenden Agents ausgeführt werden und Verbindungen mit den Computern in einer Replikationstopologie herstellen:  
  
-   Der Momentaufnahme-Agent für alle Veröffentlichungen.  
  
-   Der Protokolllese-Agent für alle Transaktionsveröffentlichungen.  
  
-   Der Warteschlangenlese-Agent für Transaktionsveröffentlichungen, die Abonnements mit Aktualisierung gestatten. Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agentauftrag wird erstellt, wenn Sie **Transaktionsveröffentlichung mit aktualisierbaren Abonnements** auf der Seite **Veröffentlichungstyp** angegeben haben, unabhängig vom Typ der verwendeten aktualisierbaren Abonnements. Weitere Informationen zu aktualisierbaren Abonnements finden Sie unter [Aktualisierbare Abonnements für die Transaktionsreplikation](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 Weitere Informationen zu den für Agents erforderlichen Berechtigungen und zu bewährten Methoden der Replikationssicherheit finden Sie unter [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md) und [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## <a name="options"></a>Tastatur  
 **Momentaufnahme-Agent**  
 Wird für alle Veröffentlichungen angezeigt. Klicken Sie auf **Sicherheitseinstellungen** , um die Sicherheitseinstellungen im Dialogfeld **Sicherheit für den Momentaufnahme-Agent** anzugeben.  
  
 Klicken Sie im Dialogfeld **Sicherheit für den Momentaufnahme-Agent** auf **Hilfe** , um weitere Informationen zu den Berechtigungen zu erhalten, die für die vom Momentaufnahme-Agent verwendeten Konten erforderlich sind.  
  
 **Protokolllese-Agent**  
 Wird für alle Transaktionsveröffentlichungen angezeigt. Klicken Sie auf **Sicherheitseinstellungen** , um die Sicherheitseinstellungen im Dialogfeld **Sicherheit für den Protokolllese-Agent** anzugeben.  
  
 Klicken Sie im Dialogfeld **Sicherheit für den Protokolllese-Agent** auf **Hilfe** , um weitere Informationen zu den Berechtigungen zu erhalten, die für die vom Protokolllese-Agent verwendeten Konten erforderlich sind.  
  
> [!NOTE]  
>  Es gibt einen Protokolllese-Agent für jede Datenbank, die mithilfe der Transaktionsreplikation veröffentlicht wird. Wenn bereits eine Transaktionsveröffentlichung in der Datenbank vorhanden ist, sind die Sicherheitseinstellungen schreibgeschützt. Sie können die Einstellungen im Dialogfeld **Veröffentlichungseigenschaften** ändern, diese Änderungen wirken sich jedoch auf alle Transaktionsveröffentlichungen in der Datenbank aus.  
  
 **Warteschlangenlese-Agent**  
 Wird für Momentaufnahme- oder Transaktionsveröffentlichungen angezeigt, die aktualisierbare Abonnements zulassen. Klicken Sie auf **Sicherheitseinstellungen** , um die Sicherheitseinstellungen im Dialogfeld **Sicherheit für den Warteschlangenlese-Agent** anzugeben. Bei Abschluss dieses Assistenten wird ein Auftrag des Warteschlangenlese-Agents erstellt, unabhängig davon, ob Sie Abonnements mit verzögertem Update über eine Warteschlange erstellen. Wenn Sie keine Abonnements mit verzögertem Update über eine Warteschlange erstellen möchten, können Sie den Auftrag deaktivieren. Mit der rechten Maustaste klicken Sie auf den Auftrag (mit dem Namen in der Form: *[\<Publisher >].\< ganze Zahl >*.) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent **Aufträge** Ordner, und klicken Sie dann auf **Deaktivieren**  
  
 Klicken Sie im Dialogfeld **Sicherheit für den Warteschlangenlese-Agent** auf **Hilfe** , um weitere Informationen zu den Berechtigungen zu erhalten, die für die vom Warteschlangenlese-Agent verwendeten Konten erforderlich sind.  
  
> [!NOTE]  
>  Für jede Verteilungsdatenbank (und alle dazugehörigen Verleger) gibt es einen Warteschlangenlese-Agent. Wenn eine Transaktionsveröffentlichung, die Abonnements mit verzögertem Update über eine Warteschlange gestattet, bereits auf einem der Verleger vorhanden ist, die eine bestimmte Verteilungsdatenbank verwenden, sind die Sicherheitseinstellungen schreibgeschützt. Sie können das Konto, unter dem der Warteschlangenlese-Agent ausgeführt wird und Verbindungen herstellt, im Dialogfeld **Verteilereigenschaften** ändern. Die Änderungen wirken sich jedoch auf alle Veröffentlichungen aller Verleger aus, die die Verteilungsdatenbank verwenden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Erstellen von aktualisierbaren Abonnements für eine Transaktionsveröffentlichung](publish/create-updatable-subscription-to-transactional-publication.md)   
 [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Verwalten von Anmeldeinformationen und Kennwörtern bei der Replikation](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Übersicht über Replikations-Agents](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
