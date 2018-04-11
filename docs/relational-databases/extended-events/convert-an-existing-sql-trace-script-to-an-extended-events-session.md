---
title: Konvertieren eines vorhandenen SQL-Ablaufverfolgungsskripts in eine Sitzung für erweiterte Ereignisse | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: xevents
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Trace, convert script to extended events
- extended events [SQL Server], convert SQL Trace script
ms.assetid: 4c8f29e6-0a37-490f-88b3-33493871b3f9
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e863ae549ad388a3e10d6d0bfd667602ff2572d
ms.sourcegitcommit: 094c46e7fa6de44735ed0040c65a40ec3d951b75
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="convert-an-existing-sql-trace-script-to-an-extended-events-session"></a>Konvertieren eines vorhandenen SQL-Ablaufverfolgungsskripts in eine Sitzung für erweiterte Ereignisse
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Wenn Sie ein vorhandenes SQL-Ablaufverfolgungsskript haben, das Sie in eine Sitzung für erweiterte Ereignisse konvertieren möchten, können Sie die Vorgehensweisen in diesem Thema verwenden, um eine entsprechende Sitzung für erweiterte Ereignisse zu erstellen. Mit den Informationen in den Systemtabellen „trace_xe_action_map“ und „trace_xe_event_map“ können Sie die Informationen sammeln, die für die Konvertierung erforderlich sind.  
  
 Die Schritte umfassen Folgendes:  
  
1.  Führen Sie das vorhandene Skript aus, um eine SQL-Ablaufverfolgungssitzung zu erstellen, und rufen Sie dann die ID der Ablaufverfolgung ab.  
  
2.  Führen Sie eine Abfrage aus, die die Funktion „fn_trace_geteventinfo“ verwendet, um die entsprechenden Ereignisse in „Erweiterte Ereignisse“ und die Aktionen für die einzelnen Ereignisklassen der SQL-Ablaufverfolgung sowie ihre zugeordneten Spalten zu suchen.  
  
3.  Verwenden Sie die Funktion „fn_trace_getfilterinfo“, um die zu verwendenden Filter und die entsprechenden Aktionen für „Erweiterte Ereignisse“ aufzulisten.  
  
4.  Erstellen Sie mithilfe der entsprechenden Ereignisse, Aktionen und Prädikate (Filter) für erweiterte Ereignisse manuell eine Sitzung für erweiterte Ereignisse.  
  
## <a name="to-obtain-the-trace-id"></a>So rufen Sie die Ablaufverfolgungs-ID ab  
  
1.  Öffnen Sie das SQL-Ablaufverfolgungsskript im Abfrage-Editor, und führen Sie dann das Skript aus, um die Ablaufverfolgungssitzung zu erstellen. Die Ablaufverfolgungssitzung muss nicht ausgeführt werden, um diese Vorgehensweise auszuführen.  
  
2.  Rufen Sie die ID der Ablaufverfolgung ab. Verwenden Sie hierzu die folgende Abfrage:  
  
    ```  
    SELECT * FROM sys.traces;  
    GO  
    ```  
  
    > [!NOTE]  
    >  Die Ablaufverfolgungs-ID 1 gibt in der Regel die Standardablaufverfolgung an.  
  
## <a name="to-determine-the-extended-events-equivalents"></a>So bestimmen Sie die Entsprechungen für erweiterte Ereignisse  
  
1.  Führen Sie die folgende Abfrage aus, wobei *trace_id* auf den Wert der Ablaufverfolgungs-ID festgelegt wird, die Sie in der vorherigen Prozedur abgerufen haben, um die entsprechenden Ereignisse und Aktionen für „Erweiterte Ereignisse“ zu bestimmen.  
  
    > [!NOTE]  
    >  In diesem Beispiel wird die Ablaufverfolgungs-ID für die Standardablaufverfolgung (1) verwendet.  
  
    ```  
    USE MASTER;  
    GO  
    DECLARE @trace_id int;  
    SET @trace_id = 1;  
    SELECT DISTINCT el.eventid, em.package_name, em.xe_event_name AS 'event'  
       , el.columnid, ec.xe_action_name AS 'action'  
    FROM (sys.fn_trace_geteventinfo(@trace_id) AS el  
       LEFT OUTER JOIN sys.trace_xe_event_map AS em  
          ON el.eventid = em.trace_event_id)  
    LEFT OUTER JOIN sys.trace_xe_action_map AS ec  
       ON el.columnid = ec.trace_column_id  
    WHERE em.xe_event_name IS NOT NULL AND ec.xe_action_name IS NOT NULL;  
    ```  
  
     Die entsprechende Ereignis-ID für erweiterte Ereignisse, der Paketname, der Ereignisname, die Spalten-ID und der Aktionsname werden zurückgegeben. Diese Ausgabe verwenden Sie in der Vorgehensweise "So erstellen Sie die Sitzung für erweiterte Ereignisse" weiter unten in diesem Thema.  
  
     In einigen Fällen wird einem Ereignisdatenfeld, das standardmäßig im Ereignis für erweiterte Ereignisse enthalten ist, die gefilterte Spalte zugeordnet. Daher ist die Spalte "Extended_Events_action_name" NULL. Wenn dies auftritt, müssen Sie wie folgt vorgehen, zu bestimmen, welches Datenfeld der gefilterten Spalte entspricht:  
  
    1.  Identifizieren Sie für die Aktionen, die NULL zurückgeben, welche SQL-Ablaufverfolgungs-Ereignisklassen in dem Skript die gefilterte Spalten enthalten.  
  
         Möglicherweise haben Sie z.B. die Ereignisklasse „SP:StmtCompleted“ verwendet und einen Filter für den Namen der Ablaufverfolgungsspalte „Dauer“ (Ereignisklassen-ID 45 und Spalten-ID 13 der SQL-Ablaufverfolgung) angegeben. In diesem Fall wird der Aktionsname in den Abfrageergebnissen als NULL angezeigt.  
  
    2.  Suchen Sie für jede SQL-Ablaufverfolgungs-Ereignisklasse, die Sie im vorherigen Schritt identifiziert haben, den entsprechenden Namen des Ereignisses für erweiterte Ereignisse. (Wenn Sie sich bzgl. des entsprechenden Ereignisnamens unsicher sind, verwenden Sie die Abfrage aus dem Thema [Anzeigen der Entsprechungen von erweiterten Ereignissen für SQL-Ablaufverfolgungsklassen](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md).)  
  
    3.  Verwenden Sie die folgende Abfrage, um die richtigen Datenfelder zu identifizieren, die für die Ereignisse verwendet werden sollen, die Sie im vorherigen Schritt identifiziert haben. Die Abfrage zeigt die Datenfelder für erweiterte Ereignisse in der "event_field"-Spalte an. Ersetzen Sie in der Abfrage *<Ereignisname>* durch den Namen eines Ereignisses, das Sie im vorherigen Schritt angegeben haben.  
  
        ```  
        SELECT xp.name package_name, xe.name event_name  
           ,xc.name event_field, xc.description  
        FROM sys.trace_xe_event_map AS em  
        INNER JOIN sys.dm_xe_objects AS xe  
           ON em.xe_event_name = xe.name  
        INNER JOIN sys.dm_xe_packages AS xp  
           ON xe.package_guid = xp.guid AND em.package_name = xp.name  
        INNER JOIN sys.dm_xe_object_columns AS xc  
           ON xe.name = xc.object_name  
        WHERE xe.object_type = 'event' AND xc.column_type <> 'readonly'  
           AND em.xe_event_name = '<event_name>';  
        ```  
  
         Beispielsweise ist die Ereignisklasse „SP:StmtCompleted“ dem erweiterten Ereignis „sp_statement_completed“ zugeordnet. Wenn Sie „sp_statement_completed“ in der Abfrage als Ereignisnamen angeben, werden in der Spalte „event_field“ die Felder angezeigt, die standardmäßig in dem Ereignis enthalten sind. Wenn Sie sich die Felder ansehen, werden Sie sehen, dass es ein Feld "duration" gibt. Um den Filter in der entsprechenden Sitzung für erweiterte Ereignisse zu erstellen, würden Sie ein Prädikat, z. B. "WHERE duration > 0" hinzufügen. Ein Beispiel finden Sie in der Vorgehensweise "So erstellen Sie die Sitzung für erweiterte Ereignisse" weiter unten in diesem Thema.  
  
## <a name="to-create-the-extended-events-session"></a>So erstellen Sie die Sitzung für erweiterte Ereignisse  
 Verwenden Sie den Abfrage-Editor, um die Sitzung für erweiterte Ereignisse zu erstellen und die Ausgabe in eine Dateiziel zu schreiben. Die folgenden Schritte beschreiben eine einzelne Abfrage, mit Erklärungen, um Ihnen zu zeigen, wie die Abfrage erstellt wird. Die vollständige Beispielabfrage finden Sie im Abschnitt "Beispiel" dieses Themas.  
  
1.  Fügen Sie Anweisungen hinzu, um die Ereignissitzung zu erstellen, und ersetzten Sie*Sitzungsname* durch den Namen, den Sie für die Sitzung für erweiterte Ereignisse verwenden möchten.  
  
    ```  
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='session_name')  
       DROP EVENT SESSION [Session_Name] ON SERVER;  
    CREATE EVENT SESSION [Session_Name]  
    ON SERVER;  
    ```  
  
2.  Fügen Sie die Ereignisse und Aktionen für erweiterte Ereignisse hinzu, die in der Vorgehensweise "So bestimmen Sie die Entsprechungen für erweiterte Ereignisse" als Ausgabe zurückgegeben wurden, und fügen Sie die Prädikate (Filter) hinzu, die Sie in der Vorgehensweise "So bestimmen Sie die Filter, die im Skript verwendet werden" identifiziert haben.  
  
     Im folgenden Beispiel wird ein SQL-Ablaufverfolgungsskript, das die Ereignisklassen „SQL:StmtStarting“ und „SP:StmtCompleted“ einschließt, mit Filtern für die Sitzungs-ID und die Dauer verwendet. Die Beispielausgabe für die Abfrage in der Vorgehensweise "So bestimmen Sie die Entsprechungen für erweiterte Ereignisse" gab das folgende Resultset zurück:  
  
    ```  
    Eventid  package_name  event                   columnid  action  
    44       sqlserver     sp_statement_starting   6         nt_username  
    44       sqlserver     sp_statement_starting   9         client_pid  
    44       sqlserver     sp_statement_starting   10        client_app_name  
    44       sqlserver     sp_statement_starting   11        server_principal_name  
    44       sqlserver     sp_statement_starting   12        session_id  
    45       sqlserver     sp_statement_completed  6         nt_username  
    45       sqlserver     sp_statement_completed  9         client_pid  
    45       sqlserver     sp_statement_completed  10        client_app_name  
    45       sqlserver     sp_statement_completed  11        server_principal_name  
    45       sqlserver     sp_statement_completed  12        session_id  
    ```  
  
     Die Ereignisse „sqlserver.sp_statement_starting“ und „sqlserver.sp_statement_completed“ werden mit einer Liste von Aktionen hinzugefügt, um dies in die Entsprechung für erweiterte Ereignisse konvertieren. Prädikatanweisungen sind als WHERE-Klauseln eingeschlossen.  
  
    ```  
    ADD EVENT sqlserver.sp_statement_starting  
       (ACTION  
          (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
          )  
       WHERE sqlserver.session_id = 59   
       ),  
  
    ADD EVENT sqlserver.sp_statement_completed  
       (ACTION  
          (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
          )  
       WHERE sqlserver.session_id = 59 AND duration > 0  
       )  
    ```  
  
3.  Fügen Sie das asynchrone Dateiziel hinzu, und ersetzen Sie dabei die Dateipfade durch den Speicherort, an dem Sie die Ausgabe speichern möchten. Wenn Sie das Dateiziel angeben, müssen Sie einen Dateipfad für die Protokolldatei sowie die Metadatendatei angeben.  
  
    ```  
    ADD TARGET package0.asynchronous_file_target(  
       SET filename='c:\temp\ExtendedEventsStoredProcs.xel', metadatafile='c:\temp\ExtendedEventsStoredProcs.xem');  
    ```  
  
## <a name="to-view-the-results"></a>So zeigen Sie die Ergebnisse an  
  
1.  Sie können die Funktion „sys.fn_xe_file_target_read_file“ verwenden, um die Ausgabe anzuzeigen. Führen Sie hierzu die folgende Abfrage aus, und ersetzen Sie dabei die Dateipfade durch die angegebenen Pfade:  
  
    ```  
    SELECT *, CAST(event_data as XML) AS 'event_data_XML'  
    FROM sys.fn_xe_file_target_read_file('c:\temp\ExtendedEventsStoredProcs*.xel', 'c:\temp\ExtendedEventsStoredProcs*.xem', NULL, NULL);  
  
    ```  
  
    > [!NOTE]  
    >  Die Umwandlung der Ereignisdaten in XML ist optional.  
  
     Weitere Informationen über die Funktion „sys.fn_xe_file_target_read_file“ finden Sie unter [sys.fn_xe_file_target_read_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md).  
  
    ```  
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='session_name')  
       DROP EVENT SESSION [session_name] ON SERVER;  
    CREATE EVENT SESSION [session_name]  
    ON SERVER  
  
    ADD EVENT sqlserver.sp_statement_starting  
       (ACTION  
       (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
       )  
       WHERE sqlserver.session_id = 59   
       ),  
  
    ADD EVENT sqlserver.sp_statement_completed  
       (ACTION  
       (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
       )  
       WHERE sqlserver.session_id = 59 AND duration > 0  
       );  
  
    ADD TARGET package0.asynchronous_file_target  
       (SET filename='c:\temp\ExtendedEventsStoredProcs.xel', metadatafile='c:\temp\ExtendedEventsStoredProcs.xem');  
    ```  
  
## <a name="example"></a>Beispiel  
  
```  
IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='session_name')  
   DROP EVENT SESSION [session_name] ON SERVER;  
CREATE EVENT SESSION [session_name]  
ON SERVER  
  
ADD EVENT sqlserver.sp_statement_starting  
   (ACTION  
   (  
      sqlserver.nt_username,  
      sqlserver.client_pid,  
      sqlserver.client_app_name,  
      sqlserver.server_principal_name,  
      sqlserver.session_id  
   )  
   WHERE sqlserver.session_id = 59   
   ),  
  
ADD EVENT sqlserver.sp_statement_completed  
   (ACTION  
   (  
      sqlserver.nt_username,  
      sqlserver.client_pid,  
      sqlserver.client_app_name,  
      sqlserver.server_principal_name,  
      sqlserver.session_id  
   )  
   WHERE sqlserver.session_id = 59 AND duration > 0  
   )  
  
ADD TARGET package0.asynchronous_file_target  
   (SET filename='c:\temp\ExtendedEventsStoredProcs.xel', metadatafile='c:\temp\ExtendedEventsStoredProcs.xem');  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Anzeigen der Entsprechungen von erweiterten Ereignissen für SQL-Ablaufverfolgungsklassen](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)  
  
  
