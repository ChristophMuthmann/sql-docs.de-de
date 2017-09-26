---
title: Catalog. operation_messages (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- catalog.operation_messages view [Integration Services]
- operation_messages view [Integration Services]
ms.assetid: 0b3cbe38-ce24-47ca-83ef-6538a5299d1a
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 235e9896cbf075bdc26e3df120b23091b8e82d6d
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogoperationmessages-ssisdb-database"></a>catalog.operation_messages (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt Meldungen an, die während der Vorgänge im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog protokolliert werden.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|operation_message_id|**bigint**|Der eindeutige Bezeichner (ID) der Meldung.|  
|operation_id|**bigint**|Die eindeutige ID des Vorgangs.|  
|message_time|**DateTimeOffset(7)**|Zeitpunkt, zu dem die Meldung erstellt wurde.|  
|message_type|**smallint**|Typ der angezeigten Meldung.|  
|message_source_type|**smallint**|Die ID des Typs der Nachrichtenquelle.|  
|message|**nvarchar(max)**|Der Text der Meldung.|  
|extended_info_id|**bigint**|Die ID der zusätzliche Informationen, die auf die vorgangsmeldung beziehen gefunden wird, der [Extended_operation_info](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md) anzeigen.|  
  
## <a name="remarks"></a>Hinweise  
 In dieser Sicht wird eine Zeile für jede Meldung angezeigt, die während eines Vorgangs im Katalog protokolliert wird. Die Meldung kann durch den Server, den Paketausführungsprozess oder das Ausführungsmodul generiert werden.  
  
 In dieser Sicht werden die folgenden Meldungstypen angezeigt:  
  
|**Message_type** Wert|Description|  
|-----------------------------|-----------------|  
|-1|Unknown|  
|120|Fehler|  
|110|Warnung|  
|70|Informationen|  
|10|Vor der Überprüfung|  
|20|Nach der Überprüfung|  
|30|Vor der Ausführung|  
|40|Nach der Ausführung|  
|60|Status|  
|50|StatusChange|  
|100|QueryCancel|  
|130|TaskFailed|  
|90|Diagnostic|  
|200|Benutzerdefiniert|  
|140|DiagnosticEx<br /><br /> Jedes Mal, wenn der Task "Paket ausführen" ein untergeordnetes Paket ausführt, wird dieses Ereignis protokolliert. Die Ereignismeldung besteht aus den Parameterwerten, die an untergeordnete Pakete übergeben wurden.<br /><br /> Der Wert der Meldungsspalte für DiagnosticEx ist XML-Text.|  
|400|NonDiagnostic|  
|80|VariableValueChanged|  
  
 In dieser Sicht werden die folgenden Meldungsquelltypen angezeigt:  
  
|**message_source_type**|Description|  
|-------------------------------|-----------------|  
|10|Eintrag-APIs, z. B. T-SQL und gespeicherte CLR-Prozeduren|  
|20|Externer Prozess, der verwendet wurde, um das Paket (ISServerExec.exe) auszuführen|  
|30|Objekte auf Paketebene|  
|40|Ablaufsteuerungsaufgaben|  
|50|Ablaufsteuerungscontainer|  
|60|Datenflusstask|  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Sicht erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung für den Vorgang  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
> [!NOTE]  
>  Wenn Sie über die Berechtigung verfügen, einen Vorgang auf dem Server auszuführen, verfügen Sie auch über die Berechtigung, Informationen zu dem Vorgang anzuzeigen. Sicherheit auf Zeilenebene wird erzwungen. Es werden nur Zeilen angezeigt, zu deren Anzeige Sie berechtigt sind.  
  
  
