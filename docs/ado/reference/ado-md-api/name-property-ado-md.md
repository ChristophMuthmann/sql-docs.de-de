---
title: Name-Eigenschaft (ADO MD) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Level::Name
- CubeDef::Name
- Member::Name
- Catalog::Name
- Dimension::Name
- Name
- Axis::Name
- Hierarchy::Name
helpviewer_keywords: Name property [ADO MD]
ms.assetid: 4a04380b-51dc-4aaf-8d25-123cdd589641
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0a26f37e1a3911658229258857676868af179133
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="name-property-ado-md"></a>Name-Eigenschaft (ADO MD)
Gibt den Namen eines Objekts an.  
  
## <a name="return-values"></a>Rückgabewerte  
 Gibt eine **Zeichenfolge** und ist schreibgeschützt.  
  
## <a name="remarks"></a>Hinweise  
 Sie können Abrufen der **Namen** Eigenschaft eines Objekts von einem Ordinalzahlverweis, Sie nach dem auf das Objekt, direkt anhand Ihres Namens verweisen können. Z. B. wenn `cdf.CubeDefs(0).Name` ergibt "Bobs Video Store", können Sie auf diese verweisen [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) als `cdf.CubeDefs("Bobs Video Store")`.  
  
## <a name="applies-to"></a>Gilt für  
  
||||  
|-|-|-|  
|[Axis-Objekt (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|[Katalogobjekt (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[CubeDef-Objekt (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|  
|[Dimensionsobjekt (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[Hierarchy-Objekt (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|[Level-Objekt (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|  
|[Member-Objekt (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)|||  
  
## <a name="see-also"></a>Siehe auch  
 [Katalog-Beispiel (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Caption-Eigenschaft (ADO MD)](../../../ado/reference/ado-md-api/caption-property-ado-md.md)   
 [Description-Eigenschaft (ADO MD)](../../../ado/reference/ado-md-api/description-property-ado-md.md)   
 [UniqueName-Eigenschaft (ADO MD)](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)
