---
title: "Ver&#246;ffentlichungseigenschaften (Allgemein) | Microsoft Docs"
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
  - "sql13.rep.newpubwizard.pubproperties.general.f1"
ms.assetid: 7912362f-c4d6-4f60-bd39-dee1f656ed18
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# Ver&#246;ffentlichungseigenschaften (Allgemein)
  Auf der Seite **Allgemein** des Dialogfelds **Veröffentlichungseigenschaften** sind grundlegende Informationen wie Name, Beschreibung und Abonnementablaufrichtlinie der Veröffentlichung enthalten  
  
## Optionen  
 **Name**  
 Der Name der Veröffentlichung (schreibgeschützt).  
  
 **Datenbank**  
 Der Name der Veröffentlichungsdatenbank (schreibgeschützt).  
  
 **Beschreibung**  
 Die Beschreibung der Veröffentlichung.  
  
 **Typ**  
 Der Typ der Veröffentlichung (schreibgeschützt).  
  
 **Abonnementablauf**  
 Wählen Sie eine der Optionen für Abonnementablauf: **Abonnements laufen nie ab** oder **Abonnementablauf**, durch einen expliziten Zeitraum (**Intervall**).  
  
 Bei Momentaufnahme- und Transaktionsveröffentlichungen empfiehlt [!INCLUDE[msCoName](../../includes/msconame-md.md)] , die Standardeinstellung **Abonnements laufen nie ab**zu übernehmen.  
  
 Bei Mergereplikationen empfiehlt [!INCLUDE[msCoName](../../includes/msconame-md.md)] , die Standardeinstellung **Abonnements laufen ab** zu übernehmen und einen möglichst niedrigen Wert für **Intervall**festzulegen. Je länger der Ablaufzeitraum des Abonnements ist, desto mehr Metadaten werden auch gespeichert, was sich nachteilig auf die Leistung auswirken kann. Wägen Sie die Notwendigkeit, die Verbindung mit Abonnenten zu trennen oder diese über einen längeren Zeitraum nicht zu synchronisieren, gegen die Leistungsprobleme ab, die das Speichern und Verarbeiten großer Datenmengen nach sich ziehen kann.  
  
 Weitere Informationen finden Sie unter [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 **Kompatibilitätsgrad**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höhere Versionen. nur mergeveröffentlichungen. Wählen Sie die niedrigste [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Version aus, die für Abonnenten, die mit dieser Veröffentlichung synchronisiert werden, erforderlich ist. Für die Bestimmung des Kompatibilitätsgrades gibt es eine Reihe von Regeln.  
  
## Siehe auch  
 [Erstellen einer Veröffentlichung](../../relational-databases/replication/publish/create-a-publication.md)   
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  