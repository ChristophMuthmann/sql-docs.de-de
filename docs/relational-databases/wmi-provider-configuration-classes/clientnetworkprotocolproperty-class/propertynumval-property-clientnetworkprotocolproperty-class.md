---
title: PropertyNumVal-Eigenschaft (ClientNetworkProtocolProperty-Klasse) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- PropertyNumVal Property (ClientNetworkProtocolProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- PropertyNumVal property
ms.assetid: 12b02d97-702b-434f-baf6-e49a6b2cd4de
caps.latest.revision: 28
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 02585007b677fe740cfb5079ee54ed752cb9aa94
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="propertynumval-property-clientnetworkprotocolproperty-class"></a>PropertyNumVal-Eigenschaft (ClientNetworkProtocolProperty-Klasse)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Ruft den numerischen Wert der aktuellen Eigenschaft ab, auf die durch den Wert der [PropertyIdx-Eigenschaft (ClientNetworkProtocolProperty-Klasse)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/propertyidx-property-clientnetworkprotocolproperty-class.md) verwiesen wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.PropertyNumVal [= value]  
```  
  
## <a name="parts"></a>Bestandteile  
 *Objekt*  
 Ein [ClientNetworkProtocolProperty-Klassenobjekt](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md) , das ein Attribut des vom [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Client verwendeten Netzwerkprotokolls darstellt.  
  
## <a name="property-valuereturn-value"></a>Eigenschaftswert/Rückgabewert  
 Ein u**int32** -Wert, der den numerischen Wert der aktuellen Eigenschaft angibt.  
  
## <a name="remarks"></a>Hinweise  
  
