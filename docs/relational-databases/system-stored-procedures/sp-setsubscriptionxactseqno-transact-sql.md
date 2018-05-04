---
title: Sp_setsubscriptionxactseqno (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_setsubscriptionxactseqno
- sp_setsubscriptionxactseqno_TSQL
helpviewer_keywords:
- sp_setsubscriptionxactseqno
ms.assetid: cdb4e0ba-5370-4905-b03f-0b0c6f080ca6
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ed413bbb2c3b0f57658b496a828952f5c0702ca4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spsetsubscriptionxactseqno-transact-sql"></a>sp_setsubscriptionxactseqno (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt bei der Problembehandlung die Protokollfolgenummer (LSN, Log Sequence Number) der nächsten vom Verteilungs-Agent auf dem Abonnenten anzuwendenden Transaktion an. Der Agent hat dadurch die Möglichkeit, eine Transaktion, die einen Fehler erzeugt hat, auszulassen. Diese gespeicherte Prozedur wird auf dem Abonnenten für die Abonnementdatenbank ausgeführt. Wird nicht für Nicht-SQL Server-Abonnenten unterstützt.  
  
> [!CAUTION]  
>  Eine falsche Verwendung dieser gespeicherten Prozedur oder die Angabe eines falschen LSN-Werts kann den Verteilungs-Agent dazu veranlassen, Änderungen, die bereits auf den Abonnenten angewendet wurden, rückgängig zu machen oder alle noch verbleibenden Änderungen auszulassen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_setsubscriptionxactseqno [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @xact_seqno = ] xact_seqno   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publisher=** ] **"***Publisher***"**  
 Der Name des Verlegers. *Publisher* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@publisher_db=** ] **"***Publisher_db***"**  
 Der Name der Veröffentlichungsdatenbank. *Publisher_db* ist **Sysname**, hat keinen Standardwert. Für einen nicht - SQL Server-Verleger, *Publisher_db* ist der Name der Verteilungsdatenbank.  
  
 [  **@publication=** ] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert. Wenn der Verteilungs-Agent von mehreren Veröffentlichungen gemeinsam verwendet wird, müssen Sie angeben, dass Wert ALL für *Veröffentlichung*.  
  
 [  **@xact_seqno=** ] *Xact_seqno*  
 Die LSN der nächsten Transaktion auf dem Verteiler, die auf dem Abonnenten angewendet werden soll. *Xact_seqno* ist **varbinary(16)**, hat keinen Standardwert.  
  
## <a name="result-set"></a>Resultset  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**URSPRÜNGLICHE XACT_SEQNO**|**varbinary(16)**|Die ursprüngliche LSN der nächsten Transaktion, die auf dem Abonnenten angewendet werden soll.|  
|**AKTUALISIERTE XACT_SEQNO**|**varbinary(16)**|Die aktualisierte LSN der nächsten Transaktion, die auf dem Abonnenten angewendet werden soll.|  
|**STREAM-ANZAHL FÜR ABONNEMENT**|**int**|Die Anzahl der bei der letzten Synchronisierung verwendeten Abonnementdatenströme.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_setsubscriptionxactseqno** wird bei der Transaktionsreplikation verwendet.  
  
 **Sp_setsubscriptionxactseqno** kann nicht in einer Peer-zu-Peer-transaktionsreplikationstopologie verwendet werden.  
  
 **Sp_setsubscriptionxactseqno** können verwendet werden, um eine bestimmte Transaktion zu überspringen, die einen Fehler verursacht, wird beim Anwenden auf dem Abonnenten. Wenn ein Fehler auftritt und der Verteilungs-Agent wird beendet, rufen Sie [Sp_helpsubscriptionerrors &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helpsubscriptionerrors-transact-sql.md) auf dem Verteiler den Xact_seqno-Wert, der die fehlgeschlagene Transaktion abzurufen, und rufen Sie anschließend **Sp_setsubscriptionxactseqno**, übergeben Sie diesen Wert für *Xact_seqno*. Dadurch wird sichergestellt, dass nur die Befehle nach dieser LSN verarbeitet werden.  
  
 Geben Sie den Wert **0** für *Xact_seqno* alle ausstehenden Befehle in der Verteilungsdatenbank auf dem Abonnenten übermittelt.  
  
 **Sp_setsubscriptionxactseqno** kann fehlschlagen, wenn der Verteilungs-Agent Datenströme für mehrere Abonnements verwendet.  
  
 Wenn dieser Fehler auftritt, müssen Sie den Verteilungs-Agent mit einem Datenstrom für ein einzelnes Abonnement ausführen. Weitere Informationen finden Sie unter [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_setsubscriptionxactseqno**.  
  
  
