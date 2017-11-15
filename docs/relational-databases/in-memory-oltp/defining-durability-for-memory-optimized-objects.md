---
title: "Definieren von Dauerhaftigkeit für speicheroptimierte Objekte | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0fe85fbf-8e8d-4983-96fd-d04b3c7d6d65
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3129d20b59cc0b42888aa9cbcee5f1940cdb4876
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="defining-durability-for-memory-optimized-objects"></a>Definieren von Dauerhaftigkeit für speicheroptimierte Objekte
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Es gibt zwei Dauerhaftigkeitsoptionen für speicheroptimierte Tabellen:  
  
 SCHEMA_AND_DATA (Standard)  
 Diese Option gewährleistet Dauerhaftigkeit für Schema und Daten. Der Grad der Datendauerhaftigkeit ist abhängig davon, ob Sie ein Commit für eine Transaktion mit vollständiger oder verzögerter Dauerhaftigkeit ausführen. Vollständig dauerhafte Transaktionen bieten die gleiche Dauerhaftigkeitsgarantie für Daten und Schemas – ähnlich einer datenträgerbasierten Tabelle. Verzögerte Dauerhaftigkeit verbessert die Leistung, kann aber im Falle eines Serverabsturzes oder Failovers zu Datenverlusten führen. (Weitere Informationen zur verzögerten Dauerhaftigkeit finden Sie unter [Steuern der Transaktionsdauerhaftigkeit](../../relational-databases/logs/control-transaction-durability.md).)  
  
 SCHEMA_ONLY  
 Diese Option stellt die Dauerhaftigkeit des Tabellenschemas sicher. Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu gestartet wird oder eine Neukonfiguration in einer Azure SQL-Datenbank auftritt, besteht das Tabellenschema weiterhin, Daten in der Tabelle gehen jedoch verloren. (Dies steht im Gegensatz zu einer Tabelle in tempdb, bei der sowohl die Tabelle als auch die Daten beim Neustart verloren gehen.) Ein typisches Szenario zum Erstellen einer nichtdauerhaften Tabelle besteht darin, kurzlebige Daten wie eine Stagingtabelle für einen ETL-Vorgang zu speichern. Durch SCHEMA_ONLY-Dauerhaftigkeit werden Transaktionsprotokollierung und -prüfpunkt vermieden, was zu einer erheblichen Reduzierung von E/A-Vorgängen führen kann.  
  
 Bei der Verwendung der Standardtabelle SCHEMA_AND_DATA bietet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die gleiche Dauerhaftigkeit, die auch bei datenträgerbasierten Tabellen gewährleistet wird:  
  
 Dauerhaftigkeit von Transaktionen  
 Wenn Sie ein Commit für eine vollständig dauerhafte Transaktion ausführen, die DDL- oder DML-Änderungen an einer speicheroptimierten Tabelle vorgenommen hat, werden die Änderungen, die an einer dauerhaften speicheroptimierten Tabelle vorgenommen wurden, dauerhaft gespeichert.  
  
 Wenn Sie für eine verzögert dauerhafte Transaktion ein Commit in einer speicheroptimierte Tabelle ausführen, wird die Transaktion erst dauerhaft, nachdem das Transaktionsprotokoll im Arbeitsspeicher auf dem Datenträger gespeichert wurde. (Weitere Informationen zur verzögerten Dauerhaftigkeit finden Sie unter [Steuern der Transaktionsdauerhaftigkeit](../../relational-databases/logs/control-transaction-durability.md).)  
  
 Dauerhaftigkeit bei Neustarts  
 Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nach einem Systemabsturz oder einem geplanten Herunterfahren neu gestartet wird, werden die speicheroptimierten Tabellen erneut instanziiert, um den Status der Tabellen vor dem Herunterfahren oder Systemabsturz wiederherzustellen.  
  
 Dauerhaftigkeit bei Medienfehlern  
 Wenn sich auf einem fehlerhaften oder beschädigten Datenträger eine oder mehrere persistente Kopien von dauerhaften speicheroptimierten Objekten befinden, werden durch die Sicherungs- und Wiederherstellungsfunktion von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] speicheroptimierte Tabellen auf dem neuen Medium wiederhergestellt.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Verwalten von Speicher für speicheroptimierte Objekte](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
