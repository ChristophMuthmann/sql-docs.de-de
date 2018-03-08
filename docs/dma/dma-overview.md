---
title: "Übersicht über Data Migration Assistant (SQLServer) | Microsoft Docs"
ms.custom: 
ms.date: 02/07/2018
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: 
ms.topic: article
keywords: 
helpviewer_keywords:
- Data Migration Assistant, overview
ms.assetid: 
caps.latest.revision: 
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c23ed7d07474cc763da951e782badd42458dacdb
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="overview-of-data-migration-assistant"></a>Übersicht über Data-Migrations-Assistenten

Die Daten Migration Assistant (DMA) können Sie zum Aktualisieren auf eine moderne Datenplattform durch das Erkennen von Kompatibilitätsproblemen zu Fragen, die in der neuen Version von SQL Server und Azure SQL-Datenbank-Funktionalität auswirken können. DMA empfiehlt, Leistung und Zuverlässigkeit Verbesserungen für Ihre zielumgebung und können Sie Ihr Schema, Daten und nicht enthaltene Objekte vom Quellserver auf dem Zielserver zu verschieben.

> [!NOTE] 
> Für große (im Hinblick auf Anzahl und Größe der Datenbanken) Migrationen, es wird empfohlen, verwenden Sie die [Migration-Dienst von Azure-Datenbank](https://docs.microsoft.com/en-us/azure/dms/dms-overview), können die Datenbanken zu migrieren.
  
## <a name="capabilities"></a>Funktionen

- Bewerten Sie die lokale SQL Server-Instanzen, die Migration zu Azure SQL-Datenbanken. Der Assessment-Workflow können Sie die folgenden Probleme zu erkennen, die Migration zu Azure SQL-Datenbank beeinflussen können und enthält ausführliche Hinweise auf deren Behebung.

  - Blockierende Probleme bei der Paketmigration: Kompatibilitätsprobleme, dass Block Migrieren einer SQL Server lokalen-Datenbanken e zur Azure SQL-Datenbanken ermittelt. DMA Empfehlungen lassen sich diese Probleme zu beheben.

  - Teilweise unterstützte oder nicht unterstützte Funktionen: erkennt teilweise unterstützte oder nicht unterstützte Funktionen, die derzeit in der SQL Server-Quellinstanz verwendet werden. DMA bietet eine umfassende Empfehlungen, alternative Ansätze in Azure und Schritten festgelegt, damit Sie in Ihrem Migrationsprojekten integrieren können.

- Ermitteln Sie Probleme, die ein Upgrade auf eine lokale SQL Server auswirken können. Diese werden als Kompatibilitätsprobleme beschrieben und werden in den folgenden Kategorien organisiert:

  - Wichtige Änderungen

  - Verändertes Programmverhalten

  - Als veraltet markierte Funktionen

- Entdecken Sie neue Funktionen in die Zielplattform für das SQL Server, die die Datenbank nach einem Upgrade von profitieren kann. Diese werden als Funktion Empfehlungen beschrieben und werden in den folgenden Kategorien organisiert:

  - Leistung

  - Sicherheit

  - Speicherung

- Migrieren einer lokalen SQL Server-Instanz zu einem modernen SQL Server-Instanz gehostet wird, lokal oder auf einem virtuellen Azure-Computer (VM), der von Ihrem lokalen Netzwerk aus zugänglich ist. Die Azure-VM kann über eine VPN- oder anderen Technologien zugegriffen werden. Workflow bei der Migration können Sie die folgenden Komponenten migrieren:

  - Schema der Datenbanken

  - Daten und Benutzer

  - Serverrollen

  - SQL Server und Windows-Anmeldungen

- Nach der erfolgreichen Migration können Anwendungen nahtlos mit den Zieldatenbanken für SQL Server verbinden.

## <a name="supported-source-and-target-versions"></a>Unterstützte Versionen von Quelle und Ziel

DMA ersetzt alle vorherige Versionen von SQL Server Upgrade Advisor und Upgrades für die meisten SQL Server-Versionen verwendet werden soll. Führen Sie die unterstützte Versionen von Quelle und Ziel.

**Datenquellen**
- SQL Server 2005
- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012 
- SQL Server 2014
- SQL Server 2016
- SQLServer 2017 unter Windows

**Ziele**
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- SQLServer 2017 unter Windows und Linux
- Azure SQL Database

## <a name="installation"></a>Installation

Um DMA zu installieren, laden Sie die neueste Version des Tools aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595), und führen Sie dann die **DataMigrationAssistant.msi** Datei.

## <a name="see-also"></a>Siehe auch

[Bewerten Sie Ihre Migration zu SQL Server](../dma/dma-assesssqlonprem.md)

[Assistent für die Migration von Daten: Konfigurationseinstellungen](../dma/dma-configurationsettings.md)

[Migrieren einer lokalen SQL Server mit dem Daten Migrations-Assistenten](../dma/dma-migrateonpremsql.md)

[Assistent für die Migration von Daten: Bewährte Methoden](../dma/dma-bestpractices.md)



