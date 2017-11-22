---
title: Leistungsverbesserungen mit DTA-Empfehlungen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Database Engine Tuning Advisor, performance improvements
ms.assetid: 2e51ea06-81cb-4454-b111-da02808468e6
caps.latest.revision: "3"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bca7b1d7ce1a0dfeade10654a1f4242b188d5d0a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="performance-improvements-using-dta-recommendations"></a>Leistungsverbesserungen mit DTA-Empfehlungen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]


---
Die Leistung von Data Warehousing- und Analysearbeitsauslastungen kann mit **Columnstore**-Indizes enorm verbessert werden, insbesondere bei Abfragen, bei denen umfangreiche Tabellen gescannt werden müssen. **Rowstore**-Indizes (B+-Struktur) sind bei Abfragen am effektivsten, bei denen bei der Suche nach einem bestimmten Wert oder Wertebereich auf relativ kleine Datenmengen zugegriffen wird. Da Rowstore-Indizes Zeilen in sortierter Reihenfolge zurückgeben, lassen sich damit auch die Kosten der Sortierung in Abfrageausführungsplänen reduzieren. Die Wahl der Kombination von Rowstore- und Columnstore-Indizes für die Erstellung Ihrer Datenbank, hängt somit von der Arbeitsauslastung Ihrer Anwendung ab.

Der Datenbankoptimierungsratgeber (Database Engine Tuning Advisor, DTA) kann ab SQL Server 2016 durch die Analyse der Arbeitsauslastung einer bestimmten Datenbank eine geeignete **Kombination von Rowstore- und Columnstore**-Indizes empfehlen. 

Zur Veranschaulichung, welche Vorteile die DTA-Empfehlungen für die Arbeitsauslastungsleistung mit sich bringen, haben wir mit verschiedenen echten Kundenarbeitsauslastungen experimentiert. Für jede Kundenarbeitsauslastung haben wir DTA einzelne Abfragen sowie die gesamte Arbeitsauslastung mit Abfragen analysieren lassen. Dabei haben wir drei Alternativen betrachtet:
  
  1. **Nur Columnstore**: Für alle Tabellen wurden nur Columnstore-Indizes ohne Verwendung des DTA erstellt. 
  2. **DTA (nur Rowstore)**: Der DTA wurde mit der Option ausgeführt, dass nur Rowstore-Indizes empfohlen werden.
  3. **DTA (Rowstore + Columnstore)**: Der DTA wurde mit der Option ausgeführt, dass sowohl Rowstore- als auch Columnstore-Indizes empfohlen werden.  
   
Anschließend haben wir die jeweils empfohlenen Indizes implementiert. Dabei wurde die durchschnittliche CPU-Zeit (in Millisekunden) über mehrere Abfrageausführungen oder über die Arbeitsauslastung hinweg protokolliert. In der folgenden Abbildung ist die CPU-Zeit in Millisekunden für Arbeitsauslastungen über zwei verschiedene Kundendatenbanken hinweg dargestellt. Beachten Sie, dass für die y-Achse (CPU-Zeit) eine logarithmische Skalierung verwendet wird.   


![DTA-columnstore-rowstore-performance](../../relational-databases/performance/media/dta-columnstore-rowstore-performance.gif)



**Bedarf an gemischten physischen Entwürfen**: Die erste Säulengruppe entspricht Kunde 1, Abfrage 1. DTA (Rowstore + Columnstore) empfiehlt eine Gruppe von vier Columnstore- und sechs Rowstore-Indizes, was zu einer im Vergleich zu einem reinen Columnstore-Index und DTA (nur Rowstore) eine 2,5- bis 4-mal geringere CPU-Zeit zur Folge hat. Dies zeigt die Vorteile von gemischten physischen Entwürfen, die aus Rowstore- und Columnstore-Indizes bestehen, *auch bei einer einzelnen Abfrage*. 

**Effizienz von Rowstore-Indexempfehlungen**: Die zweite und die dritte Säulengruppe (die Kunde 1, Abfrage 2 und Kunde 2, Abfrage 1 entsprechen) stellen Fälle dar, bei denen die Abfragen über Auswahlfilterprädikate verfügen, die von geeigneten Rowstore-Indizes profitieren. Für beide Abfragen empfiehlt DTA (nur Rowstore) und DTA (Rowstore + Columnstore) nur Rowstore-Indizes. Diese Beispiele zeigen auch, dass selbst dann, wenn DTA mit der Option ausgeführt wird, Columnstore-Indizes zu empfehlen, das kostenbasierte Konzept sicherstellt, dass ein Columnstore-Index nur dann empfohlen wird, wenn die Arbeitsauslastung tatsächlich davon profitiert.

**Effizienz von Columnstore-Indexempfehlungen**: Die vierte Säulengruppe, die Kunde 2, Abfrage 2 entspricht, stellt einen Fall dar, bei dem die Abfrage umfangreiche Tabellen scannt, die von Columnstore-Indizes profitieren würden. DTA (nur Rowstore) generiert eine Empfehlung, bei der der Wert für die CPU-Zeit höher ist, als wenn Columnstore-Indizes verwendet werden würden. DTA (Rowstore + Columnstore) empfiehlt geeignete Columnstore-Indizes und entspricht somit der Abfrageausführungsleistung der Option „Nur Columnstore“.

**Effizienz von Empfehlungen für Arbeitsauslastungen mit mehreren Abfragen**: Die letzte Säulengruppe, die der gesamten Arbeitsauslastung für Kunde 2 entspricht, veranschaulicht die Fähigkeit von DTA, mehrere Abfragen in der Arbeitsauslastung analysieren und eine geeignete Kombination aus Rowstore- und Columnstore-Indizes empfehlen zu können, sodass die Ausführungskosten der gesamten Arbeitsauslastung verbessert werden. DTA (Rowstore + Columnstore) empfiehlt vier Columnstore-Indizes und eine Reihe von Rowstore-Indizes. Dadurch wird die Leistung für die Arbeitsauslastung im Vergleich zu der Option, mit der nur Columnstore-Indizes erstellt werden, um ein Vielfaches verbessert. Im Vergleich zu DTA (nur Rowstore) lässt sich die Leistung um ein 4- bis 5-Faches verbessern.

Die obigen Beispiele veranschaulichen also die Fähigkeit von DTA, die vom SQL Server-Datenbankmodul unterstützten Rowstore- und Columnstore-Indizes optimal nutzen und eine geeignete Indexkombination empfehlen zu können, mit der sich die CPU-Zeit für die Arbeitsauslastung deutlich reduzieren lässt. 

<a name="see-also"></a>Siehe auch
---
[Datenbankoptimierungsratgeber](../../relational-databases/performance/database-engine-tuning-advisor.md)

[Empfehlungen für Columnstore-Index im Datenbankoptimierungsratgeber (DTA)](../../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md)

[Beschreibung von Columnstore-Indizes](~/relational-databases/indexes/columnstore-indexes-overview.md)

[Columnstore-Indizes für Data Warehousing](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)

[CREATE COLUMNSTORE INDEX (Transact-SQL)](../../t-sql/statements/create-columnstore-index-transact-sql.md)

[CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)



