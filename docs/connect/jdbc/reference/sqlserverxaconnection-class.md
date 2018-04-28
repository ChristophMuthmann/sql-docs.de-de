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
ms.topic: article
ms.assetid: 5ecb4bf1-b8d1-47cf-9cb1-7a18acc11ce2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e095b498807412a40d4df1092b6c151c8c030c9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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
  
  
