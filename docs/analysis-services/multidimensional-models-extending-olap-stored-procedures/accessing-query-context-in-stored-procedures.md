---
title: Zugreifen auf den Abfragekontext in gespeicherten Prozeduren | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- execution context [Analysis Services]
- stored procedures [Analysis Services], query context
- Context object
- query context [Analysis Services]
ms.assetid: bdc7dad8-2f22-4265-aba4-a3a451527840
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a9ab0de9eae86293f25781cc5b85f175037f1ffc
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="accessing-query-context-in-stored-procedures"></a>Zugreifen auf den Abfragekontext in gespeicherten Prozeduren
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Der Ausführungskontext einer gespeicherten Prozedur steht innerhalb des Codes der gespeicherten Prozedur als der **Kontext** Objekt von der ADOMD.NET-Serverobjektmodells. Der Kontext ist schreibgeschützt und kann nicht von der gespeicherten Prozedur geändert werden. Für dieses Objekt stehen die folgenden Eigenschaften zur Verfügung.  
  
|Eigenschaft|Typ|Description|  
|--------------|----------|-----------------|  
|**CurrentCube**|Cube|Der Cube für den aktuellen Abfragekontext.|  
|**CurrentDatabaseName**|String|Der Bezeichner der aktuellen Datenbank.|  
|**CurrentConnection**|Verbindung|Ein Verweis auf das Verbindungsobjekt im aktuellen Kontext.|  
|**Übergeben Sie**|Integer|Die Durchlaufnummer für den aktuellen Kontext.|  
  
 Die **Kontext** Objekt vorhanden ist, wenn das Objektmodell von MDX (Multidimensional Expressions) in einer gespeicherten Prozedur verwendet wird. Es ist nicht verfügbar, wenn das MDX-Objektmodell auf einem Client verwendet wird. Die **Kontext** Objekt nicht explizit übergeben oder von der gespeicherten Prozedur zurückgegeben wird. Es ist während der Ausführung der gespeicherten Prozedur verfügbar.  
  
## <a name="see-also"></a>Siehe auch  
 [Mehrdimensionales Modell Assemblys-Verwaltung](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definieren gespeicherter Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
