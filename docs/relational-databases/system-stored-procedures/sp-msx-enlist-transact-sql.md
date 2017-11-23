---
title: Sp_msx_enlist (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
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
- sp_msx_enlist_TSQL
- sp_msx_enlist
dev_langs: TSQL
helpviewer_keywords: sp_msx_enlist
ms.assetid: ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7aaafbe078ffa9cedf87241bc61060fc3b61bdad
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="spmsxenlist-transact-sql"></a>sp_msx_enlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt den aktuellen Server der Liste der verfügbaren Server auf dem Masterserver hinzu.  
  
> [!CAUTION]  
>  Die gespeicherte Prozedur **sp_msx_enlist** bearbeitet die Registrierung. Die Registrierung sollte nicht manuell bearbeitet werden, da durch ungeeignete oder fehlerhafte Änderungen schwerwiegende Konfigurationsprobleme auf dem System verursacht werden können. Nur erfahrene Benutzer sollten deshalb den Registrierungs-Editor zum Bearbeiten der Registrierung verwenden. Weitere Informationen finden Sie in der Dokumentation zu Microsoft Windows.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_msx_enlist [@msx_server_name =] 'msx_server'   
     [, [@location =] 'location']  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@msx_server_name =**] **"***Msx_server***"**  
 Der Name des Multiserververwaltungsservers (Master). *msx_server* ist vom Datentyp **sysname**und hat keinen Standardwert.  
  
 [  **@location =**] **"***Speicherort***"**  
 Der Speicherort des hinzuzufügenden Zielservers. *location* ist vom Datentyp **nvarchar(100)**und hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig verfügen Mitglieder der festen Serverrolle **sysadmin** über die Berechtigungen zum Ausführen dieser Prozedur.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der aktuelle Server auf dem Masterserver `AdventureWorks1` eingetragen. Der Speicherort für den aktuellen Server lautet `Building 21, Room 309, Rack 5`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
    N'Building 21, Room 309, Rack 5' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_msx_defect &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-msx-defect-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Xp_cmdshell &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xp-cmdshell-transact-sql.md)  
  
  
