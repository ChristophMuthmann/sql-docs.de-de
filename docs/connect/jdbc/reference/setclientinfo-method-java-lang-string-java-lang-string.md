---
title: SetClientInfo-Methode (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8d050831-8305-48a8-bd22-207932111040
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b464cc1e1f63612557d6358f40b6c45cafc726e5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setclientinfo-method-javalangstring-javalangstring"></a>setClientInfo-Methode (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den Wert der angegebenen Eigenschaft für Clientinformationen fest.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setClientInfo (java.lang.String name,  
                           java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parameter  
 *name*  
  
 Eine Zeichenfolge mit dem Namen der Eigenschaft für Clientinformationen fest.  
  
 *value*  
  
 Eine Zeichenfolge, die enthält den Wert, um auf die Eigenschaft für Clientinformationen festgelegt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetClientInfo-Methode wird von der SetClientInfo-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
 Die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] unterstützt keine Eigenschaften für Clientinformationen. In der JDBC Driver-Version 2.0 wird von dieser Methode eine Warnung für eine Eigenschaft generiert. Anwendungen sollten verwenden [GetWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md) Methode der [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse, um eine Warnung abzurufen.  
  
## <a name="see-also"></a>Siehe auch  
 [SetClientInfo-Methode &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

