---
title: "&#196;ndern oder L&#246;schen einer Analysis Services-Datenbank | Microsoft Docs"
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
  - "Datenbanken [Analysis Services], ändern"
  - "Entfernen von Datenbanken"
  - "Löschen von Datenbanken"
  - "Datenbanken löschen"
  - "Datenbanken [Analysis Services], löschen"
  - "Ändern von Datenbanken"
ms.assetid: e48e3988-c091-4379-aabc-4da62f709a7e
caps.latest.revision: 34
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 34
---
# &#196;ndern oder L&#246;schen einer Analysis Services-Datenbank
  Sie können den Namen und die Beschreibung einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank vor der Bereitstellung in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] und nach der Bereitstellung in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ändern. Sie können darüber hinaus, abhängig von der Umgebung, weitere Einstellungen der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank ändern.  
  
> [!NOTE]  
>  Im Onlinemodus ist das Ändern der Datenbankeigenschaften mit [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] nicht möglich.  
  
## Ändern von Datenbanken mit SQL Server Management Studio  
 Nach dem Bereitstellen einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank können Sie mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] den Identitätswechselmodus ändern, der von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] beim Verbindungsaufbau zu Datenquellen verwendet wird, die in der Datenbank vorhanden sind. Mit dem Identitätswechselmodus können Sie den Sicherheitskontext angeben, der von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] beim Verbindungsaufbau mit einer Datenquelle verwendet wird, um Daten zu verarbeiten, zu durchsuchen oder um einen Drillthrough durchzuführen.  
  
## Ändern von Datenbanken mithilfe von SQL Server-Datentools  
 Sie können [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] im Projektmodus verwenden, um die Übersetzungen für die Beschriftung und die Beschreibung eines [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts zum Definieren einer Datenbank zu ändern. Weitere Informationen zum Verwenden von Übersetzungen in einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Datenbank finden Sie unter [Globalisierungsszenarien für Analysis Services](../../analysis-services/globalization-scenarios-for-analysis-services.md).  
  
 Sie können außerdem Aliasse und Aggregationsfunktionen festlegen, die Kontotypen zugeordnet sind, die von den Kontoattributen in Dimensionen in der Datenbank verwendet werden. Mit Aliassen können Sie die geschäftsspezifische Terminologie auswählen, die von Ihrer Organisation für Kontotypen in einem Kontodiagramm verwendet wird. Die Kontotypen werden von Elementen eines Kontoattributs verwendet, um anzugeben, wie Measures über jedem Element mithilfe der für jeden Kontotyp in der Datenbank angegebenen Aggregatfunktionen zusammengefasst werden. Weitere Informationen zu Kontoattributen finden Sie unter [Attribute und Attributhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md).  
  
## Löschen von Datenbanken  
 Beim Löschen einer vorhandenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank werden die Datenbank und alle Cubes, Dimensionen und Miningmodelle in der Datenbank gelöscht. Sie können eine vorhandene [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank nur in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]löschen.  
  
#### So löschen Sie eine Analysis Services-Datenbank  
  
1.  Stellen Sie eine Verbindung zu einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz her.  
  
2.  Erweitern Sie im **Objekt-Explorer**den Knoten für die verbundene [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz, und stellen Sie sicher, dass das zu löschende Objekt sichtbar ist.  
  
3.  Klicken Sie mit der rechten Maustaste auf das Objekt, und wählen Sie **Löschen** aus.  
  
4.  Klicken Sie im Dialogfeld **Objekt löschen** auf **OK**.  
  
## Siehe auch  
 [Dokumentieren und Skripterstellung einer Analysis Services-Datenbank](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md)  
  
  