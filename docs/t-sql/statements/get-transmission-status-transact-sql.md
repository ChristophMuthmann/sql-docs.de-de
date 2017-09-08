---
title: GET_TRANSMISSION_STATUS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STATUS_TSQL
- TRANSMISSION
- TRANSMISSION_TSQL
- GET_TRANSMISSION_STATUS
- STATUS
- GET_TRANSMISSION_STATUS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker], transmission status
- Service Broker errors, transmission status
- transmission status information
- status information [SQL Server], conversations
- GET_TRANSMISSION_STATUS statement
ms.assetid: 621805d5-49ed-4764-b3cb-2ae4a3bf797e
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b6d5152cca3f4ddb1afe0d8042c84743c31abf9b
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="gettransmissionstatus-transact-sql"></a>GET_TRANSMISSION_STATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den Status der letzten Übermittlung für eine Seite einer Konversation zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
GET_TRANSMISSION_STATUS ( conversation_handle )  
```  
  
## <a name="arguments"></a>Argumente  
 *conversation_id*  
 Bezeichnet das Konversationshandle für die Konversation. Dieser Parameter ist vom Typ **"uniqueidentifier"**.  
  
## <a name="return-types"></a>Rückgabetypen  
 **nchar**  
  
## <a name="remarks"></a>Hinweise  
 Gibt eine Zeichenfolge zurück, die eine Beschreibung des Status des letzten Übermittlungsversuchs für eine angegebene Konversation enthält. Eine leere Zeichenfolge zurückgegeben, wenn der letzte Übermittlungsversuch erfolgreich war, wenn noch kein Übermittlungsversuch vorgenommen wurde, oder wenn die *Conversation_handle* ist nicht vorhanden.  
  
 Die von dieser Funktion zurückgegebenen Informationen sind mit den in der last_transmission_error-Spalte der Verwaltungssicht sys.transmission_queue angezeigten Informationen identisch. Diese Funktion kann jedoch zum Suchen nach dem Übermittlungsstatus von Konversationen verwendet werden, für die zurzeit keine Meldungen in der Übermittlungswarteschlange vorhanden sind.  
  
> [!NOTE]  
>  GET_TRANSMISSION_STATUS stellt nur Informationen zu Meldungen bereit, für die ein Konversationsendpunkt in der aktuellen Instanz vorhanden ist. Zu Meldungen, die weitergeleitet werden müssen, sind demnach keine Informationen verfügbar.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Übermittlungsstatus für die Konversation mit dem Konversationshandle `58ef1d2d-c405-42eb-a762-23ff320bddf0` gemeldet.  
  
```  
SELECT Status =  
    GET_TRANSMISSION_STATUS('58ef1d2d-c405-42eb-a762-23ff320bddf0') ;  
```  
  
 Es folgt ein Beispielresultset, das auf Zeilenlänge umformatiert wurde:  
  
 `Status`  
  
 `-------------------------------`  
  
 `The Service Broker protocol transport is disabled or not configured.`  
  
 In diesem Fall ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] so konfiguriert, dass [!INCLUDE[ssSB](../../includes/sssb-md.md)] nicht über das Netzwerk kommunizieren darf.  
  
## <a name="see-also"></a>Siehe auch  
 [Sys. conversation_endpoints &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)   
 [Sys. transmission_queue &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-transmission-queue-transact-sql.md)  
  
  

