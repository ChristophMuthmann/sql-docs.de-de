---
title: sp_rda_set_query_mode (Transact-SQL) | Microsoft Docs
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
- sys.sp_rda_set_query_mode
- sys.sp_rda_set_query_mode_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_query_mode stored procedure
ms.assetid: 65a0b390-cf87-4db7-972a-1fdf13456c88
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 643c2af15c946853389e09658ee82cb6d6112d98
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syssprdasetquerymode-transact-sql"></a>sp_rda_set_query_mode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Gibt an, ob Abfragen an der aktuellen Stretch-aktivierte Datenbank und zugehörigen Tabellen sowohl lokale als auch Daten (Standard) oder nur lokale Daten zurückgeben.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_rda_set_query_mode [ @mode = ] @mode   
    [ , [ @force = ]  @force ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @mode = ] *@mode*  
 Ist eine der folgenden Werte.  
  
-   **Deaktivierte** alle Abfragen für Stretch-aktivierte Tabellen fehl.  
  
-   **LOCAL_ONLY** Abfragen für Stretch-aktivierte Tabellen nur lokale Daten zurückgeben.  
  
-   **LOCAL_AND_REMOTE** Abfragen für Stretch-aktivierte Tabellen zurückgegeben, lokale und Remotedaten. Dies ist das Standardverhalten.  
  
 [ @force = ]  *@force*  
 Ist ein optionale Bitwert, den auf 1 festlegen können, wenn Sie den Abfragemodus ohne Überprüfung ändern möchten.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder >0 (Fehler)  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert Db_owner-Berechtigungen.  
  
## <a name="remarks"></a>Hinweise  
 Die folgenden erweiterten gespeicherten Prozeduren legen auch den Abfragemodus für eine Stretch-aktivierte Datenbank.  
  
-   **sp_rda_deauthorize_db**  
  
     Nach dem Ausführen **Sp_rda_deauthorize_db** , alle Abfragen für Stretch aktivierte Datenbanken und Tabellen fehl. D. h., ist der Abfragemodus auf deaktiviert festgelegt. Um diesen Modus beenden, führen Sie einen der folgenden Schritte.  
  
    -   Führen Sie [sp_rda_reauthorize_db &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) eine Verbindung mit der Azure-Remotedatenbank herstellen. Dieser Vorgang setzt automatisch den Abfragemodus zu LOCAL_AND_REMOTE, dies ist das Standardverhalten für Stretch-Datenbank. D. h. zurückgeben Abfragen Ergebnisse lokale und Remotedaten.  
  
    -   Führen Sie [sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) und dem LOCAL_ONLY-Argument können Abfragen weiterhin nur lokale Daten ausführen können.  
  
-   **sp_rda_reauthorize_db**  
  
     Bei der Ausführung [sp_rda_reauthorize_db &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) zum Wiederherstellen der Verbindung mit der Azure-Remotedatenbank setzt diesen Vorgang automatisch den Abfragemodus auf LOCAL_AND_REMOTE, also das Standardverhalten für Stretch-Datenbank. D. h. zurückgeben Abfragen Ergebnisse lokale und Remotedaten.  
  
## <a name="see-also"></a>Siehe auch  
 [sys.sp_rda_deauthorize_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
