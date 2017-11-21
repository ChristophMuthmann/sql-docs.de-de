---
title: SET ANSI_DEFAULTS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET ANSI_DEFAULTS
- ANSI_DEFAULTS
- SET_ANSI_DEFAULTS_TSQL
- ANSI_DEFAULTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ANSI_DEFAULTS option
- SET ANSI_DEFAULTS statement
ms.assetid: bd721d97-6e23-488b-8c8c-c0453d5b3b86
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 170fb1f5a95b9f6fe4fbe596906595475175b1a2
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-ansidefaults-transact-sql"></a>SET ANSI_DEFAULTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Steuert eine Gruppe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Einstellungen, die zusammen einen bestimmten Teil des Standardverhaltens von ISO angeben.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server  
  
SET ANSI_DEFAULTS { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET ANSI_DEFAULTS ON;  
```  
  
## <a name="remarks"></a>Hinweise  
 SET ANSI_DEFAULTS ist eine serverseitige Einstellung, die vom Client nicht verändert wird. Der Client verwaltet eigene Einstellungen. Diese Einstellungen sind standardmäßig das Gegenstück zur Servereinstellung. Benutzer sollten die Servereinstellung nicht ändern. Zum Ändern des Clientverhaltens sollten Benutzer SQL_COPT_SS_PRESERVE_CURSORS verwenden. Weitere Informationen finden Sie unter [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
 Wird die Option aktiviert (ON), werden die folgenden ISO-Einstellungen aktiviert:  
  
|||  
|-|-|  
|SET ANSI_NULLS|SET CURSOR_CLOSE_ON_COMMIT|  
|SET ANSI_NULL_DFLT_ON|SET IMPLICIT_TRANSACTIONS|  
|SET ANSI_PADDING|SET QUOTED_IDENTIFIER|  
|SET ANSI_WARNINGS||  
  
 Diese SET-Optionen gemäß ISO-Standard definieren zusammen die Abfrageverarbeitungsumgebung für die Dauer der Arbeitssitzung des Benutzers oder für den Zeitraum, in dem ein Trigger oder eine gespeicherte Prozedur ausgeführt wird. Die aufgeführten SET-Optionen schließen jedoch nicht alle Optionen ein, die erforderlich wären, um dem ISO-Standard zu entsprechen.  
  
 Beim Verwenden von Indizes für berechnete Spalten und indizierte Sichten, müssen vier dieser Standardwerte (ANSI_NULLS, ANSI_PADDING, ANSI_WARNINGS und QUOTED_IDENTIFIER) auf ON festgelegt sein. Diese Standardwerte gehören zu den insgesamt sieben SET-Optionen, für die bestimmte Werte beim Erstellen und Ändern von Indizes für berechnete Spalten und indizierte Sichten zugewiesen werden müssen. Die anderen SET-Optionen lauten ARITHABORT (ON), CONCAT_NULL_YIELDS_NULL (ON) und NUMERIC_ROUNDABORT (OFF). Weitere Informationen zu den erforderlichen Einstellungen der SET-Option mit indizierten Sichten und Indizes für berechnete Spalten finden Sie unter "Überlegungen beim Sie mithilfe der SET-Anweisungen in [SET-Anweisungen &#40; Transact-SQL &#41; ](../../t-sql/statements/set-statements-transact-sql.md).  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "ANSI_DEFAULTS" automatisch auf ON festgelegt wird, wenn eine Verbindung herstellen. Treiber und Anbieter legen anschließend CURSOR_CLOSE_ON_COMMIT und IMPLICIT_TRANSACTIONS auf OFF fest. Die Einstellung OFF für SET CURSOR_CLOSE_ON_COMMIT und SET IMPLICIT_TRANSACTIONS kann in ODBC-Datenquellen, in ODBC-Verbindungsattributen oder in OLE DB-Verbindungseigenschaften konfiguriert werden, die in der Anwendung festgelegt werden, bevor die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hergestellt wird. SET ANSI_DEFAULTS wird für Verbindungen von DB-Library-Anwendungen standardmäßig auf OFF festgelegt.  
  
 Wenn SET ANSI_DEFAULTS ausgeführt wird, wird SET QUOTED_IDENTIFIER zur Analysezeit festgelegt, und die folgenden Optionen werden zur Ausführungszeit festgelegt:  
  
|||  
|-|-|  
|SET ANSI_NULLS|SET ANSI_WARNINGS|  
|SET ANSI_NULL_DFLT_ON|SET CURSOR_CLOSE_ON_COMMIT|  
|SET ANSI_PADDING|SET IMPLICIT_TRANSACTIONS|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `SET ANSI_DEFAULTS ON` festgelegt, und die `DBCC USEROPTIONS`-Anweisung wird zum Anzeigen der betroffenen Einstellungen verwendet.  
  
```  
-- SET ANSI_DEFAULTS ON.  
SET ANSI_DEFAULTS ON;  
GO  
-- Display the current settings.  
DBCC USEROPTIONS;  
GO  
-- SET ANSI_DEFAULTS OFF.  
SET ANSI_DEFAULTS OFF;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [DBCC USEROPTIONS &#40; Transact-SQL &#41;](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)   
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_NULL_DFLT_ON &#40; Transact-SQL &#41;](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET CURSOR_CLOSE_ON_COMMIT &#40; Transact-SQL &#41;](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)   
 [SET IMPLICIT_TRANSACTIONS &#40; Transact-SQL &#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
  

