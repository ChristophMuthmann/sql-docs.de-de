---
title: SetObject-Methode (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerPreparedStatement.setObject
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 93a2b22c-82b4-48c7-a428-369ebe98a372
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4582f5f5ea56938562570a1b5e01393fa77de76a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setobject-method-sqlserverpreparedstatement"></a>SetObject-Methode (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den Wert des angegebenen Parameters unter Verwendung des angegebenen Objekts fest.  
  
 Beginnend mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0, das Verhalten dieser Methode geändert wird, indem die **SendTimeAsDatetime** Connection-Eigenschaft ([Festlegen der Verbindungseigenschaften](../../../connect/jdbc/setting-the-connection-properties.md)) und [ SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Weitere Informationen finden Sie unter [konfigurieren wie java.sql.Time-Werte werden an den Server gesendet](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="overload-list"></a>Überladungsliste  
  
|Name|Description|  
|----------|-----------------|  
|[SetObject (Int, java.lang.Object)](../../../connect/jdbc/reference/setobject-method-int-java-lang-object.md)|Legt den Wert des angegebenen Parameters unter Verwendung des angegebenen Objekts fest.|  
|[SetObject (Int, java.lang.Object, Int)](../../../connect/jdbc/reference/setobject-method-int-java-lang-object-int.md)|Legt den Wert des angegebenen Parameters unter Verwendung des angegebenen Objekts und Ziel.|  
|[SetObject (Int, java.lang.Object, Int, Int)](../../../connect/jdbc/reference/setobject-method-int-java-lang-object-int-int.md)|Legt den Wert des angegebenen Parameters mithilfe des angegebenen Objekts, den Zieltyp und die Skalierung fest.|  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerPreparedStatement-Elemente](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement-Klasse](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  

