---
title: SetNumValue-Methode (SqlServiceAdvancedProperty-Klasse) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: SetNumValue Method (SqlServiceAdvancedProperty Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: SetNumValue method
ms.assetid: a5e1056b-0b75-4ad6-99c1-89246010d815
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 19b34c9a3a923b8cb547cef5667f045b3f911a0c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="setnumvalue-method-sqlserviceadvancedproperty-class"></a>SetNumValue-Methode (SqlServiceAdvancedProperty-Klasse)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Legt den numerischen Wert einer Eigenschaft fest.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.SetNumValue(NumValue)  
```  
  
## <a name="parts"></a>Bestandteile  
 *Objekt*  
 Ein Objekt der [SqlServiceAdvancedProperty-Klasse](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) , das eine erweiterte Eigenschaft darstellt.  
  
#### <a name="parameters"></a>Parameter  
  
|Parameter|Description|  
|---------------|-----------------|  
|*NumValue*|Ein **uint32** -Wert, der den Wert der erweiterten Eigenschaft angibt.|  
  
## <a name="property-valuereturn-value"></a>Eigenschaftswert/Rückgabewert  
 Ein **uint32** -Wert, der 0 beträgt, wenn der Dienst erfolgreich geändert wurde. Der Wert beträgt 1, wenn die Anforderung nicht unterstützt wird; jede andere Zahl gibt einen Fehler an.  
  
## <a name="remarks"></a>Hinweise  
 Der Eigenschaftswert muss numerisch sein, damit die Eigenschaft auf einen numerischen Wert festgelegt werden kann.  
  
## <a name="see-also"></a>Siehe auch  
 [Starten und Beenden von Diensten](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
