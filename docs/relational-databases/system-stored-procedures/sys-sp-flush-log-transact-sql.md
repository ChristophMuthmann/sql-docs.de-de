---
title: sp_flush_log (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_flush_log_TSQL
- sys.sp_flush_log
- sys.sp_flush_log_TSQL
- sp_flush_log
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_flush_log
ms.assetid: 75cc9f52-3b1f-4754-b1e7-ce0dd3323bc9
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7e53ff87ccdebe430594c27b673de3c106291113
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysspflushlog-transact-sql"></a>sys.sp_flush_log (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Leert das Transaktionsprotokoll der aktuellen Datenbank auf den Datenträger, wodurch alle verzögert dauerhaften Transaktionen, für die zuvor ein Commit ausgeführt wurde, festgeschrieben werden.  
  
 Wenn Sie die verzögerte Transaktionsdauerhaftigkeit aufgrund der Leistungsvorteile verwenden, gleichzeitig aber auch eine Zusicherung im Hinblick auf den maximalen Datenverlust benötigen, der bei einem Serverabsturz oder Failover auftreten darf, sollten Sie in regelmäßigen Abständen `sys.sp_flush_log` ausführen. Wenn Sie beispielsweise sicherstellen möchten, dass maximal eine Menge von Daten verloren geht, die x Sekunden entspricht, würden Sie `sp_flush_log` alle x Sekunden ausführen.  
  
 Durch die Ausführung von `sys.sp_flush_log` wird sichergestellt, dass alle verzögert dauerhaften Transaktionen, für die zuvor ein Commit ausgeführt wurde, in dauerhafte Transaktionen konvertiert werden. Finden Sie unter dem Thema [Steuern der Transaktionsdauerhaftigkeit](../../relational-databases/logs/control-transaction-durability.md) für Weitere Informationen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```sql  
  
sys.sp_flush_log  
  
```  
  
#### <a name="parameters"></a>Parameter  
 Keine.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Der Rückgabecode 1 steht für Erfolg.  Alle anderen Werte geben einen Fehler an.  
  
## <a name="result-sets"></a>Resultsets  
 Keine.  
  
## <a name="sample-code"></a>Beispielcode  
  
```sql  
.  
EXECUTE sys.sp_flush_log  
  
```  
  
  
