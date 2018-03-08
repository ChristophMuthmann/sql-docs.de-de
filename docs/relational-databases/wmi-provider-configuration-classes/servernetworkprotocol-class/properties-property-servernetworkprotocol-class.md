---
title: Properties-Eigenschaft (ServerNetworkProtocol-Klasse) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Properties Property (ServerNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Properties property
ms.assetid: 6c971bfc-c277-4c1e-a06e-146dcc34e759
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ab6a6ff58d40e5e1e5ee30e38dd8d958c8667f91
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="properties-property-servernetworkprotocol-class"></a>Properties-Eigenschaft (ServerNetworkProtocol-Klasse)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
Ruft die Eigenschaften ab, die dem Servernetzwerkprotokoll zugeordnet sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.Properties [= value]  
```  
  
## <a name="parts"></a>Bestandteile  
 *Objekt*  
 Ein [ServerNetworkProtocol-Klassenobjekt](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/servernetworkprotocol-class.md) , das das Netzwerkprotokoll darstellt, das von der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]verwendet wird.  
  
## <a name="property-valuereturn-value"></a>Eigenschaftswert/Rückgabewert  
 Ein Array von [ServerNetworkProtocolProperty-Klassenobjekten](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolproperty-class/servernetworkprotocolproperty-class.md) , die die vom Server-Netzwerkprotokoll unterstützten Eigenschaften darstellen.  
  
## <a name="remarks"></a>Hinweise  
  
