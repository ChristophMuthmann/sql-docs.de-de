---
title: GetCatalog-Methode (SQLServerConnection) | Microsoft Docs
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
- SQLServerConnection.getCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e87ef65f-4b5a-4e1c-8db5-7f0932390bb0
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6cc3aedba38d3ade6d08e1829d5970c2585cb1b6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getcatalog-method-sqlserverconnection"></a>GetCatalog-Methode (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft ab den aktuellen Katalognamen dieses [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.String getCatalog()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** , enthält der Name des Katalogs.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetCatalog-Methode wird von der GetCatalog-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
 Gibt die aktuelle Katalogeigenschaft des SQLServerConnection-Objekt oder Null zurück, wenn sie nicht festgelegt ist. Die Catalog-Eigenschaft explizit festgelegt ist, mit der [SetCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md) -Methode, oder durch Lesen der umgebungsänderung für TDS für den aktuellen Katalog implizit aktualisiert wird.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
