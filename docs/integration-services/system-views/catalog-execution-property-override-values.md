---
title: catalog.execution_property_override_values | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 83cbdd6f-ddde-47bf-abde-36bd24272621
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 138938f3ae015675c7815416dc2b17bcdc5988f4
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="catalogexecutionpropertyoverridevalues"></a>catalog.execution_property_override_values
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt die Eigenschaftenüberschreibungswerte an, die während der Ausführung des Pakets festgelegt wurden.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|property_id|**bigint**|Eindeutige ID für den Eigenschaftenüberschreibungswert.|  
|execution_id|**bigint**|Eindeutige ID für die Instanz der Ausführung.|  
|property_path|**nvarchar(4000)**|Der Pfad zur Eigenschaft im Paket.|  
|property_value|**nvarchar(max)**|Der Überschreibungswert der Eigenschaft.|  
|sensitive|**bit**|Wenn der Wert 1 lautet, ist die Eigenschaft vertraulich und wird beim Speichern verschlüsselt. Lautet der Wert 0, ist die Eigenschaft nicht vertraulich, und der Wert wird als Nur-Text gespeichert.|  
  
## <a name="remarks"></a>Hinweise  
 In dieser Sicht wird eine Zeile zu jeder Ausführung angezeigt, in der Eigenschaftswerte mit dem Abschnitt **Eigenschaftenüberschreibungen** auf der Registerkarte **Erweitert** des Dialogfelds **Paket ausführen** überschrieben wurden. Der Pfad zur Eigenschaft wird von der Eigenschaft **Paketpfad** des Pakettasks abgeleitet.  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Sicht erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung für die Instanz der Ausführung  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
> [!NOTE]  
>  Wenn Sie über die Berechtigung verfügen, einen Vorgang auf dem Server auszuführen, verfügen Sie auch über die Berechtigung, Informationen zu dem Vorgang anzuzeigen. Sicherheit auf Zeilenebene wird erzwungen. Es werden nur Zeilen angezeigt, zu deren Anzeige Sie berechtigt sind.  
  
  
