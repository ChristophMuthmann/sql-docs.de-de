---
title: SQLServerXADataSource-Klasse | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 95fc7b07-2498-4a7e-8f7f-ee0d86b598b4
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 10e470658b2f0b3954d97bc2632ca25c53745d2f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverxadatasource-class"></a>SQLServerXADataSource-Klasse
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Stellt eine Factory für [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) Objekte, die intern verwendet wird.  
  
 **Paket:** com.microsoft.sqlserver.jdbc  
  
 **Erweitert:** [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
 **Implementiert:** javax.sql.XADataSource  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public class SQLServerXADataSource  
```  
  
## <a name="remarks"></a>Hinweise  
 Ein Objekt, das die SQLServerXADataSource-Schnittstelle implementiert wird normalerweise bei einem Bezeichnungsdienst registriert, die Java Naming and Directory Interface (JNDI) verwendet.  
  
 Die SQLServerXADataSource-Klasse stellt Datenbankverbindungen zur Verwendung in verteilten (XA) Transaktionen bereit. Die SQLServerXADataSource-Klasse unterstützt außerdem Verbindungspools aus physikalischen Verbindungen. Die SQLServerXADataSource und SQLServerXAConnection-Schnittstellen, die in das Paket "javax.SQL" definiert sind, werden von implementiert [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
 SQLServerXAConnection-Objekts ist eine poolverbindung, die in einer verteilten Transaktion teilnehmen kann. Genauer gesagt, SQLServerXAConnection der SQLServerPooledConnection-Schnittstelle durch Hinzufügen der Methode erweitert [GetXAResource](../../../connect/jdbc/reference/getxaresource-method-sqlserverxaconnection.md). Diese Methode erzeugt eine [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) -Objekt, das von einem Transaktions-Manager zur Koordination der Arbeit an dieser Verbindung mit den anderen Teilnehmer an der verteilten Transaktion verwendet werden kann. Da sie die SQLServerPooledConnection-Schnittstelle zu erweitern, unterstützen SQLServerXAConnection-Objekte alle Methoden von SQLServerPooledConnection-Objekten. Sie sind wiederverwendbare physikalische Verbindungen mit einer zu Grunde liegenden Datenquelle und erzeugen logische Verbindungshandles, die an eine JDBC-Anwendung zurückgegeben werden können.  
  
 SQLServerXAConnection-Objekte werden durch ein SQLServerXADataSource-Objekt erzeugt. SQLServerConnectionPoolDataSource und SQLServerXADataSource-Objekte sind ähnlich, da sie beide unterhalb einer Datenquellenebene implementiert werden, die für die JDBC-Anwendung sichtbar ist. Dank dieser Architektur kann [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] unterstützt verteilte Transaktionen auf eine Weise, die für die Anwendung transparent ist. SQLServerXADataSource kann konfiguriert werden, um die integrieren [!INCLUDE[msCoName](../../../includes/msconame_md.md)] Distributed Transaction Coordinator (DTC) auf "true", bieten verteilte transaktionsverarbeitung.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerXADataSource-Elemente](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [API-Referenz für JDBC-Treiber](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  

