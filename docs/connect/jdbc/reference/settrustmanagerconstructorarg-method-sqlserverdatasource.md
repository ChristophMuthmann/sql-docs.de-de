---
title: SetTrustManagerConstructorArg-Methode (SQLServerDataSource) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2018
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
- SQLServerDataSource.setTrustManagerConstructorArg
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d121f141ee47d42141b190283762ab636ccdbe24
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2018
---
# <a name="settrustmanagerconstructorarg-method-sqlserverdatasource"></a>SetTrustManagerConstructorArg-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den Zeichenfolgenwert der Verbindungseigenschaft TrustManagerConstructorArg fest.
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setTrustManagerConstructorArg(java.lang.String trustManagerClass)  
```  
  
#### <a name="parameters"></a>Parameter  
 *trustManagerClass*  
  
 Ein **Zeichenfolge** , die den voll gekennzeichneten Klassennamen, der eine benutzerdefinierte javax.net.ssl.TrustManager enthält.
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
