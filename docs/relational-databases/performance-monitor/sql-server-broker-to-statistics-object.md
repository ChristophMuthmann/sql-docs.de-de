---
title: "SQL Server, Statistiken für das Broker-TO (Objekt) | Microsoft-Dokumentation"
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
- Broker Transmission Object object
- 'SQL Server: Broker Transmission Object'
ms.assetid: b5bc5dde-e540-4848-8aa3-5735c51df2fb
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f4c11e2b2152ac2a60f157f9d0f813c191ae02c4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-broker-to-statistics-object"></a>SQL Server, Statistiken für das Broker-TO (Objekt)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Das Leistungsobjekt „SQLServer:Statistiken für das Broker-TO“ übermittelt Informationen darüber, wie oft [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Dialoge Übertragungsobjekte anfordern, und wie oft Übertragungsobjekte in **tempdb** geschrieben werden.  
  
 Übertragungsobjekte zeichnen den Status von Nachrichtenübertragungen für einen [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Dialog auf. Sie werden im Arbeitsspeicher gespeichert. Um Arbeitsspeicher freizugeben, schreibt [!INCLUDE[ssSB](../../includes/sssb-md.md)] regelmäßig Batches inaktiver Übertragungsobjekte in Arbeitstabellen in **tempdb**.  
  
 In der folgenden Tabelle sind die in diesem Objekt enthaltenen Indikatoren aufgelistet.  
  
|Leistungsindikatoren für "Statistiken für das Broker-TO" in SQL Server|Description|  
|----------------------------------------------|-----------------|  
|**Mittlere Länge der Batchschreibvorgänge**|Die durchschnittliche Anzahl von Übertragungsobjekten, die in einem Batch gespeichert wurden.|  
|**Mittlere Schreibdauer für Batch (ms)**|Die durchschnittliche Anzahl von Millisekunden, die zur Speicherung eines Batches von Übertragungsobjekten erforderlich waren.|  
|**Mittlere Basis für Schreibdauer für Batch**|Nur zur internen Verwendung.|
|**Mittlere Zeit zwischen Batches (ms)**|Die durchschnittliche Anzahl von Millisekunden, die zwischen Speicherungen der Batches von Übertragungsobjekten verstrichen sind.|  
|**Mittlere Basis für Zeit zwischen Batches**|Nur zur internen Verwendung.| 
|**Übertragungsobjektabrufe/Sekunde**|Gibt an, wie oft pro Sekunde Dialoge Übertragungsobjekte angefordert haben.|  
|**Pro Sekunde als geändert markierte Übertragungsobjekte**|Gibt an, wie oft pro Sekunde Übertragungsobjekte als geändert markiert wurden. Übertragungsobjekte werden als geändert markiert, sobald eine Bearbeitung bewirkt, dass sich die Kopie im Arbeitsspeicher von der in **tempdb**gespeicherten Kopie unterscheidet. Übertragungsobjekte werden geändert, wenn [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine Änderung des Status von Nachrichtenübertragungen für einen Dialog aufzeichnen muss.|  
|**Schreibvorgänge für Übertragungsobjekte/Sekunde**|Gibt an, wie oft pro Sekunde Batches von Übertragungsobjekten in die **tempdb** -Arbeitstabellen geschrieben wurden. Ein große Anzahl von Schreibvorgängen kann darauf hinweisen, dass der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Arbeitsspeicher überbeansprucht wird.|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server, Zugriffsmethoden-Objekt](../../relational-databases/performance-monitor/sql-server-access-methods-object.md)   
 [SQL Server, Speicher-Manager-Objekt](../../relational-databases/performance-monitor/sql-server-memory-manager-object.md)   
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
