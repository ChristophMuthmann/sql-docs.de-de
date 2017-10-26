---
title: GetPacketSize-Methode (SQLServerDataSource) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.getPacketSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b2e9f01a-2e51-47e5-90bf-43c62d1be74d
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9788a804580b88d9f65f9df8e176d883863aa1a0
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getpacketsize-method-sqlserverdatasource"></a>getPacketSize-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt die aktuelle Netzwerkpaketgröße verwendet, um die Kommunikation mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], angegeben in Bytes.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int getPacketSize()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Int** Wert, der die aktuelle Netzwerkpaketgröße enthält.  
  
## <a name="remarks"></a>Hinweise  
 Wenn die PacketSize-Eigenschaft nicht festgelegt ist, gibt die GetPacketSize-Methode den Standardwert von 8000 zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

