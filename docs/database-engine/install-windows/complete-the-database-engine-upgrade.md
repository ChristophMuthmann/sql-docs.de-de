---
title: "Abschlie&#223;en des Datenbankmodul-Upgrades | Microsoft Docs"
ms.custom: ""
ms.date: "09/22/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3f08087e-e532-416c-8caa-e0ec88c57596
caps.latest.revision: 10
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 10
---
# Abschlie&#223;en des Datenbankmodul-Upgrades
  Nach Abschluss des Upgrades auf SQL Server 2016 gibt es eine Reihe zusätzlicher Schritte, die Sie möglicherweise durchführen müssen. Dabei handelt es sich z. B. um:  
  
 Führen Sie nach dem Aktualisieren von [!INCLUDE[ssDE](../../includes/ssde-md.md)]die folgenden Aufgaben aus:  
  
-   **Sichern Ihrer Datenbanken:** Führen Sie für jede aktualisierte Datenbank eine vollständige Sicherung durch.  
  
-   **Neue Funktionen aktivieren: **In SQL Server 2016 treten einige Änderungen erst in Kraft, nachdem der DATABASE_COMPATIBILITY-Grad für eine Datenbank in 130 geändert wurde.  Weitere Informationen und den empfohlenen Workflow finden Sie unter [Ändern des Datenbank-Kompatibilitätsmodus und Verwenden des Abfragespeichers](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md).  
  
-   **Integration Services:**  
  
     Migrieren Sie die Integration Services-Pakete zum [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Format. Weitere Informationen finden Sie unter [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
-   **Reporting Services:** Für ein neues Installationsupgrade stellen Sie die Reporting Services-Verschlüsselungsschlüssel wieder her. Weitere Informationen finden Sie unter [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/back-up-and-restore-reporting-services-encryption-keys.md).  
  
-   **Master Data Services:**  Aktualisieren sie das MDS-Datenbankschema, und erstellen Sie die SQL Server 2016-Webanwendung. Weitere Informationen finden Sie unter [Upgrade Master Data Services](../../database-engine/install-windows/upgrade-master-data-services.md).  
  
-   **Data Quality Services:** Aktualisieren Sie das DQS-Datenbankschema, und überprüfen Sie das Upgrade des DQS-Datenbankschemas. Weitere Informationen finden Sie unter [Upgrade Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md).  
  
-   **Volltextsuche:** Füllen Sie die Volltextkataloge wieder auf, um eine konsistente Semantik in Abfrageergebnissen zu gewährleisten. Weitere Informationen finden Sie unter [Auffüllen von Volltextindizes](../../relational-databases/search/populate-full-text-indexes.md).  
  
## Fanden Sie diesen Artikel nützlich? Wir hören Ihnen zu  
 Welche Informationen suchen Sie, und haben Sie sie gefunden? Wir nehmen uns Ihr Feedback zu Herzen, um unsere Inhalte zu verbessern. Senden Sie Ihre Kommentare an [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Complete%20the%20Database%20Engine%20Upgrade%20page).  
  
  