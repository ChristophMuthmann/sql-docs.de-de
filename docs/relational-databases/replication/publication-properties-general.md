---
title: Veröffentlichungseigenschaften (Allgemein) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
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
- sql13.rep.newpubwizard.pubproperties.general.f1
ms.assetid: 7912362f-c4d6-4f60-bd39-dee1f656ed18
caps.latest.revision: 25
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 75cec882089e5bd485f8004871c27abe3a4311f2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="publication-properties-general"></a>Veröffentlichungseigenschaften (Allgemein)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Auf der Seite **Allgemein** des Dialogfelds **Veröffentlichungseigenschaften** sind grundlegende Informationen wie Name, Beschreibung und Abonnementablaufrichtlinie der Veröffentlichung enthalten  
  
## <a name="options"></a>Tastatur  
 **Name**  
 Der Name der Veröffentlichung (schreibgeschützt).  
  
 **Datenbank**  
 Der Name der Veröffentlichungsdatenbank (schreibgeschützt).  
  
 **Beschreibung**  
 Die Beschreibung der Veröffentlichung.  
  
 **Typ**  
 Der Typ der Veröffentlichung (schreibgeschützt).  
  
 **Abonnementablauf**  
 Wählen Sie eine der Optionen für Abonnementablauf aus: **Abonnements laufen nie ab** oder **Abonnements laufen ab**, und geben Sie einen expliziten Zeitraum an (**Intervall**).  
  
 Bei Momentaufnahme- und Transaktionsveröffentlichungen empfiehlt [!INCLUDE[msCoName](../../includes/msconame-md.md)] , die Standardeinstellung **Abonnements laufen nie ab**zu übernehmen.  
  
 Bei Mergereplikationen empfiehlt [!INCLUDE[msCoName](../../includes/msconame-md.md)] , die Standardeinstellung **Abonnements laufen ab** zu übernehmen und einen möglichst niedrigen Wert für **Intervall**festzulegen. Je länger der Ablaufzeitraum des Abonnements ist, desto mehr Metadaten werden auch gespeichert, was sich nachteilig auf die Leistung auswirken kann. Wägen Sie die Notwendigkeit, die Verbindung mit Abonnenten zu trennen oder diese über einen längeren Zeitraum nicht zu synchronisieren, gegen die Leistungsprobleme ab, die das Speichern und Verarbeiten großer Datenmengen nach sich ziehen kann.  
  
 Weitere Informationen finden Sie unter [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 **Kompatibilitätsgrad**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höher; nur für Mergeveröffentlichungen. Wählen Sie die niedrigste [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Version aus, die für Abonnenten, die mit dieser Veröffentlichung synchronisiert werden, erforderlich ist. Für die Bestimmung des Kompatibilitätsgrades gibt es eine Reihe von Regeln.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
