---
title: "Zusammenfassung der PolyBase-Funktionen mit Versionsangabe | Microsoft Docs"
ms.custom: ""
ms.date: "04/13/2016"
ms.prod: "sql-non-specified"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6591994d-6109-4285-9c5b-ecb355f8a111
caps.latest.revision: 10
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 8
---
# Zusammenfassung der PolyBase-Funktionen mit Versionsangabe
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Zusammenfassung der PolyBase-Funktionen, die für SQL Server-Produkte und -Dienste verfügbar sind.  
  
## Zusammenfassung der Funktionen für Produktversionen  
 In dieser Tabelle sind die wichtigsten Funktionen für PolyBase sowie die Produkte zusammengefasst, in denen sie verfügbar sind.  
  
### [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
 Diese Funktionen gelten für das lokal ausgeführte [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] oder auf einem virtuellen Azure-Computer.  PolyBase ist in SQL Server 2014 und früheren Versionen nicht verfügbar.  
  
|||  
|-|-|  
|**Funktion**|**Verfügbarkeit**|  
|Hadoop-Daten abfragen mit [!INCLUDE[tsql](../../includes/tsql-md.md)]|ja|  
|Azure-BLOB-Speicher abfragen mit [!INCLUDE[tsql](../../includes/tsql-md.md)]|ja|  
|Daten aus Hadoop importieren|ja|  
|Daten aus Azure-BLOB-Speicher importieren|ja|  
|Daten für Hadoop exportieren|ja|  
|Daten für Azure-BLOB-Speicher exportieren|ja|  
|PolyBase-Abfragen über Microsoft BI-Tools ausführen|ja|  
|Abfrageberechnungen auf Hadoop verlagern|ja|  
  
### [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]  
 Diese Funktionen gelten für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
|||  
|-|-|  
|**Funktion**|**Verfügbarkeit**|  
|Hadoop-Daten abfragen mit [!INCLUDE[tsql](../../includes/tsql-md.md)]|Nein|  
|Azure-BLOB-Speicher abfragen mit [!INCLUDE[tsql](../../includes/tsql-md.md)]|ja|  
|Daten aus Hadoop importieren|Nein|  
|Daten aus Azure-BLOB-Speicher importieren|ja|  
|Daten für Hadoop exportieren|Nein|  
|Daten für Azure-BLOB-Speicher exportieren|ja|  
|PolyBase-Abfragen über Microsoft BI-Tools ausführen|ja|  
|Abfrageberechnungen auf Hadoop verlagern|Nein|  
  
### [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Diese Funktionen gelten für [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
|||  
|-|-|  
|**Funktion**|**Verfügbarkeit**|  
|Hadoop-Daten abfragen mit [!INCLUDE[tsql](../../includes/tsql-md.md)]|ja|  
|Azure-BLOB-Speicher abfragen mit [!INCLUDE[tsql](../../includes/tsql-md.md)]|ja|  
|Daten aus Hadoop importieren|ja|  
|Daten aus Azure-BLOB-Speicher importieren|ja|  
|Daten für Hadoop exportieren|ja|  
|Daten für Azure-BLOB-Speicher exportieren|ja|  
|PolyBase-Abfragen über Microsoft BI-Tools ausführen|ja|  
|Abfrageberechnungen auf Hadoop verlagern|ja|  
  
## Siehe auch  
 [PolyBase-Leitfaden](../../relational-databases/polybase/polybase-guide.md)  
  
  