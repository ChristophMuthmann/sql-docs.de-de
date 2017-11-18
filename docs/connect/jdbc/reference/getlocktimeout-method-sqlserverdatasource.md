---
title: GetLockTimeout-Methode (SQLServerDataSource) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.getLockTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 676094e9-ec18-4524-9b21-1f9c5b16dd52
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: edbd984352f2b75711e9fc9a445a84066fb9f0ac
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
  
  

