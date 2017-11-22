---
title: Auflistungen (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/01/2016
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- collections [Master Data Services]
- collections [Master Data Services], about collections
ms.assetid: 5aa1d1e0-b4e5-4897-8e74-01dcf418df73
caps.latest.revision: "14"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 88cf44a116a2bca8ca61bb27106bb9b080d950cf
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="collections-master-data-services"></a>Auflistungen (Master Data Services)
  Eine Auflistung ist eine Gruppe von Blatt- und konsolidierten Elementen einer einzelnen Entität. Verwenden Sie Auflistungen, wenn Sie keine vollständige Hierarchie benötigen und unterschiedliche Gruppierungen der Elemente zu Berichts- oder Analysezwecken anzeigen möchten oder wenn Sie eine Taxonomie erstellen möchten.  
  
> [!NOTE]  
>  Die Auflistung ist als veraltet markiert.  
  
## <a name="what-collections-contain"></a>Inhalte von Auflistungen  
 Es gibt bei Auflistungen keine Beschränkung hinsichtlich der Anzahl oder des Typs der Elemente, die eingebunden werden können, solange sich die Elemente in derselben Entität befinden. Eine Auflistung kann konsolidierte Elemente und Blattelemente aus mehreren verbindlichen bzw. nicht verbindlichen expliziten Hierarchien enthalten.  
  
 Wenn Sie eine Auflistung erstellen, erstellen Sie keine hierarchische Struktur; Sie erstellen eine flache Liste von Elementen. Wenn Sie einen Knoten aus einer Hierarchie auswählen und ihn der Auflistung hinzufügen, ist das konsolidierte Element, das Sie ausgewählt haben, das einzige der Auflistung hinzugefügte Element.  
  
 Außerdem kann eine Auflistung weitere Auflistungen enthalten. Zum Erstellen von Taxonomien können Sie Auflistungen verwenden, die wiederum aus Auflistungen bestehen.  
  
 Wenn Sie eine Auflistung erstellen, sind Sie automatisch als Besitzer aufgeführt. Wenn Sie Administrator sind, können Sie nach Bedarf andere Attribute für die Auflistung erstellen.  
  
## <a name="subscription-views-for-collections"></a>Abonnementsichten für Auflistungen  
 Es gibt zwei Typen von Abonnementsichten, die Auflistungen anzeigen. Das Format **Sammlungsattribute** zeigt eine Liste von Sammlungen und allen zu den jeweiligen Sammlungen gehörenden Attributen an (z.B. Beschreibung oder Besitzer). Das **Sammlungen** -Format zeigt alle Elemente in allen Auflistungen sowie jede Elementgewichtung und Sortierreihenfolge an. Weitere Informationen finden Sie unter [Übersicht: Exportieren von Daten &#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md).  
  
 Wenn Sie Gewichtungswerte für bestimmte Elemente in einer Auflistung festlegten, sind diese Werte in verwandten Abonnementsichten verfügbar.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Erstellen Sie eine neue Sammlung.|[Erstellen einer Sammlung &#40;Master Data Services&#41;](../master-data-services/create-a-collection-master-data-services.md)|  
|Fügen Sie Elemente einer vorhandenen Auflistung hinzu.|[Hinzufügen von Elementen zu einer Sammlung &#40;Master Data Services&#41;](../master-data-services/add-members-to-a-collection-master-data-services.md)|  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   [Explizite Hierarchien &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [Übersicht: Exportieren von Daten &#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md)  
  
  
