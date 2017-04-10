---
title: "Ausf&#252;hren von Skripts vor und nach dem Anwenden einer Momentaufnahme (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Momentaufnahmen [SQL Server-Replikation], Skripts"
  - "Skripts [SQL Server-Replikation], Momentaufnahmen"
  - "Momentaufnahmereplikation [SQL Server], Skripts"
ms.assetid: b7bb1e4c-5b48-4bb1-9dc8-47c911f2cc82
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Ausf&#252;hren von Skripts vor und nach dem Anwenden einer Momentaufnahme (SQL Server Management Studio)
  Geben Sie ein optionales Skript zum Ausführen vor oder nach dem Anwenden der Momentaufnahme auf die **Snapshot** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
> [!NOTE]  
>  Diese Optionen sind nur verfügbar wenn die **Momentaufnahmeformat** Option wird festgelegt, um **Zeichen**.  
  
### So führen Sie ein Skript vor und nach dem Anwenden einer Momentaufnahme aus  
  
1.  Auf der **Snapshot** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld):  
  
    -   Wenn Sie ein Skript angeben möchten, das vor dem Anwenden der Momentaufnahme ausgeführt werden soll, klicken Sie auf **Durchsuchen** , um zum entsprechenden Skript zu navigieren, oder geben Sie im Textfeld **Dieses Skript vor Anwenden der Momentaufnahme ausführen** den Pfad zum gewünschten Skript ein.  
  
        > [!NOTE]  
        >  Der Verteilungs-Agent bzw. Merge-Agent muss für das von Ihnen angegebene Verzeichnis Leseberechtigungen besitzen. Wenn Pullabonnements verwendet werden, geben Sie ein freigegebenes Verzeichnis als ein Pfad universal naming Convention (UNC), wie z. B. \\\computername\scripts\myscript.sql.  
  
    -   Wenn Sie ein Skript angeben möchten, das nach dem Anwenden der Momentaufnahme ausgeführt werden soll, klicken Sie auf **Durchsuchen** , um zum entsprechenden Skript zu navigieren, oder geben Sie im Textfeld **Dieses Skript nach Anwenden der Momentaufnahme ausführen** den UNC-Pfad zum gewünschten Skript ein.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Siehe auch  
 [Konfigurieren Sie Momentaufnahmeeigenschaften & #40. Replikationsprogrammierung mit Transact-SQL & #41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Ausführen von Skripts vor und nach dem Anwenden der Momentaufnahme](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [Initialisieren eines Abonnements mit einer Momentaufnahme](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  