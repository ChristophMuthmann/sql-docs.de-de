---
title: Analysis Services-Skriptprojekt in SQL Server Management Studio | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 86b6090d2f781d1db835752c95907fa1be182963
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="analysis-services-scripts-project-in-sql-server-management-studio"></a>Analysis Services-Skriptprojekt in SQL Server Management Studio
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]können Sie Analysis-Server-Skriptprojekt in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] erstellen, um einander ähnliche Skripts zu Entwicklungs-, Verwaltungs- und Quellcodeverwaltungszwecken in einer Gruppe zusammenzufassen. Falls noch keine Projektmappe in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]geladen ist, wird beim Erstellen eines neuen Skriptprojekts von Analysis-Server automatisch eine neue Projektmappe erstellt. Andernfalls kann das neue Skriptprojekt von Analysis-Server der vorhandenen Projektmappe hinzugefügt oder in einer neuen Projektmappe erstellt werden.  
  
 Zum Erstellen eines Skriptprojekts von Analysis-Server in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]gehen Sie die folgenden grundlegenden Schritte durch:  
  
1.  Zeigen Sie im Menü **Datei**auf **Neu**, und klicken Sie dann auf Projekt.  
  
     Wählen Sie die Vorlage **Analysis Server-Skriptprojekt** aus, und geben Sie dann einen Namen und einen Speicherort für das neue Projekt an.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Verbindungen** , um eine neue Verbindung im Ordner Verbindungen des Skriptprojekts von Analysis-Server im Projektmappen-Explorer herzustellen.  
  
     Dieser Ordner enthält Verbindungszeichenfolgen zu Instanzen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , für die die im Analysis-Serverskriptprojekt enthaltenen Skripts ausgeführt werden können. Ein Skriptprojekt von Analysis-Server kann mehrere Verbindungen enthalten. Die Verbindung, für die Sie ein Skript ausführen möchten, können Sie zum Zeitpunkt der Ausführung auswählen.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Abfragen** , um MDX- (Multidimensional Expressions), DMX- (Data Mining Extensions) und XMLA-Skripts (XML for Analysis) im Ordner Skripts von Analysis-Server im Projektmappen-Explorer zu erstellen.
  
4.  Klicken Sie mit der rechten Maustaste auf das Projekt, zeigen Sie auf **Hinzufügen**, und wählen Sie dann **Vorhandenes Element** aus, um sonstige Dateien, beispielsweise Textdateien mit Hinweisen zum Projekt, in den Ordner **Sonstiges** des Skriptprojekts von Analysis-Server im Projektmappen-Explorer hinzuzufügen. Diese Dateien werden von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ignoriert.  
  
## <a name="file-types"></a>Dateitypen  
 Je nachdem, welche Projekte in die Projektmappe und welche Elemente in die einzelnen Projekte für die betreffende Projektmappe eingefügt wurden, kann eine [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] -Projektmappe mehrere Dateitypen enthalten. Weitere Informationen zu den Dateitypen für Projektmappen in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], finden Sie unter [Dateien zum Verwalten von Projektmappen und Projekten](http://msdn.microsoft.com/library/e19d2859-0b97-4727-ac27-c4c226d86b2f). Normalerweise werden die Dateien aller Projekte in einer [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] -Projektmappe im Projektmappenordner gespeichert, wobei für jedes Projekt ein eigener Ordner angelegt wird.  
  
 Der Projektordner für ein Skriptprojekt von Analysis-Server kann die in der folgenden Tabelle aufgeführten Dateitypen enthalten:  
  
|Dateityp|Description|  
|---------------|-----------------|  
|Definitionsdatei für Skriptprojekte von Analysis-Server (.ssmsasproj)|Enthält Metadaten zu den im Projektmappen-Explorer angezeigten Ordnern sowie Informationen, aus denen hervorgeht, in welchen Ordnern dem Projekt zugehörige Dateien angezeigt werden sollten.<br /><br /> Die Projektdefinitionsdatei enthält darüber hinaus Metadaten für die im Projekt enthaltenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Verbindungen sowie Metadaten, die Zuordnungen von Verbindungen mit Skriptdateien im Projekt herstellen.|  
|DMX-Skriptdatei (.dmx)|Enthält ein in das Projekt aufgenommenes DMX-Skript.|  
|MDX-Skriptdatei (.mdx)|Enthält ein in das Projekt aufgenommenes MDX-Skript.|  
|XMLA-Skriptdatei (.xmla)|Enthält ein in das Projekt aufgenommenes XMLA-Skript.|  
  
## <a name="analysis-services-templates"></a>Vorlagen von Analysis Services  
 Wenn Sie einem Skriptprojekt von Analysis-Server neue MDX-, DMX- oder XMLA-Skripts hinzufügen, haben Sie die Möglichkeit, mithilfe des Vorlagen-Explorers [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Vorlagen zu suchen. Diese Vorlagen stellen eine Auflistung vordefinierter Skripts oder Anweisungen dar, in denen das Ausführen einer angegebenen Aktion gezeigt wird. Der Vorlagen-Explorer ist im Menü **Ansicht** verfügbar und enthält Vorlagen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]und [!INCLUDE[ssEW](../../includes/ssew-md.md)]. Weitere Informationen finden Sie unter [Use Analysis Services Templates in SQL Server Management Studio](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen mehrdimensionaler Modelle mit SQL Server-Datentools &#40;SSDT&#41;](../../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)   
 [Mehrdimensionale Ausdrücke & #40; MDX & #41; Referenz](../../mdx/multidimensional-expressions-mdx-reference.md)   
 [Datamining-Erweiterungen & #40; DMX & #41; Referenz](../../dmx/data-mining-extensions-dmx-reference.md)   
 [Analysis Services Scripting Language &#40;ASSL für XMLA&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [Analysis Services Scripting Language &#40;ASSL XMLA&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)  
  
  
