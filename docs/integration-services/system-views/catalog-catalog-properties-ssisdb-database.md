---
title: catalog.catalog_properties (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: e604a382-95c8-4764-b268-742eb5c6d4cf
caps.latest.revision: "10"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 16fa5f45b6d4368816e7d5ea115d7f4cff6aa9cb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="catalogcatalogproperties-ssisdb-database"></a>catalog.catalog_properties (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt die Eigenschaften des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalogs an.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|property_name|**nvarchar(256)**|Der Name der Katalogeigenschaft.|  
|property_value|**nvarchar(256)**|Der Wert der Katalogeigenschaft.|  
  
## <a name="remarks"></a>Hinweise  
 In dieser Sicht wird eine Zeile für jede Katalogeigenschaft angezeigt.
  
|Eigenschaftsname|Description|  
|-------------------|-----------------|  
|**DEFAULT_EXECUTION_MODE**|Der serverweite Standardausführungsmodus für Pakete – `Server` (0) oder `Scale Out` (1). |
|**ENCRYPTION_ALGORITHM**|Der Typ des Verschlüsselungsalgorithmus, mit dem sensible Daten verschlüsselt werden. Die unterstützten Werte lauten: `DES`, `TRIPLE_DES`, `TRIPLE_DES_3KEY`, `DESX`, `AES_128`, `AES_192`und `AES_256`. Hinweis: Zum Ändern dieser Eigenschaft muss sich die Katalogdatenbank im Einzelbenutzermodus befinden.|
|**IS_SCALEOUT_ENABLED**|Wenn der Wert `True` lautet, wird das SSIS Scale Out-Feature aktiviert. Wenn Sie Scale Out nicht aktiviert haben, kann diese Eigenschaft nicht in der Sicht angezeigt werden.|
|**MAX_PROJECT_VERSIONS**|Die Anzahl von neuen Projektversionen, die für ein einzelnes Projekt beibehalten werden. Wenn Versionscleanup aktiviert ist, werden frühere Versionen, die diese Anzahl überschreiten, gelöscht.|  
|**OPERATION_CLEANUP_ENABLED**|Wenn der Wert `TRUE`ist, werden Vorgangsdetails und Vorgangsmeldungen, die älter als **RETENTION_WINDOW** (Tage) sind, aus dem Katalog gelöscht. Wenn der Wert `FALSE`ist, werden alle Vorgangsdetails und Vorgangsmeldungen im Katalog gespeichert. Hinweis: Das Vorgangscleanup erfolgt durch einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Auftrag.|  
|**RETENTION_WINDOW**|Die Anzahl der Tage, für die Vorgangsdetails und Vorgangsmeldungen im Katalog gespeichert werden. Wenn der Wert `-1`lautet, ist die Beibehaltungsdauer unendlich. Hinweis: Wenn kein Cleanup erfolgen soll, legen Sie **OPERATION_CLEANUP_ENABLED** auf **FALSE**fest.|
|**SCHEMA_BUILD**|Die Buildnummer des SSISDB-Katalogdatenbankschemas. Diese Nummer ändert sich, wenn Sie der SSISDB-Katalog erstellt oder aktualisiert wird.|
|**SCHEMA_VERSION**|Die Hauptversionsnummer des SSISDB-Katalogdatenbankschemas. Diese Nummer ändert sich, wenn Sie der SSISDB-Katalog erstellt oder ein Upgrade durchgeführt wird.|
|**VALIDATION_TIMEOUT**|Überprüfungen werden beendet, wenn sie nicht innerhalb der von dieser Eigenschaft angegebenen Anzahl von Sekunden abgeschlossen werden.|  
|**SERVER_CUSTOMIZED_LOGGING_LEVEL**|Der benutzerdefinierte Standardprotokolliergrad für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Server. Wenn Sie keine benutzerdefinierte Protokolliergrade erstellt haben, kann diese Eigenschaft nicht in der Sicht angezeigt werden.|
|**SERVER_LOGGING_LEVEL**|Der Standardprotokolliergrad für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Server.|
|**SERVER_OPERATION_ENCRYPTION_LEVEL**|Wenn der Wert „1“ (`PER_EXECUTION`) lautet, werden für jede *Ausführung* das Zertifikat und der symmetrische Schlüssel erstellt, die zum Schutz von sensiblen Ausführungsparameters und -protokollen verwendet werden. Wenn der Wert „2“ (`PER_PROJECT`) lautet, werden das Zertifikat und der symmetrische Schlüssel jeweils einmal für jedes *Projekt* erstellt. Weitere Informationen zu dieser Eigenschaft finden Sie unter den Hinweisen für die gespeicherte SSIS-Prozedur [catalog.cleanup_server_log](..\system-stored-procedures\catalog-cleanup-server-log.md#remarks).|
|**VERSION_CLEANUP_ENABLED**|Wenn der Wert `TRUE`ist, wird nur die von **MAX_PROJECT_VERSIONS** angegebene Anzahl von Projektversionen im Katalog gespeichert, und alle anderen Projektversionen werden gelöscht. Wenn der Wert **FALSE**ist, werden alle Projektversionen im Katalog gespeichert. Hinweis: Das Vorgangscleanup erfolgt durch einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Auftrag.|
|||
  
## <a name="permissions"></a>Berechtigungen  
 Diese Sicht erfordert eine der folgenden Berechtigungen:  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
  
