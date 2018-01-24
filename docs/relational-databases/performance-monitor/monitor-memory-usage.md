---
title: "Überwachen der Speicherauslastung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- tuning databases [SQL Server], memory
- monitoring server performance [SQL Server], memory usage
- isolating memory [SQL Server]
- paging rate [SQL Server]
- memory [SQL Server], monitoring usage
- monitoring [SQL Server], memory usage
- low-memory conditions
- database monitoring [SQL Server], memory usage
- available memory [SQL Server]
- page faults [SQL Server]
- monitoring performance [SQL Server], memory usage
- server performance [SQL Server], memory
ms.assetid: 1aee3933-a11c-4b87-91b7-32f5ea38c87f
caps.latest.revision: "26"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 18061fa8a59ab5cd5d86a7505162e5148767b9c7
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="monitor-memory-usage"></a>Überwachen der Speicherauslastung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sollten regelmäßig überwacht werden, um sicherzustellen, dass sich die Speicherauslastung im normalen Bereich bewegt.  
  
 Um den Arbeitsspeicherstatus niedrig zu halten, verwenden Sie bei der Überwachung folgende Objektleistungsindikatoren:  
  
-   **Arbeitsspeicher: Verfügbare Bytes**  
  
-   **Arbeitsspeicher: Seiten/s**  
  
 Der **Verfügbare Bytes** -Leistungsindikator gibt an, wie viele Bytes an Arbeitsspeicher derzeit für die Verwendung durch Prozesse verfügbar sind. Der Indikator **Seiten/s** gibt die Anzahl der Seiten an, die entweder aufgrund von harten Seitenfehlern vom Datenträger abgerufen oder auf den Datenträger geschrieben wurden, um Speicherplatz im Arbeitssatz aufgrund von Seitenfehlern freizugeben.  
  
 Niedrige Werte für den **Verfügbare Bytes** -Leistungsindikator können ein Anzeichen dafür sein, dass insgesamt zu wenig Arbeitsspeicher auf dem Computer vorhanden ist oder dass eine Anwendung keinen Arbeitsspeicher freigibt. Ein hoher Wert für den Indikator **Seiten/s** kann auf überhöhte Auslagerungen hindeuten. Überwachen Sie den Indikator **Speicher: Seitenfehler/s** , um sicherzustellen, dass die Datenträgeraktivität nicht durch Auslagern verursacht wird.  
  
 Ein geringes Maß an Auslagerungen (und somit an Seitenfehlern) ist normal, selbst wenn der Computer über ausreichend Arbeitsspeicher verfügt. Der Microsoft-Manager für virtuellen Arbeitsspeicher (VMM, Virtual Memory Manager) entnimmt Seiten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und anderen Prozessen, um die Größen der Workingsets dieser Prozesse anzupassen. Infolge der VMM-Aktivität kommt es häufig zu Seitenfehlern. Sie sollten den Indikator [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Prozess: Seitenfehler/s **der** -Prozessinstanz überprüfen, um zu ermitteln, ob die überhöhten Auslagerungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder einem anderen Prozess verursacht werden.  
  
 Weitere Informationen zum Auflösen überhöhter Auslagerungen finden Sie in der Dokumentation des Windows-Betriebssystems.  
  
## <a name="isolating-memory-used-by-sql-server"></a>Isolieren des von SQL Server verwendeten Arbeitsspeichers  
 In der Standardkonfiguration werden Arbeitsspeicheranforderungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] basierend auf den verfügbaren Systemressourcen dynamisch geändert. Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mehr Arbeitsspeicher benötigt, wird das Betriebssystem nach der Verfügbarkeit von freiem physischem Arbeitsspeicher abgefragt. Anschließend wird der verfügbare Arbeitsspeicher verwendet. Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] den derzeit zugeordneten Arbeitsspeicher nicht benötigt, wird der Arbeitsspeicher für das Betriebssystem freigegeben. Sie können die Option zur dynamischen Verwendung des Arbeitsspeichers jedoch auch mithilfe der Serverkonfigurationsoptionen **minservermemory**und **maxservermemory** überschreiben. Weitere Informationen finden Sie unter [Arbeitsspeicheroptionen für den Server](../../database-engine/configure-windows/server-memory-server-configuration-options.md).  
  
 Um die Menge des von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendeten Arbeitsspeichers zu überwachen, sollten Sie die folgenden Leistungsindikatoren überprüfen:  
  
-   **Prozess: Arbeitsseiten**  
  
-   **SQL Server: Puffer-Manager: Puffercache-Trefferquote**  
  
-   **SQL Server: Puffer-Manager: Datenbankseiten**  
  
-   **SQL Server: Speicher-Manager: Serverspeicher gesamt (KB)**  
  
 Der Indikator **WorkingSet** gibt die Menge an Arbeitsspeicher an, die von einem Prozess verwendet wird. Wenn dieser Wert konstant unter der Menge an Arbeitsspeicher liegt, die in den Serveroptionen **Min. Serverarbeitsspeicher** und **Max. Serverarbeitsspeicher** festgelegt ist, wurde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] so konfiguriert, dass zu viel Arbeitsspeicher beansprucht wird.  
  
 Der **Puffercache-Trefferquote** -Leistungsindikator ist anwendungsspezifisch. Eine Rate von 90 Prozent oder höher ist jedoch wünschenswert. Fügen Sie so lange Arbeitsspeicher hinzu, bis der Wert konstant über 90 Prozent liegt. Ein Wert von über 90 Prozent gibt an, dass mehr als 90 Prozent aller Datenanforderungen vom Datencache erfüllt wurden.  
  
 Wenn der Indikator **TotalServerMemory (KB)** gegenüber der auf dem Computer verfügbaren Menge an physischem Arbeitsspeicher konstant hoch ist, kann dies bedeuten, dass zusätzlicher Arbeitsspeicher erforderlich ist.  
  
## <a name="determining-current-memory-allocation"></a>Bestimmen der aktuellen Speicherbelegung  
 Mit der folgenden Abfrage werden Informationen zur aktuellen Speicherbelegung zurückgegeben.  
  
```  
SELECT  
(physical_memory_in_use_kb/1024) AS Memory_usedby_Sqlserver_MB,  
(locked_page_allocations_kb/1024) AS Locked_pages_used_Sqlserver_MB,  
(total_virtual_address_space_kb/1024) AS Total_VAS_in_MB,  
process_physical_memory_low,  
process_virtual_memory_low  
FROM sys.dm_os_process_memory;  
```  
  
  
