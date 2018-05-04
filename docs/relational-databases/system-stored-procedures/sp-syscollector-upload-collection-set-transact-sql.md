---
title: Sp_syscollector_upload_collection_set (Transact-SQL) | Microsoft Docs
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
- sp_syscollector_upload_collection_set
- sp_syscollector_upload_collection_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_upload_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: eed9232c-2b0a-4b6a-8ba0-76b7c99f48dc
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0bb4ba04b346e6931a55d26172f0d34b27166950
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spsyscollectoruploadcollectionset-transact-sql"></a>sp_syscollector_upload_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Startet das Hochladen von Sammlungssatzdaten, wenn der Sammlungssatz aktiviert ist.  
  
> [!IMPORTANT]  
>  Diese gespeicherte Prozedur kann nur für Sammlungssätze verwendet werden, die für die Datensammlung im Modus mit Zwischenspeicherung und den Upload konfiguriert werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_syscollector_upload_collection_set [[ @collection_set_id = ] collection_set_id ]  
          , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@collection_set_id =** ] *Collection_set_id*  
 Der eindeutige lokale Bezeichner für den Sammlungssatz. *Collection_set_id* ist **Int** und muss einen Wert aufweisen, wenn *Namen* ist NULL.  
  
 [ **@name =** ] **'***name***'**  
 Ist der Name des Sammlungssatzes. *Namen* ist **Sysname** und muss einen Wert aufweisen, wenn *Collection_set_id* ist NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Entweder *Collection_set_id* oder *Namen* muss über einen Wert verfügen; beide darf nicht NULL sein.  
  
 Diese Prozedur kann zum Starten eines bedarfsgesteuerten Hochladens für einen ausgeführten Sammlungssatz verwendet werden. Sie kann nur für Sammlungssätze verwendet werden, die für die Datensammlung im Modus mit Zwischenspeicherung und den Upload konfiguriert werden. So kann ein Benutzer Daten zur Analyse erhalten, ohne auf ein geplantes Hochladen warten zu müssen.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Dc_operator** (mit EXECUTE-Berechtigung) festen Datenbankrolle "" zum Ausführen dieser Prozedur.  
  
## <a name="example"></a>Beispiel  
 Führt ein bedarfsgesteuertes Hochladen eines Sammlungssatzes mit dem Namen `Simple Collection Set` aus.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_upload_collection_set @name = 'Simple Collection Set' ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Datensammlung](../../relational-databases/data-collection/data-collection.md)  
  
  
