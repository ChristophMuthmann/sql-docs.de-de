---
title: SetServiceAccountPassword-Methode (SqlService-Klasse) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: SetServiceAccountPassword Method (SqlService Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: SetServiceAccountPassword method
ms.assetid: e577a1ac-985c-4799-bb38-9393efc3def2
caps.latest.revision: "36"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ed9af242ee2f4c3083483ccc93b5de09b1cce3be
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="setserviceaccountpassword-method-sqlservice-class"></a>SetServiceAccountPassword-Methode (SqlService-Klasse)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Ändert das Kennwort für das Konto, dem unter der referenzierte Dienst ausgeführt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.SetServiceAccountPassword(AccountOldPassword , ServiceStartPassword)  
```  
  
## <a name="parts"></a>Bestandteile  
 *Objekt*  
 Ein [SqlService-Klassenobjekt](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) , das den Dienst darstellt.  
  
#### <a name="parameters"></a>Parameter  
 *AccountOldPassword*  
 Ein Zeichenfolgenwert, der das bestehende Kennwort für das Konto angibt.  
  
 *ServiceStartPassword*  
 Ein Zeichenfolgenwert, der das neue Kennwort für das Konto angibt.  
  
## <a name="property-valuereturn-value"></a>Eigenschaftswert/Rückgabewert  
 Ein **uint32** -Wert, der 0 beträgt, wenn der Dienst erfolgreich geändert wurde. Der Wert beträgt 1, wenn die Anforderung nicht unterstützt wird; jede andere Zahl gibt einen Fehler an.  
  
## <a name="remarks"></a>Hinweise  
  
