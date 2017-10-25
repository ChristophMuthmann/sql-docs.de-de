---
title: Backup-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Backup Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Backup
- http://schemas.microsoft.com/analysisservices/2003/engine#Backup
- microsoft.xml.analysis.backup
helpviewer_keywords:
- Backup command
ms.assetid: 5bcbc14c-9db9-45b2-99de-f3a265bcb0c4
caps.latest.revision: 19
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c5617d1b0b62eabb945881041a795a1a699b4c41
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="backup-element-xmla"></a>Backup-Element (XMLA)
  Sichert eine [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Datenbank in einer Sicherungsdatei.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Command>  
   <Backup>  
      <Object>...</Object>  
      <File>...</File>  
      <Security>...</Security>  
      <ApplyCompression>...</ApplyCompression>  
      <AllowOverwrite>...</AllowOverwrite>  
      <Password>...</Password>  
      <BackupRemotePartitions>...</BackupRemotePartitions>  
      <Locations>...</Locations>  
   </Backup>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Befehl](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Untergeordnete Elemente|[AllowOverwrite](../../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md), [ApplyCompression](../../../analysis-services/xmla/xml-elements-properties/applycompression-element-xmla.md), [BackupRemotePartitions](../../../analysis-services/xmla/xml-elements-properties/backupremotepartitions-element-xmla.md), [Datei](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md), [Speicherorte](../../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md), [Objekt](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md), [Kennwort](../../../analysis-services/xmla/xml-elements-properties/password-element-xmla.md), [Sicherheit](../../../analysis-services/xmla/xml-elements-properties/security-element-xmla.md)|  
  
## <a name="remarks"></a>Hinweise  
 Die **Backup** Befehl sichert die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Datenbank in der [Objekt](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) Element, um eine Sicherungsdatei und optional sichert der Remotepartitionen in remotesicherungsdateien. Wenn die **Objekt** Element verweist auf ein Objekt als eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Datenbank, ein Fehler auftritt.  
  
 Welche Informationen mithilfe des **Backup** -Befehls gesichert werden, hängt vom von Objekten in der Datenbank verwendeten Speichermodus ab. In der folgenden Tabelle werden die Informationen dargestellt, die basierend auf dem verwendeten Speichermodus gesichert werden.  
  
|Speichermodus|Informationen, die gesichert werden|  
|------------------|-----------------------------------|  
|Mehrdimensionale OLAP (MOLAP)|Quelldaten, Aggregationen und Metadaten|  
|Hybride OLAP (HOLAP)|Aggregationen und Metadaten|  
|Relationale OLAP (ROLAP)|Metadaten|  
  
 Während einer **Sicherung** Befehl, eine gemeinsame Sperre befindet sich auf die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Datenbank in der **Objekt** Element. Die freigegebene Sperre wird nach Abschluss des **Backup** -Befehls wieder aufgehoben.  
  
 Mehrere **Sicherung** -Befehle können gleichzeitig ausgeführt werden, wenn die Befehle, in enthalten sind der [parallele](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md) Auflistung von einer [Batch](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) Befehl. Mihilfe der **Parallel** -Auflistung kann eine Datenbank in mehreren Sicherungsdateien gleichzeitig gesichert werden.  
  
 Weitere Informationen zum Sichern und Wiederherstellen von Datenbanken finden Sie unter [sichern, wiederherstellen, und Synchronisieren von Datenbanken &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
> [!IMPORTANT]  
>  Für jede Sicherungsdatei muss der Benutzer, der den Sicherungsbefehl ausführt, über die Berechtigung zum Schreiben in den für jede Datei angegebenen Sicherungsspeicherort verfügen. Dem Benutzer muss zudem eine der folgenden Rollen zugewiesen worden sein: Mitglied einer Serverrolle für die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Instanz oder Mitglied einer Datenbankrolle mit der Berechtigung „Vollzugriff“ (Administrator) für die wiederherzustellende Datenbank.  
  
## <a name="see-also"></a>Siehe auch  
 [Restore-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [Synchronisieren Sie-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [Befehle &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  

