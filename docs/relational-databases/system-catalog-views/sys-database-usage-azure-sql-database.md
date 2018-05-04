---
title: Sys. database_usage (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- database_usage
- database_usage_TSQL
- sys.database_usage_TSQL
- sys.database_usage
dev_langs:
- TSQL
helpviewer_keywords:
- database_usage
- sys.database_usage
ms.assetid: be6820de-60bf-4ddd-ace7-4077893d630f
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 7754ed63cc6325b9b6cf1650e7b71daad03393ae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdatabaseusage-azure-sql-database"></a>sys.database_usage (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **Hinweis: Dies gilt nur für Azure SQL-Datenbank V11.**  
  
 Listet Anzahl, Typ und Dauer der Datenbanken auf dem [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Server.  
  
 Die **Sys. database_usage** Ansicht enthält die folgenden Spalten.  
  
|Spaltenname|Description|  
|-----------------|-----------------|  
|Uhrzeit|Das Datum, an dem die Verwendungsereignisse eingetreten sind.|  
|sku|Der Typ der Dienstebene für die Datenbank: **Web**, **Business**, **grundlegende**, **Standard**, **Premium**|  
|quantity|Die maximale Anzahl von Datenbanken eines SKU-Typs, der an diesem Tag vorhanden war.|  
  
## <a name="permissions"></a>Berechtigungen  
 Nur-Lese Zugriff auf diese Sicht ist verfügbar für alle Benutzer mit Berechtigungen zum Verbinden mit der **master** Datenbank.  
  
## <a name="remarks"></a>Hinweise  
 Die **Sys. database_usage** Sicht gibt eine Zeile für jeden Tag des Abonnements zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [Preisdetails – SQL-Datenbank](http://go.microsoft.com/fwlink/?LinkID=394978)   
 [Konten und Abrechnung in Windows Azure SQL-Datenbank](http://msdn.microsoft.com/library/windowsazure/ee621788.aspx)  
  
  
