---
title: Erstellen und Verwalten von Speicher für speicheroptimierte Objekte | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 622aabe6-95c7-42cc-8768-ac2e679c5089
caps.latest.revision: 64
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 352a4f5dbce4bac755a981e53bfef6c5d9d61d0b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="creating-and-managing-storage-for-memory-optimized-objects"></a>Erstellen und Verwalten von Speicher für speicheroptimierte Objekte
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Das [!INCLUDE[hek_2](../../includes/hek-2-md.md)] -Modul ist in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]integriert, was es Ihnen ermöglicht, sowohl speicheroptimierte als auch (traditionelle) datenträgerbasierte Tabellen in der gleichen Datenbank zu haben. Jedoch unterscheidet sich die Speicherstruktur für speicheroptimierte Tabellen von der für datenträgerbasierte Tabellen.  
  
 Speicher für datenträgerbasierte Tabelle weisen die folgenden Schlüsselattribute auf:  
  
-   Einer Dateigruppe zugeordnet, und die Dateigruppe enthält eine oder mehrere Dateien.  
  
-   Jede Datei wird in Blöcke mit 8 Seiten unterteilt, und jede Seite hat eine Größe von 8.000 Byte.  
  
-   Ein Block kann über mehrere Tabellen gemeinsam genutzt werden, aber es gibt eine 1:1-Zuordnung zwischen der zugeordneten Seite und der Tabelle oder dem Index. Anders gesagt kann eine Tabelle keine Zeilen von zwei oder mehr Tabellen oder Indizes enthalten.  
  
-   Die Daten werden je nach Bedarf in den Arbeitsspeicher (der Pufferpool) verschoben, und die geänderten oder neu erstellten Seiten werden asynchron auf den Datenträger geschrieben, wobei hauptsächlich zufällige Ein- und Ausgaben generiert werden.  
  
 Speicher für speicheroptimierte Tabellen weisen die folgenden Schlüsselattribute auf:  
  
-   Alle speicheroptimierten Tabellen sind einer speicheroptimierten Datendateigruppe zugeordnet. Die Dateigruppe verwendet eine Syntax und Semantik ähnlich wie Filestream.  
  
-   Es gibt keine Seiten und die Daten werden als Zeile dauerhaft gespeichert.  
  
-   Alle Änderungen an speicheroptimierten Tabellen werden durch Anfügevorgänge an aktive Dateien gespeichert. Sowohl das Lesen als auch das Schreiben an Dateien ist sequenziell.  
  
-   Eine Aktualisierung wird jedoch als Vorgang implementiert, der aus einer Löschung und einer Einfügung besteht. Die gelöschten Zeilen werden nicht sofort aus dem Speicher entfernt. Die gelöschten Zeilen werden durch einen im Hintergrund ausgeführten Prozess namens MERGE entfernt; dies geschieht basierend auf einer Richtlinie wie in [Dauerhaftigkeit für speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md)beschrieben.  
  
-   Im Gegensatz zum Speicher für datenträgerbasierten Tabellen wird der Speicher für speicheroptimierte Tabellen nicht komprimiert. Beim Migrieren einer komprimierten (ZEILE oder SEITE), datenträgerbasierten Tabelle zu einer speicheroptimierten Tabelle müssen Sie die Größenänderungen berücksichtigen.  
  
-   Eine speicheroptimierte Tabelle kann sowohl dauerhaft als auch nicht dauerhaft sein. Sie müssen Speicher nur für dauerhafte speicheroptimierte Tabellen konfigurieren.  
  
 In diesem Abschnitt werden Prüfpunktdateipaare und weitere Aspekte der Speicherung von Daten in speicheroptimierten Tabellen beschrieben.  
  
 Themen in diesem Abschnitt:  
  
-   [Konfigurieren von Speicher für speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/configuring-storage-for-memory-optimized-tables.md)  
  
-   [Die speicheroptimierte Dateigruppe](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)  
  
-   [Dauerhaftigkeit für speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md)  
  
-   [Prüfpunktvorgang für speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/checkpoint-operation-for-memory-optimized-tables.md)  
  
-   [Definieren von Dauerhaftigkeit für speicheroptimierte Objekte](../../relational-databases/in-memory-oltp/defining-durability-for-memory-optimized-objects.md)  
  
-   [Vergleichen des datenträgerbasierten Tabellenspeichers mit dem speicheroptimierten Tabellenspeicher](../../relational-databases/in-memory-oltp/comparing-disk-based-table-storage-to-memory-optimized-table-storage.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [In-Memory-OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
