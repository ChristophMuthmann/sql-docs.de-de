---
title: Importieren von Daten aus Tabellen (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ad5b83b1-8e40-4ef8-9ba8-4ea17a58b672
caps.latest.revision: "10"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 952a452bc17762f9971a72b8ca0d4e38701cba6f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="import-data-from-tables-master-data-services"></a>Importieren von Daten aus Tabellen (Master Data Services)
  Sie können einem Modell in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]in einem Massenvorgang Daten hinzufügen und Datenänderungen vornehmen.  
  
 **Erforderliche Komponenten**  
  
-   Sie müssen über die Berechtigung zum Einfügen von Daten in die Tabelle „stg.\<name>_Leaf“, „stg.\<name>_Consolidated“ bzw. „stg.\<name>_Relationship“ in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]-Datenbank verfügen.  
  
-   Sie müssen über Berechtigungen zum Ausführen der gespeicherten Prozedur „stg.udp_\<name>_Leaf“, „stg.udp\_\<name>_Consolidated“, oder „stg.udp\_\<name>_Relationship“ in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]-Datenbank verfügen.  
  
-   Das Modell darf nicht den Status **Commit wurde ausgeführt**haben.  
  
 **So fügen Sie in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank Daten hinzu, aktualisieren oder löschen sie**  
  
1.  Bereiten Sie die Elemente für den Import in die entsprechende Stagingtabelle in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank vor, und geben Sie Werte für die Pflichtfelder an. Eine Übersicht der Stagingtabellen finden Sie unter [Übersicht: Importieren von Daten aus Tabellen &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)  
  
    -   Die Tabelle für Blattelemente ist „stg.\<name>_Leaf“, wobei \<name> die entsprechende Entität bezeichnet. Weitere Informationen zu Pflichtfeldern finden Sie unter [Stagingtabelle für Blattelemente &#40;Master Data Services&#41;](../master-data-services/leaf-member-staging-table-master-data-services.md)  
  
    -   Die Tabelle für konsolidierte Elemente ist „stg.\<name>_Consolidated“. Weitere Informationen zu Pflichtfeldern finden Sie unter [Konsolidierte Elementstagingtabelle &#40;Master Data Services&#41;](../master-data-services/consolidated-member-staging-table-master-data-services.md).  
  
    -   Zum Verschieben des Speicherorts von Elementen in expliziten Hierarchien wird die Tabelle „stg.\<name>_Relationship“ verwendet. Weitere Informationen zu Pflichtfeldern finden Sie unter [Stagingtabelle für Beziehungen &#40;Master Data Services&#41;](../master-data-services/relationship-staging-table-master-data-services.md).  
  
         Eine Übersicht über das Verschieben von Elementen in expliziten Hierarchien finden Sie unter [Übersicht: Importieren von Daten aus Tabellen &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md).  
  
    -   Verwenden Sie den Feldwert von **ImportType** , um anzugeben, dass Sie neue Elemente erstellen, Elemente deaktivieren oder Elemente löschen. Weitere Informationen zu den Werten finden Sie unter [Stagingtabelle für Blattelemente &#40;Master Data Services&#41;](../master-data-services/leaf-member-staging-table-master-data-services.md) und [Konsolidierte Elementstagingtabelle &#40;Master Data Services&#41;](../master-data-services/consolidated-member-staging-table-master-data-services.md).  
  
         Eine Übersicht über das Deaktivieren und Löschen von Elementen finden Sie unter [Übersicht: Importieren von Daten aus Tabellen &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md).  
  
2.  Öffnen Sie [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] , und stellen Sie eine Verbindung zur Datenbankmodulinstanz für Ihre [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank her.  
  
     Weitere Informationen finden Sie unter [SQL Server Management Studio](http://msdn.microsoft.com/library/66a6b7b1-de6a-4161-82bd-98ded486947b).  
  
3.  Importieren Sie Daten in die Stagingtabellen mithilfe des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Import- und -Export-Assistenten.  
  
     Weitere Informationen finden Sie unter [SQL Server Import and Export Wizard](~/integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md).  
  
4.  Laden Sie mit einer der folgenden Aktivitäten die Daten aus den Stagingtabellen in die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] :  
  
    -   Führen Sie die gespeicherte Stagingprozedur aus, die der Stagingtabelle entspricht, in die Sie Daten verschieben möchten.  
  
         Eine Übersicht über das gespeicherte Stagingprozeduren und Stagingtabellen finden Sie unter [Übersicht: Importieren von Daten aus Tabellen &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md). Weitere Informationen zu Parametern für gespeicherte Stagingprozeduren und ein Codebeispiel finden Sie unter [Gespeicherte Stagingprozedur &#40;Master Data Services&#41;](../master-data-services/staging-stored-procedure-master-data-services.md).  
  
    -   Verwenden Sie den Funktionsbereich **Integrationsmanagement** der Masterdatenverwaltung.  
  
         Wählen Sie auf der Seite **Stagingbatches** in der Dropdownliste das Modell aus, dem Sie Daten hinzufügen möchten, und klicken Sie anschließend auf **Batches starten**. Der Status der Batchverarbeitung wird im Feld **Status** angezeigt. Weitere Informationen zu Status finden Sie unter [Importstatus &#40;Master Data Services&#41;](../master-data-services/import-statuses-master-data-services.md).  
  
         ![Stagingbatchesseite im Master Data Manager](../master-data-services/media/mds-stagingbatchespage.png "Staging Batches Page in Master Data Manager")  
  
         Der Stagingvorgang wird mit den durch die Einstellung **Staging-Batchintervall** in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. Weitere Informationen finden Sie unter [Systemeinstellungen &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
5.  Zeigen Sie Fehler an, die während des Stagings aufgetreten sind. Weitere Informationen finden Sie unter [Anzeigen von Fehlern, die während des Stagings auftreten &#40;Master Data Services&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md) und [Fehler des Stagingprozesses &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md).  
  
6.  Überprüfen der Daten im Hinblick auf Geschäftsregeln.  
  
     Navigieren Sie im Master Data Manager zum Funktionsbereich **Explorer** für Ihr Modell, und wenden Sie dann Geschäftsregeln zur Überprüfung Ihrer Daten an. Weitere Informationen finden Sie unter [Überprüfen von bestimmten Elementen auf Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md). Sie können auch eine gespeicherte Prozedur zum Überprüfen der Daten verwenden. Weitere Informationen finden Sie unter [Gespeicherte Überprüfungsprozedur &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md).  
  
     Wenn Sie Daten aus den Stagingtabellen laden, werden die Daten nicht automatisch im Hinblick auf Geschäftsregeln überprüft. Weitere Informationen dazu, was eine Überprüfung ist und wann sie stattfindet, finden Sie unter [Überprüfung &#40;Master Data Services&#41;](../master-data-services/validation-master-data-services.md).  
  
  
