---
title: SetHostNameInCertificate-Methode (SQLServerDataSource) | Microsoft Docs
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
ms.topic: conceptual
apiname:
- setHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- setHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 2bcf4f2e-a103-4374-abc4-ffad4ce8e3c0
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aae071ffe1c3bee7017dfdf46440829d231207f4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sethostnameincertificate-method-sqlserverdatasource"></a>setHostNameInCertificate-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den Hostnamen bei der Überprüfung verwendet werden die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Secure Sockets Layer (SSL)-Zertifikat.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setHostNameInCertificate(java.lang.String hostNameInCertificate)  
```  
  
#### <a name="parameters"></a>Parameter  
 *hostNameInCertificate*  
  
 Ein **Zeichenfolge** , die den Namen des Hosts enthält.  
  
## <a name="remarks"></a>Hinweise  
 Der HostNameInCertificate-Wert dient zum Überprüfen der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL-Zertifikat, wenn die Kommunikationsschicht mit SSL verschlüsselt ist. Der Standardwert ist "null".  
  
 Wenn die HostNameInCertificate-Eigenschaft, auf null oder nicht angegeben festgelegt ist, die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] verwendet den Wert der ServerName-Eigenschaft überprüft die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SSL-Zertifikat. Ist die hostNameInCertificate-Eigenschaft auf eine Zeichenfolge oder auf eine leere Zeichenfolge festgelegt, wird das SSL-Zertifikat des Servers anhand dieses Werts überprüft.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
