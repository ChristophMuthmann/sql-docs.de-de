---
title: catalog.get_parameter_values (SSISDB-Datenbank) | Microsoft-Dokumentation
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
ms.assetid: 5b1aeaf7-c938-4aef-bafc-e4d7a82eb578
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7fcb3ffcdd35f2b526f1e84ce36c206919e8eb74
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="cataloggetparametervalues-ssisdb-database"></a>catalog.get_parameter_values (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Ermittelt die Standardparameterwerte und ruft diese aus einem Projekt und den entsprechenden Paketen im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog ab.  
  
## <a name="syntax"></a>Syntax  
  
```sql  
catalog.get_parameter_values [ @folder_name = ] folder_name  
     , [ @project_name = ] project_name  
     , [ @package_name = ] package_name  
  [  , [ @reference_id = ] reference_id  ]  
  
```  
  
## <a name="arguments"></a>Argumente  
 [ @folder_name = ] *folder_name*  
 Der Name des Ordners, der das Projekt enthält. Der *folder_name* ist **nvarchar(128)**.  
  
 [ @project_name = ] *project_name*  
 Der Name des Projekts, in dem sich die Parameter befinden. Der *project_name* ist **nvarchar(128)**.  
  
 [ @package_name = ] *package_name*  
 Der Name des Pakets. Geben Sie den Paketnamen an, um alle Projektparameter und die Parameter aus einem bestimmten Paket abzurufen. Verwenden Sie NULL, um alle Projektparameter und die Parameter aus allen Paketen abzurufen. Der *package_name* ist **nvarchar(260)**.  
  
 [ @reference_id = ] *reference_id*  
 Der eindeutige Bezeichner eines Umgebungsverweises. Dieser Parameter ist optional. Der *reference_id* ist **bigint**.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 0 (Erfolg)  
  
## <a name="result-sets"></a>Resultsets  
 Gibt eine Tabelle zurück, die das folgende Format aufweist:  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|object_type|**smallint**|Der Typ des Parameters. Für einen Projektparameter ist der Wert `20` , und für einen Paketparameter ist der Wert `30` .|  
|parameter_data_type|**nvarchar(128)**|Der Datentyp des Parameters.|  
|parameter_name|**sysname**|Der Name des Parameters.|  
|parameter_value|**sql_variant**|Der Wert des Parameters.|  
|sensitive|**bit**|Wenn der Wert `1`lautet, ist der Parameterwert vertraulich. Wenn der Wert `0`lautet, ist der Parameterwert nicht vertraulich.|  
|erforderlich|**bit**|Wenn der Wert `1`lautet, ist der Parameterwert erforderlich, um die Ausführung zu starten. Wenn der Wert `0`lautet, ist der Parameterwert nicht erforderlich, um die Ausführung zu starten.|  
|value_set|**bit**|Wenn der Wert `1`ist, wurde der Parameterwert zugewiesen. Wenn der Wert `0`ist, wurde der Parameterwert nicht zugewiesen.|  
  
> [!NOTE]  
>  Literalwerte werden als Nur-Text angezeigt. Anstelle vertraulicher Werte wird**NULL** angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Diese gespeicherte Prozedur erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigungen für das Projekt und ggf. READ-Berechtigung für die Umgebung, auf die verwiesen wird  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
## <a name="errors-and-warnings"></a>Fehler und Warnungen  
 In der folgenden Liste werden einige Bedingungen beschrieben, die möglicherweise einen Fehler oder eine Warnung auslösen:  
  
-   Das Paket kann im angegebenen Ordner oder Projekt nicht gefunden werden.  
  
-   Der Benutzer verfügt nicht über die entsprechenden Berechtigungen.  
  
-   Der angegebene Umgebungsverweis ist nicht vorhanden.  
  
  
