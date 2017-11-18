---
title: SetTrustServerCertificate-Methode (SQLServerDataSource) | Microsoft Docs
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
- setTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- setTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 6c37b518-147e-4cd9-9eff-b48a3f5888c6
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 48b6e5131a81cf79a3eddf110c20a3340cbb48d7
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
 Wenn die TrustServerCertificate-Eigenschaft, um festgelegt wird **"true"**die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL-Zertifikat wird automatisch vertraut, wenn die Kommunikationsschicht mit SSL verschlüsselt ist. Das heißt, die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] kann nicht überprüft werden die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL-Zertifikat. Der Standardwert ist **false**.  
  
 Wenn die TrustServerCertificate-Eigenschaft, um festgelegt wird **"false"**, die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] wird das SSL-Serverzertifikat überprüfen.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

