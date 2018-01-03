---
title: "Ändern ein Filters (SQL Server Profiler) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filters [SQL Server], modifying
- modifying filters, modifying
- filters [SQL Server], traces
ms.assetid: 8b317813-4918-4485-b930-77b1951aa00c
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7d8d48e66b041d09dbcbbe47ec7702656e250bdf
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="modify-a-filter-sql-server-profiler"></a>Ändern eines Filters (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Sie hinzufügen können ablaufverfolgungsvorlagen, die Ablaufverfolgungsdefinitionen, um die Anzahl der Ereignisse zu beschränken, die von einer Ablaufverfolgung gesammelten enthalten Filter. Durch die Beschränkung der gesammelten Ereignisse können die bei der Ablaufverfolgung entstehenden Leistungseinbußen reduziert werden. Wenn Sie Filter für eine Ablaufverfolgungsvorlage einrichten und feststellen, dass bei der Ablaufverfolgung nicht die von Ihnen benötigten Informationen gesammelt werden, können Sie den Filter bearbeiten.  
  
### <a name="to-modify-a-filter"></a>So ändern Sie einen Filter  
  
1.  Öffnen Sie in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]die Vorlage für den Ablaufverfolgungsfilter, den Sie ändern möchten. Klicken Sie im Menü **Datei** auf **Vorlagen**, und wählen Sie dann **Vorlage bearbeiten**aus.  
  
2.  Wählen Sie auf der Registerkarte **Allgemein** des Dialogfelds **Eigenschaften der Ablaufverfolgungsvorlage** eine Vorlage aus der Liste **Vorlagennamen auswählen** aus.  
  
3.  Klicken Sie auf die Registerkarte **Ereignisauswahl** .  
  
     Die Registerkarte **Ereignisauswahl** enthält ein Rastersteuerelement. Bei dem Rastersteuerelement handelt es sich um eine Tabelle, die alle bei der Ablaufverfolgung zu berücksichtigenden Ereignisklassen enthält. Die Tabelle enthält für jede Ereignisklasse eine Zeile. Abhängig von dem Typ und der Version des Servers, zu dem eine Verbindung hergestellt wurde, können sich die Ereignisklassen geringfügig unterscheiden. Die Ereignisklassen werden in der Spalte **Events**des Rasters identifiziert und nach Ereigniskategorie gruppiert. In den übrigen Spalten sind die Datenspalten aufgeführt, die für jede Ereignisklasse zurückgegeben werden können.  
  
4.  Klicken Sie auf **Spaltenfilter**.  
  
5.  Klicken Sie im Dialogfeld **Filter bearbeiten** auf den Wert neben dem zu bearbeitenden Vergleichsoperator, und geben Sie einen neuen Wert ein bzw. löschen Sie einen Wert. Darüber hinaus können Sie zusätzliche Filter hinzufügen.  
  
6.  Klicken Sie auf **OK** , und speichern Sie die Vorlage.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
