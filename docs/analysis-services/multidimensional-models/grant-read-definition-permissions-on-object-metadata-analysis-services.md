---
title: "Erteilen von Leseberechtigungen für der Definition für Objektmetadaten (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- metadata [Analysis Services]
- permissions [Analysis Services], read metadata
- read metadata permissions
ms.assetid: c857e48e-64b0-4ffe-900d-a0a3ddafcefb
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 55c4e6d43ffedd933e968e8fc2355871c698d290
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="grant-read-definition-permissions-on-object-metadata-analysis-services"></a>Erteilen von Berechtigungen zum Lesen von Definitionen für Objektmetadaten (Analysis Services)
  Die Berechtigung zum Lesen von Objektdefinitionen oder Metadaten für ausgewählte Objekte ermöglicht es einem Administrator, Benutzern die Berechtigung zum Anzeigen von Objektdefinitionen zu erteilen, ohne diesen Benutzern gleichzeitig auch die Berechtigung zum Ändern der Objektdefinition, der Objektstruktur oder der Ansicht der tatsächlichen Daten für das Objekt zu erteilen. **Definition lesen** Die Berechtigungen zum Lesen von Metadaten können auf Datenbank-, Datenquellen-, Dimensions-, Miningstruktur- und Miningmodellebene erteilt werden. Wenn Sie für einen Cube die Berechtigung **Definition lesen** benötigen, müssen Sie **Definition lesen** für die Datenbank aktivieren. Beachten Sie, dass Berechtigungen additiv sind. Eine Rolle kann beispielsweise einem Benutzer die Berechtigung zum Lesen eines Cubes erteilen, während eine andere Datenbankrolle demselben Benutzer die Berechtigung zum Lesen der Metadaten für eine Dimension erteilen kann. Die Berechtigungen aus den beiden unterschiedlichen Rollen werden kombiniert, um dem Benutzer die Berechtigung sowohl zum Lesen der Metadaten für den Cube als auch der Metadaten für die Dimension innerhalb dieser Datenbank zu erteilen.  
  
> [!NOTE]  
>  Die Berechtigung zum Lesen der Metadaten einer Datenbank ist die Mindestberechtigung, die zum Herstellen einer Verbindung mit einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank mithilfe von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] oder [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]erforderlich ist. Ein Benutzer, der über die Berechtigung zum Lesen von Metadaten verfügt, kann auch das DISCOVER_XML_METADATA-Schemarowset für die Abfrage des Objekts und die Ansicht seiner Metadaten verwenden. Weitere Informationen finden Sie unter [DISCOVER_XML_METADATA-Rowset](../../analysis-services/schema-rowsets/xml/discover-xml-metadata-rowset.md).  
  
## <a name="set-read-definition-permissions-on-a-database"></a>Festlegen von Berechtigungen zum Lesen von Definitionen in einer Datenbank  
 Wenn Sie die Berechtigung zum Lesen von Datenbankmetadaten gewähren, erteilen Sie auch die Berechtigung, die Metadaten aller Objekte in der Datenbank zu lesen.  
  
 Es wird empfohlen, dass Sie die Berechtigung **Definition lesen** auf Datenbankebene integrieren, wenn Sie Rollen für die dedizierte Verarbeitung erstellen. Die Berechtigung **Definition lesen** ermöglicht es Nicht-Administratoren, die Objekthierarchie eines Modells in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] anzuzeigen und für nachfolgende Verarbeitungsvorgänge zu individuellen Objekten zu navigieren.  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]her, erweitern Sie im Objekt-Explorer das **Rollen** -Element für die entsprechende Datenbank, und klicken Sie dann auf eine Datenbankrolle (oder erstellen Sie eine neue Datenbankrolle).  
  
2.  Wählen Sie auf der Registerkarte **Allgemein** die Option **Definition lesen** aus.  
  
3.  Geben Sie im **Mitgliedschaft** sbereich die Windows-Konten von Benutzern und Gruppen ein, die mit dieser Rolle eine Verbindung zu Analysis Services herstellen.  
  
4.  Klicken Sie auf **OK** , um die Erstellung der Rolle zu abzuschließen.  
  
## <a name="set-read-definition-permissions-on-individual-objects"></a>Festlegen von Berechtigungen zum Lesen von Definitionen individueller Objekte  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]her, öffnen Sie den Ordner **Datenbanken** , und wählen Sie eine Datenbank aus. Erweitern Sie im Objekt-Explorer das **Rollen** -Element für die entsprechende Datenbank, und klicken Sie dann auf eine Datenbankrolle (oder erstellen Sie eine neue Datenbankrolle).  
  
2.  Entfernen Sie im Bereich **Allgemein** die Datenbankberechtigung für **Read Definition**. Mit diesem Schritt entfernen Sie das Erben von Berechtigungen, sodass Sie Berechtigungen für individuelle Objekte festlegen können.  
  
3.  Wählen Sie das Objekt aus, für das Sie die Eigenschaft **Definition lesen** spezifizieren möchten:  
  
    -   Aktivieren Sie im Bereich **Datenquellen** für diese Datenquelle das Kontrollkästchen **Definition lesen** . Rollenmitglieder können die Verbindungszeichenfolge zur Datenquelle anzeigen, einschließlich des Servernamens und möglicherweise des Benutzernamens. Diese Berechtigung ist verfügbar, wenn Sie Informationen zur Verbindungszeichenfolge bereitstellen möchten, ohne auch die Berechtigung zum Ändern der Verbindungszeichenfolge oder Anzeigen der Definitionen beliebiger anderer Objekte zu erteilen.  
  
    -   Aktivieren Sie im Bereich **Dimensionen** für diese Dimension das Kontrollkästchen **Definition lesen** . Erfahrene Analysten und Entwickler müssen möglicherweise die Definition anzeigen, ohne sie zu ändern oder die Definitionen anderer Objekte (wie andere Dimensionen, Cubeobjekte oder Miningstrukturen oder-modelle) anzuzeigen.  
  
    -   Aktivieren Sie im Miningstrukturbereich für Miningstrukturen oder-modelle das Kontrollkästchen **Definition lesen** . **Definition lesen** ist zum Durchsuchen des Datenmodells erforderlich. Weitere Informationen finden Sie unter [Erteilen von Berechtigungen für Data Mining-Strukturen und -Modelle &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md).  
  
4.  Geben Sie im **Mitgliedschaft** sbereich die Windows-Konten von Benutzern und Gruppen ein, die mit dieser Rolle eine Verbindung zu Analysis Services herstellen.  
  
5.  Klicken Sie auf **OK** , um die Erstellung der Rolle zu abzuschließen.  
  
## <a name="see-also"></a>Siehe auch  
 [Erteilen von Datenbankberechtigungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)   
 [Erteilen von Verarbeitungsberechtigungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
  

