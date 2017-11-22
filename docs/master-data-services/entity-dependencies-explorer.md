---
title: "Entitätsabhängigkeiten-Explorer | Microsoft-Dokumentation"
ms.custom: 
ms.date: 04/06/2016
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
keywords: Master Data Services
ms.assetid: 9d922118-1412-4a9d-9c02-70d6c48d6c0d
caps.latest.revision: "5"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e1f1e9136e54c99a00cc31c30ff243fdd3356737
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="entity-dependencies-explorer"></a>Entitätsabhängigkeiten-Explorer
  
[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] In 2016 wurde eine neue Explorer-Seite namens „Entitätsabhängigkeiten“ hinzugefügt, die alternative Möglichkeiten zur Visualisierung von Beziehungen zwischen Entitätselementen innerhalb eines Modells bietet. Die Visualisierung basiert auf den Werten ihrer domänenbasierten Attribute (DBA), ohne dass eine abgeleitete Hierarchie definiert werden muss.   
  
Sie hilft dabei die Frage zu beantworten „ Wer verwendet meine Entität und wie?“. Die Ansicht ist ähnlich der Explorer-Seite der abgeleiteten Hierarchie, umfasst jedoch mehr. Sie zeigt alle DBA-Beziehungen an, nicht nur die, die als Teil einer bestimmten Hierarchie definiert sind. Eine Hierarchiedefinition ist nicht erforderlich, da die angezeigte hierarchische Struktur einfach aus vorhandenen DBAs abgeleitet wird.  
  
Im Menü der Explorer-Seite listet das Entitätsabhängigkeiten-Menüelement alle Entitäten in dem Modell auf, von denen mindestens eine Entität abhängig ist. (D.h. mindestens eine Entität verfügt über ein DBA, das auf die aufgelistete Entität verweist). Die Anzahl der Abhängigkeiten (sowohl direkte als auch indirekte) wird neben dem Namen der Entität angezeigt, und die Liste wird anhand dieser Anzahl sortiert, wobei die Entitäten auf die am häufigsten verwiesen wird, oben stehen. Der nachfolgende Screenshot aus dem Kundenmodell der [Beispieldaten](https://msdn.microsoft.com/library/master-data-services-sample.aspx)zeigt, dass sieben Entitäten (direkt oder indirekt) auf die Entität „BigArea“ verweisen:  
  
![MDS_EntityDependencies_Menu.jpg](../master-data-services/media/mds-entitydependencies-menu-jpg.jpg)  
    
Durch Klicken auf dieses Menüelement wird die neue Explorer-Seite Entitätsabhängigkeiten für die BigArea-Entität geöffnet, die anzeigt, wie die Entitätselemente verwendet werden. Sie zeigt eine hierarchische Sicht, mit BigArea-Elementen an der Spitze der Struktur und darunter geschachtelt die mit den Elemente der sieben Entitäten, die sie verwenden.  
  
![MDS_EntityDependencies_Tree.jpg](../master-data-services/media/mds-entitydependencies-tree-jpg.jpg)  
    
Eine Entität wird möglicherweise von mehr als einer Entität direkt verwendet. Im obigen Beispiel verwenden sowohl die SubRegion- als auch die RegionClimate-Entitäten die Entität „Region“ (bzw. verfügen über DBA-Verweise darauf). Die Elemente der einzelnen verwendeten Entitäten werden unter einem übergeordneten Knoten gruppiert, der den Namen der Entität trägt:   
  
![MDS_EntityDependencies_Entity_Node.jpg](../master-data-services/media/mds-entitydependencies-entity-node-jpg.jpg)  
  
Bei diesen Containerstrukturknoten steht ein raster-ähnliches Symbol links neben dem Namen der Entität, und die Textfarbe hängt von der Tiefe der Hierarchieebene ab. Im obigen Beispiel wird gezeigt, dass die SubRegion „CDSR {Canada}“ über einen DBA-Verweis an die Region „CDR {Canada}“ verfügt, welche auf die Area „CDA {Canada}“ verweist, welche auf die „NAm {N. America}”-BigArea verweist.  
  
Die Ansicht ist vollständig bearbeitbar, genau wie die Hierarchie-Explorer-Seite. Hierarchische Beziehungen können in der Struktur geändert werden, indem untergeordneten Elementen an neue übergeordnete Elemente verschoben werden. Sie können dafür entweder ausgeschnitten und eingefügt oder markiert und gezogen werden. Die Werte anderer Elementattribute können im Detailbereich rechts neben der Struktur geändert werden.   
  
  
  
  

