---
title: SQL Server-Replikation | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- replication [SQL Server], about
- replication [SQL Server]
ms.assetid: 3a5f4592-3c61-4b4d-9ceb-39716aeeba41
caps.latest.revision: 58
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Active
ms.openlocfilehash: 3615c25c15eb264eeced29dcd0e063a6d6dc667a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-replication"></a>SQL Server-Replikation
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Bei der Replikation handelt es sich um eine Reihe von Technologien zum Kopieren und Verteilen von Daten und Datenbankobjekten aus einer Datenbank in eine andere und das anschließende Synchronisieren zwischen den Datenbanken, um die Konsistenz der Daten sicherzustellen. Mithilfe von Replikation können Sie Daten an verschiedene Standorte, an Remotebenutzer oder mobile Benutzer über lokale Netzwerke und WANs (Wide Area Network), über DFÜ-Verbindungen, Funkverbindungen oder über das Internet verteilen.  
  
 Die Transaktionsreplikation wird typischerweise in reinen Serverumgebungen verwendet, die einen hohen Durchsatz erfordern, und ist für die folgenden Fälle geeignet: Verbessern der Skalierbarkeit und Verfügbarkeit, Data Warehousing und Berichterstellung, Integrieren von Daten aus mehreren Standorten, Integrieren heterogener Daten und Auslagern der Batchverarbeitung. Die Mergereplikation ist in erster Linie für mobile Anwendungen oder verteilte Serveranwendungen mit möglichen Datenkonflikten konzipiert. Dazu gehören folgende häufige Szenarien: Datenaustausch mit mobilen Benutzern, Point-of-Sale-Anwendungen (POS) und Integrieren von Daten aus mehreren Standorten. Momentaufnahmereplikation wird verwendet, um das Anfangsdataset für Transaktions- und Mergereplikation bereitzustellen. Sie kann auch verwendet werden, wenn vollständige Aktualisierungen von Daten erforderlich sind. Mit diesen drei Replikationstypen stellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein leistungsfähiges und flexibles System zum Synchronisieren von Daten im gesamten Unternehmen bereit. Die Replikation in SQLCE 3.5 und SQLCE 4.0 wird unter [!INCLUDE[win8srv](../../includes/win8srv-md.md)] und [!INCLUDE[win8](../../includes/win8-md.md)]unterstützt.  
  
 Als Alternative zur Replikation können Sie Datenbanken mit Microsoft Sync Framework synchronisieren. Sync Framework schließt Komponenten und eine intuitive und flexible API ein, die es Ihnen erleichtern, zwischen SQL Server-, SQL Server Express-, SQL Server Compact- und SQL Azure-Datenbanken zu synchronisieren. Sync Framework schließt auch Klassen ein, die angepasst werden können, um zwischen einer SQL Server-Datenbank und einer beliebigen anderen Datenbank, die mit ADO.NET kompatibel ist, zu synchronisieren. Eine ausführliche Dokumentation der Sync Framework-Datenbanksynchronisierungskomponenten finden Sie unter [Synchronisieren von Datenbanken](http://go.microsoft.com/fwlink/?LinkId=209079). Eine Übersicht über Sync Framework finden Sie im [Microsoft Sync Framework Developer Center](http://go.microsoft.com/fwlink/?LinkId=209078). Einen Vergleich zwischen Sync Framework und Mergereplikation finden Sie unter [Übersicht über das Synchronisieren von Datenbanken](http://msdn.microsoft.com/library/bb902818\(SQL.110\).aspx)  
  
 **Suchen Sie nach Bereich**  
 - [Neues](../../relational-databases/replication/what-s-new-replication.md)  
 - [Abwärtskompatibilität](../../relational-databases/replication/replication-backward-compatibility.md)  
 - [Replikationsfunktionen und -tasks](../../relational-databases/replication/replication-features-and-tasks.md)  
 - [Technische Referenz](../../relational-databases/replication/technical-reference-replication.md)  
  
  
