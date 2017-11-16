---
title: SQL Server-XTP-Transaktionen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 443d67e4-1c7f-41d7-b18d-2d657f58c22a
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 40baae3d8967f5e4f193c1264e30749d291b0b2a
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-xtp-transactions"></a>SQL Server-XTP-Transaktionen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Das Leistungsobjekt „SQL Server-XTP-Transaktionen“ enthält Leistungsindikatoren, die sich auf Transaktionen im Zusammenhang mit In-Memory-OLTP in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]beziehen.  
  
 In dieser Tabelle werden die Leistungsindikatoren für **SQL Server-XTP-Transaktionen** beschrieben.  
  
|Leistungsindikator|Beschreibung|  
|-------------|-----------------|  
|**Abbruchweitergaben/s**|Die durchschnittliche Anzahl der Transaktionen, für die pro Sekunde aufgrund eines Commitabhängigkeits-Rollbacks ein Rollback durchgeführt wurde.|  
|**Übernommene Commitabhängigkeiten/s**|Die durchschnittliche Anzahl der Commitabhängigkeiten, die pro Sekunde von Transaktionen übernommen werden.|  
|**Vorbereitete schreibgeschützte Transaktionen/s**|Die Anzahl der schreibgeschützten Transaktionen, die pro Sekunde für die Commitverarbeitung vorbereitet wurden.|  
|**Sicherungspunktaktualisierungen/s**|Die durchschnittliche Häufigkeit pro Sekunde, mit der ein Sicherungspunkt aktualisiert wurde. Eine Sicherungspunktaktualisierung erfolgt, wenn ein vorhandener Sicherungspunkt auf den aktuellen Punkt in der Lebensdauer der Transaktion zurückgesetzt wird.|  
|**Sicherungspunkt-Rollbacks/s**|Die durchschnittliche Häufigkeit, mit der für eine Transaktion pro Sekunde ein Rollback auf einen Sicherungspunkt ausgeführt wurde.|  
|**Erstellte Sicherungspunkte/s**|Die durchschnittliche Anzahl der pro Sekunde erstellten Sicherungspunkte.|  
|**Transaktionsüberprüfungsfehler/s**|Die durchschnittliche Anzahl der Transaktionen mit fehlgeschlagener Überprüfungsverarbeitung (pro Sekunde).|  
|**Vom Benutzer abgebrochene Transaktionen/s**|Die durchschnittliche Anzahl der Transaktionen, die pro Sekunde vom Benutzer abgebrochen wurden.|  
|**Abgebrochene Transaktionen/s**|Die durchschnittliche Anzahl der Transaktionen, die pro Sekunde vom Benutzer und vom System abgebrochen wurden.|  
|**Erstellte Transaktionen/s**|Die durchschnittliche Anzahl der pro Sekunde im System erstellten Transaktionen.<br /><br /> XTP-Transaktionen werden anders als datenträgerbasierte Transaktionen gezählt (wie aus Datenbanken:Transaktionen/Sekunde ersichtlich). Beispielsweise zählt Erstellte Transaktionen/s schreibgeschützte Transaktionen, Datenbanken:Transaktionen/Sekunde hingegen nicht.|  
  
## <a name="see-also"></a>Siehe auch  
 [Leistungsindikatoren für SQL Server XTP &#40;In-Memory OLTP&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  

