---
title: Dimension-Typen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- time dimensions [Analysis Services]
- quantitative dimensions [Analysis Services]
- BillOfMaterials dimension [Analysis Services]
- geography dimensions
- utility dimensions [Analysis Services]
- channel dimensions
- dimensions [Analysis Services], types
- products dimensions [Analysis Services]
- account dimensions [Analysis Services]
- organization dimensions
- currency dimensions [Analysis Services]
- rates dimensions
- promotion dimensions
- scenario dimensions [Analysis Services]
- customers dimensions [Analysis Services]
- Type property
ms.assetid: bd3195da-e762-4c98-b643-34c76e842343
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5fa77532b4c674c4b5035cf6b591b973008ae6e5
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="database-dimension-properties---types"></a>Eigenschaften von Datenbankdimensionen - Typen
  Die **Typ** Einstellung der Eigenschaft enthält Informationen zum Inhalt einer Dimension für Server- und Clientanwendungen. In einigen Fällen die **Typ** Einstellung nur stellt Hinweis für Clientanwendungen bereit und ist optional. In anderen Fällen z. B. **Konten** oder **Zeit** Dimensionen, die **Typ** eigenschafteneinstellungen für die Dimension und ihre Attribute bestimmen das Verhalten für bestimmte Server basierenden und kann erforderlich sein, um bestimmte Verhalten im Cube zu implementieren. Z. B. die **Typ** -Eigenschaft einer Dimension kann festgelegt werden, um **Konten** , um den Clientanwendungen mitzuteilen, dass die Standarddimension Kontoattribute enthält. Weitere Informationen über die Zeit, Konto und währungsdimensionen finden Sie unter [erstellen eine datumstypdimension](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md), [Erstellen eines Finanzkontos des über-und untergeordneten Typs Dimension](../../analysis-services/multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md), und [erstellen Sie eine Währung Geben Sie die Dimension](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md).  
  
 Die Standardeinstellung für den Dimensionstyp ist **reguläre**, womit keine Annahmen zum Inhalt der Dimension gemacht. Dies ist die Standardeinstellung für alle Dimensionen, wenn Sie erstmalig eine Dimension definieren, es sei denn, Sie geben **Zeit** beim Definieren der Dimensions mithilfe des Dimensions-Assistenten. Sie sollten auch lassen **reguläre** den Dimensionstyp aus, wenn der Dimensions-Assistent einen geeigneten Typ für den Dimensionstyp nicht aufgeführt ist.  
  
## <a name="available-dimension-types"></a>Verfügbare Dimensionstypen  
 Die folgende Tabelle beschreibt die in verfügbaren Dimensionstypen [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Dimensionstyp|Description|  
|--------------------|-----------------|  
|Regulär|Eine Dimension, für die kein spezieller Dimensionstyp festgelegt wurde|  
|Uhrzeit|Eine Dimension, deren Attribute Zeiträume darstellen, z. B. Jahre, Semester, Quartale, Monate und Tage|  
|Organization|Eine Dimension, deren Attribute organisatorische Informationen darstellen, z. B. Angestellte oder Tochterunternehmen|  
|Geography|Eine Dimension, deren Attribute geografische Informationen darstellen, z. B. Städte oder Postleitzahlen|  
|BillOfMaterials|Eine Dimension, deren Attribute Informationen zu Inventar oder Produktion darstellen, z. B. Stücklisten für Produkte|  
|Konten|Eine Dimension, deren Attribute ein Kontodiagramm für Finanzberichte darstellen|  
|Customers|Eine Dimension, deren Attribute Kunden- oder Kontaktinformationen darstellen|  
|Products|Eine Dimension, deren Attribute Produktinformationen darstellen|  
|Szenario|Eine Dimension, deren Attribute Informationen für Planung oder strategische Analyse darstellen|  
|Quantitative|Eine Dimension, deren Attribute quantitative Informationen darstellen|  
|Hilfsprogramm|Eine Dimension, deren Attribute verschiedene Informationen darstellen|  
|Währung|Dieser Dimensionstyp enthält Währungsdaten und Metadaten|  
|Rates|Eine Dimension, deren Attribute Währungskursinformationen darstellen|  
|Channel|Eine Dimension, deren Attribute verschiedene Kanalinformationen darstellen|  
|Promotion|Eine Dimension, deren Attribute verschiedene Marketinghöherstufungsinformationen darstellen|  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie eine Dimension anhand einer vorhandenen Tabelle](../../analysis-services/multidimensional-models/create-a-dimension-by-using-an-existing-table.md)   
 [Dimensionen &#40;Analysis Services – mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  

