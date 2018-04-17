---
title: PropertyIndex-Eigenschaft (SqlServiceAdvancedProperty-Klasse) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- PropertyIndex Property (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- PropertyIndex property
ms.assetid: b18b45a2-e187-44f5-a8c9-26fd9828b6c6
caps.latest.revision: 33
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 12605a96f4c37c30ef910001357c606b558a4bea
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="propertyindex-property-sqlserviceadvancedproperty-class"></a>PropertyIndex-Eigenschaft (SqlServiceAdvancedProperty-Klasse)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Ruft den Eigenschaftsindex ab, der die Position einer erweiterten Eigenschaft in einem Array erweiterter Eigenschaften angibt, das zu einem referenzierten Dienst gehört, oder legt diesen fest.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.PropertyIndex [= value]  
```  
  
## <a name="parts"></a>Bestandteile  
 *Objekt*  
 Ein Objekt der [SqlServiceAdvancedProperty-Klasse](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) , das eine erweiterte Eigenschaft darstellt.  
  
## <a name="property-valuereturn-value"></a>Eigenschaftswert/Rückgabewert  
 Ein **uint32** , Wert, der die Position der erweiterten Eigenschaft in dem Array erweiterter Eigenschaften angibt, das zu einem referenzierten Dienst gehört.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="see-also"></a>Siehe auch  
 [Starten und Beenden von Diensten](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
