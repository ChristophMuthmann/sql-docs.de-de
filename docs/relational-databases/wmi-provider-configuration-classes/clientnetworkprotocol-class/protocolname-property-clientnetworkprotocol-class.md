---
title: ProtocolName-Eigenschaft (ClientNetworkProtocol-Klasse) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ProtocolName Property (ClientNetworkProtocol Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: ProtocolName property
ms.assetid: f8527121-fbcd-4d30-9b4a-1461149cb5a8
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5add6edd7e374c2e6695d75d00c256b2ee95d9a9
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="protocolname-property-clientnetworkprotocol-class"></a>ProtocolName-Eigenschaft (ClientNetworkProtocol-Klasse)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Ruft den Namen des aktuellen Netzwerkprotokolls gemäß der [Konfigurieren von Clientprotokollen](http://technet.microsoft.com/library/ms181035.aspx).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.ProtocolName [= value]  
```  
  
## <a name="parts"></a>Bestandteile  
 *Objekt*  
 A [ClientNetworkProtocol-Klassenobjekt](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) , das das vom [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Client verwendete Netzwerkprotokoll darstellt.  
  
## <a name="property-valuereturn-value"></a>Eigenschaftswert/Rückgabewert  
 Ein Zeichenfolgenwert, der den Namen des aktuellen Clientnetzwerkprotokolls angibt, auf das in der [SetOrderValue-Methode (ClientNetworkProtocol-Klasse)](http://technet.microsoft.com/library/ms179295.aspx)verwiesen wird.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren von Clientnetzwerkprotokollen und Netzwerkbibliotheken](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
