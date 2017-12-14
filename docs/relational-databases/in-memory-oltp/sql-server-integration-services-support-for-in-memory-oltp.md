---
title: "SQL Server Integration Services-Unterstützung für In-Memory OLTP | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ea82a9b9-e9ed-4d6f-b3fd-917f6c687ae3
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 24f5b67b776e6ea2cdb8684a0732fd9f76114cb2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-integration-services-support-for-in-memory-oltp"></a>SQL Server Integration Services-Unterstützung für In-Memory OLTP
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Sie können eine speicheroptimierte Tabelle, eine Sicht, die auf speicheroptimierte Tabellen verweist, oder eine nativ kompilierte gespeicherte Prozedur als Quelle oder Ziel des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakets (SSIS) verwenden. Sie können [ADO NET Source](../../integration-services/data-flow/ado-net-source.md), [OLE DB Source](../../integration-services/data-flow/ole-db-source.md)oder [ODBC Source](../../integration-services/data-flow/odbc-source.md) im Datenfluss eines SSIS-Pakets verwenden und die Quellkomponente so konfigurieren, dass Daten aus einer speicheroptimierten Tabelle oder einer Sicht abgerufen werden. Sie können auch eine SQL-Anweisung angeben, um eine systemintern kompilierte gespeicherte Prozedur auszuführen. Ebenso können Sie [ADO NET Destination](../../integration-services/data-flow/ado-net-destination.md), [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md)oder [ODBC Destination](../../integration-services/data-flow/odbc-destination.md) verwenden, um Daten in eine speicheroptimierte Tabelle oder eine Sicht zu laden, oder Sie können eine SQL-Anweisung angeben, um eine systemintern kompilierte gespeicherte Prozedur auszuführen.  
  
 Sie können die oben erwähnten Quell- und Zielkomponenten in einem SSIS-Paket so konfigurieren, dass ebenso wie bei anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabellen und -Sichten aus speicheroptimierten Tabellen gelesen bzw. in speicheroptimierte Tabellen geschrieben wird. Beim Verwenden systemintern kompilierter gespeicherter Prozeduren sind jedoch die wichtigen Aspekte im folgenden Abschnitt zu beachten.  
  
## <a name="invoking-a-natively-compiled-stored-procedure-from-an-ssis-package"></a>Aufrufen einer systemintern kompilierten gespeicherten Prozedur aus einem SSIS-Paket  
 Zum Aufrufen einer systemintern kompilierten gespeicherten Prozedur aus einem SSIS-Paket empfiehlt es sich, eine ODBC-Quelle oder ein ODBC-Ziel mit einer SQL-Anweisung des folgenden Formats zu verwenden: **\<Prozedurname>** ohne das Schlüsselwort **EXEC**. Wenn Sie das EXEC-Schlüsselwort in der SQL-Anweisung angeben, wird eine Fehlermeldung zurückgegeben, weil der ODBC-Verbindungs-Manager den SQL-Befehlstext als [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung und nicht als gespeicherte Prozedur interpretiert und Cursor verwendet, die für die Ausführung von systemintern kompilierten gespeicherten Prozeduren nicht unterstützt werden. Der Verbindungs-Manager behandelt die SQL-Anweisung ohne EXEC-Schlüsselwort als Aufruf einer gespeicherten Prozedur, und es wird kein Cursor verwendet.  
  
 Sie können eine systemintern kompilierte gespeicherte Prozedur auch mit einer ADO.NET-Quelle und OLE DB-Quelle aufrufen, es wird jedoch empfohlen, eine ODBC-Quelle zu verwenden. Wenn Sie die ADO.NET-Quelle für die Ausführung einer systemintern kompilierten gespeicherten Prozedur konfigurieren, wird eine Fehlermeldung zurückgegeben, weil der Datenanbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient), der von der ADO.NET-Quelle standardmäßig verwendet wird, die Ausführung von systemintern kompilierten gespeicherten Prozeduren nicht unterstützt. Sie können die ADO.NET-Quelle für die Verwendung des ODBC-Datenanbieters, des OLE DB-Anbieters für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]oder des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client konfigurieren. Beachten Sie jedoch, dass die ODBC-Quelle eine bessere Leistung als die ADO.NET-Quelle mit dem ODBC-Datenanbieter bietet.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Unterstützung für In-Memory OLTP](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)  
  
  
