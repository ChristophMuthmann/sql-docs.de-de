---
title: "Datenbankspeicherort | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datenbanken [Analysis Services], Speicherort"
ms.assetid: cf88c62e-581e-42f2-846f-a9bf1d7c3292
caps.latest.revision: 18
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 18
---
# Datenbankspeicherort
  Es gibt oftmals Situationen, in denen ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Datenbankadministrator (DBA) eine bestimmte Datenbank außerhalb des Datenordners des Servers speichern möchte. Diese Situationen werden oft von Unternehmensanforderungen bestimmt, wie Verbesserung der Leistung oder Erweiterung des Speichers. In solchen Fällen ermöglicht die **DbStorageLocation**-Datenbankeigenschaft dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Datenbankadministrator, für den Datenbankspeicherort einen lokalen Datenträger oder ein Netzwerkgerät anzugeben.  
  
## DbStorageLocation-Datenbankeigenschaft  
 Die **DbStorageLocation**-Datenbankeigenschaft gibt den Ordner an, in dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] alle Datenbankdaten und Metadatendateien erstellt und verwaltet. Alle Metadatendateien werden im **DbStorageLocation** -Ordner gespeichert, mit Ausnahme der Datenbank-Metadatendatei. Diese wird im Datenordner des Servers abgelegt. Es gibt zwei wichtige Überlegungen beim Festlegen des Werts der **DbStorageLocation** -Datenbankeigenschaft:  
  
-   Die **DbStorageLocation** -Datenbankeigenschaft muss auf einen vorhandenen UNC-Ordnerpfad oder eine leere Zeichenfolge festgelegt werden. Bei dem vorgegebenen Datenordner des Servers handelt es sich um eine leere Zeichenfolge. Wenn dieser Ordner nicht vorhanden ist, wird beim Ausführen des Befehls **Create**, **Attach**oder **Alter** ein Fehler ausgelöst.  
  
-   Darüber hinaus kann die **DbStorageLocation** -Datenbankeigenschaft nicht so festgelegt werden, dass sie auf den Datenordner des Servers oder einen zugehörigen Unterordner verweist. Wenn der Speicherort auf den Datenordner des Servers oder einen zugehörigen Unterordner verweist, wird beim Ausführen des Befehls **Create**, **Attach**oder **Alter** ein Fehler ausgelöst.  
  
> [!IMPORTANT]  
>  Es wird empfohlen, den UNC-Pfad auf die Verwendung eines Storage Area Networks (SAN), iSCSI-basierten Netzwerks oder eines lokalen Datenträgers festzulegen. Jeder UNC-Pfad zu einer Netzwerkfreigabe bzw. jede Remotespeicherlösung mit hoher Latenzzeit führt zu einer Installation, die nicht unterstützt wird.  
  
### DbStorageLocation im Vergleich zu StorageLocation  
 **DbStorageLocation** gibt den Ordner an, in dem alle Datenbankdaten- und Metadatendateien gespeichert sind. **StorageLocation** gibt den Ordner an, in dem eine oder mehrere Partitionen eines Cubes gespeichert sind. **StorageLocation** kann unabhängig von **DbStorageLocation**festgelegt werden. Diese Entscheidung wird vom [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbankadministrator auf Grundlage der erwarteten Ergebnisse getroffen. Häufig kommt es bei der Verwendung der einen oder der anderen Eigenschaft zu Überlappungen.  
  
## Verwendung von DbStorageLocation  
 Die **DbStorageLocation**-Datenbankeigenschaft wird als Bestandteil eines **Create**-Datenbankbefehls in einer Sequenz Datenbankbefehle **Detach**/**Attach** innerhalb der Datenbank-Befehlsfolge **Backup**/**Restore** oder in einem **Synchronize**-Datenbankbefehl verwendet. Eine Änderung der **DbStorageLocation** -Datenbankeigenschaft wird als strukturelle Änderung des Datenbankobjekts betrachtet. Dies bedeutet, dass alle Metadaten neu erstellt und die Daten erneut verarbeitet werden müssen.  
  
> [!IMPORTANT]  
>  Der Datenbankspeicherort sollte nicht mit einem **Alter** -Befehl geändert werden. Es wird stattdessen empfohlen, die Datenbank-Befehlsfolge **Detach**/**Attach** zu verwenden (siehe [Verschieben einer Analysis Services Datenbank](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md), [Anfügen und Trennen von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)).  
  
## Siehe auch  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [Anfügen und Trennen von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Verschieben einer Analysis Services Datenbank](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [DbStorageLocation-Element](../../analysis-services/xmla/xml-elements-properties/dbstoragelocation-element.md)   
 [Create-Element &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)   
 [Attach-Element](../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [Synchronize-Element &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)  
  
  