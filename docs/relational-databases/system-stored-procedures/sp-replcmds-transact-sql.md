---
title: Sp_replcmds (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_replcmds_TSQL
- sp_replcmds
helpviewer_keywords:
- sp_replcmds
ms.assetid: 7e932f80-cc6e-4109-8db4-2b7c8828df73
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 279d002e0a088386440cd978410476dee8def3ac
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spreplcmds-transact-sql"></a>sp_replcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Mit dieser Prozedur werden die Transaktionsbefehle zurückgegeben, die für die Replikation gekennzeichnet sind. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
> [!IMPORTANT]  
>  Die **Sp_replcmds** Prozedur sollte nur zur Fehlerbehebung bei der Replikation ausgeführt werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_replcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@maxtrans=**] *Maxtrans*  
 Die Anzahl der Transaktionen, zu denen Informationen zurückgegeben werden sollen. *Maxtrans* ist **Int**, hat den Standardwert **1**, die angibt, dass der nächsten Transaktions Verteilung wartet.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Artikel-id**|**int**|Die ID des Artikels.|  
|**verbleiben**|**bit**|Gibt an, ob es sich um einen Teilbefehl handelt.|  
|**Befehl**|**varbinary(1024)**|Der Befehlswert.|  
|**xactid**|**binary(10)**|Transaktions-ID|  
|**xact_seqno**|**varbinary(16)**|Die Transaktionssequenznummer.|  
|**publication_id**|**int**|Die ID der Veröffentlichung.|  
|**command_id**|**int**|ID des Befehls in [MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md).|  
|**command_type**|**int**|Der Typ des Befehls.|  
|**originator_srvname**|**sysname**|Server, von dem die Transaktion stammt|  
|**originator_db**|**sysname**|Datenbank, von der die Transaktion stammt|  
|**pkHash**|**int**|Nur interne Verwendung.|  
|**originator_publication_id**|**int**|ID der Veröffentlichung, von der die Transaktion stammt|  
|**originator_db_version**|**int**|Version der Datenbank, von der die Transaktion stammt|  
|**originator_lsn**|**varbinary(16)**|Identifiziert die Protokollfolgenummer (LSN, Log Sequence Number) für den Befehl in der ursprünglichen Veröffentlichung|  
  
## <a name="remarks"></a>Hinweise  
 **Sp_replcmds** wird vom Protokollleseprozess bei der Transaktionsreplikation verwendet.  
  
 Replikation behandelt den ersten Client, der ausgeführt wird **Sp_replcmds** innerhalb einer bestimmten Datenbank als Protokollleser.  
  
 Diese Prozedur kann Befehle für mit dem Besitzer qualifizierte Tabellen erstellen oder den Tabellennamen nicht kennzeichnen (Standard). Das Hinzufügen von qualifizierten Tabellennamen ermöglicht die Datenreplikation von Tabellen mit einem bestimmten Besitzer innerhalb einer Datenbank zu Tabellen mit demselben Besitzer in einer anderen Datenbank.  
  
> [!NOTE]  
>  Da der Tabellenname in der Quelldatenbank durch den Besitzernamen qualifiziert wird, muss es sich bei dem Tabellenbesitzer in der Zieldatenbank um den gleichen Besitzernamen handeln.  
  
 Clients, die versuchen, führen Sie **Sp_replcmds** innerhalb derselben Datenbank wird die Fehlermeldung 18752, bis der erste Client die Verbindung trennt. Nachdem der erste Client die Verbindung trennt, kann ein anderer Client ausführen **Sp_replcmds**, und wird zum neuen Protokollleser.  
  
 Die Fehlermeldungsnummer 18759 wird sowohl hinzugefügt der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll und die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anwendung zu protokollieren, wenn **Sp_replcmds** kann einen Textbefehl repliziert werden, da der Textzeiger nicht wurde in der gleichen Transaktion abgerufen.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder die **Db_owner** feste Datenbankrolle können ausführen **Sp_replcmds**.  
  
## <a name="see-also"></a>Siehe auch  
 [Fehlermeldungen](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [Sp_repldone &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [Sp_replflush &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [Sp_repltrans &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
