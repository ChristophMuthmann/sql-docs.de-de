---
title: "Verbessern von Leistung und Zuverlässigkeit mit dem JDBC-Treiber | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e1592499-b87b-45ee-bab8-beaba8fde841
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d8b2d716ada4cb786eb141c0f49dcad41c5231c4
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2018
---
# <a name="improving-performance-and-reliability-with-the-jdbc-driver"></a>Verbessern von Leistung und Zuverlässigkeit mit dem JDBC-Treiber
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Ein allen Anwendungen gemeinsamer Aspekt der Anwendungsentwicklung ist die ständige Notwendigkeit, Leistung und Zuverlässigkeit zu verbessern. Es gibt eine Reihe von Techniken, um dieses Ziel mit den [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 Die Themen in diesem Abschnitt beschreiben verschiedene Verfahren, um die Leistung und Zuverlässigkeit von Anwendungen zu verbessern, wenn der JDBC-Treiber verwendet wird.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Schließen von nicht verwendeten Objekten](../../connect/jdbc/closing-objects-when-not-in-use.md)|Beschreibt die Bedeutung des Schließens von JDBC-Treiberobjekten, wenn sie nicht mehr benötigt werden.|  
|[Verwalten des Transaktionsumfangs](../../connect/jdbc/managing-transaction-size.md)|Beschreibt Verfahren zur Steigerung der Transaktionsleistung.|  
|[Arbeiten mit Anweisungen und Resultsets](../../connect/jdbc/working-with-statements-and-result-sets.md)|Beschreibt Techniken zum Verbessern der Leistung bei Verwendung der Anweisung oder ein ResultSet-Objekte.|  
|[Verwenden der adaptiven Pufferung](../../connect/jdbc/using-adaptive-buffering.md)|Beschreibt die Funktion für die adaptive Pufferung, durch die alle Daten mit großen Werten ohne den Aufwand für Servercursor abgerufen werden können.|  
|[Spalten mit geringer Dichte](../../connect/jdbc/sparse-columns.md)|Erläutert die Unterstützung von der JDBC-Treiber für [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Spalten mit geringer Dichte.|  
|[Vorbereitete Anweisungsmetadaten Zwischenspeichern für den JDBC-Treiber](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)|Erläutert die Verfahren zur Steigerung der Leistung mit vorbereitete Abfragen.|
  
## <a name="see-also"></a>Siehe auch  
 [Overview of the JDBC Driver (Übersicht über den JDBC-Treiber)](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  