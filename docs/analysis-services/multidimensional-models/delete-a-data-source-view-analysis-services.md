---
title: "Löschen eine Datenquellensicht (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deleting data source views
- data source views [Analysis Services], deleting
- removing data source views
ms.assetid: ae3f5ca0-ecbf-4b52-8386-eb457719d854
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b9566d114411dbe9c30d2cfe3ece265bc542f3c5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="delete-a-data-source-view-analysis-services"></a>Löschen einer Datenquellensicht (Analysis Services)
  Wenn Sie in einem OLAP-Projekt eine Datenquellensicht (Data Source View, DSV) nicht mehr verwenden, können Sie sie aus dem Projekt in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]löschen.  
  
 Das Löschen einer DSV kann nicht rückgängig gemacht werden. Eine gelöschte DSV kann in einem Projekt oder einer Datenbank von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nicht wiederhergestellt werden.  
  
 DSVs, von denen andere Objekte abhängen, können nicht aus einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank gelöscht werden, die von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] im Onlinemodus geöffnet wurde. Um eine DSV aus einem Projekt zu löschen, das mit einer auf einem Server ausgeführten Datenbank verbunden ist, müssen Sie zuerst alle von der DSV abhängigen Objekte in der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank löschen, bevor Sie die DSV selbst löschen können.  
  
 Durch das Löschen einer DSV werden andere [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekte, die davon abhängig sind, ungültig. Aus diesem Grund wird vor dem Löschen der DSV die Liste der Objekte angezeigt, die durch das Entfernen der DSV ungültig werden. Überprüfen Sie die Liste sorgfältig, um sicherzustellen, dass keine Objekte enthalten sind, die Sie weiterhin verwenden möchten.  
  
 ![Löschen Sie im Dialogfeld Objekte](../../analysis-services/multidimensional-models/media/ssas-olapdsv-deleteobjects.gif "Löschobjekte (Dialogfeld)")  
  
## <a name="see-also"></a>Siehe auch  
 [Datenquellsichten in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Ändern von Eigenschaften in einer Datenquellensicht &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/change-properties-in-a-data-source-view-analysis-services.md)  
  
  
