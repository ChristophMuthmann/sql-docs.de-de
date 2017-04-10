---
title: "Benutzerdefinierte Eigenschaften des Ziels des Data Mining-Modelltrainings | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f0a70216-fdac-44ae-af29-35f65626217c
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# Benutzerdefinierte Eigenschaften des Ziels des Data Mining-Modelltrainings
  Das Ziel des Data Mining-Modelltrainings verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften des Ziels des Data Mining-Modelltrainings. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaft|Datentyp|Description|  
|--------------|---------------|-----------------|  
|ASConnectionId|String|Der eindeutige Bezeichner des Verbindungs-Managers.|  
|ASConnectionString|String|Die Verbindungszeichenfolge zu einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oder einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt.|  
|ObjectRef|String|Ein XML-Tag, das die Data Mining-Struktur identifiziert, die von der Transformation verwendet wird.|  
  
 Die Eingabe und die Eingabespalten des Ziels des Data Mining-Modelltrainings verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [Data Mining Model Training Destination](../../integration-services/data-flow/data-mining-model-training-destination.md).  
  
## Siehe auch  
 [Allgemeine Eigenschaften](../Topic/Common%20Properties.md)  
  
  