---
title: Catalog. catalog_properties (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: e604a382-95c8-4764-b268-742eb5c6d4cf
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ca3d5da05126d5b71bf6d714f9e8449f9f5c8335
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcatalogproperties-ssisdb-database"></a>catalog.catalog_properties (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt die Eigenschaften der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|Der Name der Katalogeigenschaft.|  
|property_value|**nvarchar(256)**|Der Wert der Katalogeigenschaft.|  
  
## <a name="remarks"></a>Hinweise  
 In dieser Sicht wird eine Zeile für jede Katalogeigenschaft angezeigt. In dieser Sicht werden folgende Eigenschaften angezeigt:  
  
|Eigenschaftsname|Description|  
|-------------------|-----------------|  
|**ENCRYPTION_ALGORITHM**|Der Typ des Verschlüsselungsalgorithmus, mit dem sensible Daten verschlüsselt werden. Die unterstützten Werte lauten: `DES`, `TRIPLE_DES`, `TRIPLE_DES_3KEY`, `DESX`, `AES_128`, `AES_192`und `AES_256`. Hinweis: Zum Ändern dieser Eigenschaft muss sich die Katalogdatenbank im Einzelbenutzermodus befinden.|  
|**MAX_PROJECT_VERSIONS**|Die Anzahl von neuen Projektversionen, die für ein einzelnes Projekt beibehalten werden. Wenn Versionscleanup aktiviert ist, werden frühere Versionen, die diese Anzahl überschreiten, gelöscht.|  
|**OPERATION_CLEANUP_ENABLED**|Wenn der Wert `TRUE`ist, werden Vorgangsdetails und Vorgangsmeldungen, die älter als **RETENTION_WINDOW** (Tage) sind, aus dem Katalog gelöscht. Wenn der Wert `FALSE`ist, werden alle Vorgangsdetails und Vorgangsmeldungen im Katalog gespeichert. Hinweis: eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Auftrag führt den vorgangscleanup für den.|  
|**RETENTION_WINDOW AN**|Die Anzahl der Tage, für die Vorgangsdetails und Vorgangsmeldungen im Katalog gespeichert werden. Wenn der Wert `-1`lautet, ist die Beibehaltungsdauer unendlich. Hinweis: Wenn kein Cleanup erfolgen soll, legen Sie **OPERATION_CLEANUP_ENABLED** auf **FALSE**fest.|  
|**VALIDATION_TIMEOUT**|Überprüfungen werden beendet, wenn sie nicht innerhalb der von dieser Eigenschaft angegebenen Anzahl von Sekunden abgeschlossen werden.|  
|**VERSION_CLEANUP_ENABLED**|Wenn der Wert `TRUE`ist, wird nur die von **MAX_PROJECT_VERSIONS** angegebene Anzahl von Projektversionen im Katalog gespeichert, und alle anderen Projektversionen werden gelöscht. Wenn der Wert **FALSE**ist, werden alle Projektversionen im Katalog gespeichert. Hinweis: eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Auftrag führt den vorgangscleanup für den.|  
|**SERVER_LOGGING_LEVEL**|Der Standardprotokolliergrad für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Server.|  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Sicht erfordert eine der folgenden Berechtigungen:  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
  
