---
title: Veröffentlichungseigenschaften, Veröffentlichungszugriffsliste | Microsoft-Dokumentation
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
- sql13.rep.newpubwizard.pubproperties.publicationaccesslist.f1
ms.assetid: 9587bb9e-c66c-4e70-8171-09b943ec2d50
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dc7bbd26736f9754a22d45eab41393f3a0284a03
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="publication-properties-publication-access-list"></a>Veröffentlichungseigenschaften, Veröffentlichungszugriffsliste
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Auf der Seite **Veröffentlichungszugriffsliste** im Dialogfeld **Veröffentlichungseigenschaften** können Sie Anmeldungen, Konten und Gruppen zur Veröffentlichungszugriffsliste (PAL) hinzufügen und aus ihr entfernen. Die PAL ist der primäre Mechanismus für die Sicherung der Verleger. Wenn Sie eine Veröffentlichung erstellen, wird von der Replikation eine PAL für diese Veröffentlichung erstellt. Die PAL, deren Funktionen denen einer [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Zugriffskontrollliste ähneln, enthält eine Liste von Anmeldungen, Konten und Gruppen, denen die Berechtigung zum Zugriff auf die Veröffentlichung erteilt wurde.  
  
 Wenn ein Abonnent eine Verbindung mit dem Verleger oder Verteiler herstellt und den Zugriff auf eine Veröffentlichung anfordert, wird die Anmeldung des Abonnenten mit den Authentifizierungsinformationen in der PAL verglichen. Dadurch wird zusätzliche Sicherheit für den Verleger erreicht, da die Anmeldung bei Verleger und Verteiler vor einer Verwendung durch ein Clienttool geschützt ist, das direkt beim Verleger Änderungen ausführen könnte. Weitere Informationen finden Sie unter [Sichern des Verlegers](../../relational-databases/replication/security/secure-the-publisher.md).  
  
## <a name="options"></a>Tastatur  
 **Hinzufügen**  
 Fügen Sie der Liste einen neuen Eintrag hinzu. Nur Benutzer-, Konto- und Gruppennamen, die bereits sowohl auf dem Verleger als auch dem Verteiler definiert sind, können hinzugefügt werden. Sie sind auf beiden Servern definiert, wenn Domänenkonten verwendet werden oder lokale Konten auf beiden Servern erstellt wurden.  
  
 **Entfernen**  
 Entfernen Sie den ausgewählten Eintrag aus der Liste.  
  
 **Alle entfernen**  
 Entfernen Sie alle Einträge aus der Liste.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
