---
title: "Abschließen des Datenbankmodul-Upgrades | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology: server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f08087e-e532-416c-8caa-e0ec88c57596
caps.latest.revision: "10"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ba67d2b2a342b7e4e6887920b0a4ccc9dd55aadd
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="complete-the-database-engine-upgrade"></a>Abschließen des Datenbankmodul-Upgrades
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Nach Abschluss des Upgrades auf SQL Server müssen Sie möglicherweise eine Reihe zusätzlicher Schritte ausführen. Dabei handelt es sich z. B. um:  
  
Führen Sie nach dem Aktualisieren von [!INCLUDE[ssDE](../../includes/ssde-md.md)]die folgenden Aufgaben aus:  
  
- **Sichern Ihrer Datenbanken:** Führen Sie für jede Datenbank eine vollständige Sicherung durch.  

- **Neue Funktionen aktivieren:** In SQL Server 2016 und SQL Server 2017 treten einige Änderungen erst in Kraft, nachdem der DATABASE_COMPATIBILITY-Grad für eine Datenbank auf 130 oder höher geändert wurde.  Weitere Informationen und den empfohlenen Workflow finden Sie unter [Ändern des Datenbank-Kompatibilitätsmodus und Verwenden des Abfragespeichers](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md). Wenn Ihre Datenbank über speicheroptimierte Tabellen verfügt, die in SQL Server 2014 erstellt wurden, informieren Sie sich unter [Statistiken für speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md).
  
- **Integration Services:**  
  
     Migrieren Sie die Integration Services-Pakete zum [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Format. Weitere Informationen finden Sie unter [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
- **Reporting Services:** Für ein neues Installationsupgrade stellen Sie die Reporting Services-Verschlüsselungsschlüssel wieder her. Weitere Informationen finden Sie unter [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
- **Master Data Services:** Aktualisieren sie das MDS-Datenbankschema, und erstellen Sie die SQL Server 2017-Webanwendung. Weitere Informationen finden Sie unter [Upgrade Master Data Services](../../database-engine/install-windows/upgrade-master-data-services.md).  
  
- **Data Quality Services:** Aktualisieren Sie das DQS-Datenbankschema, und überprüfen Sie das Upgrade des DQS-Datenbankschemas. Weitere Informationen finden Sie unter [Upgrade Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md).  
  
- **Volltextsuche:** Füllen Sie die Volltextkataloge wieder auf, um eine konsistente Semantik in Abfrageergebnissen zu gewährleisten. Weitere Informationen finden Sie unter [Auffüllen von Volltextindizes](../../relational-databases/search/populate-full-text-indexes.md).  
  
