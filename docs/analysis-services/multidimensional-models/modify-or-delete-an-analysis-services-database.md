---
title: Ändern oder löschen eine Analysis Services-Datenbank | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 67c1c08801b31a30f9ae81b3f5edd110fee3bcc0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="modify-or-delete-an-analysis-services-database"></a>Ändern oder Löschen einer Analysis Services-Datenbank
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
  
  
