---
title: 'Tutorial: Replizieren von Daten mit mobilen Clients | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: af673514-30c7-403a-9d18-d01e1a095115
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8a11cf12fc057aba0f014fc36014fde9a52eda2a
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="tutorial-replicating-data-with-mobile-clients"></a>Lernprogramm: Replizieren von Daten mit mobilen Clients
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Die Replikation stellt eine geeignete Lösung für das Problem des Verschiebens von Daten zwischen einem zentralen Server und mobilen Clients dar, die nur gelegentlich miteinander verbunden sind. Mithilfe von Replikations-Assistenten können Sie eine Replikationstopologie auf einfache Weise konfigurieren und verwalten. In diesem Lernprogramm wird die Konfiguration einer Replikationstopologie für mobile Clients erläutert.  
  
## <a name="what-you-will-learn"></a>Lernziele  
In diesem Lernprogramm werden mithilfe einer Mergereplikation Daten aus einer zentralen Datenbank für einen oder für mehrere mobile Benutzer veröffentlicht, sodass jeder Benutzer eine eindeutig gefilterte Teilmenge von Daten erhält. In der ersten Lektion wird die Verwendung von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] zum Erstellen einer Veröffentlichung erläutert. In darauf folgenden Lektionen wird erläutert, wie ein Abonnement erstellt und synchronisiert wird.  
  
## <a name="requirements"></a>Anforderungen  
Dieses Lernprogramm ist für Benutzer vorgesehen, die mit grundlegenden Datenbankvorgängen vertraut sind, aber nur über begrenzte Kenntnisse in Bezug auf die Replikation verfügen. Bevor Sie dieses Tutorial starten, müssen Sie das [Tutorial: Vorbereiten des Servers für die Replikation](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)abschließen.  
  
Ihr System muss die folgenden installierten Komponenten aufweisen, damit dieses Lernprogramm verwendet werden kann:  
  
-   Auf dem Verlegerserver (Quelle):  
  
    -   Eine beliebige Edition von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]mit Ausnahme von Express ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) und [!INCLUDE[ssEW](../../includes/ssew-md.md)]. Diese Editionen können nicht als Replikationsverleger fungieren.  
  
    -   Die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Beispieldatenbank Aus Sicherheitsgründen werden die Beispieldatenbanken standardmäßig nicht installiert.  
  
-   Abonnentenserver (Ziel):  
  
    -   Eine beliebige Edition von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]mit Ausnahme von [!INCLUDE[ssEW](../../includes/ssew-md.md)]. [!INCLUDE[ssEW](../../includes/ssew-md.md)] wird nicht von der in diesem Lernprogramm erstellten Veröffentlichung unterstützt.  
  
    > [!NOTE]  
    > Die Replikation wird bei [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]nicht standardmäßig installiert.  
  
> [!NOTE]  
> In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]muss eine Verbindung mit dem Verleger und dem Abonnenten hergestellt werden. Dazu wird ein Anmeldename verwendet, der Mitglied der festen Serverrolle sysadmin ist.  
  
**Geschätzte Zeit zum Bearbeiten dieses Lernprogramms: 30 Minuten**  
  
## <a name="lessons-in-this-tutorial"></a>Lektionen in diesem Lernprogramm  
  
-   [Lektion 1: Veröffentlichen von Daten mithilfe der Mergereplikation](../../relational-databases/replication/lesson-1-publishing-data-using-merge-replication.md)  
  
-   [Lektion 2: Erstellen eines Abonnements für die Mergeveröffentlichung](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-merge-publication.md)  
  
[Lernprogramm starten](../../relational-databases/replication/lesson-1-publishing-data-using-merge-replication.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Konzepte für die Replikationsprogrammierung](../../relational-databases/replication/concepts/replication-programming-concepts.md)  
  
  
  
