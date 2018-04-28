---
title: SetLockTimeout-Methode (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerDataSource.setLockTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 10dca5aa-1851-4326-9ae9-7a8430d12d11
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 93c6502ea87623c39c7a013e694378b4e967f4ce
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="setlocktimeout-method-sqlserverdatasource"></a>setLockTimeout-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt eine **Int** Wert, der die Anzahl von Millisekunden, die gewartet wird, bevor die Datenbank ein Sperrtimeout meldet.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setLockTimeout(int lockTimeout)  
```  
  
#### <a name="parameters"></a>Parameter  
 *lockTimeout*  
  
 Ein **Int** Wert, der die Anzahl der zu wartenden Millisekunden enthält.  
  
## <a name="remarks"></a>Hinweise  
 Das Sperrtimeout ist die Anzahl von Millisekunden bis zur Meldung eines Sperrtimeouts durch die Datenbank. Der Standardwert "-1" bedeutet, dass unbegrenzt gewartet wird. Wenn angegeben, wird dieser Wert den Standardwert für alle Anweisungen für die Verbindung sein.  
  
> [!NOTE]  
>  Bei dem Wert "0" wird nicht gewartet. Wenn die LockTimeout-Eigenschaft nicht festgelegt ist, die [GetLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md) Methode der Standardwert "-1" zurückgegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
