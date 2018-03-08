---
title: Eigenschaften - Benutzerhierarchien Ebene | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
ms.assetid: dabb7335-887b-442a-b67c-4901ba1242b7
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: db94622cfc84d97cb6f8e7578421f4933a63af94
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="user-hierarchies---level-properties"></a>Benutzerhierarchien - Eigenschaften auf Serverebene
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
In der folgenden Tabelle sind die Eigenschaften einer Ebene in einer benutzerdefinierten Hierarchie aufgelistet und beschrieben.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|Description|Enthält die Beschreibung der Ebene.|  
|HideMemberIf|Gibt an, ob und wann ein Element auf einer Ebene aus Clientanwendungen ausgeblendet werden sollte. Diese Eigenschaft kann die folgenden Werte annehmen:<br /><br /> Never<br /> Elemente werden nie ausgeblendet. Dies ist der Standardwert.<br /><br /> OnlyChildWithNoName<br /> Ein Element wird ausgeblendet, wenn das Element das einzige untergeordnete Element eines übergeordneten Elements ist und der Name des Elements leer ist.<br /><br /> OnlyChildWithParentName<br /> Ein Element wird ausgeblendet, wenn das Element das einzige untergeordnete Element eines übergeordneten Elements ist und der Name des Elements identisch mit dem des übergeordneten Elements ist.<br /><br /> NoName<br /> Ein Element wird ausgeblendet, wenn der Name des Elements leer ist.<br /><br /> ParentName<br /> Ein Element wird ausgeblendet, wenn der Name des Elements identisch mit dem Namen des übergeordneten Elements ist.|  
|ID|Enthält den eindeutigen Bezeichner (ID) der Ebene.|  
|Name|Enthält den Anzeigenamen der Ebene. Standardmäßig stimmt der Name einer Ebene mit dem Namen des Quellattributs überein.|  
|SourceAttribute|Enthält den Namen des Quellattributs, auf dem die Ebene basiert.|  
  
## <a name="see-also"></a>Siehe auch  
 [Eigenschaften der Benutzerhierarchie](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)  
  
  
