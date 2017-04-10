---
title: "Angeben eines alternativen Speicherortes f&#252;r den Momentaufnahmeordner (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Momentaufnahmen [SQL Server-Replikation], alternative Ordner"
  - "Momentaufnahmereplikation [SQL Server], alternative Ordner"
  - "Alternative Momentaufnahmeordner [SQL Server-Replikation]"
ms.assetid: 9293f0eb-5531-47ec-b6e2-0392823ce5cc
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# Angeben eines alternativen Speicherortes f&#252;r den Momentaufnahmeordner (SQL Server Management Studio)
  Geben Sie einen alternativen Speicherort für Snapshots auf die **Snapshot** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### So geben Sie einen alternativen Momentaufnahmespeicherort an  
  
1.  Auf der **Snapshot** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld):  
  
    1.  Aktivieren Sie **Dateien im folgenden Ordner speichern**, und klicken Sie dann auf **Durchsuchen** , um ein Verzeichnis auszuwählen, oder geben Sie den Pfad zu dem Verzeichnis ein, in dem Sie die Momentaufnahmedateien speichern möchten.  
  
        > [!NOTE]  
        >  Der Momentaufnahme-Agent muss Schreibberechtigungen für das angegebene Verzeichnis und der Verteilungs-Agent oder Merge-Agent muss Leseberechtigungen besitzen. Wenn Pullabonnements verwendet werden, geben Sie ein freigegebenes Verzeichnis als ein Pfad universal naming Convention (UNC), wie z. B. \\\computername\snapshot. Weitere Informationen finden Sie unter [Sichern des Momentaufnahmeordners](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
    2.  Deaktivieren Sie **Dateien im Standardordner speichern** , es sei denn Momentaufnahmedateien müssen in beide Speicherorte geschrieben werden.  
  
     Zum Komprimieren von Momentaufnahmedateien aktivieren Sie **Momentaufnahmedateien in diesem Ordner komprimieren**. Die Komprimierung wird in der Regel für Verbindungen mit niedriger Bandbreite und für alternative Momentaufnahmespeicherorte auf Wechselmedien verwendet, z. B. einer CD-ROM.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## Siehe auch  
 [Alternative Speicherorte für Momentaufnahmeordner](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Konfigurieren Sie Momentaufnahmeeigenschaften & #40. Replikationsprogrammierung mit Transact-SQL & #41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Geben Sie den Standard-Snapshotspeicherort & #40. SQL Server Management Studio & #41;](../../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)   
 [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Initialisieren eines Abonnements mit einer Momentaufnahme](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  