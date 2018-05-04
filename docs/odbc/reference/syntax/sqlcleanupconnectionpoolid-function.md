---
title: SQLCleanupConnectionPoolID Funktion | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLCleanupConnectionPoolID function [ODBC]
ms.assetid: 1fc61908-e003-4587-b91a-32f40569fb99
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b417ddc7b2aedcf2c23e2f607ceb53ee7ffb4c6b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlcleanupconnectionpoolid-function"></a>SQLCleanupConnectionPoolID-Funktion
**Konformität**  
 Version eingeführt: ODBC 3,81 Standardkonformität: ODBC  
  
 **Zusammenfassung**  
 **SQLCleanupConnectionPoolID** informiert einen Treiber, der eine Anwendungspool-ID überschritten wurde. Timeout bei ein Pool ID können Timeout auf, wenn alle Verbindungen in einem Pool mit diesem Anwendungspool-ID zugeordnet wurden. Finden Sie unter [in der Microsoft Data Access Components Pooling](http://msdn.microsoft.com/library/ms810829.aspx) für Weitere Informationen zum Verbindungstimeout.  
  
## <a name="syntax"></a>Syntax  
  
```  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>Argumente  
 *EnvironmentHandle*  
 [Eingabe] Das Umgebungshandle des Pools.  
  
 *PoolID*  
 [Eingabe] Der Pool zugeordnet sind die Pool-ID, die überschritten wurde.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Der Treiber-Manager verarbeitet keine Diagnoseinformationen Merry **SQLCleanupConnectionPoolID**.  
  
 Eine Anwendung kann nicht vom Treiber zurückgegebene Fehlermeldung empfangen.  
  
## <a name="remarks"></a>Hinweise  
 **SQLCleanupConnectionPoolID** kann jederzeit aufgerufen werden, aber der Treiber-Manager wird sichergestellt, dass keine anderen Threads gleichzeitig aufruft **SQLGetPoolID** und keine anderen Threads gleichzeitig aufruft  **SQLRateConnection** und **SQLPoolConnect** mit einem Verbindungs-Info-Token mit dieser ID Pool zugewiesen Aus diesem Grund muss der Treiber stellen Sie sicher, dass diese Funktion threadsicher ist.  
  
 Ein Treiber kann bereinigen die Ressourcen, die die Pool-ID zugeordnet ist  
  
 Anwendungen sollten diese Funktion nicht direkt aufrufen. Ein ODBC-Treiber, der treiberfähiges Verbindungspooling unterstützt, muss diese Funktion implementieren.  
  
 Schließen Sie sqlspi.h für die Entwicklung von ODBC-Treiber.  
  
## <a name="see-also"></a>Siehe auch  
 [Entwickeln einen ODBC-Treiber](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Treiberfähiges Verbindungspooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Developing Connection-Pool Awareness in an ODBC Driver (Entwickeln von Verbindungspool-Unterstützung in einem ODBC-Treiber)](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
