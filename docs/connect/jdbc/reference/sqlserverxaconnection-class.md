---
title: SQLServerXAConnection-Klasse | Microsoft Docs
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
ms.assetid: 5ecb4bf1-b8d1-47cf-9cb1-7a18acc11ce2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba48701c441a75f0d7c6b7f78c964384c47f94e7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverxaconnection-class"></a>SQLServerXAConnection-Klasse
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Stellt JDBC-Verbindungen dar, die an verteilten Transaktionen (XA-Transaktionen) beteiligt sein können.  
  
 **Paket:** com.microsoft.sqlserver.jdbc  
  
 **Erweitert:** [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
 **Implementiert:** javax.sql.XAConnection  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public class SQLServerXAConnection  
```  
  
## <a name="remarks"></a>Hinweise  
 Ein SQLServerXAConnection-Objekt kann in einer verteilten Transaktion mithilfe von eingetragen werden ein [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) Objekt. Ein Transaktions-Manager in der Regel Teil des Servers auf mittlerer Ebene, verwaltet ein SQLServerXAConnection-Objekt, über das SQLServerXAResource-Objekt.  
  
> [!NOTE]  
>  Anwendungsprogrammierer verwenden diese Schnittstelle normalerweise nicht direkt. Sie wird in erster Linie von einem Transaktions-Manager verwendet, der auf dem Server auf mittlerer Ebene arbeitet.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerXAConnection-Elemente](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [API-Referenz für JDBC-Treiber](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
