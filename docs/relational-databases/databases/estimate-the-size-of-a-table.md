---
title: "Sch&#228;tzen der Gr&#246;&#223;e einer Tabelle | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Seiten [SQL Server], Speicherplatz"
  - "Speicherplatz [SQL Server], Tabellen"
  - "Zeilengröße [SQL Server]"
  - "Größe [SQL Server], Tabellen"
  - "Spaltengröße [SQL Server]"
  - "Vorhersagen der Tabellengröße [SQL Server]"
  - "Tabellengröße [SQL Server]"
  - "Schätzen der Tabellengröße"
  - "gruppierte Indizes, Tabellengröße"
  - "Datenträgerspeicherplatz [SQL Server], Tabellen"
  - "Speicherplatzreservierung [SQL Server], Tabellengröße"
  - "Entwerfen von Datenbanken [SQL Server], Schätzen der Größe"
  - "Reservierte freie Zeilen pro Seite [SQL Server]"
  - "Berechnen der Tabellengröße"
ms.assetid: 15c17c92-616f-402e-894b-907a296efe5f
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# Sch&#228;tzen der Gr&#246;&#223;e einer Tabelle
  Mit den folgenden Schritten können Sie den Umfang des Speicherplatzes schätzen, der zum Speichern von Daten in einer Tabelle erforderlich ist:  
  
1.  Berechnen Sie den erforderlichen Speicherplatz für den Heap oder gruppierten Index mithilfe der Anweisungen in den Artikeln [Schätzen der Größe eines Heaps](../../relational-databases/databases/estimate-the-size-of-a-heap.md) oder [Schätzen der Größe eines gruppierten Indexes](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md).  
  
2.  Den für jeden nicht gruppierten Index benötigten Speicherplatz berechnen Sie, indem Sie die Anweisungen ausführen, die Sie unter [Schätzen der Größe eines nicht gruppierten Index](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md) finden.  
  
3.  Fügen Sie die in den Schritten 1 und 2 berechneten Werte hinzu.  
  
## Siehe auch  
 [Schätzen der Größe einer Datenbank](../../relational-databases/databases/estimate-the-size-of-a-database.md)   
 [Schätzen der Größe eines Heaps](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [Schätzen der Größe eines gruppierten Indexes](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [Schätzen der Größe eines nicht gruppierten Index](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)  
  
  