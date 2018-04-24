---
title: Löschen einer Abonnementsicht (Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
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
ms.assetid: ff1e2566-ac8f-467d-a6d9-12c3f13879b9
caps.latest.revision: 9
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e0a8915291cc561dda9fd9846fb715ab57ca81e0
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="subscription-view-formats-master-data-services"></a>Abonnementsichtformate (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Auf Grundlage der ausgewählten Entität oder abgeleiteten Hierarchie sind die folgenden Formate für die Abonnementansicht verfügbar.  
  
## <a name="subscription-view-formats"></a>Abonnementsichtformate  
  
|Name|Description|  
|----------|-----------------|  
|**Blattelemente**|Enthält Blattelemente und ihre zugeordneten Attributwerte.|  
|**Verlauf von Blattelementen**|Enthält Verlaufsdaten zu Blattelementen und die zugeordneten Attributwerte. Das Anzeigeformat ist Slowly Changing Dimension Typ 4.|  
|**Blattelemente SCD-Typ 2**|Enthält Verlaufsdaten und aktuelle Daten zu Blattelementen und die zugeordneten Attributwerte. Das Anzeigeformat ist Slowly Changing Dimension Typ 2.|  
|**Konsolidierte Elemente**|Enthält konsolidierte Elemente und ihre zugeordneten Attributwerte.|  
|**Verlauf von konsolidierten Elementen**|Enthält Verlaufsdaten zu konsolidierten Elementen und die zugeordneten Attributwerte. Das Anzeigeformat ist Slowly Changing Dimension Typ 4.|  
|**Konsolidierte Elemente SCD-Typ 2**|Enthält Verlaufsdaten und aktuelle Daten zu konsolidierten Elementen und die zugeordneten Attributwerte. Das Anzeigeformat ist Slowly Changing Dimension Typ 2.|  
|**Zugehörigkeit zu Sammlungen**|Enthält eine Liste von Auflistungen und ihre zugeordneten Attributwerte.|  
|**Auflistungen**|Enthält eine Liste von Auflistungen und die zugehörigen Elemente sowie Gewichtungswerte und Sortierreihenfolge.|  
|**Verlauf von Sammelelementen**|Enthält Verlaufsdaten zu Sammelelementen und die zugeordneten Attributwerte. Das Anzeigeformat ist Slowly Changing Dimension Typ 4.|  
|**Sammelelemente SCD-Typ 2**|Enthält Verlaufsdaten und aktuelle Daten zu Sammelelementen und die zugeordneten Attributwerte. Das Anzeigeformat ist Slowly Changing Dimension Typ 2.|  
|**Explizite Strukturen über- und untergeordneter Elemente**|Enthält Strukturen expliziter Hierarchien für eine Entität im Format über- und untergeordneter Elemente.|  
|**Explizite Ebenen**|Enthält Strukturen expliziter Hierarchien für eine Entität im Ebenenformat.|  
|**Abgeleitete Hierarchie über- und untergeordneter Elemente (Sicht der abgeleiteten Hierarchie)**|Enthält die Struktur einer abgeleiteten Hierarchie im Format über- und untergeordneter Elemente.|  
|**Abgeleitete Ebenen (Sicht der abgeleiteten Hierarchie)**|Enthält die Struktur einer abgeleiteten Hierarchie im Ebenenformat.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht: Exportieren von Daten &#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md)   
 [Erstellen einer Abonnementsicht zum Exportieren von Daten &#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)  
  
  
