---
title: "Ver&#246;ffentlichungseigenschaften (Agentsicherheit) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.agentsecurity.f1"
ms.assetid: 03945aac-66f2-4370-b5d1-c1de694bc4c1
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# Ver&#246;ffentlichungseigenschaften (Agentsicherheit)
  Mithilfe der Seite **Agentsicherheit** des Dialogfelds **Veröffentlichungseigenschaften** können Sie auf die Eigenschaften für die Konten zugreifen, unter denen die folgenden Agents ausgeführt werden und Verbindungen mit Computern in einer Replikationstopologie herstellen:  
  
-   Der Momentaufnahme-Agent für alle Veröffentlichungen.  
  
-   Der Protokolllese-Agent für alle Transaktionsveröffentlichungen. Es gibt einen Protokolllese-Agent für jede Datenbank, die zur Transaktionsreplikation veröffentlicht wird. Das Ändern der Einstellungen des Protokolllese-Agents betrifft alle Transaktionsveröffentlichungen in einer Datenbank.  
  
-   Der Warteschlangenlese-Agent für Transaktionsveröffentlichungen, die Abonnements mit verzögertem Update über eine Warteschlange gestatten. Es gibt einen Warteschlangenlese-Agent für jede Verteilungsdatenbank. Das Ändern der Einstellungen für den Warteschlangenlese-Agent betrifft alle Transaktionsveröffentlichungen mit Abonnements mit verzögertem Update über eine Warteschlange, die dieselbe Verteilungsdatenbank verwenden. Weitere Informationen zu den Sicherheitseinstellungen des Warteschlangenlese-Agent finden Sie unter [anzeigen und Ändern von Replikationssicherheitseinstellungen](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 Weitere Informationen zu den für die einzelnen Agents erforderlichen Sicherheitseinstellungen und Berechtigungen finden Sie unter [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## Optionen  
 **Sicherheitseinstellungen** oder **-Agent erstellen**  
 Wenn kein Agentauftrag erstellt wurde, klicken Sie auf **Security Settings** auf ein Dialogfeld zugreifen, die Ihnen ermöglicht, die Einstellung für einen Agent zu ändern. Wenn kein Agentauftrag erstellt wurde, klicken Sie zum Erstellen eines Agentauftrags auf **Agent erstellen** , und geben Sie die Sicherheitseinstellungen an.  
  
## Siehe auch  
 [Erstellen einer Veröffentlichung](../../relational-databases/replication/publish/create-a-publication.md)   
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Sicherheit und Schutz & #40; Replikation & #41;](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  