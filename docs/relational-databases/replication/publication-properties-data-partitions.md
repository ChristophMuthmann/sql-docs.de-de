---
title: "Ver&#246;ffentlichungseigenschaften (Datenpartitionen) | Microsoft Docs"
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
  - "sql13.rep.newpubwizard.pubproperties.datapartitions.f1"
ms.assetid: 5869edb7-d05f-495b-b828-b7fd5e828d20
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Ver&#246;ffentlichungseigenschaften (Datenpartitionen)
  Mithilfe der Seite **Datenpartitionen** des Dialogfelds **Veröffentlichungseigenschaften** können Sie Datenpartitionen für Mergeveröffentlichungen mit parametrisierter Filterung definieren. Nach dem Definieren von Partitionen können Sie Momentaufnahmen für diese Partitionen generieren und verschiedenen Abonnenten auf der Grundlage ihrer Verbindungseigenschaften (Anmelde- und Computername) verschiedene Anfangsdatasets zur Verfügung stellen. Sie können es Abonnenten auch ermöglichen, die Übermittlung und das Generieren von Momentaufnahmen anzufordern, wenn für ihre Partition zum Zeitpunkt der ersten Synchronisierung keine Momentaufnahme verfügbar ist. Weitere Informationen finden Sie unter [Create a Snapshot for a Merge Publication with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## Optionen  
 **Hinzufügen**  
 Klicken Sie auf **Hinzufügen** eine Partition definieren. In der **Datenpartition hinzufügen** Dialogfeld geben Werte für **HOST_NAME()** und/oder **SUSER_SNAME()**, und definieren Sie einen Zeitplan zum Aktualisieren von Momentaufnahmen.  
  
 **Bearbeiten**  
 Wählen Sie im Raster eine vorhandene Partition aus, und klicken Sie auf **Bearbeiten** um die Partition zu bearbeiten.  
  
 **Delete**  
 Wählen Sie im Raster eine vorhandene Partition aus, und klicken Sie auf **Löschen** um die Partition zu löschen.  
  
 **Die ausgewählten Momentaufnahmen jetzt generieren**  
 Wählen Sie eine oder mehrere Partitionen im Raster, und klicken Sie auf **die ausgewählten Momentaufnahmen jetzt generieren** Momentaufnahmen für diese Partitionen zu generieren.  
  
 **Cleanup der vorhandenen Momentaufnahmen durchführen**  
 Wählen Sie eine oder mehrere Partitionen im Raster, und klicken Sie auf **Cleanup der vorhandenen Momentaufnahmen** um Momentaufnahmen für diese Partitionen zu bereinigen.  
  
 **Bei Bedarf automatisch eine Partition definieren und eine Momentaufnahme generieren, wenn ein neuer Abonnent zu synchronisieren versucht**  
 Wählen Sie diese Option aus, wenn Sie es Abonnenten ermöglichen möchten, das Generieren und die Anwendung von Momentaufnahmen anzufordern. Abonnenten benötigen diese Option möglicherweise, wenn zum Zeitpunkt der ersten Synchronisierung keine Momentaufnahme für ihre Partition verfügbar ist.  
  
## Siehe auch  
 [Erstellen einer Veröffentlichung](../../relational-databases/replication/publish/create-a-publication.md)   
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Parametrisierte Zeilenfilter](../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Momentaufnahmen für Mergeveröffentlichungen mit parametrisierten Filtern](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  