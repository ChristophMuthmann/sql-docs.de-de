---
title: GetApplicationName-Methode (SQLServerDataSource) | Microsoft Docs
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
apiname: SQLServerDataSource.getApplicationName
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: f71e501c-ccd7-4a1e-b6ea-4d47a81c18c6
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1003b679dc8e34da4196fbfd92bef729a17310ba
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="getapplicationname-method-sqlserverdatasource"></a>getApplicationName-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt den Anwendungsnamen zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.String getApplicationName()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** , enthält den Anwendungsnamen oder "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]" ist kein Wert festgelegt ist.  
  
## <a name="remarks"></a>Hinweise  
 Der Anwendungsname wird verwendet, um die jeweilige Anwendung in verschiedenen identifiziert [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] -profilerstellungs- und Protokollierungstools. Wenn der Anwendungsname nicht festgelegt ist, gibt die GetApplicationName-Methode der nicht lokalisierte Zeichenfolge "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]".  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
