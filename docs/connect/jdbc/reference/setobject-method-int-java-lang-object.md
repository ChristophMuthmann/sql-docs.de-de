---
title: SetObject-Methode (Int, java.lang.Object) | Microsoft Docs
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
apiname:
- SQLServerPreparedStatement.setObject (int, java.lang.Object)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 61f19faa-3006-4a1c-974c-55951e3b3000
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2116f0662e21e4cb38d60560a680e90e6b2321d9
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setobject-method-int-javalangobject"></a>setObject-Methode (int, java.lang.Object)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den Wert des angegebenen Parameters unter Verwendung des angegebenen Objekts fest.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final void setObject(int index,  
                            java.lang.Object obj)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Index*  
  
 Ein **Int** , der die Parameteranzahl angibt.  
  
 *obj*  
  
 Ein Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetObject-Methode wird von der SetObject-Methode in der java.sql.PreparedStatement-Schnittstelle angegeben.  
  
 Vor dem Aufrufen dieser SetObject-Methode kann die Anwendung den angegebenen Parameter festlegen, mithilfe einer der folgenden Methoden:  
  
-   Der Satz\<Typ >-Methoden der SQLServerPreparedStatement-Klasse oder der SQLServerCallableStatement-Klasse  
  
-   SetNull-Methoden von der SQLServerPreparedStatement-Klasse oder der SQLServerCallableStatement-Klasse  
  
-   Die [RegisterOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) -Methode der SQLServerCallableStatement-Klasse  
  
 In diesem Fall wird der Parametertyp automatisch festgelegt. Wenn die Anwendung diese SetObject-Methode mit einer Objektwert NULL aufgerufen wird, wird der Treiber davon ausgegangen, dass der Typ des Parameters ist, die von der zuvor aufgerufenen Methode festgelegt ist.  
  
 Wenn der Objektwert NULL ist und keine Typinformationen für diesen Parameter bestimmt werden kann, konvertiert diese SetObject-Methode den angegebenen Parameter in einen CHAR vor dem Senden an die Datenbank an.  
  
 Beginnend mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0, das Verhalten dieser Methode geändert wird, indem die **SendTimeAsDatetime** Connection-Eigenschaft ([Festlegen der Verbindungseigenschaften](../../../connect/jdbc/setting-the-connection-properties.md)) und [ SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Weitere Informationen finden Sie unter [konfigurieren wie java.sql.Time-Werte werden an den Server gesendet](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SetObject-Methode &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement-Elemente](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement-Klasse](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  

