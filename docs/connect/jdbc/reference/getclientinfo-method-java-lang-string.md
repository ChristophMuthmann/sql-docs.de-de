---
title: GetClientInfo-Methode (java.lang.String) | Microsoft Docs
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
ms.assetid: e8e632c4-d6cc-4c5e-b6ad-873579343b19
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e0f92e5db61ef0b778e293ea61b25ad61956986a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getclientinfo-method-javalangstring"></a>getClientInfo-Methode (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert einer angegebenen Eigenschaft für Clientinformationen ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.String getClientInfo (java.lang.String name)  
```  
  
#### <a name="parameters"></a>Parameter  
 *name*  
  
 Eine Zeichenfolge, die den Namen der abzurufenden Eigenschaft für Clientinformationen enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Eine Zeichenfolge, die den Wert der Eigenschaft für Clientinformationen enthält.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetClientInfo-Methode wird von der GetClientInfo-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
 Die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] unterstützt keine Client-Info-Eigenschaften. Folglich Methodenrückgabe **null**.  
  
 Auf ähnliche Weise können Anwendungen die [GetClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) Methode der [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) Klasse zum Abrufen einer Liste von den Eigenschaften für Clientinformationen, die der Treiber unterstützt. Die [GetClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) Methode gibt ein leeres Resultset zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [GetClientInfo-Methode &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

