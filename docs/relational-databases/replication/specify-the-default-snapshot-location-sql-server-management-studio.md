---
title: "Angeben des standardm&#228;&#223;igen Momentaufnahmespeicherorts (SQL Server Management Studio) | Microsoft Docs"
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
  - "Momentaufnahmen [SQL Server-Replikation], Standardspeicherorte"
  - "Standard-Momentaufnahmespeicherorte"
ms.assetid: 27c5d9ad-a915-4c59-a8b7-82e3af61ac4d
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Angeben des standardm&#228;&#223;igen Momentaufnahmespeicherorts (SQL Server Management Studio)
  Geben Sie den standardmäßigen Momentaufnahmespeicherort im Verteilungskonfigurations-Assistenten auf der Seite **Snapshotordner** an. Weitere Informationen zum Verwenden dieses Assistenten finden Sie unter [Verleger- und Verteilereigenschaften](../../relational-databases/replication/configure-publishing-and-distribution.md). Wenn Sie eine Veröffentlichung auf einem Server erstellen, der nicht als Verteiler konfiguriert ist, geben Sie im Assistenten für neue Veröffentlichung auf der Seite **Momentaufnahmeordner** einen standardmäßigen Momentaufnahmespeicherort an. Weitere Informationen zum Verwenden dieses Assistenten finden Sie unter [Erstellen einer Publikation](../../relational-databases/replication/publish/create-a-publication.md).  
  
 Ändern Sie den standardmäßigen Snapshotspeicherort auf die **Herausgeber** auf der Seite der **Verteilereigenschaften - \< Verteiler>** (Dialogfeld). Weitere Informationen finden Sie unter [anzeigen und ändern, Verteiler und Verlegereigenschaften](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md). Legen Sie den Snapshotordner für jede Veröffentlichung in der **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen finden Sie unter [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### So ändern Sie den standardmäßigen Momentaufnahmespeicherort  
  
1.  Auf der **Herausgeber** auf der Seite der **Verteilereigenschaften - \< Verteiler>** Dialogfeld klicken Sie auf die Eigenschaftenschaltfläche (**...**) für den Verleger, für die Sie den Standard-Snapshotspeicherort ändern möchten.  
  
2.  In der **Verlegereigenschaften - \< Publisher>** Dialogfeld Geben Sie einen Wert für die **Standardmomentaufnahmeordner** Eigenschaft.  
  
    > [!NOTE]  
    >  Der Momentaufnahme-Agent muss Schreibberechtigungen für das angegebene Verzeichnis und der Verteilungs-Agent oder Merge-Agent muss Leseberechtigungen besitzen. Wenn Pullabonnements verwendet werden, geben Sie ein freigegebenes Verzeichnis als ein Pfad universal naming Convention (UNC), wie z. B. \\\computername\snapshot. Weitere Informationen finden Sie unter [Sichern des Momentaufnahmeordners](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Siehe auch  
 [Alternative Speicherorte für Momentaufnahmeordner](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Initialisieren eines Abonnements mit einer Momentaufnahme](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  