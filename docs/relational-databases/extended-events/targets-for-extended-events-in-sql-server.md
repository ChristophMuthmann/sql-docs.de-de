---
title: "Ziele für erweiterte Ereignisse in SQL Server | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
- xevents
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 47c64144-4432-4778-93b5-00496749665b
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 66e1984acfa86bea31f2cedbea70dbac5195a090
ms.lasthandoff: 04/11/2017

---
# <a name="targets-for-extended-events-in-sql-server"></a>Ziele für erweiterte Ereignisse in SQL Server
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]


Dieser Artikel erläutert Zweck und Art der Verwendung von package0-Zielen für erweiterte Ereignisse in SQL Server. Der vorliegende Artikel erläutert für jedes Ziel:

- dessen Fähigkeiten im Sammeln und Melden der von Ereignissen gesendeten Daten
- dessen Parameter, es sei denn, der Parameter ist selbsterklärend


#### <a name="xquery-example"></a>XQuery-Beispiel


Der [ring_buffer-Abschnitt](#h2_target_ring_buffer) enthält ein Beispiel zur Verwendung von [XQuery in Transact-SQL](../../xquery/xquery-language-reference-sql-server.md) zum Kopieren einer XML-Zeichenfolge in ein relationales Rowset.


### <a name="prerequisites"></a>Erforderliche Komponenten


- Allgemeine Kenntnisse der Grundlagen von erweiterten Ereignissen, wie in [Schnellstart: Erweiterte Ereignisse in SQL Server](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)beschrieben.


- Vorhandene Installation einer neueren Version des häufig aktualisierten Hilfsprogramms SQL Server Management Studio (SSMS.exe). Einzelheiten dazu finden Sie unter:
    - [Herunterladen von SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)


- In SSMS.exe sollte die Verwendung des **Objekt-Explorers** bekannt sein, um mit der rechten Maustaste auf den Zielknoten für die Ereignissitzung zu klicken, um die [bequeme Anzeige der Ausgabedaten](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)zu erreichen.
    - Die Ereignisdaten werden als XML-Zeichenfolge erfasst. Hingegen werden die Daten in diesem Artikel als relationale Zeilen angezeigt. SSMS wurde zum Anzeigen der Daten verwendet, daraus wurden sie kopiert und in diesen Artikel eingefügt.
    - Die alternative T-SQL-Technik zum Generieren von Rowsets aus XML wird im [ring_buffer-Abschnitt](#h2_target_ring_buffer)erläutert. Sie umfasst den Einsatz von XQuery.



## <a name="parameters-actions-and-fields"></a>Parameter, Aktionen und Felder


In Transact-SQL spielt die Anweisung [CREATE EVENT SESSION](~/t-sql/statements/create-event-session-transact-sql.md) die zentrale Rolle bei erweiterten Ereignissen. Zum Erstellen der Anweisung benötigen Sie in vielen Fällen eine Liste und eine Beschreibung folgender Punkte:

- die dem ausgewählten Ereignis zugeordneten Felder
- die dem ausgewählten Ziel zugeordneten Parameter

SELECT-Anweisungen, die solche Listen aus Systemansichten zurückgeben, können aus dem folgenden Artikel in Abschnitt C kopiert werden:

- [SELECT- und JOIN-Anweisungen von Systemsichten für erweiterte Ereignisse in SQL Server](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md)
    - [C.4](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_4_data_fields) SELECT von Feldern für ein Ereignis
    - [C.6](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_6_parameters_targets) SELECT von Parametern für ein Ziel
    - [C.3](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_3_select_all_available_objects) SELECT von Aktionen


Sie können die im Kontext einer realen CREATE EVENT SESSION-Anweisung verwendeten Parameter, Felder und Aktionen über [diesen Link](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_B_2_TSQL_perspective)anzeigen.



<a name="h2_target_etw_classic_sync_target"></a>

## <a name="etwclassicsynctarget-target"></a>etw_classic_sync_target-Ziel


Erweiterte Ereignisse von SQL Server können mit der Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW) zusammenwirken, um die Systemaktivität zu überwachen. Weitere Informationen finden Sie in den folgenden Themen:

- [Ereignisablaufverfolgung für Windows-Ziel](../../relational-databases/extended-events/event-tracing-for-windows-target.md)
- [Überwachen der Systemaktivität mit erweiterten Ereignissen](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)


Dieses ETW-Ziel verarbeitet die empfangenen Daten *synchron* , während die meisten Ziele *asynchrone*Verarbeitung aufweisen.


\<! – Rufen Sie diesen ETW-Abschnitt später erneut auf.
-->



<a name="h2_target_event_counter"></a>

## <a name="eventcounter-target"></a>event_counter-Ziel


Das event_counter-Ziel zählt lediglich, wie oft jedes angegebene Ereignis eintritt.


Im Gegensatz zu den meisten anderen Zielen:

- besitzt event_counter keine Parameter


- Im Gegensatz zu den meisten Zielen verarbeitet das event_counter-Ziel die empfangenen Daten *synchron*
    - Die synchrone Verarbeitung ist für den einfachen event_counter akzeptabel, da event_counter sehr wenig Verarbeitungsleitung beansprucht
    - Das Datenbankmodul bewirkt die Trennung von jedem Ziel, das zu langsam ist und dadurch die Leistung des Datenbankmoduls zu beeinträchtigen (bremsen) droht. Das ist ein Grund, warum die meisten Ziele *asynchrone*Verarbeitung aufweisen.


#### <a name="example-output-captured-by-eventcounter"></a>Von event_counter erfasste Beispielausgabe


```
package_name   event_name         count
------------   ----------         -----
sqlserver      checkpoint_begin   4
```


Der nächste Punkt ist die CREATE EVENT SESSION, die zu den vorstehenden Ergebnissen geführt hat. Für diesen Test wurde in der EVENT...WHERE-Klausel das Feld **package0.counter** verwendet, um die Zählung abzubrechen, nachdem die Anzahl auf 4 angestiegen ist.


```tsql
CREATE EVENT SESSION [event_counter_1]
    ON SERVER 
    ADD EVENT sqlserver.checkpoint_begin   -- Test by issuing CHECKPOINT; statements.
    (
        WHERE ([package0].[counter] <= (4))   -- A predicate filter.
    )
    ADD TARGET package0.event_counter
    WITH
    (
        MAX_MEMORY = 4096 KB,
        MAX_DISPATCH_LATENCY = 3 SECONDS
    );
```



<a name="h2_target_event_file"></a>

## <a name="eventfile-target"></a>event_file-Ziel


Das Ziel **event_file** schreibt Ereignissitzungsausgaben vom Puffer in eine Datenträgerdatei:


- Sie geben den Parameter *filename=* in der ADD TARGET-Klausel an.
    - Die Erweiterung der Datei muss**.xel** lauten.


- Der gewählte Dateiname wird vom System als Präfix verwendet, an das eine auf Datum-/Uhrzeit basierende Ganzzahl vom Typ long integer angehängt wird, gefolgt von der XEL-Erweiterung.


#### <a name="create-event-session-with-eventfile-target"></a>CREATE EVENT SESSION mit **event_file**


Nun folgt die CREATE EVENT SESSION, die wir für den Test verwendet haben. Eine der ADD TARGET-Klauseln gibt eine event_file-Datei an.


```tsql
CREATE EVENT SESSION [locks_acq_rel_eventfile_22]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
    (
        SET
            collect_database_name=(1),
            collect_resource_description=(1)

        ACTION (sqlserver.sql_text,sqlserver.transaction_id)

        WHERE
        (
            [database_name]=N'InMemTest2'
            AND
            [object_id]=(370100359)
        )
    ),
    ADD EVENT sqlserver.lock_released
    (
        SET
            collect_database_name=(1),
            collect_resource_description=(1)

        ACTION(sqlserver.sql_text,sqlserver.transaction_id)

        WHERE
        (
            [database_name]=N'InMemTest2'
            AND
            [object_id]=(370100359)
        )
    )
    ADD TARGET package0.event_counter,
    ADD TARGET package0.event_file
    (
        SET     filename=N'C:\Junk\locks_acq_rel_eventfile_22-.xel'
    )
    WITH
    (
        MAX_MEMORY=4096 KB,
        MAX_DISPATCH_LATENCY=10 SECONDS
    );
```


#### <a name="sysfnxefiletargetreadfile-function"></a>sys.fn_xe_file_target_read_file-Funktion


Das event_file-Ziel speichert die empfangenen Daten in einem binären Format, das für Menschen nicht lesbar ist. Transact-SQL kann den Inhalt der XEL-Datei mithilfe von SELECT FROM aus der Funktion [**sys.fn_xe_file_target_read_file**](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md) melden.


Für SQL Server **2016** und höher hat die folgende T-SQL SELECT-Anweisung die Daten gemeldet. Das XEL-Suffix in 


```
SELECT f.*
        --,CAST(f.event_data AS XML)  AS [Event-Data-Cast-To-XML]  -- Optional
    FROM
        sys.fn_xe_file_target_read_file(
            'C:\junk\locks_acq_rel_eventfile_22-*.xel',
            null, null, null)  AS f;
```


Für SQL Server **2014**würde eine SELECT-Anweisung ähnlich der folgenden die Meldung der Daten übernehmen. Nach SQL Server 2014 werden keine XEM-Dateien mehr verwendet.


```
SELECT f.*
        --,CAST(f.event_data AS XML)  AS [Event-Data-Cast-To-XML]  -- Optional
    FROM
        sys.fn_xe_file_target_read_file(
            'C:\junk\locks_acq_rel_eventfile_22-*.xel',
            'C:\junk\metafile.xem',
            null, null)  AS f;
```


Natürlich können Sie die XEL-Daten auch manuell auf der SSMS-Benutzeroberfläche anzeigen:


#### <a name="data-stored-in-the-eventfile-target"></a>Im event_file-Ziel gespeicherte Daten


Der nächste Punkt ist der Bericht, der sich durch den SELECT aus **sys.fn_xe_file_target_read_file**in SQL Server 2016 ergibt.


```
module_guid                            package_guid                           object_name     event_data                                                                                                                                                                                                                                                                                          file_name                                                      file_offset
-----------                            ------------                           -----------     ----------                                                                                                                                                                                                                                                                                          ---------                                                      -----------
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   lock_acquired   <event name="lock_acquired" package="sqlserver" timestamp="2016-08-07T20:13:35.827Z"><action name="transaction_id" package="sqlserver"><value>39194</value></action><action name="sql_text" package="sqlserver"><value>\<![CDATA[  select top 1 * from dbo.T_Target;  ]]></value></action></event>   C:\junk\locks_acq_rel_eventfile_22-_0_131150744126230000.xel   11776
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   lock_released   <event name="lock_released" package="sqlserver" timestamp="2016-08-07T20:13:35.832Z"><action name="transaction_id" package="sqlserver"><value>39194</value></action><action name="sql_text" package="sqlserver"><value>\<![CDATA[  select top 1 * from dbo.T_Target;  ]]></value></action></event>   C:\junk\locks_acq_rel_eventfile_22-_0_131150744126230000.xel   11776
```



<a name="h2_target_histogram"></a>

## <a name="histogram-target"></a>histogram-Ziel


Das **histogram** -Ziel ist cooler als das event_counter-Ziel. histogram kann Folgendes:

- Vorkommen für mehrere Elemente separat zählen
- Vorkommen von verschiedenen Elementtypen zählen
    - Ereignisfelder
    - Aktionen


Der Parameter **source_type** bildet den Schlüssel bei der Steuerung des histogram-Ziels:

- **source_type=0** : Sammeln von Daten für *Ereignisfelder*
- **source_type=1** : Sammeln von Daten für *Aktionen*
    - 1 ist der Standardwert


Der Standardwert des Parameters „slots“ ist 256. Wenn Sie einen anderen Wert zuweisen, wird der Wert auf die nächste Potenz von 2 aufgerundet.

- Beispielsweise würde „slots=59“ auf „=64“ aufgerundet.


### <a name="action-example-for-histogram"></a>*Action* -Beispiel für histogram


In der TARGET...SET-Klausel legt die folgende Transact-SQL CREATE EVENT SESSION-Anweisung die Zielparameterzuweisung als **source_type=1**fest. Die 1 bedeutet, dass das histogram-Ziel eine Aktion nachverfolgt.

Im aktuellen Beispiel bietet die Klausel EVENT...ACTION dem Ziel zufällig nur eine Aktion zur Auswahl an, nämlich **sqlos.system_thread_id**. In der TARGET...SET-Klausel sehen wir die Zuweisung **source=N'sqlos.system_thread_id'** .

- Um mehr als eine Quellaktion nachzuverfolgen, können Sie der CREATE EVENT SESSION-Anweisung ein zweites histogram-Ziel hinzufügen.


```tsql
CREATE EVENT SESSION [histogram_lockacquired]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
        (
        ACTION
            (
            sqlos.system_thread_id
            )
        )
    ADD TARGET package0.histogram
        (
        SET
            filtering_event_name=N'sqlserver.lock_acquired',
            slots=(16),
            source=N'sqlos.system_thread_id',
            source_type=1
        )
    WITH
        (
        \<.... (For brevity, numerous parameter assignments generated by SSMS.exe are not shown here.) ....>
        );
```


 Die folgenden Daten wurden erfasst. Die Werte in der Spalte **value** waren system_thread_id-Werte. Beispielsweise wurden im Thread 6540 insgesamt 236 Sperren in Anspruch genommen.


```
value   count
-----   -----
 6540     236
 9308      91
 9668      74
10144      49
 5244      44
 2396      28
```


#### <a name="select-to-discover-available-actions"></a>Verwenden von SELECT zum Entdecken der verfügbaren Aktionen


Die [C.3](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_3_select_all_available_objects) SELECT-Anweisung kann die Aktionen finden, die Ihnen im System zur Angabe in Ihrer CREATE EVENT SESSION-Anweisung zur Verfügung stehen. In der WHERE-Klausel müssten Sie dazu zuerst den Filter **o.name LIKE** bearbeiten, sodass er den Aktionen entspricht, die Sie interessieren.


Hier sehen Sie ein Beispielrowset, das von der C.3 SELECT-Anweisung zurückgegeben wird. Die Aktion **system_thread_id** befindet sich in der zweiten Zeile.


```
Package-Name   Action-Name                 Action-Description
------------   -----------                 ------------------
package0       collect_current_thread_id   Collect the current Windows thread ID
sqlos          system_thread_id            Collect current system thread ID
sqlserver      create_dump_all_threads     Create mini dump including all threads
sqlserver      create_dump_single_thread   Create mini dump for the current thread
```


### <a name="event-field-example-for-histogram"></a>*Ereignisfeld* -Beispiel für histogram


Im folgenden Beispiel ist **source_type=0**festgelegt. Der **source=** zugewiesene Wert ist ein Ereignisfeld (keine Aktion).



```tsql
CREATE EVENT SESSION [histogram_checkpoint_dbid]
    ON SERVER 
    ADD EVENT  sqlserver.checkpoint_begin
    ADD TARGET package0.histogram
    (
    SET
        filtering_event_name = N'sqlserver.checkpoint_begin',
        source               = N'database_id',
        source_type          = (0)
    )
    WITH
    ( \<....> );
```


Die folgenden Daten wurden vom histogram-Ziel erfasst. Die Daten zeigen, dass in der Datenbank mit ID=5 7 checkpoint_begin-Ereignisse aufgetreten sind.


```
value   count
-----   -----
5       7
7       4
6       3
```


#### <a name="select-to-discover-available-fields-on-your-chosen-event"></a>Verwenden von SELECT zum Ermitteln der für das ausgewählte Ereignis verfügbaren Felder


Die [C.4](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_4_data_fields) SELECT-Anweisung zeigt Ereignisfelder an, unter denen Sie wählen können. Sie müssten hier zunächst den Filter **o.name LIKE** bearbeiten, um ihn auf den Namen des ausgewählten Ereignisses festzulegen.


Das folgende Rowset wurde von C.4 SELECT zurückgegeben. Das Rowset zeigt, dass database_id das einzige Feld des Ereignisses checkpoint_begin ist, das Werte für das histogram-Ziel bereitstellen kann.


```
Package-Name   Event-Name         Field-Name   Field-Description
------------   ----------         ----------   -----------------
sqlserver      checkpoint_begin   database_id  NULL
sqlserver      checkpoint_end     database_id  NULL
```


<a name="h2_target_pair_matching"></a>

## <a name="pairmatching-target"></a>pair_matching-Ziel


Mithilfe des pair_matching-Ziels können Sie aufgetretene Startereignisse ermitteln, denen kein Endeereignis entspricht. Es kann beispielsweise auf ein Problem hinweisen, wenn ein lock_acquired-Ereignis eintritt, dem kein entsprechendes lock_released-Ereignis in angemessener Zeit folgt.


Das System ordnet Start- und Endeereignisse nicht automatisch zu. Vielmehr müssen Sie dem System die Zuordnung mithilfe Ihrer CREATE EVENT SESSION-Anweisung erläutern. Wenn ein Start- und ein Endeereignis zugeordnet wurden, wird das Paar verworfen, damit die Konzentration ganz auf den nicht zugeordneten Startereignissen liegt.


#### <a name="finding-matchable-fields-for-the-start-and-end-event-pair"></a>Suchen von zuzuordnenden Feldern für das Start- und Endeereignispaar


Mithilfe von [C.4 SELECT](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_4_data_fields)sehen wir im folgenden Rowset, dass etwa 16 Felder für das lock_acquired-Ereignis vorhanden sind. Das hier angezeigte Rowset wurde manuell geteilt, um zu zeigen, welche Felder in unserem Beispiel zugeordnet wurden. Bei einigen Feldern wäre der Versuch der Zuordnung unsinnig, wie etwa für **duration** bei beiden Ereignissen.


```
Package-Name   Event-Name   Field-Name               Field-Description
------------   ----------   ----------               -----------------
sqlserver   lock_acquired   database_name            NULL
sqlserver   lock_acquired   mode                     NULL
sqlserver   lock_acquired   resource_0               The ID of the locked object, when lock_resource_type is OBJECT.
sqlserver   lock_acquired   resource_1               NULL
sqlserver   lock_acquired   resource_2               The ID of the lock partition, when lock_resource_type is OBJECT, and resource_1 is 0.
sqlserver   lock_acquired   transaction_id           NULL

sqlserver   lock_acquired   associated_object_id     The ID of the object that requested the lock that was acquired.
sqlserver   lock_acquired   database_id              NULL
sqlserver   lock_acquired   duration                 The time (in microseconds) between when the lock was requested and when it was canceled.
sqlserver   lock_acquired   lockspace_nest_id        NULL
sqlserver   lock_acquired   lockspace_sub_id         NULL
sqlserver   lock_acquired   lockspace_workspace_id   NULL
sqlserver   lock_acquired   object_id                The ID of the locked object, when lock_resource_type is OBJECT. For other lock resource types it will be 0
sqlserver   lock_acquired   owner_type               NULL
sqlserver   lock_acquired   resource_description     The description of the lock resource. The description depends on the type of lock. This is the same value as the resource_description column in the sys.dm_tran_locks view.
sqlserver   lock_acquired   resource_type            NULL
```


### <a name="example-of-pairmatching"></a>Beispiel für pair_matching


Die folgende CREATE EVENT SESSION-Anweisung gibt zwei Ereignisse und zwei Ziele an. Das pair_matching-Ziel gibt zwei Mengen von Feldern für die Zuordnung der Ereignisse zu Paaren an. Die Reihenfolge der durch Trennzeichen getrennten Felder, die **begin_matching_columns=** und **end_matching_columns=** zugewiesen werden, muss übereinstimmen. Zwischen den durch Trennzeichen getrennten Feldern sind keine Tabstopp- oder Zeilenvorschubzeichen zulässig, jedoch Leerzeichen.

Um die Ergebnisse einzuschränken, haben wir zuerst in sys.objects per SELECT ausgewählt, um die object_id unserer Testtabelle zu ermitteln. Wir haben der EVENT...WHERE-Klausel einen Filter für die betreffende ID hinzugefügt.


```tsql
CREATE EVENT SESSION [pair_matching_lock_a_r_33]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
    (
        SET
            collect_database_name = (1),
            collect_resource_description = (1)

        ACTION (sqlserver.transaction_id)

        WHERE
        (
            [database_name] = 'InMemTest2'
            AND
            [object_id] = 370100359
        )
    ),
    ADD EVENT sqlserver.lock_released
    (
        SET
            collect_database_name = (1),
            collect_resource_description = (1)

        ACTION (sqlserver.transaction_id)

        WHERE
        (
            [database_name] = 'InMemTest2'
            AND
            [object_id] = 370100359
        )
    )
    ADD TARGET package0.event_counter,
    ADD TARGET package0.pair_matching
    (
        SET
            begin_event = N'sqlserver.lock_acquired',
            begin_matching_columns =
                N'resource_0, resource_1, resource_2, transaction_id, database_id',

            end_event = N'sqlserver.lock_released',
            end_matching_columns =
                N'resource_0, resource_1, resource_2, transaction_id, database_id',

            respond_to_memory_pressure = (1)
    )
    WITH
    (
        MAX_MEMORY = 8192 KB,
        MAX_DISPATCH_LATENCY = 15 SECONDS
    );
```


Zum Testen der Ereignissitzung haben wir absichtlich die Freigabe von erworbenen Sperren verhindert. Dies haben wir mit den folgenden T-SQL-Schritten erreicht:

1. BEGIN TRANSACTION.
2. UPDATE MeineTabelle....
3. Absichtlich wird COMMIT TRANSACTION erst nach dem Untersuchen der Ziele ausgegeben.
4. Später, nach den Tests, haben wir ein COMMIT TRANSACTION ausgegeben.


Das einfache **event_counter** -Ziel hat die folgenden Ausgabezeilen bereitgestellt. Da 52-50=2, erfahren wir aus der Ausgabe, dass wir 2 nicht gepaarte lock_acquired-Ereignisse sehen sollten, wenn wir die Ausgabe aus dem pair-matching-Ziel untersuchen.


```
package_name   event_name      count
------------   ----------      -----
sqlserver      lock_acquired   52
sqlserver      lock_released   50
```


Das **pair_matching** -Ziel hat die folgende Ausgabe bereitgestellt. Wie aus der event_counter-Ausgabe bereits zu erfahren war, sehen wir tatsächlich 2 lock_acquired-Zeilen. Die Tatsache, dass wir diese zwei Zeilen überhaupt finden, bedeutet, dass diese zwei lock_acquired-Ereignisse nicht gepaart wurden.


```
package_name   event_name      timestamp                     database_name   duration   mode   object_id   owner_type   resource_0   resource_1   resource_2   resource_description   resource_type   transaction_id
------------   ----------      ---------                     -------------   --------   ----   ---------   ----------   ----------   ----------   ----------   --------------------   -------------   --------------
sqlserver      lock_acquired   2016-08-05 12:45:47.9980000   InMemTest2      0          S      370100359   Transaction  370100359    3            0            [INDEX_OPERATION]      OBJECT          34126
sqlserver      lock_acquired   2016-08-05 12:45:47.9980000   InMemTest2      0          IX     370100359   Transaction  370100359    0            0                                   OBJECT          34126
```


Die Zeilen für die nicht gepaarten lock_acquired-Ereignisse könnten den T-SQL-Text oder **sqlserver.sql_text**aus der Sperranforderung enthalten. Allerdings wollten wir die Ausgabe schlank halten.


<a name="h2_target_ring_buffer"></a>

## <a name="ringbuffer-target"></a>ring_buffer-Ziel


Das ring_buffer-Ziel ist praktisch für schnelle und einfache Ereignistests. Beim Beenden der Ereignissitzung wird die gespeicherte Ausgabe verworfen.

In diesem ring_buffer-Abschnitt zeigen wir Ihnen außerdem, wie Sie die Transact-SQL-Implementierung von XQuery verwenden können, um den XML-Inhalt von ring_buffer in ein besser lesbares relationales Rowset zu kopieren.


#### <a name="create-event-session-with-ringbuffer"></a>CREATE EVENT SESSION mit ring_buffer


Diese CREATE EVENT SESSION-Anweisung, die das ring_buffer-Ziel verwendet, hat nichts Bemerkenswertes.


```tsql
CREATE EVENT SESSION [ring_buffer_lock_acquired_4]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
    (
        SET collect_resource_description=(1)

        ACTION(sqlserver.database_name)

        WHERE
        (
            [object_id]=(370100359)  -- ID of MyTable
            AND
            sqlserver.database_name='InMemTest2'
        )
    )
    ADD TARGET package0.ring_buffer
    (
        SET max_events_limit=(98)
    )
    WITH
    (
        MAX_MEMORY=4096 KB,
        MAX_DISPATCH_LATENCY=3 SECONDS
    );
```


### <a name="xml-output-received-for-lockacquired-by-ringbuffer"></a>Für lock_acquired von ring_buffer empfangene XML-Ausgabe


Wenn er mithilfe einer SELECT-Anweisung abgerufen wird, liegt der Inhalt in Form einer XML-Zeichenfolge vor. Die folgende Abbildung zeigt die XML-Zeichenfolge, die vom ring_buffer-Ziel in unserem Test gespeichert wurde. Um die folgende XML-Ausgabe halbwegs kurz zu halten, wurden jedoch alle &#x3c;event&#x3e;-Elemente bis auf zwei gelöscht. Und innerhalb der einzelnen &#x3c;event&#x3e;s wurde eine Reihe von überflüssigen &#x3c;data&#x3e;-Elementen gelöscht.


```xml
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="6" eventCount="6" droppedCount="0" memoryUsed="1032">
  <event name="lock_acquired" package="sqlserver" timestamp="2016-08-05T23:59:53.987Z">
    <data name="mode">
      <type name="lock_mode" package="sqlserver"></type>
      <value>1</value>
      <text>\<![CDATA[SCH_S]]></text>
    </data>
    <data name="transaction_id">
      <type name="int64" package="package0"></type>
      <value>111030</value>
    </data>
    <data name="database_id">
      <type name="uint32" package="package0"></type>
      <value>5</value>
    </data>
    <data name="resource_0">
      <type name="uint32" package="package0"></type>
      <value>370100359</value>
    </data>
    <data name="resource_1">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="resource_2">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="database_name">
      <type name="unicode_string" package="package0"></type>
      <value>\<![CDATA[]]></value>
    </data>
    <action name="database_name" package="sqlserver">
      <type name="unicode_string" package="package0"></type>
      <value>\<![CDATA[InMemTest2]]></value>
    </action>
  </event>
  <event name="lock_acquired" package="sqlserver" timestamp="2016-08-05T23:59:56.012Z">
    <data name="mode">
      <type name="lock_mode" package="sqlserver"></type>
      <value>1</value>
      <text>\<![CDATA[SCH_S]]></text>
    </data>
    <data name="transaction_id">
      <type name="int64" package="package0"></type>
      <value>111039</value>
    </data>
    <data name="database_id">
      <type name="uint32" package="package0"></type>
      <value>5</value>
    </data>
    <data name="resource_0">
      <type name="uint32" package="package0"></type>
      <value>370100359</value>
    </data>
    <data name="resource_1">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="resource_2">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="database_name">
      <type name="unicode_string" package="package0"></type>
      <value>\<![CDATA[]]></value>
    </data>
    <action name="database_name" package="sqlserver">
      <type name="unicode_string" package="package0"></type>
      <value>\<![CDATA[InMemTest2]]></value>
    </action>
  </event>
</RingBufferTarget>
```


Um den vorstehenden XML-Code anzuzeigen, können Sie die folgende SELECT-Anweisung ausgeben, während die Ereignissitzung aktiv ist. Die aktiven XML-Daten werden aus der Systemansicht **sys.dm_xe_session_targets**abgerufen.


```tsql
SELECT
        CAST(LocksAcquired.TargetXml AS XML)  AS RBufXml,
    INTO
        #XmlAsTable
    FROM
        (
        SELECT
                CAST(t.target_data AS XML)  AS TargetXml
            FROM
                     sys.dm_xe_session_targets  AS t
                JOIN sys.dm_xe_sessions         AS s

                    ON s.address = t.event_session_address
            WHERE
                t.target_name = 'ring_buffer'
                AND
                s.name        = 'ring_buffer_lock_acquired_4'
        )
            AS LocksAcquired;


SELECT * FROM #XmlAsTable;
```


### <a name="xquery-to-see-the-xml-as-a-rowset"></a>XQuery zur Ausgabe des XML-Codes als Rowset


Um den vorstehenden XML-Code als relationales Rowset darzustellen, fahren Sie nach der vorstehenden SELECT-Anweisung durch Ausgeben der folgenden T-SQL-Anweisung fort. In den kommentierten Zeilen ist jede Verwendung von XQuery erläutert.


```tsql
SELECT
         -- (A)
         ObjectLocks.value('(@timestamp)[1]',
            'datetime'     )  AS [OccurredDtTm]

        -- (B)
        ,ObjectLocks.value('(data[@name="mode"]/text)[1]',
            'nvarchar(32)' )  AS [Mode]

        -- (C)
        ,ObjectLocks.value('(data[@name="transaction_id"]/value)[1]',
            'bigint' )  AS [TxnId]

        -- (D)
        ,ObjectLocks.value('(action[@name="database_name" and @package="sqlserver"]/value)[1]',
            'nvarchar(128)')  AS [DatabaseName]
    FROM
        #TableXmlCell
    CROSS APPLY
        -- (E)
        TargetDateAsXml.nodes('/RingBufferTarget/event[@name="lock_acquired"]')  AS T(ObjectLocks);
```


#### <a name="xquery-notes-from-preceding-select"></a>XQuery-Anmerkungen zur vorstehenden SELECT-Anweisung


(A)
- timestamp= Wert des Attributs auf dem &#x3c;event&#x3e;-Element.
- Das Konstrukt '(...)[1]' stellt sicher, dass pro Iteration nur 1 Wert zurückgegeben wird, da dies eine erforderliche Einschränkung der .value() XQuery-Methode für Variablen und Spalten vom XML-Datentyp darstellt.


(B)
- &#x3c;text&#x3e; der innere Wert des Elements innerhalb eines &#x3c;data&#x3e;-Elements, dessen Attribut name= auf „mode“ festgelegt ist.


(C)
- &#x3c;value&#x3e; der innere Wert des Elements innerhalb eines &#x3c;data&#x3e;-Elements, dessen Attribut name= auf „transaction_id“ festgelegt ist.


(D)
- &#x3c;event&#x3e; enthält &#x3c;action&#x3e;.
- Das Attribut name= von &#x3c;action&#x3e; ist auf „database_name“ und das Attribut package= auf „sqlserver“ festgelegt (nicht „package0“), der innere Wert des Elements &#x3c;value&#x3e; wird abgerufen.


(E)
- C.A. bewirkt die Wiederholung der Verarbeitung für jedes einzelne Element &#x3c;event&#x3e;, dessen Attribut name= auf „lock_acquired“ festgelegt ist.
- Dies gilt für den von der vorherigen FROM-Klausel zurückgegebenen XML-Code.


#### <a name="output-from-xquery-select"></a>Ausgabe von XQuery SELECT


Die nächste Abbildung zeigt das vom vorhergehenden T-SQL-Code, des XQuery enthält, generierte Rowset.


```
OccurredDtTm              Mode    DatabaseName
------------              ----    ------------
2016-08-05 23:59:53.987   SCH_S   InMemTest2
2016-08-05 23:59:56.013   SCH_S   InMemTest2
```



## <a name="xevent-net-namespaces-and-cx23"></a>XEvent .NET-Namespaces und C&#x23;


Package0 weist zwei weitere Ziele auf, die aber in Transact-SQL nicht verwendet werden können:

- compressed_history
- event_stream


Ein Grund, warum wir wissen, dass diese beiden Ziele in T-SQL nicht verwendet werden können, besteht darin, dass ihre Werte ungleich NULL in der Spalte *sys.dm_xe_objects.capabilities* das 0x1-Bit nicht enthalten.


Das event_stream-Ziel kann in .NET-Programmen verwendet werden, die in Sprachen wie C# erstellt wurden. C#- und andere .NET-Entwickler können auf einen Ereignisstream mithilfe einer .NET Framework-Klasse zugreifen, wie etwa im Namespace Microsoft.SqlServer.XEvents.Linq.

Wenn er auftritt, bedeutet Fehler **25726** , dass der Ereignisstream sich schneller mit Daten gefüllt hat, als der Client die Daten nutzen konnte. Dadurch wurde die Verbindung des Datenbankmoduls mit dem Ereignisstream getrennt, um eine Beeinträchtigung der Serverleistung zu vermeiden.


### <a name="xevent-namespaces"></a>XEvent-Namespaces


- [Microsoft.SqlServer.Management.XEvent Namespace](https://msdn.microsoft.com/library/microsoft.sqlserver.management.xevent.aspx)

- [Microsoft.SqlServer.XEvent.Linq Namespace](https://msdn.microsoft.com/library/microsoft.sqlserver.xevent.linq.aspx)




