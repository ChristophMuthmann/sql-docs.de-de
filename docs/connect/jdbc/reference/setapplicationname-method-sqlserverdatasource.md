---
title: SetApplicationName-Methode (SQLServerDataSource) | Microsoft Docs
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
- SQLServerDataSource.setApplicationName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 24d6e48d-53c4-4da2-a6de-1cdff463c9cd
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d266d7b3853fdb75cee7f00fb64dbec045d6d737
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setapplicationname-method-sqlserverdatasource"></a>setApplicationName-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den Anwendungsnamen fest.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setApplicationName(java.lang.String applicationName)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Parameter "ApplicationName"*  
  
 Ein **Zeichenfolge** , die den Namen der Anwendung enthält.  
  
## <a name="remarks"></a>Hinweise  
 Der Anwendungsname wird verwendet, um die jeweilige Anwendung in verschiedenen identifiziert [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] -profilerstellungs- und Protokollierungstools. Wenn der Anwendungsname nicht festgelegt ist, gibt die GetApplicationName-Methode der nicht lokalisierte Zeichenfolge "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]".  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
