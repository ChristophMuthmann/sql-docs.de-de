---
title: SQL Server XTP-Phantomprozessor | Microsoft-Dokumentation
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
ms.assetid: 0f691b3d-a8fd-4459-ad21-2cfc8574a8c0
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ec14c4271d2dd6e73fe21f8ce9a4a1ef8e6f7ee3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-xtp-phantom-processor"></a>SQL Server XTP-Phantomprozessor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Das SQL Server-XTP-Leistungsobjekt „Phantomprozessor“ enthält Leistungsindikatoren, die sich auf den für das zur Phantomverarbeitung verwendete Subsystem des XTP-Moduls beziehen. Diese Komponente ist dafür verantwortlich, Phantomzeilen in Transaktionen zu erkennen, die auf der SERIALIZABLE-Isolationsstufe ausgeführt werden sowie Einschränkungsvalidierung in Parallelitätsszenarios.  
  
 In dieser Tabelle werden die Leistungsindikatoren für **SQL Server-XTP-Phantomprozessor** beschrieben.  
  
|Leistungsindikator|Beschreibung|  
|-------------|-----------------|  
|**Dusty-Corner-Scanwiederholungen/s (durch Phantom ausgegeben)**|Die durchschnittliche Anzahl von Scanwiederholungen aufgrund von Schreibkonflikten während Dusty-Corner-Sweep-Vorgängen, die pro Sekunde durch den Phantomprozessor ausgegeben werden. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|  
|**Entfernte abgelaufene Phantomzeilen/s**|Die durchschnittliche Anzahl abgelaufener Zeilen, die pro Sekunde von Phantomscans entfernt werden.|  
|**Berührte abgelaufene Phantomzeilen/s**|Die durchschnittliche Anzahl abgelaufener Zeilen, die pro Sekunde von Phantomscans berührt werden.|  
|**Berührte ablaufende Phantomzeilen/s**|Die durchschnittliche Anzahl ablaufender Zeilen, die pro Sekunde von Phantomscans berührt werden.|  
|**Berührte Phantomzeilen/s**|Die durchschnittliche Anzahl von Zeilen, die pro Sekunde von Phantomscans berührt werden.|  
|**Gestartete Phantomscans/s**|Die durchschnittliche Anzahl der pro Sekunde gestarteten Phantomscans.|  
  
## <a name="see-also"></a>Siehe auch  
 [Leistungsindikatoren für SQL Server XTP &#40;In-Memory OLTP&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
