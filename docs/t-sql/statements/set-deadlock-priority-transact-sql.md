---
title: SET DEADLOCK_PRIORITY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET DEADLOCK_PRIORITY
- DEADLOCK_PRIORITY_TSQL
- SET_DEADLOCK_PRIORITY_TSQL
- DEADLOCK_PRIORITY
dev_langs:
- TSQL
helpviewer_keywords:
- deadlocks [SQL Server], priority settings
- DEADLOCK_PRIORITY option
- locking [SQL Server], deadlocks
- priority deadlock settings [SQL Server]
- SET DEADLOCK_PRIORITY statement
ms.assetid: 810a3a8e-3da3-4bf9-bb15-7b069685a1b6
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 12be78ffb2e899170095415a03dccc69511f7424
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-deadlockpriority-transact-sql"></a>SET DEADLOCK_PRIORITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Gibt die relative Bedeutung an, um zu bestimmen, ob die aktuelle Sitzung die Verarbeitung fortsetzt, wenn ein Deadlock mit einer anderen Sitzung vorliegt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET DEADLOCK_PRIORITY { LOW | NORMAL | HIGH | <numeric-priority> | @deadlock_var | @deadlock_intvar }  
  
<numeric-priority> ::= { -10 | -9 | -8 | … | 0 | … | 8 | 9 | 10 }  
```  
  
## <a name="arguments"></a>Argumente  
 LOW  
 Gibt an, dass die aktuelle Sitzung das Deadlockopfer ist, wenn sie von einem Deadlock betroffen ist und für die anderen Sitzungen in der Deadlockkette als Deadlockpriorität entweder NORMAL oder HIGH oder ein ganzzahliger Wert größer -5 festgelegt ist. Die aktuelle Sitzung ist nicht das Deadlockopfer, wenn für die anderen Sitzungen als Deadlockpriorität ein ganzzahliger Wert kleiner -5 festgelegt ist. Außerdem wird angegeben, dass die aktuelle Sitzung als Deadlockopfer in Frage kommt, wenn für eine andere Sitzung die Deadlockpriorität auf LOW oder einen ganzzahligen Wert gleich -5 festgelegt wurde.  
  
 NORMAL  
 Gibt an, dass die aktuelle Sitzung das Deadlockopfer ist, wenn für die anderen Sitzungen in der Deadlockkette als Deadlockpriorität HIGH oder ein ganzzahliger Wert größer 0 festgelegt ist. Ist für die anderen Sitzungen als Deadlockpriorität LOW oder ein ganzzahliger Wert kleiner 0 festgelegt, ist die aktuelle Sitzung nicht das Deadlockopfer. Außerdem wird angegeben, dass die aktuelle Sitzung als Deadlockopfer in Frage kommt, wenn für eine andere Sitzung die Deadlockpriorität auf NORMAL oder einen ganzzahligen Wert gleich 0 festgelegt wurde. NORMAL ist die Standardpriorität.  
  
 HIGH  
 Gibt an, dass die aktuelle Sitzung das Deadlockopfer ist, wenn für die anderen Sitzungen in der Deadlockkette die Deadlockpriorität auf einen ganzzahligen Wert größer 5 festgelegt ist. Die aktuelle Sitzung kommt auch dann als Deadlockopfer in Frage, wenn bei einer anderen Sitzung die Deadlockpriorität auf HIGH oder einen ganzzahligen Wert gleich 5 festgelegt ist.  
  
 \<numerische Priorität >  
 Ein Bereich ganzer Zahlen (-10 bis 10) zur Darstellung der 21 Stufen der Deadlockpriorität. Über diesen Bereich wird angegeben, dass die aktuelle Sitzung das Deadlockopfer ist, wenn für andere Sitzungen in der Deadlockkette ein höherer Wert für die Deadlockpriorität festgelegt wurde. Die aktuelle Sitzung ist dann nicht das Deadlockopfer, wenn für die anderen Sitzungen eine Deadlockpriorität festgelegt wurde, die niedriger ist als der Wert der aktuellen Sitzung. Außerdem wird angegeben, dass die aktuelle Sitzung als Deadlockopfer in Frage kommt, wenn für andere Sitzungen der gleiche Wert für die Deadlockpriorität festgelegt ist wie für die aktuelle Sitzung. LOW entspricht -5, NORMAL entspricht 0 und HIGH entspricht 5.  
  
 **@***Deadlock_var*  
 Eine Zeichenvariable, die die Deadlockpriorität angibt. Für die Variable muss einer der Werte 'LOW', 'NORMAL' oder 'HIGH' festgelegt werden. Die Variable muss groß genug sein, um die gesamte Zeichenfolge aufzunehmen.  
  
 **@***Deadlock_intvar*  
 Eine ganzzahlige Variable, die die Deadlockpriorität angibt. Für die Variable muss ein ganzzahliger Wert innerhalb des Bereichs (-10 bis 10) angegeben werden.  
  
## <a name="remarks"></a>Hinweise  
 Deadlocks entstehen, wenn zwei Sitzungen auf den Zugriff auf Ressourcen warten, die jeweils durch die andere gesperrt wurden. Wenn eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ermittelt, dass für zwei Sitzungen ein Deadlock vorliegt, wird dieser Deadlock aufgelöst, indem eine der Sitzungen als Deadlockopfer ausgewählt wird. Es erfolgt ein Rollback der aktuellen Transaktion des Deadlockopfers, und die Deadlockfehlermeldung 1205 wird an den Client zurückgegeben. Damit werden alle von dieser Sitzung verhängten Sperren freigegeben, sodass die andere Sitzung den Vorgang fortsetzen kann.  
  
 Von der für die Sitzungen festgelegten Deadlockpriorität hängt ab, welche Sitzung als Deadlockopfer ausgewählt wird:  
  
-   Wenn für beide Sitzungen die gIeiche Deadlockprioriät festgelegt wurde, wählt die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diejenige Sitzung als Deadlockopfer aus, für die das Rollback weniger aufwändig ist. Wenn beispielsweise für beide Sitzungen die Deadlockpriorität HIGH festgelegt wurde, wählt die Instanz diejenige Sitzung als Opfer aus, bei der das Rollback voraussichtlich weniger aufwändig sein wird.  
  
-   Wenn die Sitzungen verschiedene Deadlockprioritäten aufweisen, wird die Sitzung mit der niedrigsten Deadlockpriorität als Deadlockopfer ausgewählt.  
  
 SET DEADLOCK_PRIORITY wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Variable zum Festlegen der Deadlockpriorität `LOW` verwendet.  
  
```  
DECLARE @deadlock_var NCHAR(3);  
SET @deadlock_var = N'LOW';  
  
SET DEADLOCK_PRIORITY @deadlock_var;  
GO  
```  
  
 Im folgenden Beispiel wird die Deadlockpriorität `NORMAL` festgelegt.  
  
```  
SET DEADLOCK_PRIORITY NORMAL;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [@@LOCK_TIMEOUT &#40;Transact-SQL&#41;](../../t-sql/functions/lock-timeout-transact-sql.md)   
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET LOCK_TIMEOUT &#40; Transact-SQL &#41;](../../t-sql/statements/set-lock-timeout-transact-sql.md)  
  
  

