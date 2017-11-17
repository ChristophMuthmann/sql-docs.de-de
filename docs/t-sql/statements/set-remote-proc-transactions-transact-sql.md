---
title: SET REMOTE_PROC_TRANSACTIONS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- REMOTE_PROC_TRANSACTIONS_TSQL
- SET REMOTE_PROC_TRANSACTIONS
- REMOTE_PROC_TRANSACTIONS
- SET_REMOTE_PROC_TRANSACTIONS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- remote stored procedures [SQL Server]
- SET REMOTE_PROC_TRANSACTIONS statement
- distributed transactions [SQL Server], starting
- REMOTE_PROC_TRANSACTIONS option
- active transactions
ms.assetid: 4d284ae9-3f5f-465a-b0dd-1328a4832a03
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9ad924fa239801adb78cb391a26249cb1c2a21d1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-remoteproctransactions-transact-sql"></a>SET REMOTE_PROC_TRANSACTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt an, dass durch das Ausführen einer remote gespeicherten Prozedur, sofern eine lokale Transaktion aktiv ist, eine verteilte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Transaktion gestartet wird, die von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Manager (MS DTC) verwaltet wird.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Diese Option wird aus Gründen der Abwärtskompatibilität mit Anwendungen bereitgestellt, die remote gespeicherte Prozeduren verwenden. Verwenden Sie statt dem Aufruf von remote gespeicherten Prozeduren verteilte Abfragen, die auf Verbindungsserver verweisen. Diese sind mit definiert [Sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET REMOTE_PROC_TRANSACTIONS { ON | OFF }   
```  
  
## <a name="arguments"></a>Argumente  
 ON | OFF  
 Bei ON wird eine verteilte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Transaktion gestartet, wenn eine remote gespeicherte Prozedur von einer lokalen Transaktion aus ausgeführt wird. Bei OFF wird keine verteilte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Transaktion gestartet, wenn eine remote gespeicherte Prozedur von einer lokalen Transaktion aus aufgerufen wird.  
  
## <a name="remarks"></a>Hinweise  
 Wenn REMOTE_PROC_TRANSACTIONS auf ON festgelegt ist und eine remote gespeicherte Prozedur aufgerufen wird, wird eine verteilte Transaktion gestartet und bei MS DTC eingetragen. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz, die die remote gespeicherte Prozedur aufruft, wird als Transaktionsurheber bezeichnet und steuert die Beendigung der Transaktion. Wenn im Anschluss eine COMMIT TRANSACTION- oder ROLLBACK TRANSACTION-Anweisung für die Verbindung ausgegeben wird, fordert die steuernde Instanz MS DTC auf, die Beendigung der verteilten Transaktion auf den beteiligten Computern zu verwalten.  
  
 Nachdem eine verteilte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Transaktion gestartet wurde, können Aufrufe remote gespeicherter Prozeduren für weitere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanzen erfolgen, die als Remoteserver definiert wurden. Alle Remoteserver werden in der verteilten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Transaktion eingetragen, und MS DTC stellt sicher, dass die Transaktion für jeden Remoteserver abgeschlossen wird.  
  
 REMOTE_PROC_TRANSACTIONS ist eine Einstellung auf Verbindungsebene, die verwendet werden kann, auf der Instanzebene überschreiben **Sp_configure remote Proc Trans** Option.  
  
 Wenn REMOTE_PROC_TRANSACTIONS auf OFF festgelegt ist, werden Aufrufe remote gespeicherter Prozeduren nicht als Teil einer lokalen Transaktion ausgeführt. Für die Änderungen, die von der remote gespeicherten Prozedur vorgenommen werden, wird ein Commit oder ein Rollback durchgeführt, wenn die gespeicherte Prozedur abgeschlossen wird. Weitere COMMIT TRANSACTION- oder ROLLBACK TRANSACTION-Anweisungen der Verbindung, die die remote gespeicherte Prozedur aufgerufen hat, wirken sich nicht  auf die von der Prozedur durchgeführte Verarbeitung aus.  
  
 Die Option REMOTE_PROC_TRANSACTIONS ist eine Kompatibilitätsoption, die nur remote gespeicherte Prozedur-Aufrufe an Instanzen von wirkt sich auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als Remoteserver mit definiert **Sp_addserver**. Die Option gilt nicht für verteilte Abfragen, die Ausführen einer gespeicherten Prozedur in einer Instanz, die als Verbindungsserver mithilfe definiert **Sp_addlinkedserver**.  
  
 Die Einstellung von SET REMOTE_PROC_TRANSACTIONS wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="see-also"></a>Siehe auch  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

