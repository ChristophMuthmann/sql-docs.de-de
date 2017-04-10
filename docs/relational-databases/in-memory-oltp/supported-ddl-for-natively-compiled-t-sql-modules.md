---
title: "Unterst&#252;tzte DDL f&#252;r nativ kompilierte T-SQL-Module | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6b21f47e-bceb-4054-8b3c-9d39bb9583c0
caps.latest.revision: 12
author: "MightyPen"
ms.author: "genemi"
manager: "jhubbard"
caps.handback.revision: 12
---
# Unterst&#252;tzte DDL f&#252;r nativ kompilierte T-SQL-Module
  Dieses Thema listet die unterstützten DDL-Konstrukte für nativ kompilierte T-SQL-Module auf, wie z. B. gespeicherte Prozeduren, benutzerdefinierte Skalarfunktionen, Inline-Tabellenwertfunktionen und Trigger.  
  
 Informationen zu Funktionen und T-SQL-Oberflächenbereichen, die als Teil von nativ kompilierten T-SQL-Modulen verwendet werden können, finden Sie unter [Unterstützte Funktionen für nativ kompilierte T-SQL-Module](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).  
  
 Informationen zu nicht unterstützten Knstrukten finden Sie unter [Von In-Memory OLTP nicht unterstützte Transact-SQL-Konstrukte](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md).  
  
 Folgende werden unterstützt:  
  
-   [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
  
-   [DROP PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-procedure-transact-sql.md)  
  
-   [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)  
  
-   [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)- und INSERT SELECT-Anweisungen  
  
-   SCHEMABINDING und BEGIN ATOMIC (in nativ kompilierten gespeicherten Prozeduren erforderlich)  
  
     Weitere Informationen finden Sie unter [Creating Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/creating-natively-compiled-stored-procedures.md).  
  
-   NATIVE_COMPILATION  
  
     Weitere Informationen finden Sie unter [Native Compilation of Tables and Stored Procedures](../../relational-databases/in-memory-oltp/native-compilation-of-tables-and-stored-procedures.md).  
  
-   Parameter und Variablen können als NOT NULL deklariert werden (nur für nativ kompilierte Module verfügbar: nativ kompilierte gespeicherte Prozeduren und nativ kompilierte benutzerdefinierte Skalarfunktionen).  
  
-   Tabellenwertparameter.  
  
     Weitere Informationen finden Sie unter [Use Table-Valued Parameters &#40;Database Engine&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
-   EXECUTE AS OWNER, SELF, CALLER und Benutzer.  
  
-   GRANT- und DENY-Berechtigungen in Tabellen und Prozeduren.  
  
     Weitere Informationen finden Sie unter [GRANT (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)[DENY (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md).  
  
## Siehe auch  
 [Systemintern kompilierte gespeicherte Prozeduren](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  