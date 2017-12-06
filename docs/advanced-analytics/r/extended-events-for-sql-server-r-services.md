---
title: Erweiterte Ereignisse bei SQL Server R Services | Microsoft-Dokumentation
ms.custom: SQL2016_New_Updated
ms.date: 11/29/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4e90e057-aacb-4adc-8da6-64861f4e87df
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 76350c58a9ef7dc52eaf1a260ec04a231f362872
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="extended-events-for-sql-server-r-services"></a>Erweiterte Ereignisse bei SQL Server R Services
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] bietet eine Reihe von erweiterten Ereignissen, die bei der Problembehandlung von Vorgängen im Zusammenhang mit [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] oder R-Aufträgen an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet werden können.  
  
 Um eine Liste der mit SQL Server verknüpften Ereignisse anzuzeigen, führen Sie die folgende Abfrage in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aus.  
  
```  
select o.name as event_name, o.description  
  from sys.dm_xe_objects o  
  join sys.dm_xe_packages p  
    on o.package_guid = p.guid  
 where o.object_type = 'event'  
   and p.name = 'SQLSatellite';  
```  
  
 Einige zusätzliche erweiterte Ereignisse mit [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] werden allerdings nur von externen Prozessen wie [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]und BXLServer ausgelöst, dem Satellitenprozess, der die Laufzeit von R startet. Weitere Informationen zum Erfassen dieser Ereignisse finden Sie unter [Collecting Events from External Processes](#bkmk_externalevents).  
  
 Allgemeine Informationen zur Verwendung von erweiterten Ereignissen finden Sie unter [SQL Server Extended Events Sessions](../../relational-databases/extended-events/sql-server-extended-events-sessions.md).  

  
##  <a name="bkmk_xeventtable"></a> Tabelle erweiterter Ereignisse  
  
|Ereignis|Beschreibung|Verwenden Sie|  
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
|satellite_data_send_start|Wird ausgelöst, wenn die Datenübertragung beginnt (unmittelbar bevor der erste Datensegment gesendet wird).||  
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
  
###  <a name="bkmk_externalevents"></a> Collecting Events from External Processes  
 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] startet einige Dienste, die außerhalb des SQL Server-Prozesses ausgeführt werden. Um Ereignisse, die im Zusammenhang mit diesen externen Prozessen auftreten, zu erfassen, müssen Sie eine Konfigurationsdatei zur Ereignisnachverfolgung erstellen. Diese Datei müssen Sie im gleichen Verzeichnis wie die ausführbare Datei für den Prozess ablegen.  
  
-   **[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]**   
  
     Legen Sie die *.config*-Datei im Binn-Verzeichnis für die SQL Server-Instanz ab, um Ereignisse zu erfassen, die im Zusammenhang mit Launchpad auftreten.  In einer Standardinstallation wäre dies `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\MSSQL\Binn`.  
  
-   **BXLServer** ist der Satellitenprozess, der die Erweiterbarkeit von SQL auf R und andere externe Skriptsprachen unterstützt.  
  
     Um Ereignisse, die im Zusammenhang mit BXLServer auftreten, zu erfassen, legen Sie die *.config*-Datei im Installationsverzeichnis von R ab.  In einer Standardinstallation wäre dies `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64`.  
  
> [!IMPORTANT]
>   Der Name der Konfigurationsdatei muss identisch mit dem der ausführbaren Datei sein und dem Format „[Name].xevents.xml“ entsprechen. Mit anderen Worten: Die Dateien müssen folgendermaßen benannt werden:  
>   
> - Launchpad.xevents.xml  
> - bxlserver.xevents.xml  
  
 Die Konfigurationsdatei weist das folgende Format auf:  
  
```  
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
  
 **Hinweise:**  
  
-   Bearbeiten Sie zum Konfigurieren der Verfolgung den Platzhalter für den Namen der Sitzung *session name*, den Platzhalter für den Dateinamen `[SessionName].xel` und die Namen der Ereignisse, die Sie erfassen möchten (z.B. `[XEvent Name 1]` oder `[XEvent Name 1]`).  
  
-   Eine beliebige Anzahl von `event package`-Tags kann angezeigt werden und wird gesammelt, solange das Namensattribut korrekt ist.  
  
### <a name="example-capturing-launchpad-events"></a>Beispiel: Erfassen von Launchpad-Ereignissen  
 Das folgende Beispiel zeigt die Definition einer Ereignisnachverfolgung für den Launchpad-Dienst.  
  
```  
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
  
 **Hinweise:**  
  
-   Platzieren Sie die *.config*-Datei im Binn-Verzeichnis für die SQL Server-Instanz.  
  
-   Diese Datei muss den Namen *Launchpad.xevents.xml*tragen.  
  
### <a name="example-capturing-bxlserver-events"></a>Beispiel: Erfassen von BXLServer-Ereignissen  
 Das folgende Beispiel zeigt die Definition einer Ereignisablaufverfolgung für die ausführbare Datei von BXLServer.  
  
```  
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
  
 **Hinweise:**  
  
-   Legen Sie die *.config*-Datei im gleichen Verzeichnis ab wie die ausführbare BXLServer-Datei.  
  
-   Diese Datei muss den Namen *bxlserver.xevents.xml*tragen.  
  
## <a name="see-also"></a>Siehe auch
[Custom Management Studio Reports for R Services (Benutzerdefinierte Management Studio-Berichte für R Services)](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md)  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [Managing and Monitoring R Solutions (Verwalten und Überwachen von R-Lösungen)](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
  
  
