---
title: Veröffentlichungseigenschaften (Datenpartitionen) | Microsoft-Dokumentation
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
- sql13.rep.newpubwizard.pubproperties.datapartitions.f1
ms.assetid: 5869edb7-d05f-495b-b828-b7fd5e828d20
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: be93a22a7dc0410f78c86774bd6ca59ca5dda4fa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="publication-properties-data-partitions"></a>Veröffentlichungseigenschaften (Datenpartitionen)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Mithilfe der Seite **Datenpartitionen** des Dialogfelds **Veröffentlichungseigenschaften** können Sie Datenpartitionen für Mergeveröffentlichungen mit parametrisierter Filterung definieren. Nach dem Definieren von Partitionen können Sie Momentaufnahmen für diese Partitionen generieren und verschiedenen Abonnenten auf der Grundlage ihrer Verbindungseigenschaften (Anmelde- und Computername) verschiedene Anfangsdatasets zur Verfügung stellen. Sie können es Abonnenten auch ermöglichen, die Übermittlung und das Generieren von Momentaufnahmen anzufordern, wenn für ihre Partition zum Zeitpunkt der ersten Synchronisierung keine Momentaufnahme verfügbar ist. Weitere Informationen finden Sie unter [Erstellen einer Momentaufnahme für eine Mergeveröffentlichung mit parametrisierten Filtern](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## <a name="options"></a>Tastatur  
 **Hinzufügen**  
 Klicken Sie auf **Hinzufügen** , um eine Partition zu definieren. Geben Sie im Dialogfeld **Datenpartition hinzufügen** Werte für **HOST_NAME()** und/oder **SUSER_SNAME()**an, und definieren Sie einen Zeitplan zum Aktualisieren von Momentaufnahmen.  
  
 **Bearbeiten**  
 Wählen Sie im Raster eine vorhandene Partition aus, und klicken Sie auf **Bearbeiten** , um die Partition zu bearbeiten.  
  
 **Delete**  
 Wählen Sie im Raster eine vorhandene Partition aus, und klicken Sie auf **Löschen** , um die Partition zu löschen.  
  
 **Die ausgewählten Momentaufnahmen jetzt generieren**  
 Wählen Sie im Raster eine oder mehrere Partitionen aus, und klicken Sie auf **Die ausgewählten Momentaufnahmen jetzt generieren** , um Momentaufnahmen für diese Partitionen zu generieren.  
  
 **Cleanup der vorhandenen Momentaufnahmen durchführen**  
 Wählen Sie im Raster eine oder mehrere Partitionen aus, und klicken Sie auf **Cleanup der vorhandenen Momentaufnahmen durchführen** , um einen Cleanup der Momentaufnahmen für diese Partitionen durchzuführen.  
  
 **Bei Bedarf automatisch eine Partition definieren und eine Momentaufnahme generieren, wenn ein neuer Abonnent zu synchronisieren versucht**  
 Wählen Sie diese Option aus, wenn Sie es Abonnenten ermöglichen möchten, das Generieren und die Anwendung von Momentaufnahmen anzufordern. Abonnenten benötigen diese Option möglicherweise, wenn zum Zeitpunkt der ersten Synchronisierung keine Momentaufnahme für ihre Partition verfügbar ist.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Momentaufnahmen für Mergeveröffentlichungen mit parametrisierten Filtern](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
