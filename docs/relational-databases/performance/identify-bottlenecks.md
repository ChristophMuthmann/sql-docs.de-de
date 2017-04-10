---
title: "Identifizieren von Engp&#228;ssen | Microsoft Docs"
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
  - "Ressourcenengpässe [SQL Server]"
  - "Datenbanküberwachung [SQL Server], Engpässe"
  - "Leistung [SQL Server], Engpässe"
  - "Optimieren von Datenbanken [SQL Server], Engpässe"
  - "Überwachen der Serverleistung [SQL Server], Engpässe"
  - "Überwachen der Leistung [SQL Server], Engpässe"
  - "Datenbankleistung [SQL Server], Engpässe"
  - "Serverleistung [SQL Server], Engpässe"
  - "Engpässe [SQL Server]"
  - "Erkennen von Engpässen [SQL Server]"
ms.assetid: db079e65-ee80-4105-aec9-f8230d0d6635
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# Identifizieren von Engp&#228;ssen
  Der gleichzeitige Zugriff auf freigegebene Ressourcen verursacht Engpässe. Im Allgemeinen entstehen Engpässe in jedem Softwaresystem und sind unvermeidlich. Eine überhöhte Nachfrage nach freigegebenen Ressourcen führen jedoch zu einer schlechten Antwortzeit. Dieses Situation muss identifiziert und optimiert werden.  
  
 Mögliche Ursachen für Engpässe:  
  
-   Unzureichende Ressourcen, wodurch zusätzliche oder aktualisierte Komponenten notwendig werden.  
  
-   Ressourcen desselben Typs, auf die die Arbeitsauslastung nicht gleichmäßig verteilt wird (z. B., wenn ein Datenträger monopolisiert wird).  
  
-   Fehlerhaft funktionierende Ressourcen.  
  
-   Falsch konfigurierte Ressourcen.  
  
## Analysieren von Engpässen  
 Sehr lange Ausführungszeiten für verschiedene Ereignisse sind Anzeichen von Engpässen, die optimiert werden können.  
  
 Beispiel:  
  
-   Eine andere Komponente verhindert, dass die Arbeitsauslastung diese Komponente erreicht, wodurch die erforderliche Zeit zum Verarbeiten der Arbeitsauslastung zunimmt.  
  
-   Clientanforderungen können aufgrund einer Netzwerküberlastung länger dauern.  
  
 Es gibt die folgenden fünf Schlüsselbereiche, die Sie überwachen sollten, um die Serverleistung nachzuverfolgen und Engpässe zu identifizieren.  
  
|Mögliche Bereiche für Engpässe|Auswirkungen auf den Server|  
|------------------------------|---------------------------|  
|Speicherauslastung|Ein für Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unzureichender Arbeitsspeicherumfang beeinträchtigt die Leistung. Die Daten müssen vom Datenträger gelesen werden, anstatt direkt aus dem Datencache. Microsoft Windows-Betriebssysteme lagern zu häufig aus, indem Daten vom Datenträger hin und her übertragen werden, wenn die Seiten benötigt werden.|  
|CPU-Auslastung|Eine konstant hohe CPU-Auslastungsrate kann ein Hinweis darauf sein, dass [!INCLUDE[tsql](../../includes/tsql-md.md)]-Abfragen optimiert werden müssen oder dass ein CPU-Upgrade erforderlich ist.|  
|Datenträger-E/A|[!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfragen können optimiert werden, um unnötige E/A zu reduzieren. Dies geschieht beispielsweise durch die Verwendung von Indizes.|  
|Benutzerverbindungen|Möglicherweise greifen zu viele Benutzer gleichzeitig auf den Server zu, wodurch die Leistung beeinträchtigt wird.|  
|Blockierende Sperren|Fehlerhaft entworfene Anwendungen können zu Sperren führen und behindern die Parallelität, wodurch sich längere Antwortzeiten und niedrigere Durchsatzraten für Transaktionen ergeben.|  
  
## Siehe auch  
 [Überwachen der CPU-Auslastung](../../relational-databases/performance-monitor/monitor-cpu-usage.md)   
 [Überwachen der Datenträgerverwendung](../../relational-databases/performance-monitor/monitor-disk-usage.md)   
 [Überwachen der Speicherauslastung](../../relational-databases/performance-monitor/monitor-memory-usage.md)   
 [SQL Server, Allgemeine Statistik-Objekt](../../relational-databases/performance-monitor/sql-server-general-statistics-object.md)   
 [SQL Server, Sperren-Objekt](../../relational-databases/performance-monitor/sql-server-locks-object.md)  
  
  