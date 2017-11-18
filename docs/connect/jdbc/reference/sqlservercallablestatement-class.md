---
title: SQLServerCallableStatement-Klasse | Microsoft Docs
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
ms.assetid: 30710a63-c05d-47d9-9cf9-c087a1c76373
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 15c8a944d4130e496c051d163c4724fe6d87f74e
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlservercallablestatement-class"></a>SQLServerCallableStatement-Klasse
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Mit dieser Klasse kann der gespeicherte Prozedurname angegeben werden, der mit Eingabe- und Ausgabeparametern aufgerufen wird. Mit dieser Klasse kann der Rückgabestatus mit der Syntax "? = call( ?, ..)" abgerufen werden.  
  
 **Paket:** com.microsoft.sqlserver.jdbc  
  
 **Implementiert:** [ISQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
 **Erweitert:** [sqlserverpreparedstatement-Klasse](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final class SQLServerCallableStatement  
```  
  
## <a name="remarks"></a>Hinweise  
 SQLServerCallableStatement können Sie den Namen der gespeicherten Prozedur aufrufen, zusammen mit Eingabe-und Ausgabeparameter angeben. SQLServerCallableStatement bietet auch die Möglichkeit zum Abrufen des Werts der Rückgabestatus mit der `? = call( ?, ..)` Syntax.  
  
 Diese Klasse unterstützt das Entpacken in die SQLServerCallableStatement-Klasse, ISQLServerCallableStatement-Schnittstelle, java.sql.CallableStatement-Schnittstelle, und die Klassen und Schnittstellen, die von SQLServerPreparedStatement für das Entpacken unterstützt werden. Weitere Informationen finden Sie unter [Wrapper und Schnittstellen](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
 Wenn eines der SQLServerCallableStatement Methoden festlegen für einen Typ aufgerufen wird, wenn dieses Typs von Konflikten mit den angegebenen Typ [RegisterOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md), mit der letzten Set-Methode der SQLServerCallableStatement verwendet wird. Dies kann jedoch zu Konvertierungsfehlern aufgrund von inkompatiblen Datentypen führen. Wenn ein SQLServerCallableStatement-Methode festlegen, wird nicht aufgerufen, mit dem ersten angegebenen Typs [RegisterOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) Aufruf wird verwendet.  
  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0 ist kompatibel mit der JDBC 4.0-Empfehlung, die ein Resultset und updatezählungen abgerufen werden müssen, bevor Out-Parameter. Sollten OUT-Parameter vor Abschluss der Verarbeitung des Resultsets und der Updatezählungen abgerufen werden, gehen alle noch nicht verarbeiteten Resultsets und Updatezählungen verloren.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerCallableStatement-Elemente](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [API-Referenz für JDBC-Treiber](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  

