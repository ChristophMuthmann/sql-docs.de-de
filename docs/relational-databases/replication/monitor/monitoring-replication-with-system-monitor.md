---
title: "&#220;berwachen der Replikation mit dem Systemmonitor | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Überwachen der Leistung [SQL Server-Replikation], Systemmonitor"
  - "Systemmonitor [SQL Server], Replikation"
  - "Leistungsindikatoren [SQL Server-Replikation]"
ms.assetid: 8cd3a270-0328-4bfd-bf23-b1d759cc120c
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# &#220;berwachen der Replikation mit dem Systemmonitor
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows-Systemmonitor ermöglicht Ihnen die Verwendung von Grafiken, Diagramme und Berichte zum Beurteilen der Effizienz des Computers zu identifizieren und beheben mögliche Probleme (z. B. unausgeglichene Ressourcenverwendung, unzureichende Hardware oder schlechten Programmentwurf) und um zusätzlichen Hardwarebedarf zu planen. Weitere Informationen finden Sie unter [Überwachen der Ressourcenauslastung & #40; Systemmonitor & #41;](../../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md).  
  
 Der Systemmonitor verwendet Leistungsobjekte und -indikatoren, die Informationen zur Leistung verschiedener Prozesse bereitstellen. Die Replikationsleistung kann mithilfe von Indikatoren gemessen werden, die den Replikations-Agents zugeordnet sind.  
  
|Agent|Leistungsobjekt|Leistungsindikator|Beschreibung|  
|-----------|------------------------|-------------|-----------------|  
|Alle Agents|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replikations-Agents|Wird ausgeführt|Die Anzahl der Replikations-Agents, die gerade ausgeführt werden.|  
|Momentaufnahme-Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replikationsmomentaufnahme|Momentaufnahme: Übermittelte Befehle/Sekunde|Die Anzahl der Befehle, die pro Sekunde an den Verteiler übermittelt wurden.|  
|Momentaufnahme-Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replikationsmomentaufnahme|Momentaufnahme: Übermittelte Transaktionen/Sekunde|Die Anzahl der Transaktionen, die pro Sekunde an den Verteiler übermittelt wurden.|  
|Protokolllese-Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replikationsprotokollleser|Protokollleser: Übermittelte Befehle/Sekunde|Die Anzahl der Befehle, die pro Sekunde an den Verteiler übermittelt wurden.|  
|Protokolllese-Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replikationsprotokollleser|Protokollleser: Übermittelte Transaktionen/Sekunde|Die Anzahl der Transaktionen, die pro Sekunde an den Verteiler übermittelt wurden.|  
|Protokolllese-Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replikationsprotokollleser|Protokollleser: Latenzzeit für Übermittlung|Die aktuelle Zeitspanne (in Millisekunden), die vom Zeitpunkt der Übernahme von Transaktionen auf dem Verleger bis zu ihrer Übermittlung an den Verteiler verstrichen ist.|  
|Verteilungs-Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replikationsverteilung|Verteiler: Übermittelte Befehle/Sekunde|Die Anzahl der Befehle, die pro Sekunde an den Abonnenten übermittelt wurden.|  
|Verteilungs-Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replikationsverteilung|Verteiler: Übermittelte Transaktionen/Sekunde|Die Anzahl der Transaktionen, die pro Sekunde an den Abonnenten übermittelt wurden.|  
|Verteilungs-Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replikationsverteilung|Verteiler: Latenzzeit für Übermittlung|Die aktuelle Zeitspanne (in Millisekunden), die vom Zeitpunkt der Übermittlung von Transaktionen an den Verteiler bis zu ihrer Übernahme auf dem Abonnenten verstrichen ist.|  
|Merge-Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replikationsmerge|Konflikte/Sekunde|Die Anzahl der Konflikte pro Sekunde, die im Rahmen des Mergevorgangs aufgetreten sind.|  
|Merge-Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replikationsmerge|Änderungen per Download/Sekunde|Die Anzahl der Zeilen, die pro Sekunde vom Verleger auf den Abonnenten repliziert wurden.|  
|Merge-Agent|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replikationsmerge|Änderungen per Upload/Sekunde|Die Anzahl der Zeilen, die pro Sekunde vom Abonnenten auf den Verleger repliziert wurden.|  
  
## Siehe auch  
 [Überwachung & #40; Replikation & #41;](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  