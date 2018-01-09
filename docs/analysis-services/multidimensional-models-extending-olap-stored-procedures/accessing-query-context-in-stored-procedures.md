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
ms.openlocfilehash: 5b7a0c3e57a5249a26bf13a2cf9709e58df85da8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="accessing-query-context-in-stored-procedures"></a>Zugreifen auf den Abfragekontext in gespeicherten Prozeduren
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Der Ausführungskontext einer gespeicherten Prozedur steht innerhalb des Codes der gespeicherten Prozedur als der **Kontext** Objekt von der ADOMD.NET-Serverobjektmodells. Der Kontext ist schreibgeschützt und kann nicht von der gespeicherten Prozedur geändert werden. Für dieses Objekt stehen die folgenden Eigenschaften zur Verfügung.  
  
|Eigenschaft|Typ|Description|  
|--------------|----------|-----------------|  
|**CurrentCube**|Cube|Der Cube für den aktuellen Abfragekontext.|  
|**CurrentDatabaseName**|Zeichenfolge|Der Bezeichner der aktuellen Datenbank.|  
|**CurrentConnection**|Verbindung|Ein Verweis auf das Verbindungsobjekt im aktuellen Kontext.|  
|**Übergeben Sie**|Integer|Die Durchlaufnummer für den aktuellen Kontext.|  
  
 Die **Kontext** Objekt vorhanden ist, wenn das Objektmodell von MDX (Multidimensional Expressions) in einer gespeicherten Prozedur verwendet wird. Es ist nicht verfügbar, wenn das MDX-Objektmodell auf einem Client verwendet wird. Die **Kontext** Objekt nicht explizit übergeben oder von der gespeicherten Prozedur zurückgegeben wird. Es ist während der Ausführung der gespeicherten Prozedur verfügbar.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Mehrdimensionales Modell Assemblys-Verwaltung](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definieren gespeicherter Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
