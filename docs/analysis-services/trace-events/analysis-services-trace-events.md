---
title: Analysis Services-Ablaufverfolgungsereignisse | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Profiler, Analysis Services
- monitoring Analysis Services [SQL Server]
- performance [Analysis Services], SQL Server Profiler
- events [Analysis Services]
- event classes [Analysis Services], about event classes
- Profiler [SQL Server Profiler], Analysis Services
- event classes [Analysis Services]
ms.assetid: 6fb219cc-f37e-437a-a544-01cec0953571
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 94ed69a366d8e9cc8a622e10176086ba1c32686e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="analysis-services-trace-events"></a>Analysis Services-Ablaufverfolgungsereignisse
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Sie können der Aktivität einer Microsoft SQL Server Analysis Services (SSAS)-Instanz verfolgen, indem Sie die von der Instanz generierten Ablaufverfolgungsereignisse erfassen und anschließend analysieren.  Ablaufverfolgungsereignisse werden so gruppiert, dass verwandte Ablaufverfolgungsereignisse einfacher gefunden werden können.  Jedes Ablaufverfolgungsereignis enthält einen Satz von Daten, der für das Ereignis relevant ist. Nicht alle Datenelemente sind für sämtliche Ereignisse von Bedeutung.  
  
 Ablaufverfolgungsereignisse können mithilfe von **[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]** gestartet und aufgezeichnet werden (siehe [Verwenden von SQL Server Profiler zum Überwachen von Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)). Alternativ können sie mit einem XMLA-Befehl als **Erweiterte Ereignisse von SQL Server** gestartet und später analysiert werden (siehe [Überwachen von Analysis Services mit den erweiterten Ereignissen von SQL Server](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)).  
  
 In den folgenden Tabellen werden jede Ereigniskategorie und die Ereignisse in dieser Kategorie beschrieben. Jede Tabelle enthält die folgenden Spalten:  
  
**Ereignis-ID**  
 Ein ganzzahliger Wert, durch den der Ereignistyp identifiziert wird. Dieser Wert ist hilfreich, wenn Sie in Tabellen oder XML-Dateien konvertierte Ablaufverfolgungen lesen, um den Ereignistyp zu filtern.  
  
**Ereignisname**  
 Der dem Ereignis in Analysis Services-Clientanwendungen zugewiesene Name.  
  
**Ereignisbeschreibung**  
 Eine kurze Beschreibung des Ereignisses.  
  
 **[Befehlsereignisse (Ereigniskategorie)](../../analysis-services/trace-events/command-events-event-category.md)**  
  
 Sammeln von Ereignissen für Befehle.  
  
|**Ereignis-ID**|**Ereignisname**|**Ereignisbeschreibung**|  
|------------------|--------------------|---------------------------|  
|15|Command Begin|Beginn des Befehls.|  
|16|Command End|Ende des Befehls.|  
  
 **[Ermittlungsereignisse-Ereigniskategorie](../../analysis-services/trace-events/discover-events-event-category.md)**  
  
 Sammeln von Ereignissen für Ermittlungsanforderungen.  
  
|**Ereignis-ID**|**Ereignisname**|**Ereignisbeschreibung**|  
|------------------|--------------------|---------------------------|  
|36|Discover Begin|Start der Ermittlungsanforderung.|  
|38|Discover End|Ende der Ermittlungsanforderung.|  
  
 **[Serverstatusermittlung (Ereigniskategorie)](../../analysis-services/trace-events/discover-server-state-event-category.md)**  
  
 Sammeln von Ereignissen für Serverstatus-Ermittlungen.  
  
|**Ereignis-ID**|**Ereignisname**|**Ereignisbeschreibung**|  
|------------------|--------------------|---------------------------|  
|33|Server State Discover Begin|Start der Serverstatusermittlung.|  
|34|Server State Discover Data|Inhalt der Antwort der Serverstatusermittlung.|  
|35|Server State Discover End|Ende der Serverstatusermittlung.|  
  
 **[Fehler und Warnungen-Ereigniskategorie](../../analysis-services/trace-events/errors-and-warnings-event-category.md)**  
  
 Sammeln von Ereignissen für Serverfehler.  
  
|**Ereignis-ID**|**Ereignisname**|**Ereignisbeschreibung**|  
|------------------|--------------------|---------------------------|  
|17|Fehler|Serverfehler.|  
  
 **[File Load- und Save-Ereigniskategorie](../../analysis-services/trace-events/file-load-and-save-event-category.md)**  
  
 Sammlung von Ereignissen für die Berichterstellung zu Dateilade- und Speichervorgängen.  
  
|**Ereignis-ID**|**Ereignisname**|**Ereignisbeschreibung**|  
|------------------|--------------------|---------------------------|  
|90|File Load Begin|Beginnt das Laden der Datei.|  
|91|File Load End|Beendet das Laden der Datei.|  
|92|File Save Begin|Beginnt das Speichern der Datei.|  
|93|File Save End|File Save End|  
|94|PageOut Begin|Beginnt den PageOut-Vorgang.|  
|95|PageOut End|PageOut End|  
|96|PageIn Begin|Beginnt den PageIn-Vorgang.|  
|97|PageIn End|PageIn End|  
  
 **[Sperren-Ereigniskategorie](../../analysis-services/trace-events/lock-events-category.md)**  
  
 Sammlung von sperrenbezogenen Ereignissen.  
  
|**Ereignis-ID**|**Ereignisname**|**Ereignisbeschreibung**|  
|------------------|--------------------|---------------------------|  
|50|Deadlock|Deadlock für Metadatensperren.|  
|51|Lock Timeout|Timeout für Metadatensperre.|  
|52|Lock Acquired|Lock Acquired|  
|53|Lock Released|Lock Released|  
|54|Lock Waiting|Lock Waiting|  
  
 **[Benachrichtigungsereignisse (Ereigniskategorie)](../../analysis-services/trace-events/notification-events-event-category.md)**  
  
 Sammeln von Benachrichtigungsereignissen.  
  
|**Ereignis-ID**|**Ereignisname**|**Ereignisbeschreibung**|  
|------------------|--------------------|---------------------------|  
|39|Benachrichtigung|Benachrichtigungsereignis.|  
|40|Benutzerdefiniert|Benutzerdefiniertes Ereignis.|  
  
 **[Fortschrittsbericht-Ereigniskategorie](../../analysis-services/trace-events/progress-reports-event-category.md)**  
  
 Sammeln von Ereignissen für Fortschrittsberichte.  
  
|**Ereignis-ID**|**Ereignisname**|**Ereignisbeschreibung**|  
|------------------|--------------------|---------------------------|  
|5|Progress Report Begin|Fortschrittsbericht beginnt.|  
|6|Progress Report End|Der Statusbericht wurde beendet.|  
|7|Progress Report Current|Der Statusbericht wird ausgeführt.|  
|8|Progress Report Error|Es ist ein Statusberichtfehler aufgetreten.|  
  
 **[Abfrageereigniskategorie](../../analysis-services/trace-events/queries-events-category.md)**  
  
 Sammeln von Ereignissen für Abfragen.  
  
|**Ereignis-ID**|**Ereignisname**|**Ereignisbeschreibung**|  
|------------------|--------------------|---------------------------|  
|9|Query Begin|Beginn der Abfrage.|  
|10|Abfrageende|Ende der Abfrage.|  
  
 **[Abfrageverarbeitung (Ereigniskategorie)](../../analysis-services/trace-events/query-processing-events-category.md)**  
  
 Sammeln von wichtigen Ereignissen während einer Abfrageausführung.  
  
|**Ereignis-ID**|**Ereignisname**|**Ereignisbeschreibung**|  
|------------------|--------------------|---------------------------|  
|70|Query Cube Begin|Beginn des Abfragecubes.|  
|71|Query Cube End|Ende des Abfragecubes.|  
|72|Calculate Non Empty Begin|Die Berechnung von nicht leeren Elementen wird gestartet.|  
|73|Calculate Non Empty Current|Die Berechnung nicht leerer Elemente wird ausgeführt.|  
|74|Calculate Non Empty End|Die Berechnung nicht leerer Elemente wird beendet.|  
|75|Serialize Results Begin|Die Serialisierung von Ergebnissen wird gestartet.|  
|76|Serialize Results Current|Die Serialisierung von Ergebnissen wird ausgeführt.|  
|77|Serialize Results End|Die Serialisierung von Ergebnissen wird beendet.|  
|78|Execute MDX Script Begin|Die Ausführung des MDX-Skripts wird gestartet.|  
|79|Execute MDX Script Current|Das MDX-Skript wird ausgeführt. Veraltet.|  
|80|Execute MDX Script End|Die Ausführung des MDX-Skripts wird beendet.|  
|81|Query Dimension|Die Abfragedimension.|  
|11|Query Subcube|Query Subcube für verwendungsbasierte Optimierung.|  
|12|Query Subcube Verbose|Query Subcube mit detaillierten Informationen. Dieses Ereignis kann sich bei Aktivierung negativ auf die Leistung auswirken.|  
|60|Get Data From Aggregation|Abfrage durch Abrufen von Daten aus der Aggregation beantworten. Dieses Ereignis kann sich bei Aktivierung negativ auf die Leistung auswirken.|  
|61|Get Data From Cache|Abfrage durch Abrufen von Daten aus einem der Caches beantworten. Dieses Ereignis kann sich bei Aktivierung negativ auf die Leistung auswirken.|  
|82|VertiPaq SE Query Begin|VertiPaq SE-Abfrage|  
|83|VertiPaq SE Query End|VertiPaq SE-Abfrage|  
|84|Resource Usage|Lese- und Schreibvorgänge für Berichte, CPU-Auslastung nach Ende von Befehlen und Abfragen.|  
|85|VertiPaq SE Query Cache Match|Cacheverwendung in VertiPaq SE-Abfrage|  
|98|Direct Query Begin|Beginn der direkten Abfrage.|  
|99|Direct Query End|Ende der direkten Abfrage.|  
  
 **[Sicherheitsüberwachung-Ereigniskategorie](../../analysis-services/trace-events/security-audit-event-category.md)**  
  
 Sammeln von Datenbanküberwachungs-Ereignisklassen.  
  
|**Ereignis-ID**|**Ereignisname**|**Ereignisbeschreibung**|  
|------------------|--------------------|---------------------------|  
|1|Audit Login|Sammelt alle neuen Verbindungsereignisse seit dem Start der Ablaufverfolgung (z. B., wenn ein Client eine Verbindung mit einem Server anfordert, auf dem eine SQL Server-Instanz ausgeführt wird).|  
|2|Audit Logout|Sammelt alle neuen Ereignisse zum Trennen einer Verbindung, die seit dem Start der Ablaufverfolgung eingetreten sind, z. B. wenn ein Client einen Befehl zum Trennen der Verbindung ausgibt.|  
|4|Audit Server Starts and Stops|Erfasst das Herunterfahren von Diensten, startet Aktivitäten und hält sie an.|  
|18|Audit Object Permission Event|Erfasst Objektberechtigungsänderungen.|  
|19|Audit Admin Operations-Ereignis|Erfasst Serversicherung/-wiederherstellung/-synchronisierung/-anfügung/-trennung/Laden von Bildern (imageload)/Speichern von Bildern (imagesave).|  
  
 [Sitzungsereignisse (Ereigniskategorie)](../../analysis-services/trace-events/session-events-event-category.md)  
  
 Sammeln von Sitzungsereignissen.  
  
|**Ereignis-ID**|**Ereignisname**|**Ereignisbeschreibung**|  
|------------------|--------------------|---------------------------|  
|41|Existing Connection|Vorhandene Benutzerverbindung.|  
|42|Vorhandene Sitzung|Vorhandene Sitzung.|  
|43|Sitzungsinitialisierung|Sitzungsinitialisierung.|  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von SQL Server Profiler zum Überwachen von Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)  
  
  
