---
title: "Starten des Datenbankspiegelungs-Monitors (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Überwachen der Datenbankspiegelung [SQL Server]"
  - "Datenbankspiegelungs-Monitor [SQL Server], starten"
  - "Datenbankspiegelung [SQL Server], Überwachung"
ms.assetid: 53165335-97ca-4f88-8e78-22f1839dee98
caps.latest.revision: 20
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 20
---
# Starten des Datenbankspiegelungs-Monitors (SQL Server Management Studio)
  Der Datenbankspiegelungs-Monitor ist Teil des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Monitors, der aus [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]gestartet wird.  
  
> [!NOTE]  
>  Der Datenbankspiegelungs-Monitor ist nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md).  
  
### So starten Sie den Datenbankspiegelungs-Monitor  
  
1.  Nachdem Sie eine Verbindung mit der Prinzipalserverinstanz hergestellt haben, klicken Sie im Objekt-Explorer auf den Servernamen, um die Serverstruktur zu erweitern.  
  
2.  Erweitern Sie **Datenbanken**, und wählen Sie die zu überwachende Datenbank aus.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Datenbank, wählen Sie **Tasks** aus, und klicken Sie dann auf **Datenbankspiegelungs-Monitor starten**.  
  
4.  Klicken Sie im Dialogfeld **Datenbankspiegelungs-Monitor** auf **Gespiegelte Datenbank registrieren** , um eine oder mehrere gespiegelte Datenbanken zu registrieren.  
  
    > [!NOTE]  
    >  Wenn Sie eine Datenbank bei einem der Partner registrieren, wird sie automatisch auch bei dem anderen Partner registriert. Wenn der Monitor bereits über Verbindungsanmeldeinformationen für die andere Partnerinstanz verfügt, werden diese für die Herstellung der Verbindung verwendet. Andernfalls versucht der Monitor, die Verbindung mithilfe der Windows-Authentifizierung herzustellen. Wenn Sie für das Herstellen der Verbindung mit einer der Serverinstanzen andere Anmeldeinformationen verwenden möchten, klicken Sie auf **Beim Klicken auf 'OK' das Dialogfeld 'Serververbindungen verwalten' anzeigen**.  
  
 Weitere Informationen zur Datenbankspiegelung finden Sie unter [Datenbankspiegelungs-Monitor (Übersicht)](../../database-engine/database-mirroring/database-mirroring-monitor-overview.md).  
  
## Siehe auch  
 [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Einrichten einer Datenbank-Spiegelungssitzung mithilfe der Windows-Authentifizierung &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish database mirroring session - windows authentication.md)  
  
  