---
title: Sys. sp_rda_deauthorize_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_deauthorize_db
- sys.sp_rda_deauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_deauthorize_db stored procedure
ms.assetid: 2e362e15-2cd5-4856-9f0b-54df56b0866b
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e01204dbd28c114daed84a6c3d7d92691952694e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syssprdadeauthorizedb-transact-sql"></a>Sys. sp_rda_deauthorize_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Entfernt die authentifizierte Verbindung zwischen einer lokalen Stretch-aktivierte Datenbank und der Azure-Remotedatenbank an. Führen Sie **Sp_rda_deauthorize_db** Wenn die Remotedatenbank nicht erreichbar ist oder in einem inkonsistenten Zustand und Verhaltens der Abfrage für alle Stretch-aktivierten Tabellen in der Datenbank geändert werden soll.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
sp_rda_deauthorize_db   
```  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder >0 (Fehler)  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert Db_owner-Berechtigungen.  
  
## <a name="remarks"></a>Hinweise  
 Nach dem Ausführen **Sp_rda_deauthorize_db** , alle Abfragen für Stretch aktivierte Datenbanken und Tabellen fehl. D. h., ist der Abfragemodus auf deaktiviert festgelegt. Um diesen Modus beenden, führen Sie einen der folgenden Schritte.  
  
-   Führen Sie [sp_rda_reauthorize_db &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) eine Verbindung mit der Azure-Remotedatenbank herstellen. Dieser Vorgang setzt automatisch den Abfragemodus zu LOCAL_AND_REMOTE, dies ist das Standardverhalten für Stretch-Datenbank. D. h. zurückgeben Abfragen Ergebnisse lokale und Remotedaten.  
  
-   Führen Sie [sp_rda_set_query_mode &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) und dem LOCAL_ONLY-Argument können Abfragen weiterhin nur lokale Daten ausführen können.  
  
## <a name="see-also"></a>Siehe auch  
 [sys.sp_rda_set_query_mode &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)   
 [sys.sp_rda_reauthorize_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
