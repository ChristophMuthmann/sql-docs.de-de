---
title: Transaktionen (SQL Data Warehouse) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 87e5e593-a121-4428-9d3c-3af876224e35
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4ea7244857dcd25b1e36f3420811ef035d4ee3b2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="transactions-sql-data-warehouse"></a>Transaktionen (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Eine Transaktion ist eine Gruppe von mindestens einer Datenbankanweisung, für die als Ganzes entweder ein Commit oder ein Rollback ausgeführt wird. Alle Transaktionen sind unteilbar, konsistent, isoliert und von Dauer (atomic, consistent, isolated, durable: ACID). Wenn die Transaktion erfolgreich ist, wird für alle Anweisungen darin ein Commit ausgeführt. Wenn die Transaktion fehlschlägt, d.h. bei mindestens einer Anweisung in der Gruppe ein Fehler auftritt, wird für die gesamte Gruppe ein Rollback ausgeführt.  
  
 Start und Ende von Transaktionen hängen von der Einstellung AUTOCOMMIT, sowie den Anweisungen BEGIN TRANSACTION, COMMIT und ROLLBACK ab. In [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] werden die folgenden Typen von Transaktionen unterstützt:  
  
-   *Explizite Transaktionen* beginnen mit der BEGIN TRANSACTION-Anweisung und enden mit der COMMIT- oder ROLLBACK-Anweisung.  
  
-   *Autocommit-Transaktionen* werden automatisch innerhalb einer Sitzung initiiert und beginnen nicht mit der BEGIN TRANSACTION-Anweisung. Wenn die AUTOCOMMIT-Einstellung auf ON festgelegt ist, wird jede Anweisung in einer Transaktion ausgeführt, und es ist kein explizites COMMIT oder ROLLBACK notwendig. Wenn die AUTOCOMMIT-Einstellung auf OFF festgelegt ist, ist eine COMMIT- oder ROLLBACK-Anweisung erforderlich, um das Ergebnis der Transaktion zu bestimmen. In [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] beginnen AUTOCOMMIT-Transaktionen sofort nach einer COMMIT- oder ROLLBACK-Anweisung oder nach einer SET AUTOCOMMIT OFF-Anweisung.  
  
 ![Symbol zum Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions &#40;Transact-SQL&#41; (Transact-SQL-Syntaxkonventionen (Transact-SQL))](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
BEGIN TRANSACTION [;]  
COMMIT [ TRAN | TRANSACTION | WORK ] [;]  
ROLLBACK [ TRAN | TRANSACTION | WORK ] [;]  
SET AUTOCOMMIT { ON | OFF } [;]  
SET IMPLICIT_TRANSACTIONS { ON | OFF } [;]  
```  
  
## <a name="arguments"></a>Argumente  
 BEGIN TRANSACTION  
 Markiert den Startpunkt einer expliziten Transaktion.  
  
 COMMIT [ WORK ]  
 Markiert das Ende einer expliziten oder AUTOCOMMIT-Transaktion. Diese Anweisung bewirkt, dass die Änderungen in der Transaktion endgültig an die Datenbank übergeben werden. Die Anweisung COMMIT ist identisch mit COMMIT WORK, COMMIT TRAN und COMMIT TRANSACTION.  
  
 ROLLBACK [ WORK ]  
 Führt für eine Transaktion einen Rollback zum Anfang der Transaktion aus. Es werden keine Änderungen der Transaktion an die Datenbank übergeben. Die Anweisung ROLLBACK ist identisch mit ROLLBACK WORK, ROLLBACK TRAN und ROLLBACK TRANSACTION.  
  
 SET AUTOCOMMIT { **ON** | OFF }  
 Bestimmt, wie Transaktionen gestartet und beendet werden können.  
  
 ON  
 Jede Anweisung wird unter ihrer eigenen Transaktion ausgeführt, und keine explizite COMMIT- oder ROLLBACK-Anweisung ist erforderlich. Explizite Transaktionen sind zulässig, wenn AUTOCOMMIT auf ON festgelegt ist.  
  
 OFF  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] initiiert automatisch eine Transaktion, wenn nicht bereits eine ausgeführt wird. Alle nachfolgenden Anweisungen werden als Teil der Transaktion ausgeführt, und ein COMMIT oder ROLLBACK ist erforderlich, um das Ergebnis der Transaktion zu ermitteln. Sobald eine Transaktion ein Commit oder Rollback unter diesem Betriebsmodus ausführt, bleibt der Modus auf OFF festgelegt, und [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] initialisiert eine neue Transaktion. Explizite Transaktionen sind nicht zulässig, wenn AUTOCOMMIT auf OFF festgelegt ist.  
  
 Wenn Sie die AUTOCOMMIT-Einstellung innerhalb einer aktiven Transaktion verändern, wirkt sich die Einstellung nicht auf die laufende Transaktion aus und wird erst aktiv, wenn die Transaktion abgeschlossen ist.  
  
 Wenn AUTOCOMMIT auf ON festgelegt ist, hat das Ausführen einer anderen SET AUTOCOMMIT ON-Anweisung keine Auswirkung. Dementsprechend hat das Ausführen einer anderen SET AUTOCOMMIT OFF-Anweisung keine Auswirkung, wenn AUTOCOMMIT auf OFF festgelegt ist.  
  
 SET IMPLICIT_TRANSACTIONS { ON | **OFF** }  
 Diese Funktion aktiviert die gleichen Modi wie AUTOCOMMIT. Wenn SET IMPLICIT_TRANSACTIONS auf ON festgelegt ist, so wird für die Verbindung der implizite Transaktionsmodus festgelegt. Bei OFF wechselt die Verbindung wieder in den Autocommitmodus zurück.  Weitere Informationen finden Sie unter [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Es sind keine speziellen Berechtigungen erforderlich, um die transaktionsbezogenen Anweisungen auszuführen. Berechtigungen sind erforderlich, um die Anweisungen innerhalb der Transaktion auszuführen.  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Wenn COMMIT oder ROLLBACK ausgeführt werden und keine aktive Transaktion vorhanden ist, wird ein Fehler ausgelöst.  
  
 Wenn BEGIN TRANSACTION ausgeführt wird, während bereits eine Transaktion ausgeführt wird, wird ein Fehler ausgelöst. Dies kann auftreten, wenn BEGIN TRANSACTION nach einer erfolgreichen BEGIN TRANSACTION-Anweisung auftritt oder sich die Sitzung unter SET AUTOCOMMIT OFF befindet.  
  
 Wenn eine explizite Transaktion aufgrund eines anderen Fehlers als eines Anweisungsfehlers zur Laufzeit nicht erfolgreich beendet werden kann, führt [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] automatisch ein Rollback für die Transaktion aus und gibt alle Ressourcen frei, die von der Transaktion beansprucht wurden. Wenn z.B. die Netzwerkverbindung des Clients mit einer Instanz von [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] unterbrochen ist oder sich der Client von der Anwendung abmeldet, wird für alle Transaktionen dieser Verbindung, für die noch kein Commit ausgeführt wurde, ein Rollback ausgeführt, sobald das Netzwerk die Instanz über die Unterbrechung benachrichtigt.  
  
 Wenn ein Anwendungsfehler zur Laufzeit in einem Batch auftritt, verhält sich [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] konsistent mit der auf **ON** festgelegten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**XACT_ABORT**-Einstellung, und für die gesamte Transaktion wird ein Rollback ausgeführt. Weitere Informationen zur **XACT_ABORT**-Einstellung finden Sie unter [SET XACT_ABORT (Transact-SQL)](http://msdn.microsoft.com/library/ms188792.aspx).  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Eine Sitzung kann jeweils nur eine Transaktion zu einem bestimmten Zeitpunkt ausführen. Sicherungspunkte und geschachtelte Transaktionen werden nicht unterstützt.  
  
 Es liegt in der Verantwortung des [!INCLUDE[DWsql](../../includes/dwsql-md.md)]-Programmierers, COMMIT nur zu einem Zeitpunkt auszugeben, zu dem alle Daten, auf die die Transaktion verweist, logisch richtig sind.  
  
 Wenn eine Sitzung beendet wird, bevor eine Transaktion abgeschlossen ist, wird für die Transaktion ein Rollback ausgeführt.  
  
 Die Transaktionsmodi werden auf der Sitzungsebene verwaltet. Wenn eine Sitzung z.B. eine explizite Transaktion startet oder AUTOCOMMIT auf OFF oder IMPLICIT_TRANSACTIONS auf ON festlegt ist, hat dies keine Auswirkung auf die Transaktionsmodi einer anderen Sitzung.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Nach der Ausgabe einer COMMIT-Anweisung kann kein Rollback für eine Transaktion ausgeführt werden, da die Datenänderungen zu einem dauerhaften Bestandteil der Datenbank geworden sind.  
  
 Die Befehle [CREATE DATABASE &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-database-azure-sql-data-warehouse.md) und [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md) können nicht innerhalb einer expliziten Transaktion verwendet werden.  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] verfügt nicht über einen Mechanismus für die Freigabe von Transaktionen. Das bedeutet, dass zu einem bestimmten Zeitpunkt nur eine Sitzung an einer Transaktion im System arbeiten kann.  
  
## <a name="locking-behavior"></a>Sperrverhalten  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] verwendet Sperren, um die Integrität von Transaktionen sicherzustellen und die Konsistenz der Datenbanken beizubehalten, wenn mehrere Benutzer gleichzeitig auf Daten zugreifen. Sperren werden sowohl von impliziten als auch von expliziten Transaktionen verwendet. Jede Transaktion fordert Sperren verschiedener Typen für die Ressourcen, z.B. Tabellen oder Datenbanken an, von denen die Transaktion abhängt. Alle [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]-Sperren befinden sich auf Tabellenebene oder höher. Diese Sperren verhindern, dass die Ressourcen durch andere Transaktionen in einer Weise geändert werden, die zu Problemen für die Transaktion führen würde, die die Sperre angefordert hat. Jede Transaktion hebt ihre Sperren wieder auf, wenn sie nicht mehr über eine Abhängigkeit von den gesperrten Ressourcen verfügt. Explizite Transaktionen behalten Sperren bis zum Abschluss der Transaktion bei, wenn für diese entweder ein Commit oder ein Rollback ausgeführt wird.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="a-using-an-explicit-transaction"></a>A. Verwenden expliziter Transaktionen  
  
```  
BEGIN TRANSACTION;  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT;  
```  
  
### <a name="b-rolling-back-a-transaction"></a>B. Ausführen eines Rollbacks für eine Transaktion  
 Im folgenden Beispiel werden die Auswirkungen des Rollbacks einer Transaktion veranschaulicht.  In diesem Beispiel führt die ROLLBACK-Anweisung ein Rollback der INSERT-Anweisung aus, die erstellte Tabelle bleibt jedoch weiterhin vorhanden.  
  
```  
CREATE TABLE ValueTable (id int);  
BEGIN TRANSACTION;  
       INSERT INTO ValueTable VALUES(1);  
       INSERT INTO ValueTable VALUES(2);  
ROLLBACK;  
```  
  
### <a name="c-setting-autocommit"></a>C. AUTOCOMMIT-Einstellung  
 Im folgenden Beispiel wird die Einstellung AUTOCOMMIT auf `ON` festgelegt.  
  
```  
SET AUTOCOMMIT ON;  
```  
  
 Im folgenden Beispiel wird die Einstellung AUTOCOMMIT auf `OFF` festgelegt.  
  
```  
SET AUTOCOMMIT OFF;  
```  
  
### <a name="d-using-an-implicit-multi-statement-transaction"></a>D. Verwenden einer impliziten Transaktion mit mehreren Anweisungen  
  
```  
SET AUTOCOMMIT OFF;  
CREATE TABLE ValueTable (id int);  
INSERT INTO ValueTable VALUES(1);  
INSERT INTO ValueTable VALUES(2);  
COMMIT;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
