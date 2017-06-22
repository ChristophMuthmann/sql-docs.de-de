---
title: Leistung (Ereigniskategorie) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server event classes, Performance event category
- Performance event category [SQL Server]
- event classes [SQL Server], Performance event category
ms.assetid: 708f3585-d8be-4980-bbff-672d7c59397e
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c74104068ce59f26b98d30b9e5af31704347d14a
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="performance-event-category"></a>Leistung (Ereigniskategorie)
  Verwenden Sie die **Leistung** -Ereigniskategorie zum Überwachen von **Showplan** -Ereignisklassen und von Ereignisklassen, die durch das Ausführen von SQL-DML-Operatoren (SQL Data Manipulation Language) erzeugt werden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Beschreibung|  
|-----------|-----------------|  
|[Auto Stats-Ereignisklasse](../../relational-databases/event-classes/auto-stats-event-class.md)|Gibt an, dass eine automatische Aktualisierung der Index- und Spaltenstatistiken aufgetreten ist.|  
|[Degree of Parallelism &#40;7.0 Insert&#41;-Ereignisklasse](../../relational-databases/event-classes/degree-of-parallelism-7-0-insert-event-class.md)|Zeigt an, dass von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine SELECT-, INSERT-, UPDATE- oder DELETE-Anweisung mit einem seriellen oder parallelen Plan ausgeführt wurde. Darüber hinaus wird die Anzahl der CPUs, die für den Vorgang verwendet wurden, zurückgegeben.|  
|[Performance Statistics-Ereignisklasse](../../relational-databases/event-classes/performance-statistics-event-class.md)|Überwacht die Leistung der Abfragen, die ausgeführt werden.|  
|[Showplan All (Ereignisklasse)](../../relational-databases/event-classes/showplan-all-event-class.md)|Identifiziert **Showplan** -Operatoren in einer SQL-Anweisung.|  
|[Showplan All for Query Compile-Ereignisklasse](../../relational-databases/event-classes/showplan-all-for-query-compile-event-class.md)|Zeigt Kompilierzeitdaten für **Showplan** -Operatoren an.|  
|[Showplan Statistics Profile (Ereignisklasse)](../../relational-databases/event-classes/showplan-statistics-profile-event-class.md)|Zeigt die geschätzten Kosten einer Abfrage an.|  
|[Showplan XML (Ereignisklasse)](../../relational-databases/event-classes/showplan-xml-event-class.md)|Identifiziert die **Showplan** -Operatoren in einer SQL-Anweisung. Die Ereignisklasse speichert jedes Ereignis als definiertes XML-Dokument.|  
|[Showplan XML for Query Compile (Ereignisklasse)](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md)|Zeigt Kompilierzeitdaten für **Showplan** -Operatoren im XML-Format an.|  
|[Showplan XML Statistics Profile-Ereignisklasse](../../relational-databases/event-classes/showplan-xml-statistics-profile-event-class.md)|Identifiziert die einer SQL-Anweisung zugeordneten **Showplan** -Operatoren. Die Ausgabe erfolgt als XML-Dokument.|  
|[SQL:FullTextQuery-Ereignisklasse](../../relational-databases/event-classes/sql-fulltextquery-event-class.md)|Gibt an, dass in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Volltextabfrage ausgeführt wurde.|  
|[Plan Guide Successful (Ereignisklasse)](../../relational-databases/event-classes/plan-guide-successful-event-class.md)|Zeigt an, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erfolgreich einen Ausführungsplan für eine Abfrage oder einen Batch mit einer Planhinweisliste erzeugt hat.|  
|[Plan Guide Unsuccessful (Ereignisklasse)](../../relational-databases/event-classes/plan-guide-unsuccessful-event-class.md)|Zeigt an, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keinen Ausführungsplan für eine Abfrage oder einen Batch mit einer Planhinweisliste erzeugen konnte.|  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)  
  
  
