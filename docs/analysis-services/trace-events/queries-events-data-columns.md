---
title: Fragt Events Data Columns | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- Queries Events event category
ms.assetid: 28aa7df5-3e1f-4f4f-8a1c-8bbd29d5da13
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 48f2e8dec1939bedda904845dd2e56a237ddc10c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="queries-events-data-columns"></a>Datenspalten der Abfrageereignisse
  Die Ereigniskategorie "Abfrageereignisse" besitzt folgende Ereignisklassen:  
  
|**Ereignis-ID**|**Ereignisname**|**Ereignisbeschreibung**|  
|------------------|--------------------|---------------------------|  
|9|Query Begin|Beginn der Abfrage.|  
|10|Abfrageende|Ende der Abfrage.|  
  
 In den folgenden Tabellen sind die Datenspalten für jede dieser Ereignisklassen aufgeführt.  
  
## <a name="query-begin-classdata-columns"></a>Query Begin-Klasse – Datenspalten  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|EventSubclass|1|1|Die Ereignisunterklasse enthält zusätzliche Informationen zu jeder Ereignisklasse.<br /><br /> 0: MDXQuery<br /><br /> 1: DMXQuery<br /><br /> 2: SQLQuery<br /><br /> 3: DAXQuery|  
|CurrentTime|2|5|Enthält die aktuelle Zeit des Ereignisses (wenn verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Enthält den Zeitpunkt, zu dem das Ereignis begonnen hat, falls verfügbar. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|ConnectionID|25|1|Enthält die mit dem Abfrageereignis verbundene eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Enthält den Namen der Datenbank, in der die Abfrage ausgeführt wird.|  
|NTUserName|32|8|Enthält den mit dem Abfrageereignis verbundenen Windows-Benutzernamen.|  
|NTDomainName|33|8|Enthält den mit dem Abfrageereignis verbundenen Windows-Domänennamen.|  
|ClientProcessID|36|1|Enthält die Prozess-ID der Clientanwendung.|  
|ApplicationName|37|8|Enthält den Namen der Clientanwendung, die die Verbindung mit dem Server hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|  
|SessionID|39|8|Enthält die eindeutige Sitzungs-ID der XMLA-Anforderung.|  
|NTCanonicalUserName|40|8|Enthält den mit dem Abfrageereignis verbundenen Windows-Benutzernamen. Der Benutzername liegt im kanonischen Format vor. Beispiel: engineering.microsoft.com/software/user.|  
|SPID|41|1|Enthält die SPID (Server Process ID), die die mit dem Abfrageereignis verbundene Benutzersitzung eindeutig kennzeichnet. Die SPID entspricht direkt dem von XMLA verwendeten Sitzungs-GUID.|  
|TextData|42|9|Enthält die mit dem Abfrageereignis verbundenen Textdaten.|  
|ServerName|43|8|Enthält den Namen der Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , in der das Abfrageereignis aufgetreten ist.|  
|RequestParameters|44|9|Enthält die Parameter für parametrisierte Abfragen und Befehle, die dem Abfrageereignis zugeordnet sind.|  
|RequestProperties|45|9|Enthält die Eigenschaften der XMLA-Anforderung.|  
  
## <a name="query-end-classdata-columns"></a>Query End-Klasse – Datenspalten  
  
|**Spaltenname**|**Spalten-ID**|**Spaltentyp**|**Spaltenbeschreibung**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|Die Ereignisklasse dient zur Kategorisierung von Ereignissen.|  
|EventSubclass|1|1|Die Ereignisunterklasse enthält zusätzliche Informationen zu jeder Ereignisklasse.<br /><br /> 0: MDXQuery<br /><br /> 1: DMXQuery<br /><br /> 2: SQLQuery<br /><br /> 3: DAXQuery|  
|CurrentTime|2|5|Enthält die aktuelle Zeit des Ereignisses (wenn verfügbar). Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|StartTime|3|5|Enthält den Zeitpunkt, zu dem das Ereignis begonnen hat, falls verfügbar. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|EndTime|4|5|Enthält die Uhrzeit, zu der das Ereignis beendet wurde. Diese Spalte wird für Startereignisklassen (z. B. SQL:BatchStarting oder SP:Starting) nicht aufgefüllt. Für das Filtern lauten die erwarteten Formate "JJJJ-MM-TT" und "JJJJ-MM-TT HH:MM:SS".|  
|Dauer|5|2|Enthält die abgelaufene Zeit (in Millisekunden), die für das Ereignis benötigt wurde.|  
|CPUTime|6|2|Enthält die CPU-Zeit (in Millisekunden), die vom Ereignis verwendet wurde.|  
|Severity|22|1|Enthält den Schweregrad einer mit dem Abfrageereignis verbundenen Ausnahme. Die Werte sind:<br /><br /> 0 = Erfolg<br /><br /> 1 = Information<br /><br /> 2 = Warnung<br /><br /> 3 = Fehler|  
|Success|23|1|Enthält den Erfolg oder Fehler des Abfrageereignisses. Die Werte sind:<br /><br /> 0 = Fehler<br /><br /> 1 = Erfolg|  
|Fehler|24|1|Enthält die Fehlernummer aller mit dem Abfrageereignis verbundenen Fehler.|  
|ConnectionID|25|1|Enthält die mit dem Abfrageereignis verbundene eindeutige Verbindungs-ID.|  
|DatabaseName|28|8|Enthält den Namen der Datenbank, in der die Abfrage ausgeführt wird.|  
|NTUserName|32|8|Enthält den mit dem Abfrageereignis verbundenen Windows-Benutzernamen.|  
|NTDomainName|33|8|Enthält den mit dem Abfrageereignis verbundenen Windows-Domänennamen.|  
|ClientProcessID|36|1|Enthält die Prozess-ID der Clientanwendung.|  
|ApplicationName|37|8|Enthält den Namen der Clientanwendung, die die Verbindung mit dem Server hergestellt hat. Diese Spalte wird mit den Werten aufgefüllt, die von der Anwendung übergeben werden, und nicht mit dem angezeigten Namen des Programms.|  
|SessionID|39|8|Enthält die eindeutige Sitzungs-ID der XMLA-Anforderung.|  
|NTCanonicalUserName|40|8|Enthält den mit dem Abfrageereignis verbundenen Windows-Benutzernamen. Der Benutzername liegt im kanonischen Format vor. Beispiel: engineering.microsoft.com/software/user.|  
|SPID|41|1|Enthält die SPID (Server Process ID), die die mit dem Abfrageereignis verbundene Benutzersitzung eindeutig kennzeichnet. Die SPID entspricht direkt dem von XMLA verwendeten Sitzungs-GUID.|  
|TextData|42|9|Enthält die mit dem Abfrageereignis verbundenen Textdaten.|  
|ServerName|43|8|Enthält den Namen der Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , in der das Abfrageereignis aufgetreten ist.|  
  
## <a name="see-also"></a>Siehe auch  
 [Abfrageereigniskategorie](../../analysis-services/trace-events/queries-events-category.md)  
  
  
