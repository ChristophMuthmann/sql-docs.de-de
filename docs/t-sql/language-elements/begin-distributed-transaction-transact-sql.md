---
title: BEGIN DISTRIBUTED TRANSACTION (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/29/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DISTRIBUTED
- BEGIN_DISTRIBUTED_TRANSACTION_TSQL
- DISTRIBUTED_TSQL
- BEGIN DISTRIBUTED TRANSACTION
dev_langs:
- TSQL
helpviewer_keywords:
- BEGIN DISTRIBUTED TRANSACTION statement
- distributed transactions [SQL Server], starting
- MS DTC, transaction management
- distributed transactions [SQL Server], BEGIN DISTRIBUTED TRANSACTION statement
- servers [SQL Server], distributed transactions
- starting distributed transactions
- remote servers [SQL Server], distributed transactions
- starting transactions
ms.assetid: c3bc2716-39d3-4061-8c6a-8734899231ac
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ba68a3a1a4cde26a94acd47000f46d1a0ceb40ef
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="begin-distributed-transaction-transact-sql"></a>BEGIN DISTRIBUTED TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den Anfang einer verteilten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Transaktion an, die von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC) verwaltet wird.  
    
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BEGIN DISTRIBUTED { TRAN | TRANSACTION }   
     [ transaction_name | @tran_name_variable ]   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *transaction_name*  
 Der benutzerdefinierte Transaktionsname, unter dem die verteilte Transaktion in den MS DTC-Hilfsprogrammen nachverfolgt wird. *Transaction_name* muss den Regeln für Bezeichner entsprechen und muss \<= 32 Zeichen.  
  
 @*tran_name_variable*  
 Der Name einer benutzerdefinierten Variablen, die einen Transaktionsnamen enthält. Mithilfe dieses Namens wird die verteilte Transaktion in den MS DTC-Hilfsprogrammen nachverfolgt. Die Variable muss deklariert werden, mit einem **Char**, **Varchar**, **Nchar**, oder **Nvarchar** -Datentyp.  
  
## <a name="remarks"></a>Hinweise  
 Die Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], die die BEGIN DISTRIBUTED TRANSACTION-Anweisung ausführt, wird als Transaktionsurheber bezeichnet und steuert den Abschluss der Transaktion. Wenn im Anschluss eine COMMIT TRANSACTION- oder ROLLBACK TRANSACTION-Anweisung für die Sitzung ausgegeben wird, fordert die steuernde Instanz MS DTC auf, die Beendigung der verteilten Transaktion auf allen beteiligten Instanzen zu verwalten.  
  
 Die Momentaufnahmeisolation auf Transaktionsebene unterstützt keine verteilten Transaktionen.  
  
 Remoteinstanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)] werden in erster Linie in eine verteilte Transaktion eingetragen, wenn eine bereits in der verteilten Transaktion eingetragene Sitzung eine verteilte Abfrage ausführt, die auf einen Verbindungsserver verweist.  
  
 Wenn BEGIN DISTRIBUTED TRANSACTION beispielsweise auf Server A ausgegeben wird, ruft die Sitzung eine gespeicherte Prozedur auf Server B und eine weitere gespeicherte Prozedur auf Server C auf. Die gespeicherte Prozedur auf Server C führt eine verteilte Abfrage für Server D aus. In diesem Fall sind alle vier Computer an der verteilten Transaktion beteiligt. Die Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf Server A ist die ursprüngliche steuernde Instanz für die Transaktion.  
  
 Die Sitzungen, die an den verteilten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Transaktionen beteiligt sind, erhalten kein Transaktionsobjekt, das sie an eine andere Sitzung weitergeben können, um explizit in die verteilte Transaktion eingetragen zu werden. Ein Remoteserver kann nur in die Transaktion eingetragen werden, wenn er das Ziel einer verteilten Abfrage oder eines Aufrufs einer remote gespeicherten Prozedur ist.  
  
 Wenn eine verteilte Abfrage in einer lokalen Transaktion ausgeführt wird, wird die Transaktion automatisch zu einer verteilten Transaktion höher gestuft, wenn die OLE DB-Zieldatenquelle ITransactionLocal unterstützt. Wenn die OLE DB-Zieldatenquelle ITransactionLocal nicht unterstützt, sind nur für schreibgeschützte Vorgänge in der verteilten Abfrage zulässig.  
  
 Eine in die verteilte Transaktion bereits eingetragene Sitzung führt einen Aufruf einer remote gespeicherten Prozedur aus, die auf einen Remoteserver verweist.  
  
 Die **Sp_configure remote Proc Trans** option steuert, ob Aufrufe remote gespeicherter Prozeduren in einer lokalen Transaktion automatisch bewirken, dass die lokale Transaktion zu einer verteilten Transaktion von MS DTC verwaltet höher gestuft werden. Der Verbindungsebene SET-Option REMOTE_PROC_TRANSACTIONS können verwendet werden, um das Überschreiben der Standardeinstellung der Instanz von **Sp_configure remote Proc Trans**. Wenn diese Option aktiviert ist, bewirkt der Aufruf einer remote gespeicherten Prozedur, dass eine lokale Transaktion zu einer verteilten Transaktion höher gestuft wird. Die Verbindung, die die MS DTC-Transaktion erstellt, wird Urheber der Transaktion. COMMIT TRANSACTION startet einen von MS DTC koordinierten Commit. Wenn die **Sp_configure remote Proc Trans** Option auf ON festgelegt ist, Aufrufe remote gespeicherter Prozeduren in lokalen Transaktionen werden automatisch als Teil einer verteilten Transaktion geschützt, ohne Clientanwendungen mit speziell Problem umgeschrieben werden müssen BEGIN DISTRIBUTED TRANSACTION statt BEGIN TRANSACTION.  
  
 Weitere Informationen zur verteilten Transaktionsumgebung und zum verteilten Transaktionsprozess finden Sie in der Dokumentation zu [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel wird ein Kandidat aus der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank sowohl auf der lokalen Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] als auch auf einer Instanz auf einem Remoteserver gelöscht. Für die Transaktion wird sowohl in der lokalen Datenbank als auch in der Remotedatenbank entweder ein Commit oder ein Rollback ausgeführt.  
  
> [!NOTE]  
>  Wenn MS DTC derzeit nicht auf dem Computer installiert ist, auf dem die Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] ausgeführt wird, erzeugt dieses Beispiel eine Fehlermeldung. Weitere Informationen zum Installieren von MS DTC finden Sie in der Dokumentation zu Microsoft Distributed Transaction Coordinator.  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN DISTRIBUTED TRANSACTION;  
-- Delete candidate from local instance.  
DELETE AdventureWorks2012.HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
-- Delete candidate from remote instance.  
DELETE RemoteServer.AdventureWorks2012.HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT TRANSACTION;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [COMMIT WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)  
  
  
