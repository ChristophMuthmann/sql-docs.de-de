---
title: "&#220;berwachen der Datentr&#228;gerverwendung | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datenbanküberwachung [SQL Server], Datenträgerverwendung"
  - "Datenträger [SQL Server]"
  - "Überwachen der Leistung [SQL Server], Datenträgerverwendung"
  - "Serverleistung [SQL Server], Datenträgerverwendung"
  - "Überwachung [SQL Server], Datenträgeraktivität"
  - "Häufiges Auslagern [SQL Server]"
  - "Optimieren von Datenbanken [SQL Server], Datenträgerverwendung"
  - "E/A [SQL Server], überwachen"
  - "Datenträger [SQL Server], Überwachen der Aktivität"
  - "Isolieren der Datenträgeraktivität [SQL Server]"
  - "Datenbankleistung [SQL Server], Datenträgerverwendung"
  - "Überwachen der Serverleistung [SQL Server], Datenträgerverwendung"
ms.assetid: 1525449c-ea7d-4222-b294-1ba1fe99c9ac
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# &#220;berwachen der Datentr&#228;gerverwendung
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet Aufrufe für die Microsoft Windows-Betriebssystemeingabe/-ausgabe, um Lese- und Schreibvorgänge auf dem Datenträger auszuführen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwaltet wann und wie Datenträger-E/A ausgeführt wird, aber das Windows-Betriebssystem führt die zugrunde liegenden E/A-Vorgänge aus. Das E/A-Teilsystem umfasst Systembus, Datenträgercontrollerkarten, Datenträger, Bandlaufwerke, CD-ROM-Laufwerk und zahlreiche andere E/A-Geräte. Datenträger-E/A ist häufig die Ursache von Engpässen in einem System.  
  
 Die Überwachung der Datenträgeraktivitäten ist auf zwei Bereiche konzentriert:  
  
-   Überwachen der Datenträger-E/A und Erkennen von zu häufigem Auslagern  
  
-   Isolieren der Datenträgeraktivitäten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 Weitere Informationen finden Sie unter [Überwachen der Datenträgernutzung](http://social.technet.microsoft.com/wiki/contents/articles/monitoring-disk-usage.aspx)  
  
  