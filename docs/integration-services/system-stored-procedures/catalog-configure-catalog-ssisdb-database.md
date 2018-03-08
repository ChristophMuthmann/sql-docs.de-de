---
title: catalog.configure_catalog (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 72690c61-f462-4c25-9fce-08a687b0bd41
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6d1f8926d398a90214a5ad1903f04ac1e29d8854
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="catalogconfigurecatalog-ssisdb-database"></a>catalog.configure_catalog (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Konfiguriert den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog durch das Festlegen einer Katalogeigenschaft auf einen angegebenen Wert.  
  
## <a name="syntax"></a>Syntax  
  
```sql
catalog.configure_catalog [ @property_name = ] property_name , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>Argumente  
 [ @property_name = ] *property_name*  
 Der Name der Katalogeigenschaft. Das Argument *property_name* ist vom Typ **nvarchar(255)**. Weitere Informationen zu verfügbaren Eigenschaften siehe [catalog.catalog_properties &#40;SSISDB Database&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) (catalog.catalog_properties &#40;SSISDB-Datenbank&#41;).  
  
 [ @property_value = ] *property_value*  
 Der Wert der Katalogeigenschaft. Das Argument *property_value* ist vom Typ **nvarchar(255)**. Weitere Informationen zu Eigenschaftswerten siehe [catalog.catalog_properties &#40;SSISDB Database&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) (catalog.catalog_properties &#40;SSISDB-Datenbank&#41;).  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>Remarks  
 Diese gespeicherte Prozedur bestimmt, ob der *property_value* für jeden *property_name* gültig ist.  
  
 Diese gespeicherte Prozedur kann nur ausgeführt werden, wenn keine aktiven Ausführungen, z. B. ausstehende, in der Warteschlange stehende, in Ausführung befindliche oder angehaltene Ausführungen, vorhanden sind.  
  
 Während der Katalog konfiguriert wird, wird bei dem Versuch, andere im Katalog gespeicherte Prozeduren auszuführen, die Fehlermeldung „Server wird gerade konfiguriert“ angezeigt.
  
 Wenn der Katalog konfiguriert ist, wird ein Eintrag in das Vorgangsprotokoll geschrieben.  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden einige Bedingungen beschrieben, die möglicherweise einen Fehler oder eine Warnung auslösen:  
  
-   Die Eigenschaft ist nicht vorhanden.  
  
-   Der Eigenschaftswert ist ungültig.  
  
  
