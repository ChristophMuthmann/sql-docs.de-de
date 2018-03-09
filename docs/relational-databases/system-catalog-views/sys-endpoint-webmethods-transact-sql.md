---
title: endpoint_webmethods (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.endpoint_webmethods_TSQL
- sys.endpoint_webmethods
- endpoint_webmethods_TSQL
- sys.http_soap_methods_TSQL
- endpoint_webmethods
- sys.http_soap_methods
dev_langs:
- TSQL
helpviewer_keywords:
- sys.endpoint_webmethods catalog view
ms.assetid: 7dad0cf6-eafa-47cf-98cc-75ba8d3c7959
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 93053b36893b6812128d2bb397a656d395f839af
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sysendpointwebmethods-transact-sql"></a>sys.endpoint_webmethods (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Enthält eine Zeile mit einer FOR EACH SOAP-Methode, die für einen SOAP-aktivierten HTTP-Endpunkt definiert ist. Die Kombination der Spalten Endpoint_id und dem angegebenen Namespace ist eindeutig.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|endpoint_id|**int**|ID des Endpunktes, für die die Webmethode definiert ist|  
|namespace|**nvarchar(384)**|Namespace für die Webmethode|  
|method_alias|**nvarchar(64)**|Alias für die Methode<br /><br /> Hinweis: [!INCLUDE[tsql](../../includes/tsql-md.md)] -Bezeichner lassen Zeichen, die nicht in WSDL-Methodennamen zulässig sind.<br /><br /> Mit dem Alias wird der in der WSDL-Beschreibung des Endpunktes verfügbar gemachte Name dem eigentlichen zugrunde liegenden ausführbaren [!INCLUDE[tsql](../../includes/tsql-md.md)]-Objekt zugeordnet, das beim Starten der Webmethode aufgerufen wird.|  
|object_name|**nvarchar(776)**|Der Name des Objekts gemäß der Option NAME =, an das die Webmethode umgeleitet wird. Namensteile werden durch einen Punkt (.) getrennt, und mit eckigen Klammern, `[``]`.<br /><br /> Der Objektname muss gemäß der WSDL-Option dreiteilig sein.|  
|result_schema|**tinyint**|Option, die bestimmt, welches XSD ggf. mit einer Antwort zurückgesendet wird.<br /><br /> 0 = Keine<br /><br /> 1 = Standard<br /><br /> 2 = Standardwert|  
|result_schema_desc|**nvarchar(60)**|Beschreibung der Option, die bestimmt, welches XSD ggf. mit einer Antwort zurückgesendet wird.<br /><br /> Keine<br /><br /> Standardwert<br /><br /> DEFAULT|  
|result_format|**tinyint**|Option, die bestimmt, wie Ergebnisse in der Antwort formatiert werden.<br /><br /> 1 = ALL_RESULTS<br /><br /> 2 = ROWSETS_ONLY<br /><br /> 3 = KEINE|  
|result_format_desc|**nvarchar(60)**|Beschreibung der Option, die bestimmt, wie Ergebnisse in der Antwort formatiert werden.<br /><br /> ALL_RESULTS<br /><br /> ROWSETS_ONLY<br /><br /> Keine|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Endpunkte-Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
