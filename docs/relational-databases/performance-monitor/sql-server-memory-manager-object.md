---
title: "SQL Server, Speicher-Manager-Objekt | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQLServer:Speicher-Manager"
  - "Speicher-Manager-Objekt"
ms.assetid: dbf49000-eeb0-4e9c-a361-5092363920dc
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# SQL Server, Speicher-Manager-Objekt
  Das **Speicher-Manager** -Objekt in Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt Leistungsindikatoren bereit, mit denen Sie die gesamte Speicherauslastung des Servers überwachen können. Das Überwachen der gesamten Speicherauslastung des Servers zur Messung der Benutzeraktivität und der Ressourcennutzung kann Ihnen dabei helfen, Leistungsengpässe zu erkennen. Durch Überwachen des Arbeitsspeichers, der von einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet wird, können Sie Folgendes ermitteln:  
  
-   Ob es zu Engpässen kommt, da nicht genügend Arbeitsspeicher vorhanden ist, um Daten, auf die häufig zugegriffen wird, im Cache zu speichern. In diesem Fall muss [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Daten vom Datenträger abrufen.  
  
-   Ob die Abfrageleistung durch Hinzufügen von Arbeitsspeicher oder durch Zuordnen von zusätzlichem Arbeitsspeicher für den Datencache bzw. für interne Strukturen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verbessert werden kann.  
  
## Speicher-Manager-Leistungsindikatoren  
 In dieser Tabelle werden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Speicher-Manager** beschrieben.  
  
|Speicher-Manager-Leistungsindikatoren von SQL Server|Beschreibung|  
|----------------------------------------|-----------------|  
|**Verbindungsspeicher (KB)**|Gibt den Gesamtumfang des dynamischen Arbeitsspeichers an, den der Server für die Aufrechterhaltung von Verbindungen verwendet.|  
|**Datenbankcachespeicher (KB)**|Gibt den Umfang des Arbeitsspeichers an, den der Server derzeit für den Datenbankseitencache verwendet.|  
|**Externer Speichernutzen**|Der externe Wert des Arbeitsspeichers (in ms pro Seite pro ms) multipliziert mit 10 Milliarden und auf eine ganze Zahl gekürzt.| 
|**Freier Arbeitsspeicher (KB)**|Gibt den Umfang des zugesicherten Arbeitsspeichers an, der derzeit nicht vom Server verwendet wird.|  
|**Zugewiesener Arbeitsbereichsspeicher (KB)**|Gibt den Gesamtumfang des Arbeitsspeichers an, der derzeit dem Ausführen von Prozessen, z. B. Hash-, Sortier-, Massenkopier- und Indexerstellungsvorgängen, zugewiesen ist.|  
|**Sperrblöcke**|Gibt die aktuelle Anzahl der Sperrblöcke an, die auf dem Server verwendet werden. Wird regelmäßig aktualisiert. Ein Sperrblock stellt eine einzelne gesperrte Ressource, wie z. B. eine Tabelle, Seite oder Zeile, dar.|  
|**Zugeordnete Sperrblöcke**|Gibt die aktuelle Anzahl der zugeordneten Sperrblöcke an. Beim Starten des Servers hängt die Anzahl der zugeordneten Sperrblöcke plus die Anzahl der zugeordneten Sperrenbesitzerblöcke von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **-Konfigurationsoption von** ab. Wenn mehr Sperrblöcke benötigt werden, steigt der Wert.|  
|**Sperrspeicher (KB)**|Gibt den Gesamtumfang des dynamischen Arbeitsspeichers an, den der Server für Sperren verwendet.|  
|**Sperrenbesitzerblöcke**|Gibt die Anzahl der Sperrenbesitzerblöcke an, die zurzeit auf dem Server verwendet werden. Wird regelmäßig aktualisiert. Ein Sperrenbesitzerblock stellt den Besitz einer Sperre für ein Objekt durch einen einzelnen Thread dar. Wenn also drei Threads jeweils über eine freigegebene Sperre (S) für eine Seite verfügen, liegen drei Sperrenbesitzerblöcke vor.|  
|**Zugeordnete Sperrenbesitzerblöcke**|Gibt die aktuelle Anzahl der zugeordneten Sperrenbesitzerblöcke an. Beim Starten des Servers hängt die Anzahl der zugeordneten Sperrenbesitzerblöcke und die Anzahl der zugeordneten Sperrblöcke von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **-Konfigurationsoption von** ab. Wenn mehr Sperrenbesitzerblöcke benötigt werden, steigt der Wert dynamisch an.|  
|**Protokollpoolspeicher (KB)**|Die Gesamtkapazität des dynamischen Speichers, den der Server für den Protokollpool verwendet.| 
|**Maximaler Arbeitsbereichsspeicher (KB)**|Gibt den maximalen Umfang des Arbeitsspeichers an, der für das Ausführen von Prozessen, z. B. Hash-, Sortier,- Massenkopier- und Indexerstellungsvorgängen, zur Verfügung steht.|  
|**Ausstehende Speicherzuweisungen**|Gibt die Gesamtanzahl der Prozesse an, die erfolgreich eine Zuweisung für Arbeitsbereichsspeicher erhalten haben.|  
|**Ausstehende Speicherzuweisungen**|Gibt die Gesamtanzahl der Prozesse an, die auf eine Zuweisung von Arbeitsbereichsspeicher warten.|  
|**Optimiererspeicher (KB)**|Gibt den Gesamtumfang des dynamischen Arbeitsspeichers an, den der Server für die Abfrageoptimierung verwendet.|  
|**Reservierter Serverarbeitsspeicher (KB)**|Gibt den Umfang des Arbeitsspeichers an, den der Server für die zukünftige Verwendung reserviert hat. Dieser Leistungsindikator gibt den derzeit nicht verwendeten Umfang des ursprünglich zugewiesenen Arbeitsspeichers an, der in **Erteilter Arbeitsbereichsspeicher (KB)** angezeigt wird.|  
|**SQL-Cachespeicher (KB)**|Gibt den Gesamtumfang des dynamischen Arbeitsspeichers an, den der Server für den dynamischen SQL-Cache verwendet.|  
|**Gestohlener Serverarbeitsspeicher (KB)**|Gibt den Umfang des Arbeitsspeichers an, den der Server derzeit für andere Zwecke als Datenbankseiten verwendet.|  
|**Zielserverspeicher (KB)**|Gibt den idealen Umfang des Arbeitsspeichers an, den der Server belegen kann.|  
|**Serverspeicher gesamt (KB)**|Gibt den Umfang des Arbeitsspeichers an, den der Server mit dem Speicher-Manager zugesichert hat.|  
  
## Siehe auch  
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, Puffer-Manager-Objekt](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
[sys.dm_os_performance_counters (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  