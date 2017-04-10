---
title: "Komprimieren von Momentaufnahmedateien (SQL Server Management Studio) | Microsoft Docs"
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
  - "Momentaufnahmen [SQL Server-Replikation], komprimiert"
  - "Momentaufnahmereplikation [SQL Server], komprimierte Momentaufnahmen"
ms.assetid: 174ade3e-74a1-4e67-a6da-b874be3ff50f
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Komprimieren von Momentaufnahmedateien (SQL Server Management Studio)
  Gibt an, dass Dateien komprimiert werden sollen die **Snapshot** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### So komprimieren Sie Momentaufnahmedateien  
  
1.  Auf der **Snapshot** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld):  
  
    1.  Aktivieren Sie **Dateien im folgenden Ordner speichern**, und klicken Sie dann auf **Durchsuchen** , um ein Verzeichnis auszuwählen, oder geben Sie den Pfad zu dem Verzeichnis ein, in dem Sie die Momentaufnahmedateien speichern möchten.  
  
        > [!NOTE]  
        >  Der Momentaufnahme-Agent muss Schreibberechtigungen für das angegebene Verzeichnis und der Verteilungs-Agent oder Merge-Agent muss Leseberechtigungen besitzen. Wenn Pullabonnements verwendet werden, geben Sie ein freigegebenes Verzeichnis als ein Pfad universal naming Convention (UNC), wie z. B. \\\computername\snapshot. Weitere Informationen finden Sie unter [Sichern des Momentaufnahmeordners](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
    2.  Deaktivieren Sie **Dateien im Standardordner speichern** , es sei denn Momentaufnahmedateien müssen in beide Speicherorte geschrieben werden.  
  
        > [!NOTE]  
        >  Wenn dieses Kontrollkästchen aktiviert ist, werden die im Standardordner gespeicherten Dateien nicht komprimiert. Komprimierte Dateien können nur im alternativen im vorigen Schritt angegebenen Speicherort gespeichert werden.  
  
2.  Wählen Sie **Momentaufnahmedateien in diesem Ordner komprimieren**aus.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## Siehe auch  
 [Konfigurieren Sie Momentaufnahmeeigenschaften & #40. Replikationsprogrammierung mit Transact-SQL & #41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Komprimierte Momentaufnahmen](../../../relational-databases/replication/compressed-snapshots.md)   
 [Initialisieren eines Abonnements mit einer Momentaufnahme](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  