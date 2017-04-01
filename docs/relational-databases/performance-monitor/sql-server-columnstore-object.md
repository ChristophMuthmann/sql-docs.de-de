---
title: "SQL Server, Columnstore-Objekt | Microsoft Docs"
ms.custom: ""
ms.date: "04/12/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ae663a49-012f-4ffe-a332-f03157843052
caps.latest.revision: 8
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 8
---
# SQL Server, Columnstore-Objekt
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Das **SQLServer:Columnstore**-Objekt bietet Leistungsindikatoren zum Überwachen der Ausführung des Columnstore-Index in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Die folgende Tabelle beschreibt die **Columnstore**-Leistungsindikatoren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Columnstore-Leistungsindikatoren|Beschreibung|  
|--------------------------|-----------------|  
|**Geschlossene Delta-Zeilengruppen**|Die Anzahl von geschlossenen Delta-Zeilengruppen.|  
|**Komprimierte Delta-Zeilengruppen**|Die Anzahl von komprimierten Delta-Zeilengruppen.|  
|**Erstellte Delta-Zeilengruppen**|Die Anzahl von erstellten Delta-Zeilengruppen.|  
|**Segmentcache-Trefferquote**|Der Prozentsatz der Spaltensegmente, die im Columnstore-Pool gefunden wurden, ohne dass ein Lesevorgang vom Datenträger erforderlich war.|  
|**Basis für Segmentcache-Trefferquote**|Nur zur internen Verwendung.|
|**Segmentlesevorgänge/Sek.**|Die Anzahl von ausgegebenen physischen Segmentlesevorgängen.|  
|**Migrierte Löschpuffer gesamt**|Die Anzahl von Bereinigungen des Löschpuffers durch den Tupelverschiebungsvorgang.|  
|**Auswertungen der Zusammenführungsrichtlinie gesamt**|Die Anzahl von Auswertungen der Zusammenführungsrichtlinie für den Columnstore.|  
|**Komprimierte Zeilengruppen gesamt**|Die Gesamtzahl von komprimierten Zeilengruppen.|  
|**Zeilengruppen bereit für Zusammenführung gesamt**|Die Anzahl von Quellzeilengruppen, die seit dem Start von SQL Server für MERGE bereit sind.|  
|**Komprimierte zusammengeführte Zeilengruppen gesamt**|Die Anzahl von komprimierten Zielzeilengruppen, die seit dem Start von SQL Server mit MERGE erstellt wurden.|  
|**Zusammengeführte Quellzeilengruppen gesamt**|Die Anzahl von Quellzeilengruppen, die seit dem Start von SQL Server zusammengeführt wurden.|  
  
## Siehe auch  
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  