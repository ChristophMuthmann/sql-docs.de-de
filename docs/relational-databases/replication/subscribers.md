---
title: "Abonnenten | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.subscribers.f1"
helpviewer_keywords: 
  - "Abonnenten [SQL Server-Replikation]"
ms.assetid: 43fb2454-c220-4d25-a826-83c332eb00d2
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# Abonnenten
  Geben Sie die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten, die ein Abonnement für die ausgewählte Veröffentlichung erhalten.  
  
## Optionen  
 **Abonnenten**  
 Aktivieren Sie das Kontrollkästchen im Raster an, aktivieren Sie das entsprechende [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenquelle als Abonnent für die Veröffentlichung ausgewählt werden, auf die **Veröffentlichung** Seite. Wenn der Abonnent nicht aufgeführt ist, klicken Sie auf **-Abonnenten hinzufügen** oder **SQL Server-Abonnenten hinzufügen**.  
  
 **Abonnementdatenbank**  
 Die Informationen im angezeigten und Aktionen in dieser Spalte hängt vom Typ des Abonnenten, die gemäß den **Abonnenten** Spalte:  
  
-   Für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten, wählen Sie eine Abonnementdatenbank aus der **Abonnementdatenbank** auflisten oder Erstellen einer neuen Datenbank durch Auswählen der **neue Datenbank** derselben Liste den Befehl.  
  
    > [!NOTE]  
    >  Wenn Sie den Verleger als einen Abonnenten aktivieren, darf die Abonnementdatenbank nicht mit der Veröffentlichungsdatenbank identisch sein.  
  
-   Bei Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten wird die Abonnementdatenbank nicht angezeigt. Geben Sie in der Datenbank zusammen mit anderen Informationen zur Verbindung der **Datenquellenname** Feld der **nicht-SQL-Server hinzufügen** Dialogfeld. Dieses Dialogfeld ist verfügbar, indem Sie auf **-Abonnenten hinzufügen** klicken und dann auf **nicht-SQL Server-Abonnenten hinzufügen**.  
  
 **Abonnent hinzufügen**  
 Fügen Sie einen Server zur Liste der Server hinzu, die als Abonnenten aktiviert werden können. Diese Schaltfläche wird angezeigt, wenn alle der folgenden Bedingungen erfüllt sind:  
  
-   Die von Ihnen ausgewählte Veröffentlichung ist eine Momentaufnahme- oder Transaktionsveröffentlichung, die keine Updateabonnements unterstützt.  
  
    > [!NOTE]  
    >  Wenn die Veröffentlichung, die Sie abonnieren, über [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnements verfügt und die Veröffentlichung für Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnenten noch nicht aktiviert ist, können Sie kein Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abonnement hinzufügen.  
  
-   Das Abonnement ist ein Pushabonnement.  
  
-   Der Verleger für die ausgewählte Veröffentlichung ist [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oder höher.  
  
 Auf **-Abonnenten hinzufügen** wird ein Menü mit zwei Optionen: **SQL Server-Abonnenten hinzufügen** und **nicht-SQL Server-Abonnenten hinzufügen**. Klicken Sie auf **nicht-SQL Server-Abonnenten hinzufügen** einen Oracle- oder IBM DB2-Abonnenten hinzufügen.  
  
 **SQL Server-Abonnenten hinzufügen**  
 Fügen Sie einen Server zur Liste der Server hinzu, die als Abonnenten aktiviert werden können. Diese Schaltfläche wird angezeigt, wenn eine oder mehrere der folgenden Bedingungen zutreffen:  
  
-   Die von Ihnen ausgewählte Veröffentlichung ist eine Mergeveröffentlichung oder eine Momentaufnahme- oder Transaktionsveröffentlichung, die Updateabonnements unterstützt.  
  
-   Das Abonnement ist ein Pullabonnement.  
  
-   Als Verleger für die ausgewählte Veröffentlichung wird eine Version vor [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] verwendet. Bei früheren Versionen wird die Schaltfläche nur angezeigt, wenn eine oder mehrere der folgenden Bedingungen zutreffen:  
  
    -   Sie sind Mitglied der **Sysadmin** festen Serverrolle auf dem Verleger.  
  
    -   Auf der Abonnenten hinzugefügt wurde die **Abonnenten** auf der Seite der **Verlegereigenschaften** Dialogfeld.  
  
    -   Die Veröffentlichung lässt anonyme Abonnements zu.  
  
## Siehe auch  
 [Erstellen eines Pullabonnements](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Erstellen eines Pushabonnements](../../relational-databases/replication/create-a-push-subscription.md)   
 [Nicht-SQL Server-Abonnenten](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  