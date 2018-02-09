---
title: "Gewähren von Gastberechtigungen für einen Webservercomputer | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- guest privileges in RDS [ADO]
ms.assetid: e851a22d-01bc-4eb0-bc42-92b8f65d1c63
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4c9e1f3dace4916b7d8044a5b21f480bacb04238
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="granting-guest-privileges-to-a-web-server-computer"></a>Gewähren von Gastberechtigungen für eine Web-Server-Computer
Das anonyme Konto der Web-Server (IUSR_*ComputerName*) muss zur lokalen Gruppe Gäste auf dem Webservercomputer RDS verwendet hinzugefügt werden  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
### <a name="to-grant-guest-privileges-to-a-web-server-computer"></a>Gastberechtigungen auf einem Web-Server-Computer zu gewähren.  
  
1.  Klicken Sie auf dem Microsoft Windows 2000 Server-Computer auf **starten**, zeigen Sie auf **Programme**, zeigen Sie auf **Verwaltung**, und klicken Sie dann auf **Computer Management**.  
  
2.  In der Konsolenstruktur in **lokale Benutzer und Gruppen**, klicken Sie auf **Gruppen**.  
  
3.  Wählen Sie die **Gäste** lokalen Gruppe ". Aus der **Aktion** Menü wählen **Eigenschaften**.  
  
4.  In der **Gäste Eigenschaften** (Dialogfeld), klicken Sie auf **hinzufügen**.  
  
5.  Wenn das anonyme Konto der Web-Server nicht in der Liste angezeigt wird der **Benutzer oder Gruppen auswählen** Dialogfeld Feld, geben Sie seinen Namen (IUSR_*ComputerName*) in das leere Feld unten ein, und klicken Sie dann auf **hinzufügen** .  
  
6.  Klicken Sie auf **OK**.


