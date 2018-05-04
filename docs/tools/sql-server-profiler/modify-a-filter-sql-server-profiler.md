---
title: Ändern ein Filters (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: profiler
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], modifying
- modifying filters, modifying
- filters [SQL Server], traces
ms.assetid: 8b317813-4918-4485-b930-77b1951aa00c
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2bc42acf774fb9f9b25147998a604e9afa7565eb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="modify-a-filter-sql-server-profiler"></a>Ändern eines Filters (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Sie können Ablaufverfolgungsvorlagen, die Ablaufverfolgungsdefinitionen enthalten, Filter hinzufügen, um die Anzahl der von einer Ablaufverfolgung gesammelten Ereignisse zu beschränken. Durch die Beschränkung der gesammelten Ereignisse können die bei der Ablaufverfolgung entstehenden Leistungseinbußen reduziert werden. Wenn Sie Filter für eine Ablaufverfolgungsvorlage einrichten und feststellen, dass bei der Ablaufverfolgung nicht die von Ihnen benötigten Informationen gesammelt werden, können Sie den Filter bearbeiten.  
  
### <a name="to-modify-a-filter"></a>So ändern Sie einen Filter  
  
1.  Öffnen Sie in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]die Vorlage für den Ablaufverfolgungsfilter, den Sie ändern möchten. Klicken Sie im Menü **Datei** auf **Vorlagen**, und wählen Sie dann **Vorlage bearbeiten**aus.  
  
2.  Wählen Sie auf der Registerkarte **Allgemein** des Dialogfelds **Eigenschaften der Ablaufverfolgungsvorlage** eine Vorlage aus der Liste **Vorlagennamen auswählen** aus.  
  
3.  Klicken Sie auf die Registerkarte **Ereignisauswahl** .  
  
     Die Registerkarte **Ereignisauswahl** enthält ein Rastersteuerelement. Bei dem Rastersteuerelement handelt es sich um eine Tabelle, die alle bei der Ablaufverfolgung zu berücksichtigenden Ereignisklassen enthält. Die Tabelle enthält für jede Ereignisklasse eine Zeile. Abhängig von dem Typ und der Version des Servers, zu dem eine Verbindung hergestellt wurde, können sich die Ereignisklassen geringfügig unterscheiden. Die Ereignisklassen werden in der Spalte **Events**des Rasters identifiziert und nach Ereigniskategorie gruppiert. In den übrigen Spalten sind die Datenspalten aufgeführt, die für jede Ereignisklasse zurückgegeben werden können.  
  
4.  Klicken Sie auf **Spaltenfilter**.  
  
5.  Klicken Sie im Dialogfeld **Filter bearbeiten** auf den Wert neben dem zu bearbeitenden Vergleichsoperator, und geben Sie einen neuen Wert ein bzw. löschen Sie einen Wert. Darüber hinaus können Sie zusätzliche Filter hinzufügen.  
  
6.  Klicken Sie auf **OK** , und speichern Sie die Vorlage.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
