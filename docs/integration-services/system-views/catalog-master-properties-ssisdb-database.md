---
title: catalog.master_properties (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 00bfa716-5390-48e3-b30c-d954d5e0be47
caps.latest.revision: "3"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 28f72cd6a5ea50bdc310d89bf16dbe498e06a638
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="catalogmasterproperties-ssisdb-database"></a>catalog.master_properties (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Zeigt die Eigenschaften des ausgewählten [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Masters an.

|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|Der Name der Scale Out Master-Eigenschaft.|  
|property_value|**nvarchar(max)**|Der Wert der Scale Out Master-Eigenschaft.|

## <a name="remarks"></a>Hinweise
In dieser Sicht wird für jede Scale Out Master-Eigenschaft eine Zeile angezeigt. In dieser Sicht werden folgende Eigenschaften angezeigt:

|Eigenschaftsname|Description|  
|-------------------|-----------------| 
|**CLUSTER_LOGDB_SERVER**|Die SQL Server-Instanz, die die Protokolldatenbank enthält.|
|**LAST_ONLINE_TIME**|Zeitpunkt, zu dem der Scale Out Master zuletzt online war.|
|**MACHINE_IP**|Die IP-Adresse des Computers.|
|**MACHINE_NAME**|Der Name des Computers.|
|**MASTER_ADDRESS**|Der Endpunkt des Scale Out Masters.|
|**MASTER_SERVICE_PORT**|Der Port im Endpunkt des Scale Out Masters.|
|**SSLCERT_THUMBPRINT**|Der Fingerabdruck des Scale Out Master-Zertifikats.|

## <a name="permissions"></a>Berechtigungen
Alle Mitglieder der öffentlichen Datenbankrolle besitzen die Leseberechtigung für diese Sicht. 
