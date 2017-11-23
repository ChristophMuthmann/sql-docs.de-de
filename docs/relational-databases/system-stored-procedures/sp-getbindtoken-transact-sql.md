---
title: Sp_getbindtoken (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_getbindtoken
- sp_getbindtoken_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_getbindtoken
ms.assetid: 5db87d77-85fa-45a3-a23a-3ea500f9a5ac
caps.latest.revision: "47"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9313b111c17e637a01e0a9c615eecd7719b1d17d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spgetbindtoken-transact-sql"></a>sp_getbindtoken (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt einen eindeutigen Bezeichner für die Transaktion zurück. Dieser eindeutige Bezeichner ist eine Zeichenfolge, mit der Sitzungen mithilfe von sp_bindsession gebunden werden.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden Sie stattdessen Multiple Active Results Sets (MARS) oder verteilte Transaktionen. Weitere Informationen finden Sie unter [mithilfe von Multiple Active Result Sets &#40; MARS &#41; ](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_getbindtoken [@out_token =] 'return_value' OUTPUT   
```  
  
## <a name="arguments"></a>Argumente  
 [@out_token=]'*Rückgabewert*"  
 Das Token, das zum Binden von Sitzungen verwendet wird. *Rückgabewert* ist **varchar(255)** hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Sp_getbindtoken gibt ein gültiges Token zurück, nur, wenn die gespeicherte Prozedur innerhalb einer aktiven Transaktion ausgeführt wird. Andernfalls gibt [!INCLUDE[ssDE](../../includes/ssde-md.md)] eine Fehlermeldung zurück. Beispiel:  
  
```  
-- Declare a variable to hold the bind token.  
-- No active transaction.  
DECLARE @bind_token varchar(255);  
-- Trying to get the bind token returns an error 3921.  
EXECUTE sp_getbindtoken @bind_token OUTPUT;  
Server: Msg 3921, Level 16, State 1, Procedure sp_getbindtoken, Line 4  
Cannot get a transaction token if there is no transaction active.  
Reissue the statement after a transaction has been started.  
```  
  
 Wenn Sp_getbindtoken zum Eintragen einer verteilten transaktionsverbindung innerhalb einer geöffneten Transaktion verwendet wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] das gleiche Token zurück. Beispiel:  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @bind_token varchar(255);  
  
BEGIN TRAN;  
  
EXECUTE sp_getbindtoken @bind_token OUTPUT;  
SELECT @bind_token AS Token;  
  
BEGIN DISTRIBUTED TRAN;  
  
EXECUTE sp_getbindtoken @bind_token OUTPUT;  
SELECT @bind_token AS Token;  
```  
  
 Beide `SELECT`-Anweisungen geben dasselbe Token zurück:  
  
```  
Token  
-----  
PKb'gN5<9aGEedk_16>8U=5---/5G=--  
(1 row(s_) affected)  
  
Token  
-----  
PKb'gN5<9aGEedk_16>8U=5---/5G=--  
(1 row(s_) affected)  
```  
  
 Das Bindungstoken kann zusammen mit sp_bindsession verwendet werden, um neue Sitzungen an dieselbe Transaktion zu binden. Das Bindungstoken ist nur lokal innerhalb jeder Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] gültig und kann nicht für mehrere Instanzen freigegeben werden.  
  
 Zum Erhalten und Übergeben eines Bindungstokens muss sp_getbindtoken vor sp_bindsession ausgeführt werden, um denselben Sperrbereich gemeinsam verwenden zu können. Wenn Sie ein Bindungstoken erhalten, wird sp_bindsession ordnungsgemäß ausgeführt.  
  
> [!NOTE]  
>  Um ein Bindungstoken zu erhalten, das von einer erweiterten gespeicherten Prozedur verwendet werden kann, sollte die API-Funktion srv_getbindtoken von Open Data Services verwendet werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein Bindungstoken erhalten und der Bindungstokenname angezeigt.  
  
```  
DECLARE @bind_token varchar(255);  
BEGIN TRAN;  
EXECUTE sp_getbindtoken @bind_token OUTPUT;  
SELECT @bind_token AS Token;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Token`  
  
 `----------------------------------------------------------`  
  
 `\0]---5^PJK51bP<1F<-7U-]ANZ`  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_bindsession &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindsession-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Srv_getbindtoken &#40; Erweiterte gespeicherte Prozedur API &#41;](../../relational-databases/extended-stored-procedures-reference/srv-getbindtoken-extended-stored-procedure-api.md)  
  
  
