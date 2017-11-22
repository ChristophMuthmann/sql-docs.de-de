---
title: "Leistungsindikatoren für SQL Server XTP (In-Memory OLTP) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 04/06/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fe3cbaf4-65f4-44c5-acc6-7b735cda0c5d
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 30850b8749e062d47c5c89fd28cc140e05610967
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-xtp-in-memory-oltp-performance-counters"></a>Leistungsindikatoren für SQL Server XTP (In-Memory OLTP)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bietet Objekte und Leistungsindikatoren, die vom Systemmonitor zum Überwachen der In-Memory OLTP-Aktivität verwendet werden können. Die Objekte und Leistungsindikatoren sind für alle Instanzen einer bestimmten Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf dem Computer freigegeben, beginnend mit [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
 In der Vergangenheit begann die Namen von Objekten und Leistungsindikatoren mit *XTP*, wie in **XTP-Cursors**. Ab jetzt beginnen die Namen mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]und entsprechen folgendem Muster:  
  
-   **SQL Server** *\<Version>* **XTP-Cursor**  
  
 Der Wert für *\<Version>* ist z.B. 2016.  
  
##  <a name="SQLServerPOs"></a> SQL Server-XTP-Leistungsobjekte  
 In der folgenden Tabelle werden diese [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Leistungsobjekte beschrieben.  
  
|Leistungsobjekt|Beschreibung|  
|------------------------|-----------------|  
|[SQL Server-XTP-Cursor](../../relational-databases/performance-monitor/sql-server-xtp-cursors.md)|Das Leistungsobjekt für SQL Server-XTP-Cursors enthält Leistungsindikatoren für interne Cursor des In-Memory-OLTP-Moduls. Cursor sind die Bausteine auf unterer Ebene, die das In-Memory-OLTP-Modul zur Verarbeitung von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfragen verwendet. Daher können Sie diese in der Regel nicht direkt steuern.|  
|[SQL Server XTP-Datenbanken](../../relational-databases/performance-monitor/sql-server-xtp-databases.md)|Das Leistungsobjekt „SQL Server XTP-Datenbanken“ stellt spezielle Leistungsindikatoren für In-Memory-OLTP-Datenbanken bereit.|  
|[SQL Server-XTP Garbage Collection](../../relational-databases/performance-monitor/sql-server-xtp-garbage-collection.md)|Das SQL Server-XTP-Leistungsobjekt für die Garbage Collection enthält Leistungsindikatoren für die Garbage Collection des In-Memory-OLTP-Moduls.|  
|[SQL Server 2016 XTP IO Governor](../../relational-databases/performance-monitor/sql-server-xtp-io-governor.md)|Das Leistungsobjekt „SQL Server 2016 XTP IO Governor“ enthält Leistungsindikatoren, die sich auf den In-Memory OLTP IO Rate Governor beziehen.|
|[SQL Server XTP-Phantomprozessor](../../relational-databases/performance-monitor/sql-server-xtp-phantom-processor.md)|Das SQL Server-XTP-Leistungsobjekt „Phantomprozessor“ enthält Leistungsindikatoren, die sich auf das zur Phantomverarbeitung verwendete Subsystem des In-Memory-OLTP-Moduls beziehen. Diese Komponente ist dafür verantwortlich, Phantomzeilen in Transaktionen zu erkennen, die auf der SERIALIZABLE-Isolationsstufe ausgeführt werden.|  
|[SQL Server-XTP-Speicher](../../relational-databases/performance-monitor/sql-server-xtp-storage.md)|Das Leistungsobjekt „SQL Server-XTP-Speicher“ enthält Leistungsindikatoren für den In-Memory-OLTP-Speicher in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[XTP-Transaktionsprotokoll für SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-transaction-log.md)|Das Leistungsobjekt „SQL Server-XTP-Transaktionsprotokoll“ enthält Leistungsindikatoren für die In-Memory-OLTP-Transaktionsprotokollierung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[SQL Server-XTP-Transaktionen](../../relational-databases/performance-monitor/sql-server-xtp-transactions.md)|Das Leistungsobjekt „SQL Server-XTP-Transaktionen“ enthält Leistungsindikatoren für die In-Memory-OLTP-Modultransaktionen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
  
