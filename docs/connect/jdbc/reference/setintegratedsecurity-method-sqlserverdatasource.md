---
title: SetIntegratedSecurity-Methode (SQLServerDataSource) | Microsoft Docs
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
- SQLServerDataSource.setIntegratedSecurity
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c968ee4-b041-424a-bf69-cc2c4a4f51c6
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e2dca7a3c3cb2f6ac80fd9901c05e03135a42dc4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setintegratedsecurity-method-sqlserverdatasource"></a>setIntegratedSecurity-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt eine **booleschen** -Wert, der angibt, ob die IntegratedSecurity-Eigenschaft aktiviert ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setIntegratedSecurity(boolean enable)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Aktivieren*  
  
 **"true"** Wenn "IntegratedSecurity" aktiviert ist. Andernfalls lautet der Wert **false**.  
  
## <a name="remarks"></a>Hinweise  
 Legen Sie auf "**" true "**", um anzugeben, dass von Windows-Anmeldeinformationen verwendet werden [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] zur Authentifizierung des Benutzers der Anwendung. Wenn "**" true "**", die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] sucht den lokalen Computer im Cache für Anmeldeinformationen, die bereits bei der Anmeldung für Computer oder Netzwerk angegeben wurden. Wenn "**" false "**", den Benutzernamen und das Kennwort müssen angegeben werden.  
  
> [!NOTE]  
>  Diese Eigenschaft wird nur unterstützt, auf [!INCLUDE[msCoName](../../../includes/msconame_md.md)] Windows-Betriebssystemen.  
  
 Weitere Informationen zur Verwendung der integrierten Authentifizierung finden Sie unter [Erstellen der Verbindungs-URL](../../../connect/jdbc/building-the-connection-url.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
