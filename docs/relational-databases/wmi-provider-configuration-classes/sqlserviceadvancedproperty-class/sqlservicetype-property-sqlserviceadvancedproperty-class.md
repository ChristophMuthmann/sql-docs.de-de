---
title: SqlServiceType-Eigenschaft (SqlServiceAdvancedProperty-Klasse) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- SqlServiceType Property (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServiceType property
ms.assetid: 20f1663a-9a14-4f14-8c1b-8aa133e272c3
caps.latest.revision: 42
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d7f05fed535cd25016287672d22c541d8f5d474c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlservicetype-property-sqlserviceadvancedproperty-class"></a>SqlServiceType-Eigenschaft (SqlServiceAdvancedProperty-Klasse)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Ruft den Typ des verwalteten Diensts ab, der der erweiterten Eigenschaft zugeordnet ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.SetBoolValue(NumValue)  
```  
  
## <a name="parts"></a>Bestandteile  
 *Objekt*  
 Ein Objekt der [SqlServiceAdvancedProperty-Klasse](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) , das eine erweiterte Eigenschaft darstellt.  
  
## <a name="property-valuereturn-value"></a>Eigenschaftswert/Rückgabewert  
 Ein uint32-Wert, der den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Diensttyp angibt.  
  
## <a name="remarks"></a>Hinweise  
 Folgenden Rückgabewerte sind möglich:  
  
|Typ|Definition|  
|----------|----------------|  
|*1*|MSSQLSERVER ist der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienst.|  
|*2*|SQLSERVERAGENT ist der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent-Dienst.|  
|*3*|MSFTESQL ist der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienst für das Volltextsuchmodul.|  
|*4*|MsDtsServer ist der [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Dienst.|  
|*5*|MSSQLServerOLAPService ist der [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Dienst.|  
|*6*|ReportServer ist der [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] -Dienst.|  
|*7*|SQLBrowser ist der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Browser-Dienst.|  
  
## <a name="see-also"></a>Siehe auch  
 [Starten und Beenden von Diensten](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
