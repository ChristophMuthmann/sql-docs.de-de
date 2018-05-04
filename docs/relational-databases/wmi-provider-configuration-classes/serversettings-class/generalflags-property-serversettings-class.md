---
title: GeneralFlags-Eigenschaft (ServerSettings-Klasse) | Microsoft Docs
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
- GeneralFlags Property (ServerSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- GeneralFlags property
ms.assetid: 129bff8d-d2bc-4297-952f-d0a919d169f7
caps.latest.revision: 14
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0dc04c511ac575db0818fd1e0add63fb22107b2b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="generalflags-property-serversettings-class"></a>GeneralFlags-Eigenschaft (ServerSettings-Klasse)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Ruft die allgemeinen Flags ab, die der Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]zugeordnet sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.GeneralFlags [= value]  
```  
  
## <a name="parts"></a>Bestandteile  
 *Objekt*  
 Ein [ServerSettings-Klassenobjekt](../../../relational-databases/wmi-provider-configuration-classes/serversettings-class/serversettings-class.md) , das Servereinstellungen in einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]darstellt.  
  
## <a name="property-valuereturn-value"></a>Eigenschaftswert/Rückgabewert  
 Ein Array von [ServerSettingsGeneralFlag-Klassenobjekten](../../../relational-databases/wmi-provider-configuration-classes/serversettingsgeneralflag-class/serversettingsgeneralflag-class.md) , das die allgemeinen, der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]zugeordneten Flags angibt.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren von Servernetzwerkprotokollen und Netzwerkbibliotheken](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
