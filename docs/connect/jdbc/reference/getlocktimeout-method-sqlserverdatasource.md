---
title: GetLockTimeout-Methode (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLockTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 676094e9-ec18-4524-9b21-1f9c5b16dd52
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: feac1b27f0a76492083b4cfcdb63968ff09ac5af
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getlocktimeout-method-sqlserverdatasource"></a>getLockTimeout-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt eine **Int** Wert, der die Anzahl von Millisekunden angibt, die die Datenbank bis zum Melden eines Sperrtimeouts gewartet wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int getLockTimeout()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Int** Wert, der die Anzahl der Millisekunden enthält, die die Datenbank gewartet wird.  
  
## <a name="remarks"></a>Hinweise  
 Das Sperrtimeout ist die Anzahl von Millisekunden bis zur Meldung eines Sperrtimeouts durch die Datenbank. Der Standardwert "-1" bedeutet, dass unbegrenzt gewartet wird. Wenn angegeben, wird dieser Wert den Standardwert für alle Anweisungen für die Verbindung sein.  
  
> [!NOTE]  
>  Bei dem Wert "0" wird nicht gewartet. Ist die lockTimeout-Eigenschaft nicht festgelegt, wird von der getLockTimeout-Methode der Standardwert "-1" zurückgegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
