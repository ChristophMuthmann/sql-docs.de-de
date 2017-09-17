---
title: Catalog.master_properties (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 00bfa716-5390-48e3-b30c-d954d5e0be47
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: 0fcbdca57c7764eaec758d2ad9ef3ab8675a3a9b
ms.contentlocale: de-de
ms.lasthandoff: 09/08/2017

---
# <a name="catalogmasterproperties-ssisdb-database"></a>Catalog.master_properties (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Zeigt die Eigenschaften der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale-Out-Master.

|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|Der Name des der horizontalen Skalierung der master-Eigenschaft.|  
|property_value|**nvarchar(max)**|Der Wert der horizontalen Skalierung der master-Eigenschaft.|

## <a name="remarks"></a>Hinweise
Diese Ansicht zeigt eine Zeile für jede Dezentrales Skalieren master-Eigenschaft. In dieser Sicht werden folgende Eigenschaften angezeigt:

|Eigenschaftsname|Description|  
|-------------------|-----------------| 
|**CLUSTER_LOGDB_SERVER**|Die SQL-Server, bei der Datenbank anmelden sucht in.|
|**LAST_ONLINE_TIME**|Zeitpunkt der letzten Wenn Scale-Out-Master online ist.|
|**MACHINE_IP**|Die IP-Adresse des Computers.|
|**COMPUTERNAME**|Der Name des Computers.|
|**MASTER_ADDRESS**|Der Endpunkt der Scale-Out-Master.|
|**MASTER_SERVICE_PORT**|Der Port in der Endpunkt des Scale-Out-Master.|
|**SSLCERT_THUMBPRINT**|Der Fingerabdruck des Zertifikats Scale-Out-Master.|

## <a name="permissions"></a>Berechtigungen
Alle Mitglieder der Datenbankrolle public verfügen über die Leseberechtigung für diese Sicht. 

