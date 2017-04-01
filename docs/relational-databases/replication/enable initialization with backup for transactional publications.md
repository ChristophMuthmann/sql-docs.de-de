---
title: "Aktivieren der Initialisierung von einer Sicherung f&#252;r Transaktionsver&#246;ffentlichungen (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Manuelle Abonnementinitialisierung [SQL Server-Replikation]"
  - "Abonnements [SQL Server-Replikation], initialisieren"
  - "Initialisieren von Abonnements [SQL Server-Replikation], ohne Momentaufnahmen"
  - "Transaktionsreplikation, Sicherung und Wiederherstellung"
  - "Sicherung [SQL Server-Replikation], Transaktionsreplikation"
ms.assetid: 9df00514-aa9d-4ac6-9766-d226c9958175
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Aktivieren der Initialisierung von einer Sicherung f&#252;r Transaktionsver&#246;ffentlichungen (SQL Server Management Studio)
  Wenn Sie ein Abonnement für eine Transaktionsveröffentlichung von einer Sicherung initialisieren möchten, aktivieren Sie die Veröffentlichung, um das Initialisieren von einer Sicherung zuzulassen. Geben Sie dann beim Erstellen des Abonnements die Sicherungsinformationen ein:  
  
-   Aktivieren Sie die Veröffentlichung auf der **Abonnementoptionen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
-   Geben Sie mit der gespeicherten Prozedur Sicherungsinformationen [Sp_addsubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Weitere Informationen zu den erforderlichen Parametern **Sp_addsubscription**, finden Sie unter [Initialisieren eines Transaktionsabonnements von einer Sicherung & #40; Replikationsprogrammierung mit Transact-SQL & #41;](../../relational-databases/replication/initialize a transactional subscription from a backup.md).  
  
### So aktivieren Sie die Initialisierung mit einer Sicherung  
  
1.  Auf der **Abonnementoptionen** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** Wert wählen Sie im Dialogfeld **True** für das **Initialisierung aus Sicherungsdateien zulassen** Option.  
  
## Siehe auch  
 [Initialisieren eines Transaktionsabonnements ohne Momentaufnahme](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  