---
title: "Transact-SQL-Unterst&#252;tzung f&#252;r In-Memory OLTP | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b1cc7c30-1747-4c21-88ac-e95a5e58baac
caps.latest.revision: 52
author: "MightyPen"
ms.author: "genemi"
manager: "jhubbard"
caps.handback.revision: 52
---
# Transact-SQL-Unterst&#252;tzung f&#252;r In-Memory OLTP
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen enthalten Syntaxoptionen, um In-Memory-OLTP zu unterstützen:  
  
-   [ALTER DATABASE-Optionen für Dateien und Dateigruppen &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20File%20and%20Filegroup%20Options%20\(Transact-SQL\).md) (**MEMORY_OPTIMIZED_DATA** hinzugefügt)  
  
-   [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
-   [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md) (**MEMORY_OPTIMIZED_DATA** hinzugefügt)  
  
-   [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
  
-   [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
  
-   [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
-   [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)  
  
-   [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
    In einer nativ kompilierten gespeicherten Prozedur können Sie eine Variable als **NOT NULL** deklarieren. Dies ist bei einer regulären gespeicherten Prozedur nicht möglich.  
  
 **AUTO_UPDATE_STATISTICS** kann ab SQL Server 2016 für speicheroptimierte Tabellen **ON** sein. Weitere Informationen finden Sie unter [sp_autostats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md).  
  
 [SET STATISTICS XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-xml-transact-sql.md) ON wird für nativ kompilierte gespeicherte Prozeduren nicht unterstützt.  
  
 Informationen zu nicht unterstützten Funktionen finden Sie unter [Von In-Memory-OLTP nicht unterstützte Transact-SQL-Konstrukte](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md).  
  
 Informationen zu unterstützten Konstrukten und nativ kompilierten gespeicherten Prozeduren finden Sie unter [Unterstützte Funktionen für nativ kompilierte T-SQL-Module](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md) und [Unterstützte DDL für nativ kompilierte T-SQL-Module](../../relational-databases/in-memory-oltp/supported-ddl-for-natively-compiled-t-sql-modules.md).  
  
## Siehe auch  
 [In-Memory-OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)   
 [Migrationsprobleme bei systemintern kompilierten gespeicherten Prozeduren](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [Nicht unterstützte SQL Server-Funktionen für In-Memory OLTP](../../relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)   
 [Systemintern kompilierte gespeicherte Prozeduren](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  