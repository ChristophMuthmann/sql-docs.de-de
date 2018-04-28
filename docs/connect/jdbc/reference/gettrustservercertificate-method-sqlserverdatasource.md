---
title: GetTrustServerCertificate-Methode (SQLServerDataSource) | Microsoft Docs
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
- getTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- getTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: e4f443cc-b5d7-4859-81df-836a8642ed07
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fc7678ab661973525fab4219acbcacd3c874aa34
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="gettrustservercertificate-method-sqlserverdatasource"></a>getTrustServerCertificate-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt eine **booleschen** -Wert, der angibt, ob die Eigenschaft "TrustServerCertificate" aktiviert ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean getTrustServerCertificate()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** Wenn "TrustServerCertificate" aktiviert ist. Andernfalls lautet der Wert **false**.  
  
## <a name="remarks"></a>Hinweise  
 Wenn die TrustServerCertificate-Eigenschaft, um festgelegt wird **"true"** die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Secure Sockets Layer (SSL)-Zertifikat wird automatisch vertraut, wenn die Kommunikationsschicht mit SSL verschlüsselt ist. Das heißt, die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] kann nicht überprüft werden die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL-Zertifikat. Der Standardwert ist **false**.  
  
 Wenn die TrustServerCertificate-Eigenschaft, um festgelegt wird **"false"**, die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] wird das SSL-Serverzertifikat überprüfen.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
