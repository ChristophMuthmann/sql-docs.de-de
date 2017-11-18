---
title: GetPortNumber-Methode (SQLServerDataSource) | Microsoft Docs
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
- SQLServerDataSource.getPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e5dc38d0-4340-4ad7-a56e-1d2a0f0fd846
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2cf2e36d551a3b9e2e6e990c4945708043277e6a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getportnumber-method-sqlserverdatasource"></a>getPortNumber-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt die aktuelle Portnummer, die verwendet wird, für die Kommunikation mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int getPortNumber()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Int** Wert, der die aktuelle Portnummer enthält.  
  
## <a name="remarks"></a>Hinweise  
 Die Portnummer ist die TCP/IP-Portnummer, die verwendet wird, beim Öffnen einer Socketverbindung [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Ist die portNumber-Eigenschaft nicht festgelegt, wird von der getPortNumber-Methode der Standardwert "1433" zurückgegeben.  
  
> [!NOTE]  
>  Die [SetPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md) Methode führt kein bereichsprüfung auf dem Portwert übergeben. Sie können Portnummern weitergeben, die nicht gültig ist, z. B. 99999, ohne dabei einen Fehler auszulösen.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

