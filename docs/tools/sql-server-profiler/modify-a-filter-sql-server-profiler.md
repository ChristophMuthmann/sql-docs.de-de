---
title: "&#196;ndern eines Filters (SQL Server Profiler) | Microsoft Docs"
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
  - "Filter [SQL Server], ändern"
  - "Ändern von Filtern, ändern"
  - "Filter [SQL Server], Ablaufverfolgungen"
ms.assetid: 8b317813-4918-4485-b930-77b1951aa00c
caps.latest.revision: 15
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 15
---
# &#196;ndern eines Filters (SQL Server Profiler)
  Sie können Ablaufverfolgungsvorlagen, die Ablaufverfolgungsdefinitionen enthalten, Filter hinzufügen, um die Anzahl der von einer Ablaufverfolgung gesammelten Ereignisse zu beschränken. Durch die Beschränkung der gesammelten Ereignisse können die bei der Ablaufverfolgung entstehenden Leistungseinbußen reduziert werden. Wenn Sie Filter für eine Ablaufverfolgungsvorlage einrichten und feststellen, dass bei der Ablaufverfolgung nicht die von Ihnen benötigten Informationen gesammelt werden, können Sie den Filter bearbeiten.  
  
### So ändern Sie einen Filter  
  
1.  Öffnen Sie in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]die Vorlage für den Ablaufverfolgungsfilter, den Sie ändern möchten. Klicken Sie im Menü **Datei** auf **Vorlagen**, und wählen Sie dann **Vorlage bearbeiten**aus.  
  
2.  Wählen Sie auf der Registerkarte **Allgemein** des Dialogfelds **Eigenschaften der Ablaufverfolgungsvorlage** eine Vorlage aus der Liste **Vorlagennamen auswählen** aus.  
  
3.  Klicken Sie auf die Registerkarte **Ereignisauswahl** .  
  
     Die Registerkarte **Ereignisauswahl** enthält ein Rastersteuerelement. Bei dem Rastersteuerelement handelt es sich um eine Tabelle, die alle bei der Ablaufverfolgung zu berücksichtigenden Ereignisklassen enthält. Die Tabelle enthält für jede Ereignisklasse eine Zeile. Abhängig von dem Typ und der Version des Servers, zu dem eine Verbindung hergestellt wurde, können sich die Ereignisklassen geringfügig unterscheiden. Die Ereignisklassen werden in der Spalte **Events**des Rasters identifiziert und nach Ereigniskategorie gruppiert. In den übrigen Spalten sind die Datenspalten aufgeführt, die für jede Ereignisklasse zurückgegeben werden können.  
  
4.  Klicken Sie auf **Spaltenfilter**.  
  
5.  Klicken Sie im Dialogfeld **Filter bearbeiten** auf den Wert neben dem zu bearbeitenden Vergleichsoperator, und geben Sie einen neuen Wert ein bzw. löschen Sie einen Wert. Darüber hinaus können Sie zusätzliche Filter hinzufügen.  
  
6.  Klicken Sie auf **OK** , und speichern Sie die Vorlage.  
  
## Siehe auch  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  