---
title: Transaktionen (SQL Datawarehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 87e5e593-a121-4428-9d3c-3af876224e35
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8202a0de588bce3a36fc048e68c283b52db7e89d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="transactions-sql-data-warehouse"></a>Transaktionen (SQL Datawarehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Eine Transaktion ist eine Gruppe von einer oder mehreren Datenbank-Anweisungen, die entweder vollständig zugesichert oder vollständig ein Rollback. Jede Transaktion wird atomic, konsistent, isoliert und dauerhaft (ACID-Eigenschaften). Wenn die Transaktion erfolgreich ausgeführt wird, sind alle Anweisungen darin ein Commit ausgeführt wurde. Beim Fehlschlagen die Transaktion ist, die mindestens eine der Anweisungen in der Gruppe ein Fehler auftritt, und klicken Sie dann die gesamte Gruppe, ein Rollback ausgeführt wird.  
  
 Anfang und Ende von Transaktionen, hängt von der AUTOCOMMIT-Einstellung und die Anweisungen BEGIN TRANSACTION, COMMIT und ROLLBACK. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]unterstützt die folgenden Typen von Transaktionen:  
  
-   *Explizite Transaktionen* beginnen Sie mit der BEGIN TRANSACTION-Anweisung und mit dem COMMIT oder ROLLBACK-Anweisung enden.  
  
-   *Autocommit-Transaktionen* automatisch innerhalb einer Sitzung zu initiieren und können nicht gestartet werden, mit der BEGIN TRANSACTION-Anweisung. Wenn die AUTOCOMMIT-Einstellung auf ON festgelegt ist, jede Anweisung in einer Transaktion ausgeführt wird und keine explizite Commit- oder ROLLBACK ist erforderlich. Wenn die AUTOCOMMIT-Einstellung auf OFF festgelegt ist, wird eine COMMIT oder ROLLBACK-Anweisung erforderlich, um das Ergebnis der Transaktion zu bestimmen. In [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], autocommittransaktionen beginnt unmittelbar nach einem COMMIT oder ROLLBACK-Anweisung oder nach einer AUTOCOMMIT SET OFF-Anweisung.  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 Markiert den Anfangspunkt einer expliziten Transaktion.  
  
 COMMIT [ARBEIT]  
 Markiert das Ende einer expliziten oder Autocommit-Transaktion. Diese Anweisung bewirkt, dass die Änderungen in der Transaktion endgültig an die Datenbank übergeben werden. Die Anweisung COMMIT ist identisch mit COMMIT TRAN, COMMIT WORK und COMMIT TRANSACTION.  
  
 ROLLBACK [ARBEIT]  
 Rollback einer Transaktion an den Anfang der Transaktion. Es sind keine Änderungen für die Transaktion ein Commit in der Datenbank ausgeführt. Die Anweisung ROLLBACK ist identisch mit der ROLLBACK WORK, ROLLBACK TRAN und ROLLBACK TRANSACTION.  
  
 SET-AUTOCOMMIT { **ON** | {OFF}  
 Bestimmt, wie Transaktionen starten und beenden können.  
  
 ON  
 Jede Anweisung, die unter einer eigenen Transaktion ausgeführt wird, und keine explizite Commit- oder ROLLBACK-Anweisung ist erforderlich. Explizite Transaktionen sind zulässig, wenn der AUTOCOMMIT auf ON festgelegt ist.  
  
 OFF  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]automatisch initiiert eine Transaktion auf, wenn eine Transaktion nicht bereits ausgeführt wird. Alle nachfolgenden Anweisungen als Teil der Transaktion ausgeführt werden, und ein COMMIT oder ROLLBACK ist erforderlich, das Ergebnis der Transaktion zu ermitteln. Sobald eine Transaktion ein Commit oder Rollback unter dieser Betriebsmodus, bleibt der Modus OFF und [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] eine neue Transaktion initiiert. Explizite Transaktionen sind nicht zulässig, wenn der AUTOCOMMIT auf OFF festgelegt ist.  
  
 Wenn Sie die Einstellung AUTOCOMMIT innerhalb einer aktiven Transaktions ändern, wird diese Einstellung wirkt sich die aktuelle Transaktion und ist nicht wirksam, bis die Transaktion abgeschlossen ist.  
  
 Wenn AUTOCOMMIT auf ON festgelegt ist, wirkt sich mit einem anderen Satz AUTOCOMMIT ON-Anweisung nicht. Ebenso, wenn AUTOCOMMIT auf OFF festgelegt ist, hat eine andere SET AUTOCOMMIT OFF ausgeführt keine Auswirkungen.  
  
 SET IMPLICIT_TRANSACTIONS {ON | **OFF** }  
 Diese Funktion schaltet die gleichen Modi als AUTOCOMMIT festgelegt. Wenn auf ON gesetzt SET IMPLICIT_TRANSACTIONS die Verbindung in den impliziten Transaktionsmodus. Bei OFF wird die Verbindung zurück in den Autocommitmodus.  Weitere Informationen finden Sie unter [SET IMPLICIT_TRANSACTIONS &#40; Transact-SQL &#41; ](../../t-sql/statements/set-implicit-transactions-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Keine speziellen Berechtigungen sind erforderlich, um die transaktionsbezogene Anweisungen ausgeführt. Berechtigungen sind erforderlich, um die Anweisungen innerhalb der Transaktion ausgeführt.  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Wenn ein COMMIT oder ROLLBACK ausgeführt werden und keine aktive Transaktion vorhanden ist, wird ein Fehler ausgelöst.  
  
 Wenn eine BEGIN TRANSACTION ausgeführt wird, während eine Transaktion bereits ausgeführt wird, wird ein Fehler ausgelöst. Dies kann auftreten, wenn eine BEGIN TRANSACTION tritt nach einer erfolgreichen BEGIN TRANSACTION-Anweisung, oder wenn die Sitzung unter AUTOCOMMIT SET OFF ist.  
  
 Wenn ein Fehler als ein Anweisungsfehler zur Laufzeit Fehler vom erfolgreichen Abschluss einer expliziten Transaktion verhindert [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] automatisch ein Rollback der Transaktion und gibt alle Ressourcen, die von der Transaktion aufrecht. Z. B. wenn der Client-Netzwerkverbindung mit einer Instanz von [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] unterbrochen oder der Client von der Anwendung abmeldet, alle Transaktionen ohne Commit für die Verbindung werden zurückgesetzt, wenn das Netzwerk die Instanz über die Unterbrechung benachrichtigt.  
  
 Wenn ein Anweisungsfehler zur Laufzeit Fehler in einem Batch auftritt [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] verhält sich konsistent mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **XACT_ABORT** festgelegt **ON** und die gesamte Transaktion zurückgesetzt wird. Weitere Informationen zu den **XACT_ABORT** finden Sie unter [SET XACT_ABORT (Transact-SQL)](http://msdn.microsoft.com/library/ms188792.aspx).  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Eine Sitzung kann nur eine Transaktion zu einem bestimmten Zeitpunkt ausgeführt; Punkte speichern und geschachtelten Transaktionen werden nicht unterstützt.  
  
 Es liegt in der Verantwortung des der [!INCLUDE[DWsql](../../includes/dwsql-md.md)] Programmierers, COMMIT nur zu einem Zeitpunkt auszugeben, wenn alle Daten von der Transaktion verwiesen logisch richtig ist.  
  
 Wenn eine Sitzung beendet wird, bevor eine Transaktion abgeschlossen ist, wird für die Transaktion ein Rollback ausgeführt.  
  
 Transaktionsmodi werden auf Sitzungsebene verwaltet. Wenn eine Sitzung eine explizite Transaktion beginnt oder AUTOCOMMIT auf OFF festgelegt oder Set auf ON IMPLICIT_TRANSACTIONS, hat es z. B. keine Auswirkungen auf die Transaktionsmodi einer anderen Sitzung.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Kann eine Transaktion kein Rollback, nachdem eine COMMIT-Anweisung ausgegeben wurde, da die datenänderungen einem dauerhaften Bestandteil der Datenbank vorgenommen wurden.  
  
 Die [Datenbank erstellen &#40; Azure SQL Datawarehouse &#41; ](../../t-sql/statements/create-database-azure-sql-data-warehouse.md) und [DROP DATABASE &#40; Transact-SQL &#41; ](../../t-sql/statements/drop-database-transact-sql.md) Befehle können nicht innerhalb einer expliziten Transaktion verwendet werden.  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]eine Transaktion, die Freigabe Mechanismus besitzt nicht. Dies bedeutet, dass zu jedem gegebenen Zeitpunkt zeitlich nur eine Sitzung für jede Transaktion im System bearbeitet werden kann.  
  
## <a name="locking-behavior"></a>Sperrverhalten  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]verwendet sperren, um die Integrität von Transaktionen sicherzustellen und die Konsistenz der Datenbanken beizubehalten, wenn mehrere Benutzer gleichzeitig auf Daten zugreifen. Sperren wird durch implizite und explizite Transaktionen verwendet. Jede Transaktion fordert Sperren verschiedener Typen für die Ressourcen, z. B. Tabellen oder Datenbanken, von denen die Transaktion abhängt. Alle [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Sperren sind Tabelle oder einem höheren. Diese Sperren verhindern, dass die Ressourcen durch andere Transaktionen in einer Weise geändert werden, die zu Problemen für die Transaktion führen würde, die die Sperre angefordert hat. Jede Transaktion hebt ihre Sperren wieder, wenn er nicht mehr eine Abhängigkeit von den gesperrten Ressourcen verfügt; explizite Transaktionen beibehalten sperren, bis die Transaktion abgeschlossen ist, wenn er ist entweder ein Commit oder Rollback.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-an-explicit-transaction"></a>A. Verwenden eine explizite Transaktion  
  
```  
BEGIN TRANSACTION;  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT;  
```  
  
### <a name="b-rolling-back-a-transaction"></a>B. Rollback einer Transaktion  
 Das folgende Beispiel zeigt die Auswirkung von Rollback einer Transaktion.  In diesem Beispiel wird die ROLLBACK-Anweisung wird ein Rollback der INSERT-Anweisung, die erstellte Tabelle sind jedoch weiterhin vorhanden.  
  
```  
CREATE TABLE ValueTable (id int);  
BEGIN TRANSACTION;  
       INSERT INTO ValueTable VALUES(1);  
       INSERT INTO ValueTable VALUES(2);  
ROLLBACK;  
```  
  
### <a name="c-setting-autocommit"></a>C. AUTOCOMMIT-Einstellung  
 Im folgenden Beispiel wird die Einstellung AUTOCOMMIT auf `ON`.  
  
```  
SET AUTOCOMMIT ON;  
```  
  
 Im folgenden Beispiel wird die Einstellung AUTOCOMMIT auf `OFF`.  
  
```  
SET AUTOCOMMIT OFF;  
```  
  
### <a name="d-using-an-implicit-multi-statement-transaction"></a>D. Verwenden eine implizite Transaktion mit mehreren Anweisungen  
  
```  
SET AUTOCOMMIT OFF;  
CREATE TABLE ValueTable (id int);  
INSERT INTO ValueTable VALUES(1);  
INSERT INTO ValueTable VALUES(2);  
COMMIT;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SET IMPLICIT_TRANSACTIONS &#40; Transact-SQL &#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL &#40; Transact-SQL &#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
