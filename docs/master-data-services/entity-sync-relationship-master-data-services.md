---
title: Entitäten-Synchronisierungspartnerschaft (Master Data Services) | Microsoft-Dokumentation
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
ms.assetid: bd627a2d-dc64-47e9-9a71-2d0ad04b4962
caps.latest.revision: 6
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e8a275645f4c8e2ceba46dea689006ab6a0d8fa0
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="entity-sync-relationship-master-data-services"></a>Entitäten-Synchronisierungspartnerschaft (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Entitäten-Synchronisierung ist eine unidirektionale und wiederholbare Synchronisierung zwischen Entitätsversionen. Sie ermöglicht Ihnen, Entitätsdaten zwischen verschiedenen Modellen freizugeben. Sie können eine Single Source of Truth in einem Modell beibehalten und diese Masterdaten in anderen Modellen wiederverwenden. Sie können beispielsweise in einer Modellentität Daten zu US-Staaten speichern und diese Daten in anderen Modellen wiederverwenden.  
  
 Durch die Entitäten-Synchronisierung können Sie auch eine einmalige Kopie der Daten vornehmen.  
  
 Alle Blattelemente mit Freiform- und Dateiattributen in der Quellentität werden während der Ausführung der Synchronisierung mit der Zielentität synchronisiert. Dadurch werden Entitätsschema und -elemente erstellt, gelöscht und geändert.  
  
 Nachdem eine Synchronisierungspartnerschaft eingerichtet wurde, kann die Zielentität nur durch den Synchronisierungsprozess geändert werden. Eine Synchronisierungspartnerschaft kann jederzeit entfernt werden, um die Zielentität bearbeitbar zu machen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen und Verwenden einer Beziehung für die Entitätensynchronisierung &#40;Master Data Services&#41;](../master-data-services/create-and-execute-an-entity-sync-relationship-master-data-services.md)   
 [Bearbeiten und Löschen einer Entitäten-Synchronisierungspartnerschaft &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-entity-sync-relationship-master-data-services.md)  
  
  
