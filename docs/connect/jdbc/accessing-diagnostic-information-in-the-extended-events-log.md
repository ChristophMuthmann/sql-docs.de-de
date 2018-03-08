---
title: "Zugreifen auf Diagnoseinformationen im Protokoll für erweiterte Ereignisse | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a79e9468-2257-4536-91f1-73b008c376c3
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 95ba6393a69eca1c5e4c235bc205438262186b21
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>Zugreifen auf Diagnoseinformationen im Protokoll der erweiterten Ereignisse
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  In der [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]wurde die Ablaufverfolgung ([Ablaufverfolgung Treibervorgänge](../../connect/jdbc/tracing-driver-operation.md)) wurde aktualisiert, um einfacher mit Diagnoseinformationen, z. B. Verbindungsfehlern, aus dem Server Connectivity Ring korreliert vereinfachen und den anwendungsbezogenen Leistungsinformationen in das Protokoll für erweiterte Ereignisse. Informationen dazu, wie Sie das Protokoll für erweiterte Ereignisse lesen, finden Sie unter [View Event Session Data](http://msdn.microsoft.com/library/hh710068(SQL.110).aspx).  
  
## <a name="details"></a>Details  
 Für Verbindungsvorgänge die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] sendet einen Client Verbindungs-ID. Wenn die Verbindung nicht hergestellt werden kann, können Sie auf den Konnektivitätsringpuffer zugreifen ([Behandlung von Konnektivitätsproblemen in SQL Server 2008 mit dem Konnektivitätsringpuffer](http://go.microsoft.com/fwlink/?LinkId=207752)), das Feld **ClientConnectionID** suchen und Diagnoseinformationen zum Verbindungsfehler abrufen. Clientverbindungs-IDs werden nur im Ringpuffer protokolliert, wenn ein Fehler auftritt. (Wenn vor dem Senden des prelogin-Pakets keine Verbindung hergestellt werden kann, wird keine Clientverbindungs-ID generiert.) Die Clientverbindungs-ID ist eine 16-Byte-GUID. Sie erhalten auch die Clientverbindungs-ID in der Zielausgabe für erweiterte Ereignisse, ob die **Client_connection_id** -Aktion Ereignissen in einer Sitzung für erweiterte Ereignisse hinzugefügt wird. Aktivieren der Ablaufverfolgung und den Verbindungsbefehl erneut ausführen und beobachten Sie die **ClientConnectionID** Feld in der Ablaufverfolgung, wenn Sie weitere clienttreiberdiagnose benötigen.  
  
 Sie können den Client abrufen Verbindungs­id programmgesteuert über [ISQLServerConnection-Schnittstelle](../../connect/jdbc/reference/isqlserverconnection-interface.md). Die Verbindungs-ID ist auch in verbindungsbezogenen Ausnahmen enthalten.  
  
 Bei einem Verbindungsfehler kann die Clientverbindungs-ID in den BID-Ablaufverfolgungsinformationen des Servers und im Konnektivitätsringpuffer nützlich sein, um die Clientverbindungen mit Verbindungen auf dem Server zu korrelieren. Weitere Informationen zur Bid-ABLAUFVERFOLGUNG auf dem Server verfolgt werden, finden Sie unter [Data Access Tracing](http://go.microsoft.com/fwlink/?LinkId=125805). Beachten Sie, dass der Artikel enthält auch Informationen zum Ausführen einer datenzugriffsablaufverfolgung, gelten nicht für die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]; finden Sie unter [Ablaufverfolgung Treibervorgänge](../../connect/jdbc/tracing-driver-operation.md) Informationen zum Ausführen einer Data Access-Ablaufverfolgung unter Verwendung der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 Der JDBC-Treiber sendet außerdem eine threadspezifische Aktivitäts-ID. Die Aktivitäts-ID wird in den Sitzungen für erweiterte Ereignisse aufgezeichnet, wenn die Sitzungen bei aktivierter TRACK_CAUSAILITY-Option gestartet werden. Bei Leistungsproblemen mit einer aktiven Verbindung können Sie die Aktivitäts-ID aus der Ablaufverfolgung des Clients (Feld „ActivityID“) abrufen und dann in der Ausgabe der erweiterten Ereignisse nach der Aktivitäts-ID suchen. Die Aktivitäts-ID in erweiterten Ereignissen ist eine 16-Byte-GUID (entspricht nicht der GUID für die Clientverbindungs-ID), an die eine 4-Byte-Sequenznummer angehängt ist. Die Sequenznummer stellt die Reihenfolge einer Anforderung in einem Thread dar. Die ActivityId wird bei SQL-Stapelanweisungen und RPC-Anforderungen gesendet. Zum Aktivieren des Sendens der ActivityId an den Server müssen Sie zunächst das folgende Schlüssel-Wert-Par in der Datei „Logging.Properties“ angeben:  
  
```  
com.microsoft.sqlserver.jdbc.traceactivity = on  
```  
  
 Jeder andere Wert als `on` (Groß-/Kleinschreibung beachten) deaktiviert das Senden der ActivityId.  
  
 Weitere Informationen finden Sie unter [Ablaufverfolgung für Treibervorgänge](../../connect/jdbc/tracing-driver-operation.md). Dieses Ablaufverfolgungsflag wird mit den entsprechenden JDBC-Objektprotokollierungen verwendet, um zu bestimmen, ob im JDBC-Treiber eine Ablaufverfolgung der ActivityId ausgeführt und diese gesendet werden soll. Zusätzlich zum Aktualisieren der Datei „Logging.Properties“ muss die Protokollierung „com.microsoft.sqlserver.jdbc“ mit dem Wert FINER oder höher aktiviert werden. Wenn die ActivityId bei Anforderungen an eine bestimmte Klasse an den Server gesendet werden soll, muss die entsprechende Klassenprotokollierung mit dem Wert FINER oder FINEST aktiviert werden. Wenn die Klasse beispielsweise SQLServerStatement lautet, aktivieren Sie die Protokollierung „com.microsoft.sqlserver.jdbc.SQLServerStatement“.  
  
 Im folgenden finden Sie ein Beispiel, verwendet [!INCLUDE[tsql](../../includes/tsql_md.md)] um eine Sitzung für erweiterte Ereignisse zu starten, die in einem Ringpuffer gespeichert wird und die Aktivitäts-ID gesendet, von einem Client bei RPC- und Stapelvorgängen:  
  
```  
create event session MySession on server  
add event connectivity_ring_buffer_recorded,  
add event sql_statement_starting (action (client_connection_id)),  
add event sql_statement_completed (action (client_connection_id)),  
add event rpc_starting (action (client_connection_id)),  
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Diagnostizieren von Problemen mit dem JDBC-Treiber](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
