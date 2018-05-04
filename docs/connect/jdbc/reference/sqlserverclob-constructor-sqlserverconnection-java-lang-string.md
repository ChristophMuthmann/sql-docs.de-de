---
title: SQLServerClob-Konstruktor (SQLServerConnection, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection.SQLServerClob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7058f4f7-ef3e-4d62-90d1-79299708b1eb
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b6c7982dd0bf12ee7314e6903e455f2bec3e090
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverclob-constructor-sqlserverconnection-javalangstring"></a>SQLServerClob-Konstruktor (SQLServerConnection, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Initialisiert eine neue Instanz der dem [SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md) Klasse, sofern eine [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) -Objekt und eine Datenzeichenfolge.  
  
> [!NOTE]  
>  Diese Methode ist seit Version 2.0 des JDBC-Treibers veraltet. Verwenden Sie stattdessen die [CreateClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md) Methode der [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public SQLServerClob(SQLServerConnection connection,  
                     java.lang.String data)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Verbindung*  
  
 Ein SQLServerConnection-Objekt.  
  
 *data*  
  
 Die CLOB-Daten.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerClob-Konstruktoren](../../../connect/jdbc/reference/sqlserverclob-constructors.md)   
 [SQLServerClob-Elemente](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob-Klasse](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
