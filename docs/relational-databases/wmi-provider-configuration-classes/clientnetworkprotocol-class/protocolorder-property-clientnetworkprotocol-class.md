---
title: ProtocolOrder-Eigenschaft (ClientNetworkProtocol-Klasse) | Microsoft Docs
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
- ProtocolOrder Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolOrder property
ms.assetid: aa09b8ab-37db-4406-8973-acf503855fd2
caps.latest.revision: 34
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9804106693da8b5f3a60cecf6d2182b5c9a9e75c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="protocolorder-property-clientnetworkprotocol-class"></a>ProtocolOrder-Eigenschaft (ClientNetworkProtocol-Klasse)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Ruft die fortlaufende Nummer des Netzwerkprotokolls ab, auf das aktuell verwiesen wird. Dies erfolgt gemäß der [SetOrderValue-Methode (ClientNetworkProtocol Class)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/setordervalue-method-clientnetworkprotocol-class.md) -Methode.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.ProtocolOrder [= value]  
```  
  
## <a name="parts"></a>Bestandteile  
 *Objekt*  
 A [ClientNetworkProtocol-Klassenobjekt](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) , das das vom [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Client verwendete Netzwerkprotokoll darstellt.  
  
## <a name="property-valuereturn-value"></a>Eigenschaftswert/Rückgabewert  
 Ein **uint32** -Wert, der die fortlaufende Nummer des derzeitig referenzierten Clientnetzwerkprotokolls angibt, das durch die **OrderValue** -Methode festgelegt ist. Wenn das Clientnetzwerkprotokoll deaktiviert ist, ist dieser Wert Null.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren von Clientprotokollen](http://technet.microsoft.com/library/ms181035.aspx)   
 [Konfigurieren von Clientnetzwerkprotokollen und Netzwerkbibliotheken](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
