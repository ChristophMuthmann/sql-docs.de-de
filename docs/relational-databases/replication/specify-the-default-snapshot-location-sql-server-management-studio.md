---
title: "Angeben des standardmäßigen Momentaufnahmespeicherorts (SQL Server Management Studio) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], default locations
- default snapshot locations
ms.assetid: 27c5d9ad-a915-4c59-a8b7-82e3af61ac4d
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0053c565a3edf4253fcfd93b75f63e9130b69ab5
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="specify-the-default-snapshot-location-sql-server-management-studio"></a>Angeben des standardmäßigen Momentaufnahmespeicherorts (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Geben Sie den standardmäßigen Momentaufnahmespeicherort im Verteilungskonfigurations-Assistenten auf der Seite **Snapshotordner** an. Weitere Informationen zum Verwenden dieses Assistenten finden Sie unter [Konfigurieren der Veröffentlichung und der Verteilung](../../relational-databases/replication/configure-publishing-and-distribution.md). Wenn Sie eine Veröffentlichung auf einem Server erstellen, der nicht als Verteiler konfiguriert ist, geben Sie im Assistenten für neue Veröffentlichung auf der Seite **Momentaufnahmeordner** einen standardmäßigen Momentaufnahmespeicherort an. Weitere Informationen zum Zugreifen auf diesen Assistenten finden Sie unter [Erstellen einer Veröffentlichung](../../relational-databases/replication/publish/create-a-publication.md).  
  
 Ändern Sie den standardmäßigen Momentaufnahmespeicherort im Dialogfeld **Verteilereigenschaften - \<Distributor>** auf der Seite **Verleger**. Weitere Informationen finden Sie unter [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md). Bestimmen Sie den Momentaufnahmeordner für die einzelnen Veröffentlichungen im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>**. Weitere Informationen finden Sie unter [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### <a name="to-modify-the-default-snapshot-location"></a>So ändern Sie den standardmäßigen Momentaufnahmespeicherort  
  
1.  Klicken Sie auf der Seite **Verleger** des Dialogfelds **Verteilereigenschaften - \<Distributor>** auf die Schaltfläche mit den drei Punkten (**…**) für den Verleger, dessen standardmäßiger Momentaufnahmespeicherort geändert werden soll.  
  
2.  Geben Sie im Dialogfeld **Verlegereigenschaften - \<Publisher>** einen Wert für die Eigenschaft **Standardmomentaufnahmeordner** ein.  
  
    > [!NOTE]  
    >  Der Momentaufnahme-Agent muss Schreibberechtigungen für das angegebene Verzeichnis und der Verteilungs-Agent oder Merge-Agent muss Leseberechtigungen besitzen. Bei Verwendung von Pullabonnements müssen Sie ein freigegebenes Verzeichnis als UNC-Pfad angeben, wie z.B. \\\Computername\Momentaufnahme. Weitere Informationen finden Sie unter [Schützen des Momentaufnahmeordners](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Alternative Speicherorte für Momentaufnahmeordner](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Initialisieren eines Abonnements mit einer Momentaufnahme](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
