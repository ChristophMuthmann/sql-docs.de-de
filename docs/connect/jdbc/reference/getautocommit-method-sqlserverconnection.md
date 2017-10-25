---
title: GetAutoCommit-Methode (SQLServerConnection) | Microsoft Docs
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
- SQLServerConnection.getAutoCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: af1f67f4-f568-4e58-abcc-5c809a89b547
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e2c8ee804ede53953f531fe945da39c7c0667cae
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# GetAutoCommit-Methode (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft ab den aktuellen Autocommit-Modus für diese [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Objekt.  
  
## Syntax  
  
```  
  
public boolean getAutoCommit()  
```  
  
## Rückgabewert  
 **"true"** Wenn Autocommit-Modus aktiviert ist, **"false"** wird jedoch nicht.  
  
## Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## Hinweise  
 Diese GetAutoCommit-Methode wird von der GetAutoCommit-Methode in der java.sql.Connection-Schnittstelle angegeben.  
  
## Siehe auch  
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection-Klasse](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

