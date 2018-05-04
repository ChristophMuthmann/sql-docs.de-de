---
title: Sp_replication_agent_checkup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- sp_replication_agent_checkup_TSQL
- sp_replication_agent_checkup
helpviewer_keywords:
- sp_replication_agent_checkup
ms.assetid: 50357c2e-71aa-4e13-9e2e-0977a3655cc9
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: af4b136a2e34ca7a4c26b2d7844209afd295b64e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spreplicationagentcheckup-transact-sql"></a>sp_replication_agent_checkup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Überprüft alle Verteilungsdatenbanken auf Replikations-Agents, die zwar ausgeführt werden, aber innerhalb des angegebenen Taktintervalls keine Verlaufsdaten protokolliert haben. Diese gespeicherte Prozedur wird auf dem Verteiler für jede Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_replication_agent_checkup [ [ @heartbeat_interval = ] heartbeat_interval ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@heartbeat_interval** =] **"***Heartbeat_interval***"**  
 Die maximale Anzahl von Minuten, für die ein Agent ausgeführt werden kann, ohne dass eine Statusmeldung protokolliert wird. *Heartbeat_interval* ist **Int**, hat den Standardwert von 10 Minuten.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **Sp_replication_agent_checkup** löst Fehler 14151 für jeden Agent, der als verdächtig erkannt wird. Außerdem wird eine Fehlerverlaufsmeldung für die Agents protokolliert.  
  
## <a name="remarks"></a>Hinweise  
 **Sp_replication_agent_checkup** wird bei der Momentaufnahme-, Transaktions- und Mergereplikation verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** -Serverrolle kann ausführen **Sp_replication_agent_checkup**.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
