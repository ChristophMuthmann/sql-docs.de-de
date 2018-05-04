---
title: GetFetchDirection-Methode (SQLServerStatement) | Microsoft Docs
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
- SQLServerStatement.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ceb4ae68-decc-46d3-83f1-0bbd23aaf58c
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ce1a90324b0cc7fd40e22b0cb90537b985f3d754
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getfetchdirection-method-sqlserverstatement"></a>getFetchDirection-Methode (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft die Richtung ab, für das Abrufen von Zeilen aus Datenbanktabellen ist die standardmäßig für Resultsets, die von diesem generiert werden [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.  
  
> [!NOTE]  
>  Diese Methode wird derzeit nicht implementiert durch den [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Aus diesem Grund wird immer "FETCH_UNKNOWN" zurückgegeben.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final int getFetchDirection()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Int** , die angibt, dass der abrufrichtung, die von angegeben wird die [SetFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md) Methode.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetFetchDirection-Methode wird von der GetFetchDirection-Methode in der java.sql.Statement-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerStatement-Elemente](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement-Klasse](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
