---
title: "Verteilereigenschaften (Allgemein) | Microsoft Docs"
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
  - "sql13.rep.configdistwizard.distproperties.general.f1"
helpviewer_keywords: 
  - "Verteilereigenschaften (Dialogfeld)"
ms.assetid: ab4120ec-e524-4c0c-8b48-f2f40adb1a3b
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Verteilereigenschaften (Allgemein)
  Mithilfe der Seite **Allgemein** des Dialogfelds **Verteilereigenschaften** können Sie Verteilungsdatenbanken hinzufügen und löschen sowie Eigenschaften von Verteilungsdatenbanken festlegen.  
  
 Die Verteilungsdatenbank speichert Metadaten und Verlaufsdaten für alle Replikationstypen und Transaktionen für die Transaktionsreplikation. In vielen Fällen reicht eine Verteilungsdatenbank aus. Wenn jedoch mehrere Verleger einen Verteiler verwenden, sollten Sie die Erstellung einer Verteilungsdatenbank für jeden Verleger in Betracht ziehen. Auf diese Weise stellen Sie sicher, dass die durch jede Verteilungsdatenbank fließenden Daten eindeutig sind.  
  
## Optionen  
 **Datenbanken**  
 Die **Datenbanken** Eigenschaftenraster zeigt die Eigenschaften Name und Aufbewahrung der Verteilungsdatenbanken auf dem Verteiler. **Transaktionsbeibehaltung** ist die Länge der Transaktionen für die Transaktionsreplikation gespeichert werden (Transaction Retention ist auch bekannt als verteilungsbeibehaltung). **Verlaufsbeibehaltung** ist die Dauer, die Metadaten des Verlaufs für jede Art von Replikation gespeichert werden. Weitere Informationen zur verteilungsbeibehaltung finden Sie unter [Abonnementablauf und-Deaktivierung](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 Klicken Sie auf die Eigenschaftenschaltfläche (**...**) in der **Datenbanken** Eigenschaftenraster zum Starten der **Eigenschaften der Verteilungsdatenbank** Dialogfeld.  
  
 **Neu**  
 Erstellt eine neue Verteilungsdatenbank  
  
 **Delete**  
 Wählen Sie eine vorhandene Verteilungsdatenbank in der **Datenbanken** Eigenschaftenraster, und klicken Sie auf **Löschen** zum Löschen der Datenbank. Die Verteilungsdatenbank kann nicht gelöscht werden, wenn es die einzige Datenbank dieser Art ist. Jeder Verteiler muss zumindest eine Verteilungsdatenbank besitzen. Zum Löschen aller Verteilungsdatenbanken müssen Sie die Verteilung auf dem Computer deaktivieren. Weitere Informationen finden Sie unter [Veröffentlichung und Verteilung deaktivieren](../../relational-databases/replication/disable-publishing-and-distribution.md).  
  
 **Profilstandards**  
 Klicken Sie, um Profile für den Replikations-Agent in der **Agentprofile** Dialogfeld. Weitere Informationen zu Profilen finden Sie unter [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## Siehe auch  
 [Konfigurieren der Verteilung](../../relational-databases/replication/configure-distribution.md)   
 [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  