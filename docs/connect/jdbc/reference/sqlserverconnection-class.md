---
title: SQLServerConnection-Klasse | Microsoft Docs
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
ms.assetid: 937292a6-1525-423e-a2b2-a18fd34c2893
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d479d779c2c438cfc10d93c0187bdc160c24d36
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverconnection-class"></a>SQLServerConnection-Klasse
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Stellt eine JDBC-Verbindung mit einem [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datenbank.  
  
 **Paket:** com.microsoft.sqlserver.jdbc  
  
 **Implementiert:** [ISQLServerConnection](../../../connect/jdbc/reference/isqlserverconnection-interface.md), java.io.Serializable  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public class SQLServerConnection  
```  
  
## <a name="remarks"></a>Hinweise  
 SQLServerConnection kann unterstützt JDBC-Verbindungspools und entweder eine physische JDBC-Verbindung oder eine logische JDBC-Verbindung. SQLServerConnection verwaltet die transaktionssteuerung für alle Anweisungen, die daraus erstellt wurden kann, und für XA-verteilte Transaktionen, die über einen XAResource-Adapter verwaltet.  
  
 SQLServerConnection verwaltet einen Pool vorbereiteter Anweisungshandles. Vorbereitete Anweisungen werden einmal vorbereitet und werden normalerweise mehrere Male mit unterschiedlichen Parameterdatenwerten ausgeführt. Vorbereitete Anweisungen werden ebenfalls über logische (als Poolverbindung verwendete) Verbindungsgrenzen hinweg beibehalten.  
  
> [!NOTE]  
>  SQLServerConnection ist nicht threadsicher. Mehrere aus einer einzelnen Verbindung erstellte Anweisungen können simultan in parallelen Threads verarbeitet werden.  
  
 Diese Klasse unterstützt das Entpacken in die SQLServerConnection-Klasse, java.sql.connection-Schnittstelle und ISQLServerConnection-Schnittstelle. Weitere Informationen finden Sie unter [Wrapper und Schnittstellen](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerConnection-Elemente](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [API-Referenz für JDBC-Treiber](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
