---
title: SetTrustServerCertificate-Methode (SQLServerDataSource) | Microsoft Docs
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
- setTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- setTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 6c37b518-147e-4cd9-9eff-b48a3f5888c6
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2b4a1788fc4e4578cf8b80893d6d1f2c80fa6e3e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="settrustservercertificate-method-sqlserverdatasource"></a>setTrustServerCertificate-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt eine **booleschen** -Wert, der angibt, ob die Eigenschaft "TrustServerCertificate" aktiviert ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setTrustServerCertificate(boolean trustServerCertificate)  
```  
  
#### <a name="parameters"></a>Parameter  
 *"TrustServerCertificate"*  
  
 **"true"** das Serverzertifikat für die Secure Sockets Layer (SSL) automatisch vertraut werden soll, wenn die Kommunikationsschicht mit SSL verschlüsselt ist. Andernfalls lautet der Wert **false**.  
  
## <a name="remarks"></a>Hinweise  
 Wenn die TrustServerCertificate-Eigenschaft, um festgelegt wird **"true"** die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL-Zertifikat wird automatisch vertraut, wenn die Kommunikationsschicht mit SSL verschlüsselt ist. Das heißt, die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] kann nicht überprüft werden die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL-Zertifikat. Der Standardwert ist **false**.  
  
 Wenn die TrustServerCertificate-Eigenschaft, um festgelegt wird **"false"**, die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] wird das SSL-Serverzertifikat überprüfen.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
