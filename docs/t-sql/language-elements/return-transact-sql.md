---
title: RETURN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RETURN_TSQL
- RETURN
dev_langs: TSQL
helpviewer_keywords:
- unconditionally exiting program
- stored procedures [SQL Server], exiting
- batches [SQL Server], exiting
- statement blocks [SQL Server]
- queries [SQL Server], exiting
- exiting queries [SQL Server]
- exiting procedures [SQL Server]
- RETURN statement
ms.assetid: 1d9c8247-fd89-4544-be9c-01c95b745db0
caps.latest.revision: "39"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: e7584bdee4d9b07706bc961db23e0090e28cc581
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="return-transact-sql"></a>RETURN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Bewirkt ein unbedingtes Beenden einer Abfrage oder einer Prozedur. RETURN wird sofort und vollständig ausgeführt und kann zu jedem Zeitpunkt zum Beenden einer Prozedur, eines Batchs oder eines Anweisungsblocks verwendet werden. Anweisungen nach RETURN werden nicht ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RETURN [ integer_expression ]   
```  
  
## <a name="arguments"></a>Argumente  
 *integer_expression*  
 Der zurückgegebene ganzzahlige Wert. Gespeicherte Prozeduren können einen ganzzahligen Wert an eine aufrufende Prozedur oder Anwendung zurückgeben.  
  
## <a name="return-types"></a>Rückgabetypen  
 Optional gibt **Int**.  
  
> [!NOTE]  
>  Sofern nicht anders angegeben, geben alle gespeicherten Systemprozeduren den Wert 0 zurück. Dieser Wert zeigt einen erfolgreichen Verlauf an. Ein Wert ungleich 0 zeigt einen Fehler an.  
  
## <a name="remarks"></a>Hinweise  
 Wenn Sie RETURN in einer gespeicherten Prozedur verwenden, kann RETURN keinen NULL-Wert zurückgeben. Falls eine Prozedur versucht, einen NULL-Wert zurückzugeben (z. B. wenn RETURN @status verwendet wird, und @status den Wert NULL hat), wird eine Warnmeldung generiert und der Wert 0 zurückgegeben.  
  
 Der Rückgabestatuswert kann in nachfolgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen des Batches oder der Prozedur verwendet werden, von der die aktuelle Prozedur ausgeführt wurde, der Aufruf muss jedoch in der folgenden Form eingegeben werden: `EXECUTE @return_status = <procedure_name>`.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-from-a-procedure"></a>A. Rückgabe aus einer Prozedur  
 Das folgende Beispiel verdeutlicht, dass `findjobs` eine Beendigung der Prozedur nach dem Senden einer Meldung an den Benutzerbildschirm bewirkt, wenn bei Ausführung von `RETURN` kein Benutzername als Parameter angegeben ist. Falls ein Benutzername angegeben wurde, werden die Namen aller von diesem Benutzer in der aktuellen Datenbank erstellten Objekte aus den entsprechenden Systemtabellen abgerufen.  
  
```  
CREATE PROCEDURE findjobs @nm sysname = NULL  
AS   
IF @nm IS NULL  
    BEGIN  
        PRINT 'You must give a user name'  
        RETURN  
    END  
ELSE  
    BEGIN  
        SELECT o.name, o.id, o.uid  
        FROM sysobjects o INNER JOIN master..syslogins l  
            ON o.uid = l.sid  
        WHERE l.name = @nm  
    END;  
```  
  
### <a name="b-returning-status-codes"></a>B. Rückgabestatuscodes  
 Im folgenden Beispiel wird der Staat für die ID des angegebenen Kontakts überprüft. Falls als Staat Washington (`WA`) ermittelt wird, wird der Status `1` zurückgegeben. Andernfalls wird für jede andere Bedingung `2` zurückgegeben (ein anderer Wert als `WA` für `StateProvince` oder ein `ContactID`-Wert, der mit keiner Zeile übereinstimmte).  
  
```  
USE AdventureWorks2012;  
GO  
CREATE PROCEDURE checkstate @param varchar(11)  
AS  
IF (SELECT StateProvince FROM Person.vAdditionalContactInfo WHERE ContactID = @param) = 'WA'  
    RETURN 1  
ELSE  
    RETURN 2;  
GO  
```  
  
 Im folgenden Beispiel wird der Rückgabestatus der Ausführung von `checkstate` gezeigt. Das erste Beispiel zeigt einen Kontakt in Washington an, das zweite einen Kontakt außerhalb Washingtons und das dritte einen ungültigen Kontakt. Die lokale Variable `@return_status` muss deklariert werden, bevor sie verwendet werden kann.  
  
```  
DECLARE @return_status int;  
EXEC @return_status = checkstate '2';  
SELECT 'Return Status' = @return_status;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Return Status 
  
 ------------- 
  
 1
 ```  
  
 Führen Sie die Abfrage mit einer anderen Kontaktnummer erneut aus.  
  
```  
DECLARE @return_status int;  
EXEC @return_status = checkstate '6';  
SELECT 'Return Status' = @return_status;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Return Status  
 -------------  
  
 2
 ```  
  
 Führen Sie die Abfrage mit einer weiteren Kontaktnummer erneut aus.  
  
```  
DECLARE @return_status int  
EXEC @return_status = checkstate '12345678901';  
SELECT 'Return Status' = @return_status;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Return Status  
 -------------  
  
 2
 ```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)   
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)  
  
  
