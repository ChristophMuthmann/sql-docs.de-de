---
title: "Anzeigen von Filterinformationen (SQL Server Profiler) | Microsoft Docs"
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
  - "Anzeigen von Filterinformationen"
  - "Filter [SQL Server], anzeigen"
  - "Filter [SQL Server], Ablaufverfolgungen"
  - "Ablaufverfolgungen [SQL Server], Filter"
  - "Anzeigen von Filterinformationen"
ms.assetid: 8d002dea-376a-452c-b3ca-3e93656ed75f
caps.latest.revision: 23
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 23
---
# Anzeigen von Filterinformationen (SQL Server Profiler)
  In diesem Thema wird beschrieben, wie Filter von Datenspalten für Ereignisklassen mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]angezeigt werden können.  
  
### So zeigen Sie Filterinformationen an  
  
1.  Öffnen Sie eine Ablaufverfolgungsdatei, eine Ablaufverfolgungstabelle oder ein SQL-Skript, und klicken Sie im Menü **Datei** auf **Eigenschaften**. Wenn Sie eine Ablaufverfolgungsvorlage bearbeiten oder eine neue Ablaufverfolgung erstellen, können Sie diesen Schritt auslassen.  
  
2.  Klicken Sie auf der Registerkarte **Ereignisauswahl** mit der rechten Maustaste auf den Namen der Datenspalte für den anzuzeigenden Filter, und klicken Sie dann auf **Spaltenfilter bearbeiten**.  
  
3.  Erweitern Sie im Dialogfeld **Filter bearbeiten** die Vergleichsoperatoren für den Filter, um den zugewiesenen Wert für das angegebene Kriterium anzuzeigen. Wiederholen Sie Schritt 2 und 3 für alle Spalten, für die Sie Filterinformationen anzeigen möchten.  
  
> [!NOTE]  
>  Vergleichsoperatoren mit zugewiesenen Werten sind fett formatiert.  
  
## Siehe auch  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  