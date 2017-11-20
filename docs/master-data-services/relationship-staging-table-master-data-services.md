---
title: "Stagingtabelle für Beziehungen (Master Data Services) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 04/01/2016
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- relationships staging table [Master Data Services]
- database [Master Data Services], relationships table
ms.assetid: e19b6002-67bd-4e7d-9f19-ecb455522b1a
caps.latest.revision: 8
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: a43b9a600e62b63468c21b9a32f1a706a7ec5eda
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="relationship-staging-table-master-data-services"></a>Stagingtabelle für Beziehungen (Master Data Services)
  Ändern Sie den Speicherort von Elementen in einer expliziten Hierarchie anhand der Beziehung der Elemente untereinander, indem Sie die Stagingtabelle für Beziehungen (stg.name_Relationship) in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank verwenden.  
  
##  <a name="TableColumns"></a> Tabellenspalten  
 Die folgende Tabelle erklärt, wofür jedes der Felder in der Stagingtabelle für Beziehungen verwendet wird.  
  
|Spaltenname|Description|Wert|  
|-----------------|-----------------|-----------|  
|**ID**|Ein automatisch zugewiesener Bezeichner.|Geben Sie in diesem Feld keinen Wert ein. Wenn der Batch nicht verarbeitet wurde, ist dieses Feld leer.|  
|**RelationshipType**|Required<br /><br /> Der festgelegte Beziehungstyp.|Folgende Werte sind möglich:<br /><br /> **1**: übergeordnet<br /><br /> **2**: gleichgeordnet (auf gleicher Ebene)|  
|**ImportStatus_ID**|Required<br /><br /> Der Status des Importvorgangs.|Folgende Werte sind möglich:<br /><br /> **0**geben Sie an, um anzuzeigen, dass der Datensatz für den Stagingprozess bereit ist.<br /><br /> **1**: wird automatisch zugewiesen und gibt an, dass der Stagingprozess für den Datensatz erfolgreich war.<br /><br /> **2**: wird automatisch zugewiesen, und gibt an, dass der Stagingprozess für den Datensatz nicht erfolgreich war.|  
|**Batch_ID**|Wird nur vom Webdienst benötigt<br /><br /> Ein automatisch zugewiesener Bezeichner, der Datensätze für das Staging gruppiert.<br /><br /> Wenn der Batch nicht verarbeitet wurde, ist dieses Feld leer.|Alle Elemente im Batch werden diesem Bezeichner zugewiesen, der in der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Benutzeroberfläche in der **ID** -Spalte angezeigt wird.|  
|**BatchTag**|Erforderlich, außer vom Webdienst<br /><br /> Ein eindeutiger Name für den Batch (bis zu 50 Zeichen).||  
|**HierarchyName**|Required<br /><br /> Der explizite Name der Hierarchie. Jedes konsolidierte Element kann nur einer Hierarchie angehören.||  
|**ParentCode**|Required<br /><br /> Für über- und untergeordnete Beziehungen der Code für das konsolidierte Element, das als übergeordnetes Element des untergeordneten Blattes oder konsolidierten Elements fungiert.<br /><br /> Für gleichgeordnete Beziehungen der Code für eines der gleichgeordneten Elemente.||  
|**ChildCode**|Required<br /><br /> Für über- und untergeordnete Beziehungen der Code für das konsolidierte Element oder Blattelement, das als untergeordnetes Element fungiert.<br /><br /> Für gleichgeordnete Beziehungen der Code für eines der gleichgeordneten Elemente.||  
|**Sortierreihenfolge**|Optional<br /><br /> Eine ganze Zahl, die die Reihenfolge des Elements im Verhältnis zu den anderen Elementen unter dem übergeordneten Element angibt. Jedes untergeordnete Element sollte über einen eindeutigen Bezeichner verfügen.||  
|**ErrorCode**|Zeigt einen Fehlercode an. Informationen zu Datensätzen mit einer **ImportStatus_ID** von **2**, finden Sie unter [Fehler des Stagingprozesses &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md).||  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht: Importieren von Daten aus Tabellen &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [Anzeigen von Fehlern, die während des Stagings auftreten &#40;Master Data Services&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)   
 [Fehler des Stagingprozesses &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md)  
  
  

