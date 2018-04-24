---
title: Anzeigen der Entsprechungen von erweiterten Ereignissen für SQL-Ablaufverfolgungsklassen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: xevents
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Trace, extended events equivalents
- extended events [SQL Server], SQL Trace equivalents
- extended events [SQL Server], user configurable events
ms.assetid: 7f24104c-201d-4361-9759-f78a27936011
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 464dbbbd6d40516a7b54e8140694a01ce34ef799
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="view-the-extended-events-equivalents-to-sql-trace-event-classes"></a>Anzeigen der Entsprechungen von erweiterten Ereignissen für SQL-Ablaufverfolgungsklassen
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Wenn Sie Erweiterte Ereignisse verwenden möchten, um Ereignisdaten zu erfassen, die SQL-Ablaufverfolgungs-Ereignisklassen und Spalten entsprechen, müssen Sie verstehen, wie die SQL-Ablaufverfolgungsereignisse Ereignissen und Aktionen für erweiterte Ereignisse zugeordnet werden.  
  
 Gehen Sie folgendermaßen vor, um die Ereignisse und Aktionen für erweiterte Ereignisse anzuzeigen, die den einzelnen SQL-Ablaufverfolgungsereignissen und deren zugeordneten Spalten entsprechen.  
  
## <a name="to-view-the-extended-events-equivalents-to-sql-trace-events-using-query-editor"></a>So zeigen Sie die Entsprechungen der erweiterten Ereignisse für SQL-Ablaufverfolgungsereignisse mit dem Abfrage-Editor an  
  
-   Führen Sie im [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]-Abfrage-Editor die folgende Abfrage aus:  
  
    ```  
    USE MASTER;  
    GO  
    SELECT DISTINCT  
       tb.trace_event_id,  
       te.name AS 'Event Class',  
       em.package_name AS 'Package',  
       em.xe_event_name AS 'XEvent Name',  
       tb.trace_column_id,  
       tc.name AS 'SQL Trace Column',  
       am.xe_action_name as 'Extended Events action'  
    FROM (sys.trace_events te LEFT OUTER JOIN sys.trace_xe_event_map em  
       ON te.trace_event_id = em.trace_event_id) LEFT OUTER JOIN sys.trace_event_bindings tb  
       ON em.trace_event_id = tb.trace_event_id LEFT OUTER JOIN sys.trace_columns tc  
       ON tb.trace_column_id = tc.trace_column_id LEFT OUTER JOIN sys.trace_xe_action_map am  
       ON tc.trace_column_id = am.trace_column_id  
    ORDER BY te.name, tc.name  
    ```  
  
 Beachten Sie beim Anzeigen der Ergebnisse Folgendes:  
  
-   Wenn alle Spalten außer der Spalte zu Ereignisklassen NULL zurückgeben, deutet dies darauf hin, dass die Ereignisklasse nicht von der SQL-Ablaufverfolgung migriert wurde.  
  
-   Wenn nur der Wert in der Aktionsspalte zu erweiterten Ereignissen NULL ist, deutet dies darauf hin, dass eine der folgenden Bedingungen zutrifft:  
  
    -   Die SQL-Ablaufverfolgungsspalte ist einem der Datenfelder zugeordnet, das dem Ereignis für erweiterte Ereignisse zugeordnet ist.  
  
        > [!NOTE]  
        >  Jedes Ereignis für erweiterte Ereignisse verfügt über ein Standardsatz von Datenfeldern, die automatisch im Resultset enthalten sind.  
  
    -   Die Aktionsspalte hat keine sinnvolle Entsprechung in den erweiterten Ereignissen. Ein Beispiel dafür ist die Spalte zu Ereignisklassen in der SQL-Ablaufverfolgung. Diese Spalte wird nicht in den erweiterten Ereignissen benötigt, da der Ereignisname demselben Zweck dient.  
  
-   Für vom Benutzer konfigurierbare SQL-Ablaufverfolgungs-Ereignisklassen (UserConfigurable:1 bis UserConfigurable:9) verwenden die erweiterten Ereignisse ein einzelnes Ereignis, um diese zu ersetzen. Das Ereignis trägt den Namen „user_event“. Dieses Ereignis wird mit „sp_trace_generateevent“ ausgelöst, die gleiche gespeicherte Prozedur, die von der SQL-Ablaufverfolgung verwendet wird. Das Ereignis „user_event“ wird unabhängig davon zurückgegeben, welche Ereignis-ID an die gespeicherte Prozedur übergeben wird. Ein „event_id“-Feld wird jedoch als Teil der Ereignisdaten zurückgegeben. Sie können auf diese Weise ein Prädikat erstellen, das auf der Ereignis-ID basiert. Wenn Sie z. B. „UserConfigurable:0“ (Ereignis-ID = 82) im Code verwenden, können Sie der Sitzung das „user_event“-Ereignis hinzufügen, und das Prädikat „event_id = 82“ angeben. Daher müssen Sie den Code nicht ändern, da die gespeicherte Prozedur „sp_trace_generateevent“ das „user_event“-Ereignis für erweiterte Ereignisse und die entsprechende SQL-Ablaufverfolgungs-Ereignisklasse generiert.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)  
  
  
