---
title: Organisieren von Spalten in einer Ablaufverfolgung (SQL Server Profiler) angezeigte | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- organizing trace columns displayed [SQL Server]
- arranging trace columns displayed
- traces [SQL Server], data columns
ms.assetid: 6b923f94-0eb1-467e-82f6-ceed43f77017
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5f1c097e900a9ed76bb5160ecab37238344d7a33
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="organize-columns-displayed-in-a-trace-sql-server-profiler"></a>Organisieren von in einer Ablaufverfolgung angezeigten Spalten (SQL Server Profiler)
  Sie können Datenspalten in einer Ablaufverfolgung gruppieren, indem Sie in der Ablaufverfolgungstabelle oder im Dialogfeld **Eigenschaften der Ablaufverfolgungsdatei** die Option **Spalten organisieren** auswählen oder wenn Sie eine Ablaufverfolgung definieren. Durch das Gruppieren der Datenspalten können Sie die [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] -Ablaufverfolgungsausgabe besser analysieren. Weitere Informationen finden Sie unter [Anzeigen und Analysieren von Ablaufverfolgungen mit SQL Server Profiler](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md).  
  
 **Spalten organisieren** ermöglicht Ihnen das Gruppieren der Ablaufverfolgungsereignisse oder das Gruppieren und Aggregieren dieser Ereignisse anhand der von Ihnen ausgewählten Datenspalten.  
  
-   Wählen Sie mehrere Datenspalten zum Gruppieren aus, um nur Ablaufverfolgungsereignisse zu gruppieren. Wenn Sie mehrere Datenspalten zum Gruppieren auswählen, zeigt das Ablaufverfolgungsfenster Ereignisse gruppiert nach den Werten in den Datenspalten an, die Sie zum Gruppieren ausgewählt haben. Das folgende Beispiel zeigt, wie das Raster für das Ablaufverfolgungsfenster aussieht, wenn Sie die Datenspalten **Duration** und **StartTime** zum Gruppieren auswählen. Beachten Sie, dass die Werte der **Duration** -Spalte in aufsteigender Reihenfolge angezeigt werden, gefolgt von den **StartTime** -Werten.  
  
|Duration|StartTime|EventClass|ClientProcessID|  
|--------------|---------------|----------------|---------------------|  
||12/12/2006 3:16:43 PM|SQL:StmtStarting|2124|  
|0|12/12/2006 5:39:23 PM|Audit Login|648|  
|1|12/12/2006 5:24:44 PM|SQL:StmtStarting|2124|  
|25|12/12/2006 5:24:44 PM|SQL:StmtCompleted|648|  
  
-   Wählen Sie nur eine Spalte zum Gruppieren aus, um Ablaufverfolgungsereignisse zu gruppieren und zu aggregieren. Wenn Sie nur eine Datenspalte zum Gruppieren auswählen, zeigt das Ablaufverfolgungsfenster Ereignisse gruppiert nach den Werten in dieser Datenspalte an, und alle Ereignisse darunter werden reduziert. Ein Pluszeichen (**+**) wird links neben dem Ereignis in der zum Gruppieren ausgewählten Datenspalte angezeigt, und die Anzahl der darunter reduzierten Ereignisse wird in Klammern rechts neben dem Ereignis angezeigt. Das folgende Beispiel zeigt, wie das Raster für das Ablaufverfolgungsfenster aussieht, wenn Sie nur die **EventClass** -Datenspalte zum Gruppieren auswählen. Beachten Sie, dass alle Ereignisse unter der **EventClass** -Datenspalte organisiert sind. Klicken Sie zum Anzeigen aller Ereignisse auf das Pluszeichen, um alle Ereignisklassen dieses Typs zu erweitern und anzuzeigen.  
  
|EventClass|StartTime|Duration|ClientProcessID|  
|----------------|---------------|--------------|---------------------|  
|+ ExistingConnection (6)||||  
|+ SQL:BatchStarting (25)||||  
|+ SQL:StmtCompleted (11)||||  
|+ SQL:SmtStarting (21)||||  
  
### <a name="to-group-data-columns-displayed-in-a-trace"></a>So gruppieren Sie in einer Ablaufverfolgung angezeigte Datenspalten  
  
1.  Öffnen Sie eine vorhandene Ablaufverfolgungsdatei oder -tabelle.  
  
2.  Klicken Sie im Menü **Datei** auf **Eigenschaften**.  
  
3.  Klicken Sie im Dialogfeld **Eigenschaften der Ablaufverfolgungsdatei** oder **Eigenschaften der Ablaufverfolgungstabelle** auf die Registerkarte **Ereignisauswahl** .  
  
4.  Klicken Sie auf der Registerkarte **Ereignisauswahl** auf **Spalten organisieren**.  
  
5.  Wählen Sie im Dialogfeld **Spalten organisieren** die Spalten aus, die in einer Gruppe angezeigt werden sollen, und klicken Sie auf **Nach oben** , um sie in die Liste **Gruppen**zu verschieben. Wenn Sie alle gewünschten Spalten in die Liste **Gruppen**verschoben haben, können Sie die Schaltflächen **Nach oben** und **Nach unten** verwenden, um ihre Reihenfolge zu ändern.  
  
     Das Verschieben der Datenspaltennamen in die Liste **Gruppen** hat zur Folge, dass die angezeigte Ablaufverfolgung zunächst nach den Werten in der obersten Datenspalte in der Liste **Gruppen** organisiert wird, dann nach der zweiten Datenspalte in der Liste **Gruppen** usw.  
  
6.  Klicken Sie im Dialogfeld **Spalten organisieren** auf **OK** , und klicken Sie dann im Dialogfeld **Eigenschaften der Ablaufverfolgungstabelle** oder **Eigenschaften der Ablaufverfolgungsdatei** auf **OK** .  
  
     Nachdem Sie im Dialogfeld **Eigenschaften der Ablaufverfolgungstabelle** oder **Eigenschaften der Ablaufverfolgungsdatei** auf **OK** geklickt haben, werden die Datenspalten in der angezeigten Ablaufverfolgung neu organisiert. Die Datenspalte, die Sie an die oberste Position in der Liste **Gruppen** verschoben haben, befindet sich an erster Stelle in der Ablaufverfolgungsanzeige, wenn Sie das Raster von links nach rechts lesen. Die Zeilen in der Ablaufverfolgung sind in aufsteigender Reihenfolge nach den Werten organisiert, die in den Datenspalten enthalten sind, die Sie in die Liste **Gruppen** aufgenommen haben. Die zum Gruppieren ausgewählten Spalten bleiben fest in der Anzeige, Sie können jedoch einen Bildlauf nach rechts oder links durchführen, um die anderen Spalten anzuzeigen.  
  
7.  Klicken Sie zum Aufheben der Gruppierung der angezeigten Ablaufverfolgungsdaten im Menü **Ansicht** auf **Gruppierte Ansicht** , um die Auswahl aufzuheben. Wenn Sie zur gruppierten Ansicht zurückkehren möchten, klicken Sie im Menü **Ansicht** erneut auf **Gruppierte Ansicht** , um den Befehl wieder auszuwählen.  
  
### <a name="to-group-and-aggregate-data-columns-in-a-trace"></a>So gruppieren und aggregieren Sie Datenspalten in einer Ablaufverfolgung  
  
1.  Öffnen Sie eine vorhandene Ablaufverfolgungsdatei oder -tabelle.  
  
2.  Klicken Sie im Menü **Datei** auf **Eigenschaften**.  
  
3.  Klicken Sie im Dialogfeld **Eigenschaften der Ablaufverfolgungsdatei** oder **Eigenschaften der Ablaufverfolgungstabelle** auf die Registerkarte **Ereignisauswahl** .  
  
4.  Klicken Sie auf der Registerkarte **Ereignisauswahl** auf **Spalten organisieren**.  
  
5.  Wählen Sie im Dialogfeld **Spalten organisieren** eine Spalte aus, nach der die angezeigten Ablaufverfolgungsereignisse gruppiert und aggregiert werden sollen. Klicken Sie auf **Nach oben** , um den Spaltennamen in die Liste **Gruppen**zu verschieben. Sie können die Schaltflächen **Nach oben** und **Nach unten** verwenden, um die übrigen Spalten unter **Spalten** bei Bedarf neu anzuordnen.  
  
6.  Klicken Sie im Dialogfeld **Spalten organisieren** auf **OK** , und klicken Sie dann im Dialogfeld **Eigenschaften der Ablaufverfolgungstabelle** oder **Eigenschaften der Ablaufverfolgungsdatei** auf **OK** .  
  
     Nachdem Sie im Dialogfeld **Eigenschaften der Ablaufverfolgungstabelle** oder **Eigenschaften der Ablaufverfolgungsdatei** auf **OK** geklickt haben, werden die Datenspalten in der angezeigten Ablaufverfolgung neu organisiert. Alle anderen Datenspaltenereignisse werden unter der Datenspalte aggregiert, die Sie in die Liste **Gruppen** verschoben haben. Klicken Sie auf das Pluszeichen (**+**) links neben dem Ereignis in der für die Aggregation ausgewählten Datenspalte, um es zu erweitern und alle Ereignisse dieses Typs anzuzeigen. Die für die Aggregation ausgewählte Spalte bleibt fest in der Anzeige, Sie können jedoch einen Bildlauf nach rechts oder links durchführen, um die anderen Spalten anzuzeigen.  
  
7.  Um zu einer normalen Ansicht der Ablaufverfolgungsdaten zurückzukehren, klicken Sie im Menü **Ansicht** auf **Aggregierte Ansicht** , sodass die Auswahl aufgehoben wird. Wenn Sie zur aggregierten Ansicht zurückkehren möchten, klicken Sie im Menü **Ansicht** erneut auf **Aggregierte Ansicht** , um den Befehl wieder auszuwählen. Beachten Sie, dass Sie auch im Menü **Ansicht** auf **Gruppierte Ansicht** klicken können, um die gruppierten Ablaufverfolgungsereignisse anzuzeigen, ohne sie zu reduzieren.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einer Ablaufverfolgung &#40; SQL Server Profiler &#41;](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)   
 [Öffnen einer Ablaufverfolgungstabelle &#40; SQL Server Profiler &#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)   
 [Öffnen einer Ablaufverfolgungsdatei &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)  
  
  

