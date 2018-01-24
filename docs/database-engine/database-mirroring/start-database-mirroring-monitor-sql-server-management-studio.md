---
title: Starten des Datenbankspiegelungs-Monitors (SQL Server Management Studio) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-mirroring
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- monitoring database mirroring [SQL Server]
- Database Mirroring Monitor [SQL Server], starting
- database mirroring [SQL Server], monitoring
ms.assetid: 53165335-97ca-4f88-8e78-22f1839dee98
caps.latest.revision: "20"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 31a23c34c9a568c560f8c09b4abb7548094a083c
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="start-database-mirroring-monitor-sql-server-management-studio"></a>Starten des Datenbankspiegelungs-Monitors (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Der Datenbankspiegelungs-Monitor ist Teil des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Monitors, der aus [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] gestartet wird.  
  
> [!NOTE]  
>  Der Datenbankspiegelungs-Monitor ist nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
### <a name="to-launch-the-database-mirroring-monitor"></a>So starten Sie den Datenbankspiegelungs-Monitor  
  
1.  Nachdem Sie eine Verbindung mit der Prinzipalserverinstanz hergestellt haben, klicken Sie im Objekt-Explorer auf den Servernamen, um die Serverstruktur zu erweitern.  
  
2.  Erweitern Sie **Datenbanken**, und wählen Sie die zu überwachende Datenbank aus.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Datenbank, wählen Sie **Tasks**aus, und klicken Sie dann auf **Datenbankspiegelungs-Monitor starten**.  
  
4.  Klicken Sie im Dialogfeld **Datenbankspiegelungs-Monitor** auf **Gespiegelte Datenbank registrieren** , um eine oder mehrere gespiegelte Datenbanken zu registrieren.  
  
    > [!NOTE]  
    >  Wenn Sie eine Datenbank bei einem der Partner registrieren, wird sie automatisch auch bei dem anderen Partner registriert. Wenn der Monitor bereits über Verbindungsanmeldeinformationen für die andere Partnerinstanz verfügt, werden diese für die Herstellung der Verbindung verwendet. Andernfalls versucht der Monitor, die Verbindung mithilfe der Windows-Authentifizierung herzustellen. Wenn Sie für das Herstellen der Verbindung mit einer der Serverinstanzen andere Anmeldeinformationen verwenden möchten, klicken Sie auf **Beim Klicken auf 'OK' das Dialogfeld 'Serververbindungen verwalten' anzeigen**.  
  
 Weitere Informationen zur Datenbankspiegelung finden Sie unter [Datenbankspiegelungs-Monitor (Übersicht)](../../database-engine/database-mirroring/database-mirroring-monitor-overview.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Einrichten einer Datenbank-Spiegelungssitzung mithilfe der Windows-Authentifizierung &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
  
