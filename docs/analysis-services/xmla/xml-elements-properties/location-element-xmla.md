---
title: Location-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Location Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.location
- urn:schemas-microsoft-com:xml-analysis#Location
- http://schemas.microsoft.com/analysisservices/2003/engine#Location
helpviewer_keywords: Location element
ms.assetid: cea5e776-f435-425a-9bce-812d727a2b71
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 64566e83f9da6579800809d40395a7fe31db36ee
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="location-element-xmla"></a>Location-Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Enthält Informationen über einen Remoteserver für den übergeordneten [Sicherung](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [wiederherstellen](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md), oder [Synchronize](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) Befehl.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Backup> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Location>  
```  
  
```  
  
<File>...</File> <!-- for Backup and Restore only -->  
<DataSourceID>...</DataSourceID>  
<DataSourceType>...</DataSourceType> <!-- for Restore and Synchronize only -->  
<ConnectionString>...</ConnectionString> <!-- for Restore and Synchronize only -->  
<Folders>...</Folders> <!-- for Restore and Synchronize only -->  
```  
  
```  
  
   </Location>  
   ...  
</Backup>  
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
|Übergeordnete Elemente|[Sicherung](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [wiederherstellen](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md), [synchronisieren](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|  
|Untergeordnete Elemente|Finden Sie in der folgenden Tabelle aus.|  
  
|Vorgänger oder übergeordnetes Element|Untergeordnetes Element|  
|------------------------|-------------------|  
|[Sicherung](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)|[DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md), [Datei](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md)|  
|[Wiederherstellen](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|["ConnectionString"](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md), [DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md), [DataSourceType](../../../analysis-services/xmla/xml-elements-properties/datasourcetype-element-xmla.md), [Datei](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md), [Ordner](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
|[Synchronisieren](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|["ConnectionString"](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md), [DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md), [DataSourceType](../../../analysis-services/xmla/xml-elements-properties/datasourcetype-element-xmla.md), [Ordner](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
  
## <a name="remarks"></a>Hinweise  
 Für **Backup** Befehle, die **Speicherort** Element enthält Informationen zum Erstellen einer remotesicherungsdatei für eine Remoteinstanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Für **wiederherstellen** Befehle, die **Speicherort** Element enthält Informationen über die Identifizierung und Verbindung mit einer [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz sowie die remotesicherungsdatei, remote wiederherstellen Partitionen, die auf dieser Remoteinstanz.  
  
 Bei **Synchronize** -Befehlen beschreibt das **Location** -Element entweder eine Datenquelle, die von der Zielinstanz verwendet wird, oder eine Remoteinstanz, die auf der Zielinstanz definiert wird und mit der Zielinstanz synchronisiert werden muss. Letzteres ist abhängig vom Wert des **DataSourceType** -Elements des übergeordneten **Synchronize** -Befehls.  
  
 Weitere Informationen zum Sichern und Wiederherstellen von Remoteinstanzen finden Sie unter [Backing Up and Restoring Objects (XMLA)](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Siehe auch  
 [BackupRemotePartitions-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/backupremotepartitions-element-xmla.md)   
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
