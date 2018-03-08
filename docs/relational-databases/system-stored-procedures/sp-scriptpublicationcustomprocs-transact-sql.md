---
title: Sp_scriptpublicationcustomprocs (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_scriptpublicationcustomprocs
- sp_scriptpublicationcustomprocs_TSQL
helpviewer_keywords: sp_scriptpublicationcustomprocs
ms.assetid: b06102d5-4284-4834-b126-bc0baea49be5
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 258a82812bbda7f572bb56178dd65973769ce357
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spscriptpublicationcustomprocs-transact-sql"></a>sp_scriptpublicationcustomprocs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt Skriptcode für die benutzerdefinierten Prozeduren INSERT, UPDATE und DELETE für alle Tabellenartikel in einer Veröffentlichung, in der die Schemaoption für das automatische Generieren von benutzerdefinierten Prozeduren aktiviert ist. **Sp_scriptpublicationcustomprocs** ist besonders nützlich zum Einrichten von Abonnements für die die Momentaufnahme manuell angewendet wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_scriptpublicationcustomprocs [ @publication = ] 'publication_name'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication** =] **"***Publication_name***"**  
 Der Name der Veröffentlichung. *Publication_name* ist **Sysname** hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Gibt ein Resultset besteht aus einer einzelnen **nvarchar(4000)** Spalte. Das Resultset enthält die vollständige CREATE PROCEDURE-Anweisung, die zum Erstellen der benutzerdefinierten, gespeicherten Prozedur notwendig ist.  
  
## <a name="remarks"></a>Hinweise  
 Für benutzerdefinierte Prozeduren wird nur bei Artikeln Skriptcode erstellt, für die die Schemaoption für das automatische Generieren von benutzerdefinierten Prozeduren (0x2) aktiviert ist.  
  
 Die folgenden Verfahren werden verwendet, indem **Sp_scriptpublicationcustomprocs** Prozeduren auf dem Abonnenten erstellen und sollte nicht direkt ausgeführt werden:  
  
 **sp_script_reconciliation_delproc**  
  
 **sp_script_reconciliation_insproc**  
  
 **sp_script_reconciliation_vdelproc**  
  
 **sp_script_reconciliation_xdelproc**  
  
 **sp_scriptdelproc**  
  
 **sp_scriptinsproc**  
  
 **sp_scriptmappedupdproc**  
  
 **sp_scriptupdproc**  
  
 **sp_scriptvdelproc**  
  
 **sp_scriptvupdproc**  
  
 **sp_scriptxdelproc**  
  
 **sp_scriptxupdproc**  
  
## <a name="permissions"></a>Berechtigungen  
 Führen Sie Berechtigung ist **öffentlichen**; eine sicherheitsüberprüfung erfolgt innerhalb dieser gespeicherten Prozedur den Zugriff auf Mitglieder der Einschränken der **Sysadmin** festen Serverrolle und **Db_ Besitzer** festen Datenbankrolle in der aktuellen Datenbank.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
