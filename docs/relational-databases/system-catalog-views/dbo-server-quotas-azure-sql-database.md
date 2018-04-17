---
title: dbo. server_quotas (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database
ms.service: sql-database
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.server_quotas
- dbo.server_quotas_TSQL
- server_quotas
- server_quotas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server_quotas
ms.assetid: 34423903-1aaa-4a55-88a6-8228315d84e7
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 66f6e2c1cae1b8743314a8a9ff844040e1f91f35
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="dboserverquotas-azure-sql-database"></a>dbo.server_quotas (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> **WICHTIG!** Dies gilt für  **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11 nur!**  
>   
>  Diese Funktion befindet sich in einem Vorschauzustand. Erstellen Sie keine Abhängigkeit von der spezifischen Implementierung dieser Funktion, da die Funktion in zukünftigen Versionen ggf. geändert oder entfernt werden kann.  
  
 Gibt die auf dem Server verfügbaren Datenbank-Kontingenttypen zurück.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|quota_name|**nvarchar**|Der Kontingenttyp für den Server. Der **Premium_database** -Typ entspricht Datenbanken mit einer Ressourcenreservierung.|  
|quota_value|**int**|Die Anzahl der im Server zulässigen Kontingenttypen.|  
  
## <a name="permissions"></a>Berechtigungen  
 Alle Benutzerrollen, die berechtigt sind, eine Verbindung mit der virtuellen **master** -Datenbank herzustellen, haben Zugriff auf diese Sicht.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Premiumdatenbanken](http://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
