---
title: Sysdac_history_internal (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysdac_history_internal
- sysdac_history_internal_TSQL
dev_langs: TSQL
helpviewer_keywords: sysdac_history_internal
ms.assetid: 774a1678-0b27-42be-8adc-a6d7a4a56510
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 55bf1ae9625c5b27c7078bbba61704eef195b0ca
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="data-tier-application-tables---sysdachistoryinternal"></a>Data-Tier-Anwendungstabellen - sysdac_history_internal
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält Informationen zu den Maßnahmen, die zur Verwaltung von Datenebenenanwendungen (DAC) ausgeführt werden. Diese Tabelle wird gespeichert, der **Dbo** Schema der **Msdb** Datenbank.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**action_id**|**int**|Bezeichner der Aktion|  
|**sequence_id**|**int**|Identifiziert einen Schritt innerhalb einer Aktion.|  
|**"instance_id"**|**uniqueidentifier**|Der Bezeichner der DAC-Instanz. Diese Spalte kann verknüpft werden, auf die **"instance_id"** Spalte [dbo.sysdac_instances &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md).|  
|**action_type**|**tinyint**|Bezeichner des Aktionstyps:<br /><br /> **0** = bereitstellen<br /><br /> **1** = erstellen<br /><br /> **2** = umbenennen<br /><br /> **3** = trennen<br /><br /> **4** = löschen|  
|**action_type_name**|**h. varchar(19)**|Name des Aktionstyps:<br /><br /> **Bereitstellen**<br /><br /> **Erstellen**<br /><br /> **Umbenennen**<br /><br /> **Trennen**<br /><br /> **Löschen**|  
|**dac_object_type**|**tinyint**|Bezeichner des Typs des von der Aktion betroffenen Objekts:<br /><br /> **0** = DACPAC-Datei<br /><br /> **1** = Anmeldename<br /><br /> **2** = Datenbank|  
|**dac_object_type_name**|**varchar(8)**|Name des Typs des von der Aktion betroffenen Objekts:<br /><br /> **DACPAC-Datei** = DAC-Instanz<br /><br /> **Anmeldung**<br /><br /> **database**|  
|**action_status**|**tinyint**|Code, der den aktuellen Status der Aktion identifiziert:<br /><br /> **0** = ausstehend<br /><br /> **1** = Erfolg<br /><br /> **2** = Fehler|  
|**action_status_name**|**varchar(11)**|Aktueller Status der Aktion:<br /><br /> **Ausstehend**<br /><br /> **Erfolg**<br /><br /> **Fehler**|  
|**Erforderlich**|**bit**|Wird von [!INCLUDE[ssDE](../../includes/ssde-md.md)] verwendet, wenn das Rollback eines DAC-Vorgangs ausgeführt wird.|  
|**dac_object_name_pretran**|**sysname**|Name des Objekts, bevor ein Commit für die Transaktion ausgeführt wird, in der die Aktion enthalten ist. Wird nur für Datenbanken und Anmeldenamen verwendet.|  
|**dac_object_name_posttran**|**sysname**|Name des Objekts, nachdem ein Commit für die Transaktion ausgeführt wurde, in der die Aktion enthalten ist. Wird nur für Datenbanken und Anmeldenamen verwendet.|  
|**in SqlScript**|**nvarchar(max)**|[!INCLUDE[tsql](../../includes/tsql-md.md)]-Skript, das eine Aktion für eine Datenbank oder einen Anmeldenamen implementiert.|  
|**Nutzlast**|**varbinary(max)**|DAC-Paketdefinition, die in einer binären codierten Zeichenfolge gespeichert ist.|  
|**Kommentare**|**varchar(max)**|Zeichnet die Anmeldung eines Benutzers auf, der potenziellen Datenverlust in einem DAC-Upgrade als akzeptabel angegeben hat.|  
|**error_string**|**nvarchar(max)**|Fehlermeldung, die im Fall eines Fehler generiert wird.|  
|**created_by**|**sysname**|Der Anmeldename, unter dem die Aktion, die diesen Eintrag erstellt hat, gestartet wurde.|  
|**date_created**|**datetime**|Datum und Uhrzeit, zu denen dieser Eintrag erstellt wurde.|  
|**DATE_MODIFIED**|**datetime**|Datum und Uhrzeit, zu denen der Eintrag zuletzt geändert wurde.|  
  
## <a name="remarks"></a>Hinweise  
 Durch DAC-Verwaltungsaktionen, z. B. das Bereitstellen oder Löschen einer DAC, werden mehrere Schritte generiert. Jeder Aktion wird ein Aktionsbezeichner zugewiesen. Jeder Schritt wird zugewiesen, eine Sequenznummer und eine Zeile in **Sysdac_history_internal**, in dem der Status des Schritts aufgezeichnet wird. Die einzelnen Zeilen werden mit Beginn des Aktionsschritts erstellt und bei Bedarf aktualisiert, um dem Status des Vorgangs zu entsprechen. Angenommen, eine DAC-Bereitstellungsaktion konnte zugewiesen werden, **Action_id** 12 und vier Zeilen **Sysdac_history_internal**:  
  
|||||  
|-|-|-|-|  
|**action_id**|**sequence_id**|**action_type_name**|**dac_object_type_name**|  
|12|0|Erstellen|dacpac|  
|12|1|Erstellen|login|  
|12|2|Erstellen|database|  
|12|3|Umbenennen|database|  
  
 DAC-Vorgänge, z. B. löschen, entfernen Sie Zeilen aus nicht **Sysdac_history_internal**. Sie können die Zeilen für DACs, die nicht mehr in einer Instanz des [!INCLUDE[ssDE](../../includes/ssde-md.md)]s bereitgestellt werden, mithilfe der folgenden Abfrage manuell löschen:  
  
```tsql  
DELETE FROM msdb.dbo.sysdac_history_internal  
WHERE instance_id NOT IN  
   (SELECT instance_id  
    FROM msdb.dbo.sysdac_instances_internal);  
```  
  
 Das Löschen von Zeilen für aktive DACs hat keinen Einfluss auf DAC-Vorgänge. Die einzige Auswirkung besteht darin, dass nicht der vollständige Verlauf für die DAC gemeldet werden kann.  
  
> [!NOTE]  
>  Es gibt derzeit keinen Mechanismus für das Löschen von **Sysdac_history_internal** Zeilen [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle sysadmin. Nur-Lese Zugriff auf diese Sicht ist für alle Benutzer mit Berechtigungen zum Verbinden mit der master-Datenbank verfügbar.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenebenenanwendungen](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [dbo.sysdac_instances &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md)   
 ["sysdac_instances_internal" &#40; Transact-SQL &#41;](../../relational-databases/system-tables/data-tier-application-tables-sysdac-instances-internal.md)  
  
  
