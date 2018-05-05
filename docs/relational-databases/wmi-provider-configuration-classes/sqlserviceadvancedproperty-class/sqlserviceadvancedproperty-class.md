---
title: SqlServiceAdvancedProperty-Klasse | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- SqlServiceAdvancedProperty Class
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServiceAdvancedProperty class
ms.assetid: a5d06bde-6058-464c-a4aa-444d83f2331f
caps.latest.revision: 32
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 1ec3b9a9bcf17ef5f18087af64950ffba0bca6f1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserviceadvancedproperty-class"></a>SqlServiceAdvancedProperty-Klasse
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Die [SqlServiceAdvancedProperty-Klasse](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) stellt eine erweiterte Eigenschaft des Dienst dar, auf den durch das Objekt der [SqlService-Klasse](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) verwiesen wird.  
  
 Die [AdvancedProperties-Eigenschaft (SqlService-Klasse)](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/advancedproperties-property-sqlservice-class.md) verweist auf ein Array von [SqlServiceAdvancedProperty-Klassenobjekten](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) .  
  
 Die Klasse zum [Starten und Beenden von Diensten](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx) stellt Eigenschaften dar, die spezifisch für den Dienst sind. Diese Eigenschaften sind nicht in der Liste der Eigenschaften aufgeführt, die der [SqlService-Klasse](http://technet.microsoft.com/library/ms186497.aspx) zugeordnet sind. Mit der [SqlServiceAdvancedProperty-Klasse](http://technet.microsoft.com/library/ms182447.aspx) können Eigenschaften vom Typ string, numeric oder Boolean dargestellt werden. Sie können mithilfe dieser Klasse die einzigartigen Eigenschaften des angegebenen Diensts anzeigen.  
  
## <a name="see-also"></a>Siehe auch  
 [Starten, beenden und Anhalten von Diensten](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
