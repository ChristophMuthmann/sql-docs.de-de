---
title: dm_xe_objects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_xe_objects
- sys.dm_xe_objects
- sys.dm_xe_objects_TSQL
- dm_xe_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_objects dynamic management view
- extended events [SQL Server], views
ms.assetid: 5d944b99-b097-491b-8cbd-b0e42b459ec0
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f9f317555f992261eb76d65dae4e7d0e91163f71
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmxeobjects-transact-sql"></a>sys.dm_xe_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jedes Objekt zurück, das von einem Ereignispaket verfügbar gemacht wird. Folgende Objekte sind möglich:  
  
-   Ereignisse. Ereignisse geben interessierende Punkte in einem Ausführungspfad an. Alle Ereignisse enthalten Informationen über einen interessierenden Punkt.  
  
-   Aktionen Aktionen werden synchron ausgeführt, wenn Ereignisse ausgelöst werden. Eine Aktion kann Laufzeitdaten an ein Ereignis anfügen.  
  
-   Ziele. Ziele verarbeiten Ereignisse entweder synchron für den Thread, der das Ereignis ausgelöst wird, oder asynchron in einem vom System bereitgestellten Thread.  
  
-   Prädikate. Prädikatquellen rufen Werte aus Ereignisquellen zur Verwendung in Vergleichsvorgängen ab. Prädikatvergleiche vergleichen bestimmte Datentypen und geben einen booleschen Wert zurück.  
  
-   Typen. Typen kapseln die Länge und Eigenschaften der Byte-Auflistung, die zum Interpretieren der Daten benötigt wird.  

 |Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|name|**nvarchar(60)**|Der Name des Objekts. Der Name ist innerhalb eines Pakets für einen bestimmten Objekttyp eindeutig. Lässt keine NULL-Werte zu.|  
|object_type|**nvarchar(60)**|Der Typ des Objekts. Object_type ist eine der folgenden:<br /><br /> Ereignis<br /><br /> action<br /><br /> target<br /><br /> pred_source<br /><br /> pred_compare<br /><br /> Typ<br /><br /> Lässt keine NULL-Werte zu.|  
|package_guid|**uniqueidentifier**|Die GUID für das Paket, das diese Aktion verfügbar macht. Es gibt eine n:1-Beziehung mit sys.dm_xe_packages.package_id. Lässt keine NULL-Werte zu.|  
|description|**nvarchar(256)**|Eine Beschreibung der Aktion. Beschreibung wird vom Paketersteller festgelegt. Lässt keine NULL-Werte zu.|  
|capabilities|**int**|Eine Bitmap, die die Fähigkeiten des Objekts beschreibt. Lässt NULL-Werte zu.|  
|capabilities_desc|**nvarchar(256)**|Listet alle Fähigkeiten des Objekts auf. Lässt NULL-Werte zu.<br /><br /> **Funktionen, die für alle Objekttypen gelten**<br /><br /> —<br />                                **Private**. Das einzige für die interne Verwendung verfügbare Objekt. Der Zugriff auf das Objekt kann nicht über CREATE/ALTER EVENT SESSION DDL erfolgen. Überwachungsereignisse und Ziele gehören zu dieser Kategorie, zusätzlich zu einer kleinen Anzahl an intern verwendeten Objekten.<br /><br /> ===============<br /><br /> **Ereignisfunktionen**<br /><br /> —<br />                                **No_block**. Das Ereignis ist in einem wichtigen Codepfad, der aus keinem Grund blockieren kann. Ereignisse mit dieser Funktion werden möglicherweise keiner Ereignissitzung hinzugefügt, die NO_EVENT_LOSS angibt.<br /><br /> ===============<br /><br /> **Funktionen, die für alle Objekttypen gelten**<br /><br /> —<br />                                **Process_whole_buffers**. Das Ziel verwendet jeweils Ereignispuffer, anstelle von Ereignis zu Ereignis vorzugehen.<br /><br /> —<br />                        **Singleton**. Nur eine Instanz des Ziels kann in einem Prozess vorhanden sein. Obwohl mehrere Ereignissitzungen auf dasselbe Singletonziel verweisen können, ist jedoch nur eine einzige Instanz vorhanden. Für diese Instanz wird jedes eindeutige Ereignis nur einmal angegeben. Dies ist wichtig, wenn das Ziel mehreren Sitzungen hinzugefügt wird, die dasselbe Ereignis erfassen.<br /><br /> —<br />                                **Synchronous**. Das Ziel wird auf dem Thread ausgeführt, der das Ereignis erzeugt, bevor die Steuerung an die aufrufende Codezeile zurückgegeben wird.|  
|type_name|**nvarchar(60)**|Der Name für das pred_source-Objekt und das pred_compare-Objekt. Lässt NULL-Werte zu.|  
|type_package_guid|**uniqueidentifier**|Die GUID für das Paket, das den Typ verfügbar, dem macht für dieses Objekt ausgeführt wird. Lässt NULL-Werte zu.|  
|type_size|**int**|Größe des Datentyps in Bytes. Dies ist nur für gültige Objekttypen vorgesehen. Lässt NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
### <a name="relationship-cardinalities"></a>Kardinalität der Beziehungen  
  
|Von|Aktion|Beziehung|  
|----------|--------|------------------|  
|sys.dm_xe_objects.package_guid|sys.dm_xe_packages.guid|n:1|  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

