---
title: Erweiterte Ereignisse für SQL Server-Machine Learning-Services | Microsoft Docs
ms.custom: ''
ms.date: 12/21/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 2e16c8c468b4e82847e65e808f357e6eefb811f7
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="extended-events-for-sql-server-machine-learning-services"></a>Erweiterte Ereignisse für SQL Server-Machine Learning-Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server bietet eine Reihe von erweiterten Ereignissen, bei der Problembehandlung von Vorgängen im Zusammenhang mit der [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]sowie Python oder R-Aufträge an gesendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Dienste

## <a name="sql-server-events-for-machine-learning"></a>SQL Server-Ereignisse für Machine learning

Um eine Liste der mit SQL Server verknüpften Ereignisse anzuzeigen, führen Sie die folgende Abfrage in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aus.

```SQL
SELECT o.name AS event_name, o.description
FROM sys.dm_xe_objects o
JOIN sys.dm_xe_packages p
ON o.package_guid = p.guid
WHERE o.object_type = 'event'
AND p.name = 'SQLSatellite';
```

Allgemeine Informationen zur Verwendung von erweiterten Ereignissen finden Sie unter [Tools für erweiterte Ereignisse](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools).

> [!TIP]
> Für erweiterte Ereignisse von SQL Server generiert, testen Sie die neue [SSMS XEvent Profiler](https://docs.microsoft.com/sql/relational-databases/extended-events/use-the-ssms-xe-profiler). Diese neue Funktion in Management Studio zeigt einen live-Viewer für erweiterte Ereignisse und weniger intrusiv mit SQL Server als eine ähnliche Profiler-Ablaufverfolgung.

## <a name="additional-events-specific-to-machine-learning-components"></a>Zusätzliche Ereignisse, die spezifisch für Machine Learning-Komponenten

Zusätzliche erweiterte Ereignisse stehen für die Komponenten, die im Zusammenhang mit und von SQL Server Machine Learning Services verwendet z. B. die [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], und BXLServer, dem satellitenprozess, der die Laufzeit von R startet. Diese zusätzliche erweiterte Ereignisse, die aus externen Prozessen ausgelöst werden und somit müssen mit einem externen Dienstprogramm aufgezeichnet werden können.

Weitere Informationen hierzu finden Sie im Abschnitt [Sammeln von Ereignissen aus externen Prozessen](#bkmk_externalevents).

##  <a name="bkmk_xeventtable"></a> Tabelle erweiterter Ereignisse

|Ereignis|Description|Hinweise|  
|-----------|-----------------|---------|  
|connection_accept|Tritt auf, wenn eine neue Verbindung akzeptiert wird. Dieses Ereignis dient dazu, alle Verbindungsversuche zu protokollieren.||  
|failed_launching|Fehler beim Starten.|Gibt einen Fehler an.|  
|satellite_abort_connection|Eintrag über einen Verbindungsabbruch||  
|satellite_abort_received|Wird ausgelöst, wenn eine Abbruchnachricht über eine Satellitenverbindung empfangen wird.||  
|satellite_abort_sent|Wird ausgelöst, wenn eine Abbruchnachricht über eine Satellitenverbindung gesendet wird.||  
|satellite_authentication_completion|Wird ausgelöst, wenn die Authentifizierung für eine TCP- oder Namedpipe-Verbindung abgeschlossen wurde.||  
|satellite_authorization_completion|Wird ausgelöst, wenn die Autorisierung für eine TCP- oder Namedpipe-Verbindung abgeschlossen wurde.||  
|satellite_cleanup|Wird ausgelöst, wenn ein Satellit Cleanup aufruft.|Nur aus externem Prozess ausgelöst. Lesen Sie die Anleitung für das Sammeln von Ereignissen aus externen Prozessen.|  
|satellite_data_chunk_sent|Wird ausgelöst, wenn die Satellitenverbindung das Senden eines einzelnen Datensegments abschließt.|Das Ereignis gibt die Anzahl der gesendeten Zeilen an, die Anzahl der Spalten, die Anzahl der SNI-Pakete „usedm“ und die beim Senden des Blocks verstrichene Zeit in Millisekunden. Anhand dieser Informationen können Sie nachvollziehen, wie viel Zeit für das Übergeben von verschiedene Datentypen benötigt wird und wie viele Pakete verwendet werden.|  
|satellite_data_receive_completion|Wird ausgelöst, wenn alle erforderlichen Abfragedaten über die Satellitenverbindung empfangen wurden.|Nur aus externem Prozess ausgelöst. Lesen Sie die Anleitung für das Sammeln von Ereignissen aus externen Prozessen.|  
|satellite_data_send_completion|Wird ausgelöst, wenn alle erforderlichen Abfragedaten über die Satellitenverbindung gesendet wurden.||  
|satellite_data_send_start|Wird ausgelöst, wenn die Datenübertragung beginnt.| Die Datenübertragung beginnt unmittelbar vor das erste Datensegment gesendet wird.|  
|satellite_error|Wird verwendet, um einen SQL-Satellitenfehler nachzuverfolgen||  
|satellite_invalid_sized_message|Länge dieser Nachricht ist ungültig.||  
|satellite_message_coalesced|Wird verwendet, um das Zusammenfügen von Nachrichten auf Netzwerkebene nachzuverfolgen||  
|satellite_message_ring_buffer_record|Eintrag über Nachrichtenringpuffer||  
|satellite_message_summary|zusammenfassende Informationen zur Nachrichtenübermittlung||  
|satellite_message_version_mismatch|Versionsfeld der Nachricht stimmt nicht überein||  
|satellite_messaging|Wird verwendet, um das Nachrichtenereignis (Binden, Bindung aufheben usw.) nachzuverfolgen.||  
|satellite_partial_message|Wird verwendet, um eine Teilnachricht auf Netzwerkebene nachzuverfolgen.||  
|satellite_schema_received|Wird ausgelöst, wenn die Schemanachricht empfangen und von SQL gelesen wird.||  
|satellite_schema_sent|Wird ausgelöst, wenn der Satellit eine Schemanachricht sendet.|Nur aus externem Prozess ausgelöst. Lesen Sie die Anleitung für das Sammeln von Ereignissen aus externen Prozessen.|  
|satellite_service_start_posted|Wird ausgelöst, wenn die Startnachricht des Diensts an Launchpad gesendet wird.|Dies erteilt Launchpad den Auftrag, den externen Prozess zu starten. Außerdem enthält das Ereignis eine ID für die neue Sitzung.|  
|satellite_unexpected_message_received|Wird ausgelöst, wenn eine unerwartete Nachricht empfangen wird.|Gibt einen Fehler an.|  
|stack_trace|Tritt auf, wenn ein Speicherabbild des Prozesses angefordert wird.|Gibt einen Fehler an.|  
|trace_event|Wird zu Protokollierungszwecken verwendet|Diese Ereignisse können Ablaufverfolgungsmeldungen von SQL Server, Launchpad und externen Prozessen enthalten. Dies schließt die Ausgabe an „stdout“ und „stderr“ aus R ein.|  
|launchpad_launch_start|Wird ausgelöst, wenn Launchpad einen Satelliten startet.|Wird nur aus Launchpad ausgelöst. Lesen Sie die Anleitung für das Sammeln von Ereignissen aus launchpad.exe.|  
|launchpad_resume_sent|Wird ausgelöst, wenn Launchpad den Satelliten gestartet und eine Fortsetzungsmeldung an SQL Server gesendet hat.|Wird nur aus Launchpad ausgelöst. Lesen Sie die Anleitung für das Sammeln von Ereignissen aus launchpad.exe.|  
|satellite_data_chunk_sent|Wird ausgelöst, wenn die Satellitenverbindung das Senden eines einzelnen Datensegments abschließt.|Enthält Informationen über die Anzahl der Spalten, Zeilen und Pakete sowie über die zum Versenden des Segments benötigten Zeit.|  
|satellite_sessionId_mismatch|Sitzungs-ID der Nachricht wird nicht erwartet||  
  
###  <a name="bkmk_externalevents"></a> Sammeln von Ereignissen aus externen Prozessen

SQL Server-Machine Learning-Services startet einige Dienste, die außerhalb des SQL Server-Prozesses ausgeführt. Um Ereignisse im Zusammenhang mit diesen externen Prozessen zu erfassen, müssen Sie eine Konfigurationsdatei zur ereignisnachverfolgung erstellen und speichern Sie die Datei im gleichen Verzeichnis wie die ausführbare Datei für den Prozess.  
  
+ **[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]**   
  
    Legen Sie die *.config*-Datei im Binn-Verzeichnis für die SQL Server-Instanz ab, um Ereignisse zu erfassen, die im Zusammenhang mit Launchpad auftreten.  In einer Standardinstallation wäre dies:

    `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\MSSQL\Binn`installiert haben.  
  
+ **BXLServer** ist der satellitenprozess, der Erweiterbarkeit von SQL mit externen Skriptsprachen, z. B. R oder Python unterstützt. Für jede Instanz des externen Sprache wird eine separate Instanz von BxlServer gestartet.
  
    Um Ereignisse im Zusammenhang mit BXLServer zu erfassen, legen Sie die *config* Datei im Installationsverzeichnis von R oder Python.  In einer Standardinstallation wäre dies:
     
    **R:** `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64`.  

    **Python:** `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\PYTHON_SERVICES\library\RevoScaleR\rxLibs\x64`.

Der Name der Konfigurationsdatei muss identisch mit dem der ausführbaren Datei sein und dem Format „[Name].xevents.xml“ entsprechen. Mit anderen Worten: Die Dateien müssen folgendermaßen benannt werden:

+ `Launchpad.xevents.xml`
+ `bxlserver.xevents.xml`

Die Konfigurationsdatei weist das folgende Format auf:

```xml
\<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
<event_session name="[session name]" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="you">Xevent for launchpad or bxl server.</description>  
    <event package="SQLSatellite" name="[XEvent Name 1]" />  
    <event package="SQLSatellite" name="[XEvent Name 2]" />  
    <target package="package0" name="event_file">  
      <parameter name="filename" value="[SessionName].xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
```

+ Bearbeiten Sie zum Konfigurieren der Verfolgung der *Sitzungsname* Platzhalter, der Platzhalter für den Dateinamen (`[SessionName].xel`), und die Namen der Ereignisse, die Sie aufzeichnen z. B., möchten `[XEvent Name 1]`, `[XEvent Name 1]`).  
+ Eine beliebige Anzahl von Paket ereignistags möglicherweise angezeigt, und gesammelt werden, solange das Namensattribut richtig ist.

### <a name="example-capturing-launchpad-events"></a>Beispiel: Erfassen von Launchpad-Ereignissen

Das folgende Beispiel zeigt die Definition einer ereignisnachverfolgung für den Launchpad-Dienst:

```xml
\<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
<event_session name="sqlsatelliteut" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="hay">Xevent for sql tdd runner.</description>  
    <event package="SQLSatellite" name="launchpad_launch_start" />  
    <event package="SQLSatellite" name="launchpad_resume_sent" />  
    <target package="package0" name="event_file">  
      <parameter name="filename" value="launchpad_session.xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
```

+ Platzieren Sie die *.config*-Datei im Binn-Verzeichnis für die SQL Server-Instanz.
+ Diese Datei muss den Namen `Launchpad.xevents.xml`.

### <a name="example-capturing-bxlserver-events"></a>Beispiel: Erfassen von BXLServer-Ereignissen  

Das folgende Beispiel zeigt die Definition einer Ereignisablaufverfolgung für die ausführbare Datei von BXLServer.
  
```xml
\<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
 <event_session name="sqlsatelliteut" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="hay">Xevent for sql tdd runner.</description>  
    <event package="SQLSatellite" name="satellite_abort_received" />  
    <event package="SQLSatellite" name="satellite_authentication_completion" />  
    <event package="SQLSatellite" name="satellite_cleanup" />  
    <event package="SQLSatellite" name="satellite_data_receive_completion" />  
    <event package="SQLSatellite" name="satellite_data_send_completion" />  
    <event package="SQLSatellite" name="satellite_data_send_start" />  
    <event package="SQLSatellite" name="satellite_schema_sent" />   
    <event package="SQLSatellite" name="satellite_unexpected_message_received" />    
    <event package="SQLSatellite" name="satellite_data_chunk_sent" />   
    <target package="package0" name="event_file">  
      <parameter name="filename" value="satellite_session.xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
```

+ Legen Sie die *.config*-Datei im gleichen Verzeichnis ab wie die ausführbare BXLServer-Datei.
+ Diese Datei muss den Namen `bxlserver.xevents.xml`.

## <a name="see-also"></a>Siehe auch

[Benutzerdefinierte Management Studio Berichte für Machine Learning-Dienste](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)
