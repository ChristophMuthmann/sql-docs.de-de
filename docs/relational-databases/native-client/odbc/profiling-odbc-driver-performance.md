---
title: Profilerstellung für ODBC-Treiber Leistung | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client|ODBC
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- profiling ODBC driver performance data [SQL Server Native Client]
- performance [ODBC]
- application statistics [ODBC]
- time statistics [ODBC]
- ODBC, performance data
- SQL Server Native Client ODBC driver, profiling performance data
- SQLPERF data structure
- statistical information [ODBC]
ms.assetid: 8f44e194-d556-4119-a759-4c9dec7ecead
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4521491e20df8eecced79fc6f49a2940647bd49b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="profiling-odbc-driver-performance"></a>Leistungsprofilerstellung des ODBC-Treibers
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber kann Profile von zwei Typen von Leistungsdaten erstellen:  
  
-   Abfragen mit langer Ausführungszeit  
  
     Der Treiber kann jede Abfrage in eine Protokolldatei schreiben, die innerhalb eines angegebenen Zeitraums keine Antwort vom Server erhält. Anwendungsprogrammierer und Datenbankadministratoren können dann die protokollierten SQL-Anweisungen untersuchen, um zu ermitteln, wie sie die Leistung verbessern können.  
  
-   Treiberleistungsdaten  
  
     Der Treiber kann Leistungsstatistiken aufzeichnen und entweder in eine Datei schreiben oder über eine treiberspezifische Datenstruktur namens SQLPERF einer Anwendung verfügbar machen. Die Datei mit den Leistungsstatistiken ist eine durch Tabstopps getrennte Datei, die mit jeder Tabellenkalkulationsanwendung, die durch Tabstopps getrennte Dateien unterstützt (beispielsweise Microsoft Excel), problemlos analysiert werden kann.  
  
 Beide Typen der Profilerstellung werden wie folgt aktiviert:  
  
-   Durch Herstellen einer Verbindung zu einer Datenquelle, die die Protokollierung angibt  
  
-   Aufrufen von [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) treiberspezifischen Attribute festlegen, die die profilerstellung steuern.  
  
 Jeder Anwendungsprozess erhält eine eigene Kopie des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treibers, und die Profilerstellung erfolgt global für die Kombination aus einer Treiberkopie und einem Anwendungsprozess. Wenn die Profilerstellung in der Anwendung aktiviert wird, zeichnet die Profilerstellung Informationen über alle im Treiber dieser Anwendung aktiven Verbindungen auf. Das betrifft auch die Verbindungen, die die Profilerstellung nicht ausdrücklich angefordert haben.  
  
 Nachdem der Treiber ein Profilerstellungsprotokoll geöffnet hat (entweder das Protokoll für Leistungsdaten oder für eine Abfrage mit längerer Ausführungszeit), schließt er es erst wieder, wenn der Treiber vom ODBC-Treiber-Manager entladen wird, weil eine Anwendung alle Umgebungshandles freigibt, die sie im Treiber geöffnet hatte. Wenn die Anwendung ein neues Umgebungshandle öffnet, wird eine neue Kopie des Treibers geladen. Wenn die Anwendung dann entweder die Verbindung zu einer Datenquelle herstellt, die dieselbe Protokolldatei angibt, oder die treiberspezifischen Attribute auf die Protokollierung in derselben Datei festlegt, überschreibt der Treiber das alte Protokoll.  
  
 Wenn eine Anwendung mit der Profilerstellung in einer Protokolldatei beginnt und eine zweite Anwendung versucht, die Profilerstellung in derselben Protokolldatei zu beginnen, kann die zweite Anwendung keine Profildaten protokollieren. Wenn die zweite Anwendung mit der Profilerstellung beginnt, nachdem die erste Anwendung ihren Treiber entladen hat, überschreibt die zweite Anwendung die Protokolldatei der ersten Anwendung.  
  
 Wenn eine Anwendung mit einer Datenquelle verbunden ist, die profilerstellung aktiviert, gibt der Treiber SQL_ERROR zurück, wenn die Anwendung aufruft, **SQLSetConnectOption** Protokollierung starten. Ein Aufruf von **SQLGetDiagRec** dann gibt Folgendes zurück:  
  
```  
SQLState: 01000, pfNative = 0  
ErrorMsg: [Microsoft][SQL Server Native Client]  
   An error has occurred during the attempt to access  
   the log file, logging disabled.  
```  
  
 Der Treiber hört auf, Leistungsdaten zu erfassen, wenn ein Umgebungshandle geschlossen wird. Wenn eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Anwendung mehrere Verbindungen hergestellt hat, von denen jede über ein eigenes Umgebungshandle verfügt, hört der Treiber mit der Erfassung von Leistungsdaten auf, wenn eines der zugewiesenen Umgebungshandles geschlossen wird.  
  
 Die Leistungsdaten des Treibers können entweder in der SQLPERF-Datenstruktur gespeichert oder in einer durch Tabstopps getrennten Datei protokolliert werden. Die Daten umfassen die folgenden Statistikkategorien:  
  
-   Anwendungsprofil  
  
-   Verbindung  
  
-   Netzwerk  
  
-   Zeit  
  
 In der folgenden Tabelle gelten die Beschreibungen der Felder in der SQLPERF-Datenstruktur auch für die in der Leistungsprotokolldatei erfassten Statistiken.  
  
### <a name="application-profile-statistics"></a>Anwendungsprofilstatistiken  
  
|SQLPERF-Feld|Description|  
|-------------------|-----------------|  
|TimerResolution|Minimale Auflösung der Uhrzeit des Servers in Millisekunden. Dies wird gewöhnlich als 0 (null) angegeben und sollte nur verwendet werden, wenn die angegebene Zahl sehr groß ist. Wenn die minimale Auflösung der Serveruhrzeit größer als das wahrscheinliche Intervall einiger der zeitgeberbasierten Statistikwerte ist, könnte die Statistikdatenmenge unnötig größer werden.|  
|SQLidu|Anzahl der INSERT-Anweisungen, DELETE-Anweisungen oder UPDATE-Anweisungen nach SQL_PERF_START|  
|SQLiduRows|Anzahl der INSERT-Anweisungen, DELETE-Anweisungen oder UPDATE-Anweisungen nach SQL_PERF_START|  
|SQLSelects|Anzahl der SELECT-Anweisungen, die nach SQL_PERF_START verarbeitet wurden|  
|SQLSelectRows|Anzahl von Zeilen, die nach SQL_PERF_START ausgewählt wurden|  
|Transaktionen|Anzahl der Benutzertransaktionen nach SQL_PERF_START, einschließlich der Rollbacks. Wenn eine ODBC-Anwendung mit SQL_AUTOCOMMIT_ON ausgeführt wird, wird jeder Befehl als Transaktion betrachtet.|  
|SQLPrepares|Anzahl der [SQLPrepare-Funktion](http://go.microsoft.com/fwlink/?LinkId=59360) -aufrufen nach SQL_PERF_START.|  
|ExecDirects|Anzahl der **SQLExecDirect** -aufrufen nach SQL_PERF_START.|  
|SQLExecutes|Anzahl der **SQLExecute** -aufrufen nach SQL_PERF_START.|  
|CursorOpens|Anzahl der Male, die der Treiber nach SQL_PERF_START einen Servercursor geöffnet hat|  
|CursorSize|Anzahl von Zeilen in den Resultsets, die nach SQL_PERF_START von Cursorn geöffnet wurden|  
|CursorUsed|Anzahl von Zeilen, die nach SQL_PERF_START über den Treiber von Cursorn abgerufen wurden|  
|PercentCursorUsed|Entspricht CursorUsed/CursorSize. Wenn beispielsweise eine Anwendung den Treiber veranlasst, einen Servercursor zu öffnen, um "SELECT COUNT(*) FROM Authors," auszuführen, enthält das Resultset für die SELECT-Anweisung 23 Zeilen. Wenn die Anwendung dann nur drei von diesen Zeilen abruft, ist CursorUsed/CursorSize = 3/23, weshalb PercentCursorUsed = 13.043478 ist.|  
|AvgFetchTime|Entspricht SQLFetchTime/SQLFetchCount|  
|AvgCursorSize|Entspricht CursorSize/CursorOpens|  
|AvgCursorUsed|Entspricht CursorUsed/CursorOpens|  
|SQLFetchTime|Kumulierte Menge an Zeit, die für das Abrufen der Servercursor benötigt wurde|  
|SQLFetchCount|Zahl von Abrufen, die nach SQL_PERF_START für Servercursor ausgeführt wurden|  
|CurrentStmtCount|Anzahl von Anweisungshandles, die aktuell für alle im Treiber geöffneten Verbindungen geöffnet sind|  
|MaxOpenStmt|Maximale Anzahl gleichzeitig geöffneter Anweisungshandles nach SQL_PERF_START|  
|SumOpenStmt|Anzahl von Anweisungshandles, die nach SQL_PERF_START geöffnet wurden|  
|**Verbindungsstatistiken:**||  
|CurrentConnectionCount|Aktuelle Anzahl aktiver Verbindungshandles, die die Anwendung für den Server geöffnet hat|  
|MaxConnectionsOpened|Maximale Anzahl gleichzeitig geöffneter Verbindungshandles nach SQL_PERF_START|  
|SumConnectionsOpened|Summe der Verbindungshandles, die nach SQL_PERF_START geöffnet wurden|  
|SumConnectionTime|Menge an Zeit insgesamt, die alle Verbindungen nach SQL_PERF_START geöffnet waren. Beispiel: Wenn eine Anwendung 10 Verbindungen geöffnet und jede 5 Sekunden lang offen gehalten hat, beträgt SumConnectionTime 50 Sekunden.|  
|AvgTimeOpened|Entspricht SumConnectionsOpened/SumConnectionTime|  
|**Netzwerkstatistik:**||  
|ServerRndTrips|Die Anzahl von Malen, die der Treiber Befehle an den Server gesendet und eine Antwort erhalten hat|  
|BuffersSent|Anzahl von TDS-Paketen (Tabular Data Stream), die vom Treiber nach SQL_PERF_START an [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gesendet wurden. Umfangreiche Befehle können mehrere Puffer belegen; wenn also ein umfangreicher Befehl an den Server gesendet wird und er sechs Pakete erfordert, wird ServerRndTrips um eins und BuffersSent um sechs erhöht.|  
|BuffersRec|Anzahl von TDS-Paketen, die der Treiber von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] empfangen hat, seit die Anwendung mit der Verwendung des Treibers begonnen hat.|  
|BytesSent|Anzahl von Datenbytes, die in TDS-Paketen an [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gesendet wurden, seit die Anwendung mit der Verwendung des Treibers begonnen hat.|  
|BytesRec|Anzahl von Datenbytes in TDS-Paketen, die der Treiber von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] empfangen hat, seit die Anwendung mit der Verwendung des Treibers begonnen hat.|  
  
### <a name="time-statistics"></a>Zeitstatistiken  
  
|SQLPERF-Feld|Description|  
|-------------------|-----------------|  
|msExecutionTime|Die kumulierte Verarbeitungszeit des Treibers nach SQL_PERF_START, einschließlich der Wartezeit des Treibers auf Antworten vom Server|  
|msNetworkServerTime|Die kumulierte Wartezeit des Treibers auf Antworten vom Server|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [Profilerstellung von ODBC-Treiber Leistung: Themen zur Vorgehensweise & #40; ODBC & #41;](../../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-odbc.md)  
  
  
