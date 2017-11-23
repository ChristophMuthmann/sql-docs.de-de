---
title: GetTrustStore-Methode (SQLServerDataSource) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: getTrustStore Method (SQLServerDataSource)
apilocation: getTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 8f5850e4-8627-49a8-ba0e-b1f4014322a5
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bbff42d43e1bc07dcb163234cab70fcdd9d0582f
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="gettruststore-method-sqlserverdatasource"></a>getTrustStore-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt den Pfad (einschließlich Dateiname) zur trustStore-Zertifikatsdatei zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.String getTrustStore()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** , enthält den Pfad (einschließlich des Dateinamens) der TrustStore-Zertifikatsdatei, oder Null, wenn kein Wert festgelegt ist.  
  
## <a name="remarks"></a>Hinweise  
 Wenn die TrustStore-Eigenschaft nicht festgelegt ist, die [GetTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md) Methode gibt null zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
