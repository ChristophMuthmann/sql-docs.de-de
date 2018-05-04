---
title: StartMode-Eigenschaft (SqlService-Klasse) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- StartMode Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- StartMode property
ms.assetid: c0c2c7f8-d4ae-44f2-ad8e-aecfcb7c2878
caps.latest.revision: 36
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 4f1878fb6f80d16e7473ed431f22a4a833e9491e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="startmode-property-sqlservice-class"></a>StartMode-Eigenschaft (SqlService-Klasse)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Ruft den Startmodus des Dienstes ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.StartMode [= value]  
```  
  
## <a name="parts"></a>Bestandteile  
 *Objekt*  
 Ein [SqlService-Klassenobjekt](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) , das den Dienst darstellt.  
  
## <a name="property-valuereturn-value"></a>Eigenschaftswert/Rückgabewert  
 Ein uint32-Wert, der den Modus des Diensts angibt.  
  
 Folgende Werte sind möglich:  
  
 Neustart  
 Wert = 0. Dienst wurde durch das Betriebssystemladeprogramm gestartet. Diese Option ist nur für Treiberdienste gültig.  
  
 System  
 Wert = 1. Dienst gestartet, indem die **IoInitSystem** Methode. Diese Option ist nur für Treiberdienste gültig.  
  
 Automatisch  
 Wert = 2. Der Dienst soll während des Systemstarts automatisch vom Dienstkontroll-Manager gestartet werden.  
  
 Manuell  
 Wert = 3. Dienst vom Computer-Manager gestartet werden kann, wenn ein Prozess aufruft der **StartService** Methode.  
  
 Disabled  
 Wert = 4. Der Dienst kann nicht gestartet werden.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="see-also"></a>Siehe auch  
 [Starten und Beenden von Diensten](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
