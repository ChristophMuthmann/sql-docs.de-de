---
title: Verlegereigenschaften - Verteiler | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.configdistwizard.distpubproperties.f1
helpviewer_keywords: Publisher Properties dialog box
ms.assetid: ab6ada76-0f99-43fe-b524-baac7b1bc483
caps.latest.revision: "19"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 788b81b9917f99197df74301f6d1ec7e222dcdeb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="publisher-properties---distributor"></a>Verlegereigenschaften - Verteiler
  Mithilfe des Dialogfelds **Verlegereigenschaften** können Sie mit der Beziehung zwischen dem Verleger und dem Verteiler verknüpfte Eigenschaften anzeigen und ändern.  
  
## <a name="options"></a>Optionen  
 **Agentverbindung mit dem Verleger**  
 Geben Sie den Kontext an, in dem die folgenden Agenten Verbindungen vom Verteiler zum Verleger herstellen können:  
  
-   Der Warteschlangenlese-Agent für Transaktionsveröffentlichungen, die Abonnements mit verzögertem Update über eine Warteschlange gestatten.  
  
-   Der Momentaufnahme-Agent und der Protokolllese-Agent für Oracle-Veröffentlichungen.  
  
 Wählen Sie **Identität des Agentprozesskontos annehmen** aus, um Verbindungen mit dem Verleger mithilfe des Kontexts des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Kontos herzustellen, unter dem diese Agents ausgeführt werden, oder geben Sie **SQL Server-Authentifizierung**an, und geben Sie dann einen Wert für **Benutzername** und **Kennwort**ein. Es wird empfohlen, **Identität des Agentprozesskontos annehmen**auszuwählen. Weitere Informationen zur Agentsicherheit finden Sie unter [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
 Die Windows-Konten, unter denen diese Agents ausgeführt werden, werden im Assistenten für neue Veröffentlichung angegeben. Diese Konten können geändert werden:  
  
-   Im Dialogfeld **Verteilereigenschaften** für den Warteschlangenlese-Agent.  
  
-   Im Dialogfeld **Veröffentlichungseigenschaften** für den Momentaufnahme-Agent und den Protokolllese-Agent.  
  
 **Sonstiges**  
 Die Eigenschaften **Verlegertyp** und **Name der Verteilungsdatenbank** sind schreibgeschützt. Die Eigenschaft **Standardmomentaufnahmeordner** kann geändert werden. Weitere Informationen zum Momentaufnahmeordner finden Sie unter [Sichern des Momentaufnahmeordners](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Eigenschaftenreferenz &#40;Replikation&#41;](../../relational-databases/replication/properties-reference-replication.md)  
  
  
