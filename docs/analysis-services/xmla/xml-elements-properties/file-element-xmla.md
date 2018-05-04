---
title: Datei-Element (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- File Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.file
- http://schemas.microsoft.com/analysisservices/2003/engine#File
- urn:schemas-microsoft-com:xml-analysis#File
helpviewer_keywords:
- File element
ms.assetid: 3dfd0e9b-746b-4ce5-8a95-610d2e573739
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 71d074a7f63333ed504b5e0832cb190d885bbf0c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="file-element-xmla"></a>File-Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Identifiziert eine Datei, die vom übergeordneten [Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) - oder [Restore](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) -Befehl oder vom übergeordneten [Location](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md) -Element verwendet werden soll.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Backup> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <File>...</File>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|String|  
|Standardwert|Keine|  
|Kardinalität|1-1: Erforderliches Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [Location](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md), [Restore](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Das **File** -Element enthält einen UNC-Dateinamen, und das übergeordnete Element bestimmt die Verwendung des **File** -Elements.  
  
 Bei **Backup** -Befehlen bestimmt das **File** -Element den Namen der vom **Backup** -Befehl erstellten Sicherungsdatei. Wenn kein Pfad als Teil des Dateinamens angegeben ist, wird der Pfad angegeben, der **BackupDir** Konfigurationseigenschaft für die Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] verwendet wird. Wenn die angegebene Datei bereits vorhanden ist, tritt ein Fehler auf, es sei denn, das **AllowOverwrite** -Element des übergeordneten **Backup** -Befehls ist auf **True**gesetzt.  
  
 Für **Restore** -Befehle bestimmt das **File** -Element den Namen der vom **Restore** -Befehl wiederherzustellenden Sicherungsdatei.  
  
 Für **Speicherort** Elemente, die **Datei** -Element beschreibt eine remotesicherungsdatei für eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Instanz, die Remotepartitionen enthält. Weitere Informationen zum Sichern und Wiederherstellen von Remotepartitionen finden Sie unter [sichern, wiederherstellen, und Synchronisieren von Datenbanken & #40; XMLA & #41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Siehe auch  
 [AllowOverwrite-Element & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md)   
 [Datenbankeigenschaften & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
