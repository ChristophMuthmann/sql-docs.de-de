---
title: SetClientInfo-Methode (java.util.Properties) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b2a8ec0b-40a2-44d1-90d9-a810d4132e56
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0785a1ee2c2aa96f6058e0dba2296af524cd345e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setclientinfo-method-javautilproperties"></a>setClientInfo-Methode (java.util.Properties)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den Wert der Eigenschaften für Clientinformationen der Verbindung fest.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setClientInfo (java.util.Properties properties)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Eigenschaften*  
  
 Ein Objekt für Eigenschaften, die die Liste der Eigenschaften für Clientinformationen festzulegende enthält.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetClientInfo-Methode wird von der SetClientInfo-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
 Die [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] unterstützt keine Eigenschaften für Clientinformationen. Diese Methode werden Warnungen generiert, wenn die *Eigenschaften* input-Parameters verweist nicht auf einen leeren Eigenschaftensatz. Das heißt, dass von dieser Methode Warnungen für die Eigenschaften generiert werden, die von der Anwendung festgelegt werden sollen. Anwendungen sollten verwenden [GetWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md) Methode der [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse, um jede Warnung abzurufen.  
  
## <a name="see-also"></a>Siehe auch  
 [SetClientInfo-Methode &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
