---
title: "Aktivieren eines Remoteverlegers auf einem Verteiler (SQL Server Management Studio) | Microsoft Docs"
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
  - "Remoteverteiler [SQL Server-Replikation]"
  - "Verleger [SQL Server-Replikation]"
ms.assetid: 6f8e2831-5c45-4e39-8e51-d37e2813cf3d
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# Aktivieren eines Remoteverlegers auf einem Verteiler (SQL Server Management Studio)
  Auf der Seite **Verleger** können Sie aktivieren, dass ein Verleger einen Remoteverteiler verwendet. Diese Seite ist verfügbar in den Verteilungskonfigurations-Assistenten und die **Verteilereigenschaften - \< Verteiler>** (Dialogfeld). Weitere Informationen zum Verwenden des Assistenten sowie Zugriff auf das Dialogfeld finden Sie unter [Verleger- und Verteilereigenschaften](../../relational-databases/replication/configure-publishing-and-distribution.md) und [anzeigen und ändern, Verteiler und Verlegereigenschaften](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
### So aktivieren Sie einen Verleger im Verteilungskonfigurations-Assistenten  
  
1.  Klicken Sie im Verteilungskonfigurations-Assistenten auf der Seite **Verleger** auf **Hinzufügen**.  
  
2.  Klicken Sie auf **SQL Server-Verleger hinzufügen**. Informationen zum Aktivieren der Verwendung eines Verteilers auf einem Oracle-Verleger finden Sie unter [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
3.  Geben Sie im Dialogfeld **Verbindung mit Server herstellen** die Verbindungsinformationen für den Verleger an, der den Remoteverteiler verwenden soll, und klicken Sie anschließend auf **Verbinden**.  
  
4.  Auf der **Verteilerkennwort** auf der Seite der **Kennwort** und **Kennwort bestätigen** Textfelder, geben Sie ein sicheres Kennwort für das **Distributor_admin** Konto, das die Replikation verwendet wird, für die Verbindung vom Verleger zum Verteiler, administrative Aufgaben durchzuführen.  
  
5.  Klicken Sie zum Anzeigen und ändern Sie die Einstellungen für einen Verleger, auf die Eigenschaftenschaltfläche (**...**).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### So aktivieren Sie einen Verleger im Dialogfeld "Verteilereigenschaften"  
  
1.  Auf der **Herausgeber** auf der Seite der **Verteilereigenschaften - \< Verteiler>** im Dialogfeld klicken Sie auf **Hinzufügen**.  
  
2.  Klicken Sie auf **SQL Server-Verleger hinzufügen**. Informationen zum Aktivieren der Verwendung eines Verteilers auf einem Oracle-Verleger finden Sie unter [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
3.  Geben Sie im Dialogfeld **Verbindung mit Server herstellen** die Verbindungsinformationen für den Verleger an, der den Remoteverteiler verwenden soll, und klicken Sie anschließend auf **Verbinden**.  
  
4.  Auf der **Herausgeber** auf der Seite der **Kennwort** und **Kennwort bestätigen** Textfelder, geben Sie ein sicheres Kennwort für das **Distributor_admin** Konto, das die Replikation verwendet wird, für die Verbindung vom Verleger zum Verteiler, administrative Aufgaben durchzuführen.  
  
5.  Klicken Sie zum Anzeigen und ändern Sie die Einstellungen für einen Verleger, auf die Eigenschaftenschaltfläche (**...**).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Siehe auch  
 [Konfigurieren der Veröffentlichung und der Verteilung](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Konfigurieren der Verteilung](../../relational-databases/replication/configure-distribution.md)   
 [Schützen des Verteilers](../../relational-databases/replication/security/secure-the-distributor.md)  
  
  