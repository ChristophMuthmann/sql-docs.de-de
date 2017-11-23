---
title: sp_flush_log (Transact-SQL) | Microsoft Docs
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
- sp_flush_log_TSQL
- sys.sp_flush_log
- sys.sp_flush_log_TSQL
- sp_flush_log
dev_langs: TSQL
helpviewer_keywords: sys.sp_flush_log
ms.assetid: 75cc9f52-3b1f-4754-b1e7-ce0dd3323bc9
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 36bc92271f4c4125c2f9d6d1b3bff014071cefff
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysspflushlog-transact-sql"></a>sys.sp_flush_log (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Leert das Transaktionsprotokoll der aktuellen Datenbank auf den Datenträger, wodurch alle verzögert dauerhaften Transaktionen, für die zuvor ein Commit ausgeführt wurde, festgeschrieben werden.  
  
 Wenn Sie die verzögerte Transaktionsdauerhaftigkeit aufgrund der Leistungsvorteile verwenden, gleichzeitig aber auch eine Zusicherung im Hinblick auf den maximalen Datenverlust benötigen, der bei einem Serverabsturz oder Failover auftreten darf, sollten Sie in regelmäßigen Abständen `sys.sp_flush_log` ausführen. Wenn Sie beispielsweise sicherstellen möchten, dass maximal eine Menge von Daten verloren geht, die x Sekunden entspricht, würden Sie `sp_flush_log` alle x Sekunden ausführen.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 Durch die Ausführung von `sys.sp_flush_log` wird sichergestellt, dass alle verzögert dauerhaften Transaktionen, für die zuvor ein Commit ausgeführt wurde, in dauerhafte Transaktionen konvertiert werden. Finden Sie unter dem Thema [Steuern der Transaktionsdauerhaftigkeit](../../relational-databases/logs/control-transaction-durability.md) für Weitere Informationen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```tsql  
  
sys.sp_flush_log  
  
```  
  
#### <a name="parameters"></a>Parameter  
 Keine.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Der Rückgabecode 1 steht für Erfolg.  Alle anderen Werte geben einen Fehler an.  
  
## <a name="result-sets"></a>Resultsets  
 Keine.  
  
## <a name="sample-code"></a>Beispielcode  
  
```tsql  
.  
EXECUTE sys.sp_flush_log  
  
```  
  
  
