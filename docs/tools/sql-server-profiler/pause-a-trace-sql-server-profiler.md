---
title: "Anhalten einer Ablaufverfolgung (SQL Server Profiler) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Anhalten von Ablaufverfolgungen"
  - "Temporäres Stoppen von Ablaufverfolgungen"
  - "Ablaufverfolgungen [SQL Server], anhalten"
  - "Beenden von Ablaufverfolgungen"
ms.assetid: 432b9b0c-b5e7-47f3-a71b-310fb3bf2445
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# Anhalten einer Ablaufverfolgung (SQL Server Profiler)
  Durch Anhalten einer Ablaufverfolgung wird verhindert, dass weitere Ereignisdaten vor dem Neustarten der Ablaufverfolgung aufgezeichnet werden.  
  
 Durch Anhalten einer Ablaufverfolgung wird verhindert, dass Ereignisdaten vor dem Neustarten der Ablaufverfolgung aufgezeichnet werden. Durch das Neustarten einer Ablaufverfolgung werden die Ablaufverfolgungsvorgänge fortgesetzt. Zuvor aufgezeichnete Daten gehen nach einem Neustart nicht verloren. Wird die Ablaufverfolgung neu gestartet, wird die Aufzeichnung der Daten von diesem Punkt an fortgesetzt. Während eine Ablaufverfolgung angehalten wird, können Sie den Namen, Ereignisse, Spalten und Filter ändern. Es ist allerdings nicht möglich, die Ziele, an die Sie die Ablaufverfolgungsdaten senden, oder die Serververbindung zu ändern.  
  
### So halten Sie eine Ablaufverfolgung an  
  
1.  Wählen Sie ein Fenster aus, das eine derzeit ausgeführte Ablaufverfolgung enthält.  
  
2.  Klicken Sie im Menü **Datei** auf **Ablaufverfolgung anhalten**.  
  
## Siehe auch  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  