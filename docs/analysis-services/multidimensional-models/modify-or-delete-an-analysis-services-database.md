---
title: "Ändern oder löschen eine Analysis Services-Datenbank | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- databases [Analysis Services], modifying
- removing databases
- deleting databases
- dropping databases
- databases [Analysis Services], deleting
- modifying databases
ms.assetid: e48e3988-c091-4379-aabc-4da62f709a7e
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 58ba47239da28dfa023bb59a1bbb6ed77e11d425
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="modify-or-delete-an-analysis-services-database"></a>Ändern oder Löschen einer Analysis Services-Datenbank
  Sie können den Namen und die Beschreibung einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank vor der Bereitstellung in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] und nach der Bereitstellung in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ändern. Sie können darüber hinaus, abhängig von der Umgebung, weitere Einstellungen der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank ändern.  
  
> [!NOTE]  
>  Im Onlinemodus ist das Ändern der Datenbankeigenschaften mit [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] nicht möglich.  
  
## <a name="modifying-databases-using-sql-server-management-studio"></a>Ändern von Datenbanken mit SQL Server Management Studio  
 Nach dem Bereitstellen einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank können Sie mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] den Identitätswechselmodus ändern, der von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] beim Verbindungsaufbau zu Datenquellen verwendet wird, die in der Datenbank vorhanden sind. Mit dem Identitätswechselmodus können Sie den Sicherheitskontext angeben, der von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] beim Verbindungsaufbau mit einer Datenquelle verwendet wird, um Daten zu verarbeiten, zu durchsuchen oder um einen Drillthrough durchzuführen.  
  
## <a name="modifying-databases-using-sql-server-data-tools"></a>Ändern von Datenbanken mithilfe von SQL Server-Datentools  
 Sie können [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] im Projektmodus verwenden, um die Übersetzungen für die Beschriftung und die Beschreibung eines [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts zum Definieren einer Datenbank zu ändern. Weitere Informationen zum Verwenden von Übersetzungen in einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank finden Sie unter [Globalisierungsszenarien für Analysis Services](../../analysis-services/globalization-scenarios-for-analysis-services.md).  
  
 Sie können außerdem Aliasse und Aggregationsfunktionen festlegen, die Kontotypen zugeordnet sind, die von den Kontoattributen in Dimensionen in der Datenbank verwendet werden. Mit Aliassen können Sie die geschäftsspezifische Terminologie auswählen, die von Ihrer Organisation für Kontotypen in einem Kontodiagramm verwendet wird. Die Kontotypen werden von Elementen eines Kontoattributs verwendet, um anzugeben, wie Measures über jedem Element mithilfe der für jeden Kontotyp in der Datenbank angegebenen Aggregatfunktionen zusammengefasst werden. Weitere Informationen zu Kontoattributen finden Sie unter [Attribute und Attributhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md).  
  
## <a name="deleting-databases"></a>Löschen von Datenbanken  
 Beim Löschen einer vorhandenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank werden die Datenbank und alle Cubes, Dimensionen und Miningmodelle in der Datenbank gelöscht. Sie können eine vorhandene [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank nur in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]löschen.  
  
#### <a name="to-delete-an-analysis-services-database"></a>So löschen Sie eine Analysis Services-Datenbank  
  
1.  Stellen Sie eine Verbindung zu einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz her.  
  
2.  Erweitern Sie im **Objekt-Explorer**den Knoten für die verbundene [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz, und stellen Sie sicher, dass das zu löschende Objekt sichtbar ist.  
  
3.  Klicken Sie mit der rechten Maustaste auf das Objekt, und wählen Sie **Löschen**aus.  
  
4.  Klicken Sie im Dialogfeld **Objekt löschen** auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
 [Dokumentieren und Skripterstellung einer Analysis Services-Datenbank](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md)  
  
  

