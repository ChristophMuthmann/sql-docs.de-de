---
title: "&#196;ndern einer Ablaufverfolgungsvorlage (SQL Server Profiler) | Microsoft Docs"
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
  - "Vorlagen [SQL Server], Ablaufverfolgungen"
  - "Ablaufverfolgungsvorlagen [SQL Server]"
  - "Ändern von Ablaufverfolgungen"
ms.assetid: b81df2a1-e202-43d8-92b0-0beb145f0116
caps.latest.revision: 26
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 26
---
# &#196;ndern einer Ablaufverfolgungsvorlage (SQL Server Profiler)
  In diesem Thema wird beschrieben, wie mit [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]eine Ablaufverfolgungsvorlage geändert wird.  
  
### So ändern Sie eine Ablaufverfolgungsvorlage  
  
1.  Zeigen Sie im Menü **Datei** auf **Vorlagen**, und klicken Sie dann auf **Vorlage bearbeiten**.  
  
2.  Im Dialogfeld **Eigenschaften der Ablaufverfolgungsvorlage** können Sie auf der Registerkarte **Allgemein** den Servertyp und den Vorlagennamen ändern oder eine Standardvorlage für den Servertyp auswählen.  
  
3.  Zeigen Sie im Menü **Ereignisauswahl**können Sie mit dem Rastersteuerelement Ereignisse und Datenspalten in der Ablaufverfolgungsdatei wie folgt hinzufügen oder entfernen.  
  
    -   Um ein Ereignis hinzuzufügen, erweitern Sie die entsprechende Ereigniskategorie in der **Ereignisse** -Spalte und wählen dann den Ereignisnamen aus.  
  
    -   Wenn Sie ein Ereignis hinzufügen, werden standardmäßig alle relevanten Datenspalten eingeschlossen. Um eine Datenspalte für ein Ereignis aus einer Ablaufverfolgung zu entfernen, deaktivieren Sie das Kontrollkästchen in der Datenspalte für das Ereignis.  
  
    -   Um Filter hinzuzufügen, klicken Sie auf den Namen der Datenspalte, und geben Sie die Filterkriterien im Dialogfeld **Filter bearbeiten** an. Sie können auch mit der rechten Maustaste auf den Namen der Datenspalte klicken und anschließend auf **Spaltenfilter bearbeiten** klicken, um das Dialogfeld **Filter bearbeiten** zu öffnen. Klicken Sie auf **OK** , um den Filter hinzuzufügen.  
  
4.  Klicken Sie auf **Speichern**, oder klicken Sie auf **Speichern As**, um die Ablaufverfolgungsvorlage unter einem anderen Namen zu speichern.  
  
## Siehe auch  
 [Angeben von Ereignissen und Datenspalten für eine Ablaufverfolgungsdatei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [Ableiten einer Vorlage von einer zurzeit ausgeführten Ablaufverfolgung &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [Ableiten einer Vorlage von einer Ablaufverfolgungsdatei oder Ablaufverfolgungstabelle &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [Vorlagen und Berechtigungen in SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  