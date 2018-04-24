---
title: 'Übersicht: Importieren von Daten aus Tabellen (Master Data Services) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- staging process [Master Data Services], about staging process
- importing data [Master Data Services]
- staging process [Master Data Services]
ms.assetid: 181d1e22-379c-45d1-b03c-e1e22ff14164
caps.latest.revision: 21
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e662f71f05e3c44637a2209f57535e1a797a7928
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="overview-importing-data-from-tables-master-data-services"></a>Übersicht: Importieren von Daten aus Tabellen (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Nach der Erstellung eines Modells für Ihre Daten in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]können Sie beginnen, Daten hinzufügen und Änderungen an den Daten vorzunehmen.   Sie verwenden [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Stagingtabellen, gespeicherte Prozeduren und Master Data Manager.  
  
 Informationen zum Hinzufügen und Ändern von Daten finden Sie unter [Importieren von Daten aus Tabellen &#40;Master Data Services&#41;](../master-data-services/import-data-from-tables-master-data-services.md).  
  
> [!NOTE]  
>  Ferner können Sie das [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]verwenden, um dem MDS-Repository ([!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank) Daten aus Excel hinzuzufügen. Weitere Informationen finden Sie unter [Übersicht: Importieren von Daten aus Excel &#40;MDS-Add-In für Excel&#41;](../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md).  
  
 Beim Hinzufügen und Ändern von Daten können Sie Folgendes tun.  
  
-   Laden und Aktualisieren von Elementen und Aktualisieren von Attributwerten  
  
-   Deaktivieren und Löschen von Elementen  
  
-   Verschieben von Elementen der expliziten Hierarchie  
  
 Das Hinzufügen und Aktualisieren von Daten besteht hauptsächlich in den folgenden Aufgaben.  
  
1.  Laden von Daten in die Stagingtabellen in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank.  
  
2.  Laden von Daten aus den Stagingtabellen in die entsprechenden [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Tabellen.  
  
     Zum Laden der Daten verwenden Sie gespeicherte Prozeduren oder [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .  
  
> [!NOTE]  
>  In [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]ist die Unterstützung für die [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] -Stagingprozesse veraltet.  
  
## <a name="deactivating-and-deleting-members-mds"></a>Deaktivieren und Löschen von Elementen (MDS)  
 Deaktivieren bedeutet, dass das Element erneut aktiviert werden kann. Wenn Sie ein Element erneut aktivieren, werden seine Attribute und Mitgliedschaft in Hierarchien und Auflistungen wiederhergestellt. Alle vorherigen Transaktionen sind intakt. Deaktivierungstransaktionen werden Administratoren im Funktionsbereich **Versionsverwaltung** von Master Data Manager angezeigt.  
  
 Löschen bedeutet, das Element dauerhaft vom System zu entfernen. Alle Transaktionen für das Element, alle Beziehungen und alle Attribute werden dauerhaft gelöscht.  
  
> [!NOTE]  
>  Per Staging können Sie keine Elemente erneut aktivieren. Diesen Vorgang müssen Sie manuell in Master Data Manager ausführen. Weitere Informationen finden Sie unter [Reaktivieren eines Elements oder einer Sammlung &#40;Master Data Services&#41](../master-data-services/reactivate-a-member-or-collection-master-data-services.md).  
>   
>  Per Staging können Sie keine Auflistungen löschen oder deaktivieren. Weitere Informationen zum manuellen Deaktivieren von Sammlungen finden Sie unter [Löschen eines Elements oder einer Sammlung &#40;Master Data Services&#41;](../master-data-services/delete-a-member-or-collection-master-data-services.md).  
  
## <a name="moving-explicit-hierarchy-members-mds"></a>Verschieben von Elementen der expliziten Hierarchie (MDS)  
 Beim Massenverschieben der Position von Elementen der expliziten Hierarchie können Sie die folgenden Festlegungen treffen.  
  
-   Ein konsolidiertes Element als übergeordnetes Element eines konsolidierten Elements  
  
-   Ein konsolidiertes Element als übergeordnetes Element eines Blattelements  
  
-   Ein Blattelement als ein gleichgeordnetes Element eines Blattelements oder eines konsolidierten Elements  
  
-   Ein konsolidiertes Element als ein gleichgeordnetes Element eines Blattelements oder eines konsolidierten Elements  
  
## <a name="staging-tables-and-stored-procedures-mds"></a>Stagingtabellen und gespeicherte Prozeduren (MDS)  
 Die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank enthält die folgenden Typen von Stagingtabellen, die Sie mit Ihren Daten auffüllen können.  
  
-   [Stagingtabelle für Blattelemente &#40;Master Data Services&#41;](../master-data-services/leaf-member-staging-table-master-data-services.md)  
  
-   [Konsolidierte Elementstagingtabelle &#40;Master Data Services&#41;](../master-data-services/consolidated-member-staging-table-master-data-services.md)  
  
-   [Stagingtabelle für Beziehungen &#40;Master Data Services&#41;](../master-data-services/relationship-staging-table-master-data-services.md)  
  
 Für jede Entität im Modell gibt es eine Stagingtabelle. Der Tabellenname gibt die entsprechende Entität und den Entitätstyp an, wie etwa ein Blattelement. In der folgenden Abbildung sind die Stagingtabellen für die Entitäten „Währung“, „Kunde“ und „Produkt“ dargestellt.  
  
 ![Stagingtabellen in der MDS-Datenbank](../master-data-services/media/mds-staging-tables.png "Staging Tables in MDS database")  
  
 Der Name der Tabelle wird beim Erstellen einer Entität angegeben und kann nicht geändert werden. Wenn der Stagingtabellenname eine _1 oder eine andere Zahl enthält, war eine andere Tabelle dieses Namens bereits vorhanden, als die Entität erstellt wurde.  
  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] beinhaltet die folgenden Typen von gespeicherten Stagingprozeduren.  
  
-   stg.udp_\<name>_Leaf  
  
-   stg.udp_\<name>_Consolidated  
  
-   stg.udp_\<name>_Relationship  
  
 Für jede Entität im Modell gibt es drei gespeicherte Prozeduren, die dem Blattelement, dem konsolidierten Element und der Stagingtabelle für Beziehungen entsprechen.  In der folgenden Abbildung sind die gespeicherten Stagingprozeduren für die Entitäten „Währung“, „Kunde“ und „Produkt“ dargestellt.  
  
 ![Gespeicherte Stagingprozeduren in der MDS-Datenbank](../master-data-services/media/mds-staging-storedprocedures.png "Staging stored procedures in the MDS database")  
  
 Weitere Informationen zu den gespeicherten Prozeduren finden Sie unter [Gespeicherte Stagingprozedur &#40;Master Data Services&#41;](../master-data-services/staging-stored-procedure-master-data-services.md).  
  
## <a name="logging-transactions-mds"></a>Protokollieren von Transaktionen (MDS)  
 Alle Transaktionen, die auftreten, wenn Daten oder Beziehungen importiert oder aktualisiert werden, können protokolliert werden. Eine Option in der gespeicherten Prozedur ermöglicht diese Protokollierung. Wenn Sie den Stagingprozess mithilfe von [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]einleiten, erfolgt keine Protokollierung.  
  
 In [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]wird die Einstellung **Protokollieren aller Stagingtransaktionen** nicht für diese Methode zum Bereitstellen von Daten angewendet.  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   [Überprüfung &#40;Master Data Services&#41;](../master-data-services/validation-master-data-services.md)  
  
-   [Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
