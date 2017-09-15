---
title: GetXAConnection-Methode () | Microsoft Docs
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
- SQLServerXADataSource.getXAConnection ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b2710613-78b1-438f-b996-c7ae6f34381a
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6fd5681b0ece55e113d03c9ee21950f1cae19f43
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getxaconnection-method-"></a>getXAConnection-Methode ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Stellt eine physische Datenbankverbindung her, die in einer verteilten Transaktion verwendet werden kann.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public javax.sql.XAConnection getXAConnection()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein XAConnection-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 java.sql.SQLException  
  
## <a name="remarks"></a>Hinweise  
 Diese GetXAConnection-Methode wird von der GetXAConnection-Methode in der javax.sql.XADataSource-Schnittstelle angegeben.  
  
> [!NOTE]  
>  Diese Methode wird normalerweise von XA-Verbindungspoolimplementierungen und nicht vom regulären JDBC-Anwendungscode aufgerufen.  
  
## <a name="see-also"></a>Siehe auch  
 [GetXAConnection-Methode &#40; SQLServerXADataSource &#41;](../../../connect/jdbc/reference/getxaconnection-method-sqlserverxadatasource.md)   
 [SQLServerXADataSource-Methoden](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [SQLServerXADataSource-Elemente](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [SQLServerXADataSource-Klasse](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
