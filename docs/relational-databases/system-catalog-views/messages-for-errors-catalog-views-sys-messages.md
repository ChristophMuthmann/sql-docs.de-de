---
title: Sys.Messages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- messages_TSQL
- sys.messages_TSQL
- sys.messages
- messages
dev_langs:
- TSQL
helpviewer_keywords:
- error messages [SQL Server]
- sys.messages catalog view
- error numbers [SQL Server]
ms.assetid: 8c16ecdf-68f4-4a2a-b594-086e3344e58a
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: aa37a19743801bea70b1c78d8c9606be74dfe2f8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="messages-for-errors-catalog-views---sysmessages"></a>(Für Fehlermeldungen) Meldungskatalogsichten - sys.messages
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jeden **Message_id** oder **Language_id** der Fehlermeldungen im System, für den systemdefinierten und benutzerdefinierte Nachrichten. Weitere Informationen finden Sie unter [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md).  
   
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**message_id**|**int**|ID der Meldung. Ist innerhalb des gesamten Servers eindeutig. Bei Meldungs-IDs unterhalb von 50000 handelt es sich um Systemmeldungen.|  
|**language_id**|**smallint**|Sprach-ID für die der Text in **Text** verwendet wird, gemäß **"syslanguages"**. Dies ist für einen angegebenen eindeutigen **Message_id**.|  
|**severity**|**tinyint**|Schweregrad des Fehlers, der zwischen 1 und 25 liegen kann. Dies ist für alle innerhalb meldungssprachen einer **Message_id**.|  
|**is_event_logged**|**bit**|1 = Bei einer Fehlerausgabe wird eine Meldung in das Ereignisprotokoll geschrieben. Dies ist für alle innerhalb meldungssprachen einer **Message_id**.|  
|**text**|**nvarchar(2048)**|Text der Nachricht verwendet wird, wenn das entsprechende **Language_id** aktiv ist.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Nachrichten &#40;Fehler&#41; Katalogsichten &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/8ac78c53-7b97-41b3-9cbd-5f97c179f1f2)   
 [Ausnahmemeldung Programmierung](http://msdn.microsoft.com/library/0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c)   
 [Fehlermeldungen](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [Datenbankmodul (Fehler und Ereignisse)](../../relational-databases/errors-events/database-engine-events-and-errors.md)  
  
  
