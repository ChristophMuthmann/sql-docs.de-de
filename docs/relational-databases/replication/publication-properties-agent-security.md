---
title: Veröffentlichungseigenschaften (Agentsicherheit) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
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
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.agentsecurity.f1
ms.assetid: 03945aac-66f2-4370-b5d1-c1de694bc4c1
caps.latest.revision: 21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b52ab3babf22f6e45ba41c941bf67ed79e5460b2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="publication-properties-agent-security"></a>Veröffentlichungseigenschaften (Agentsicherheit)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Mithilfe der Seite **Agentsicherheit** des Dialogfelds **Veröffentlichungseigenschaften** können Sie auf die Eigenschaften für die Konten zugreifen, unter denen die folgenden Agents ausgeführt werden und Verbindungen mit Computern in einer Replikationstopologie herstellen:  
  
-   Der Momentaufnahme-Agent für alle Veröffentlichungen.  
  
-   Der Protokolllese-Agent für alle Transaktionsveröffentlichungen. Es gibt einen Protokolllese-Agent für jede Datenbank, die zur Transaktionsreplikation veröffentlicht wird. Das Ändern der Einstellungen des Protokolllese-Agents betrifft alle Transaktionsveröffentlichungen in einer Datenbank.  
  
-   Der Warteschlangenlese-Agent für Transaktionsveröffentlichungen, die Abonnements mit verzögertem Update über eine Warteschlange gestatten. Es gibt einen Warteschlangenlese-Agent für jede Verteilungsdatenbank. Das Ändern der Einstellungen für den Warteschlangenlese-Agent betrifft alle Transaktionsveröffentlichungen mit Abonnements mit verzögertem Update über eine Warteschlange, die dieselbe Verteilungsdatenbank verwenden. Weitere Informationen zu den Sicherheitseinstellungen des Warteschlangenlese-Agents finden Sie unter [Anzeigen und Ändern von Replikationssicherheitseinstellungen](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 Weitere Informationen zu den für die einzelnen Agents erforderlichen Sicherheitseinstellungen und Berechtigungen finden Sie unter [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## <a name="options"></a>Tastatur  
 **Sicherheitseinstellungen** oder **Agent erstellen**  
 Klicken Sie, nachdem ein Agentauftrag erstellt wurde, auf **Sicherheitseinstellungen** , um auf ein Dialogfeld zuzugreifen, das Ihnen das Ändern der Sicherheitseinstellungen für einen Agent ermöglicht. Wenn kein Agentauftrag erstellt wurde, klicken Sie zum Erstellen eines Agentauftrags auf **Agent erstellen** , und geben Sie die Sicherheitseinstellungen an.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Sicherheit und Schutz &#40;Replikation&#41;](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
