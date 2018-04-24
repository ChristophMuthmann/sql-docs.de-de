---
title: FileTable-Schema | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: blob
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-blob
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- FileTables [SQL Server], table schema
ms.assetid: e1cb3880-cfda-40ac-91fc-d08998287f44
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 117a9e10a07960bc50968d3141e9f5e0294cb7de
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="filetable-schema"></a>FileTable-Schema
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Beschreibt das vordefinierte und feste Schema einer FileTable.  
  
|Name des Dateiattributs|Typ|Größe|Default|Description|Barrierefreiheit für das Dateisystem|  
|-------------------------|----------|----------|-------------|-----------------|-------------------------------|  
|**path_locator**|**hierarchyid**|variable|Ein **hierarchyid** , der die Position dieses Elements identifiziert.|Die Position dieses Knotens im hierarchischen FileNamespace.<br /><br /> Primärschlüssel für die Tabelle.|Kann durch Festlegen der Windows-Pfadwerte erstellt und geändert werden.|  
|**stream_id**|**[uniqueidentifier] rowguidcol**||Ein von der **NEWID()** -Funktion zurückgegebener Wert.|Eine eindeutige ID für die FILESTREAM-Daten.|Nicht verfügbar.|  
|**file_stream**|**varbinary(max)**<br /><br /> **Filestream**|variable|NULL|Enthält die FILESTREAM-Daten.|Nicht verfügbar.|  
|**file_type**|**nvarchar(255)**|variable|NULL.<br /><br /> Durch einen Erstellungs- bzw. Umbenennungsvorgang im Dateisystem wird der Dateierweiterungswert aus dem Namen übernommen.|Stellt den Typ der Datei dar.<br /><br /> Diese Spalte kann als **TYPE COLUMN** verwendet werden, wenn Sie einen Volltextindex erstellen.<br /><br /> **file_type** ist eine persistente berechnete Spalte.|Automatisch berechnet. Kann nicht festgelegt werden.|  
|**Name**|**nvarchar(255)**|variable|GUID-Wert.|Der Datei- oder Verzeichnisname.|Kann mit Windows-APIs erstellt oder geändert werden.|  
|**parent_path_locator**|**hierarchyid**|variable|Ein **hierarchyid** , der das Verzeichnis identifiziert, das dieses Element enthält.|Der **hierarchyid** des enthaltenden Verzeichnisses.<br /><br /> **parent_path_locator** ist eine persistente berechnete Spalte.|Automatisch berechnet. Kann nicht festgelegt werden.|  
|**cached_file_size**|**bigint**|||Die Größe der FILESTREAM-Daten in Byte.<br /><br /> **cached_file_size** ist eine persistente berechnete Spalte.|Obwohl die zwischengespeicherte Dateigröße automatisch auf dem aktuellen Stand gehalten wird, kann sie unter außergewöhnlichen Umständen möglicherweise nicht synchronisiert sein. Verwenden Sie die **DATALENGTH()** -Funktion, um die genaue Größe zu berechnen.|  
|**creation_time**|**datetime2(4)**<br /><br /> **nicht NULL**|8 Byte|Aktuelle Zeit.|Datum und Uhrzeit der Erstellung der Datei.|Automatisch berechnet. Kann auch mit Windows-APIs festgelegt werden.|  
|**last_write_time**|**datetime2(4)**<br /><br /> **nicht NULL**|8 Byte|Aktuelle Zeit.|Datum und Uhrzeit des letzten Updates der Datei.|Automatisch berechnet. Kann auch mit Windows-APIs festgelegt werden.|  
|**last_access_time**|**datetime2(4)**<br /><br /> **nicht NULL**|8 Byte|Aktuelle Zeit.|Datum und Uhrzeit des letzten Zugriffs auf die Datei.|Automatisch berechnet. Kann auch mit Windows-APIs festgelegt werden.|  
|**is_directory**|**bit**<br /><br /> **nicht NULL**|1 Byte|FALSE|Gibt an, ob die Zeile ein Verzeichnis darstellt. Dieser Wert wird automatisch berechnet und kann nicht festgelegt werden.|Automatisch berechnet. Kann nicht festgelegt werden.|  
|**is_offline**|**bit**<br /><br /> **nicht NULL**|1 Byte|FALSE|Attribut für Offlinedatei.|Automatisch berechnet. Kann auch mit Windows-APIs festgelegt werden.|  
|**is_hidden**|**bit**<br /><br /> **nicht NULL**|1 Byte|FALSE|Attribut für ausgeblendete Datei.|Automatisch berechnet. Kann auch mit Windows-APIs festgelegt werden.|  
|**is_readonly**|**bit**<br /><br /> **nicht NULL**|1 Byte|FALSE|Attribut für schreibgeschützte Datei.|Automatisch berechnet. Kann auch mit Windows-APIs festgelegt werden.|  
|**is_archive**|**bit**<br /><br /> **nicht NULL**|1 Byte|FALSE|Archivattribut.|Automatisch berechnet. Kann auch mit Windows-APIs festgelegt werden.|  
|**is_system**|**bit**<br /><br /> **nicht NULL**|1 Byte|FALSE|Attribut für Systemdatei.|Automatisch berechnet. Kann auch mit Windows-APIs festgelegt werden.|  
|**is_temporary**|**bit**<br /><br /> **nicht NULL**|1 Byte|FALSE|Attribut für temporäre Datei.|Automatisch berechnet. Kann auch mit Windows-APIs festgelegt werden.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen, Ändern und Löschen von FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)  
  
  
