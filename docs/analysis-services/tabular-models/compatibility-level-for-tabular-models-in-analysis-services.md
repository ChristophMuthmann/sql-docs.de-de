---
title: "Kompatibilit&#228;tsgrad f&#252;r tabellarische Modelle in Analysis Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.bidtoolset.versioncompat.f1"
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
caps.latest.revision: 27
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 27
---
# Kompatibilit&#228;tsgrad f&#252;r tabellarische Modelle in Analysis Services
  Der *Kompatibilitätsgrad* eines Modells oder einer Datenbank bezieht sich auf eine Reihe von Release-spezifischen Verhalten im [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Modul. Sie können Modelle mit jedem unterstützten Kompatibilitätsgrad erstellen, um Verhalten eines bestimmten Releases zu erhalten. Beispielsweise verfügen DirectQuery und tabellarische Objektmetadaten über verschiedene Implementierungen, abhängig von der Zuweisung des Kompatibilitätsgrads.  
  
 **SQL Server 2016 RTM (1200)**, oder abgekürzt der Kompatibilitätsgrad 1200, ist neu in SQL Server 2016 und wird nur auf tabellarische Modelle angewendet.  Tabellarische Modelle mit Kompatibilitätsgrad 1200 laufen nur auf einer tabellarischen [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]-Instanz.  
  
 Zum Erstellen oder Upgraden eines tabellarischen Modells verwenden Sie SQL Server Data Tools (SSDT) und legen beim Erstellen des Projekts die **Kompatibilitätsgrad**-Eigenschaft fest. Sie können dies auch in der Datei **model.bim** festlegen, nachdem das Projekt erstellt wurde.  
  
> [!NOTE]  
>  Mehrdimensionale Modelle halten sich im Hinblick auf Kompatibilitätsgrade an einen unabhängigen Versionspfad. Wenn die Zahlen übereinstimmen, wie es bei 1103 der Fall ist, ist dies zufällig. Weitere Informationen finden Sie unter [Kompatibilitätsgrad einer mehrdimensionalen Datenbank &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md).  
  
## Unterstützte Kompatibilitätsgrade für tabellarische Modelldatenbanken  
 Analysis Services unterstützt die folgenden Kompatibilitätsgrade, die sowohl auf Modelle als auch auf Datenbanken angewendet werden können.  Die zum Erstellen eines Modells verwendete Version des Tools bestimmt, ob höhere Kompatibilitätsgrade zur Verfügung stehen.  
  
||||  
|-|-|-|  
|Kompatibilitätsgrad|Serverversion|Version des Modellierungstools|  
|1200|Wird nur auf SQL Server 2016-Instanzen ausgeführt|[Nur SQL Server Data Tools für Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkID=690931) <sup>1</sup><br /><br /> [Neuigkeiten in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md) beschreibt die bei diesem Grad verfügbaren Funktionen.|  
|1103|SQL Server 2016<br /><br /> SQL Server 2014<br /><br /> SQL Server 2012 SP1|[SQL Server Data Tools für Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkID=690931) <sup>2</sup><br /><br /> [SQL Server Data Tools für Business Intelligence (Visual Studio 2013)](https://www.microsoft.com/en-us/download/details.aspx?id=42313)<br /><br /> [SQL Server Data Tools für Business Intelligence (Visual Studio 2012)](http://www.microsoft.com/en-us/download/details.aspx?id=36843)|  
|1100|SQL Server 2016<br /><br /> SQL Server 2014<br /><br /> SQL Server 2012 SP1<br /><br /> SQL Server 2012|[SQL Server Data Tools für Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkID=690931) <sup>1</sup><br /><br /> [SQL Server Data Tools für Business Intelligence (Visual Studio 2013)](https://www.microsoft.com/en-us/download/details.aspx?id=42313)<br /><br /> [SQL Server Data Tools für Business Intelligence (Visual Studio 2012)](http://www.microsoft.com/en-us/download/details.aspx?id=36843)<br /><br /> Business Intelligence Development Studio (wird in der Visual Studio 2010-Shell ausgeführt und über SQL Server-Setup installiert)|  
  
 <sup>1</sup> Sie können SQL Server Data Tools für Visual Studio 2015 verwenden, um ein tabellarisches 1100-Modell oder 1103-Modell in früheren Releases von Analysis Services bereitzustellen.  
  
 <sup>2</sup> Die Kompatibilitätsgrade 1100, 1103 und 1200 sind alle für Tabellenmodellprojekte in SQL Server Data Tools für Visual Studio 2015 gültig. Das 1200er-Modell steht Ihnen jedoch nur in einer SQL Server 2016-Instanz von SQL Server zur Verfügung.  
  
## Festlegen des Kompatibilitätsgrads beim Erstellen oder Upgraden eines neuen Tabellenprojekts in SSDT  
 Beim Erstellen eines neuen Tabellenmodellprojekts in SQL Server Data Tools (SSDT) können Sie im Dialogfeld **New Tabular project options** (Optionen für neues Tabellenprojekt) den Kompatibilitätsgrad angeben:  
  
 ![ssas_tabularproject_compat1200](../../analysis-services/tabular-models/media/ssas-tabularproject-compat1200.jpg "ssas_tabularproject_compat1200")  
  
 Sie können auch einen Standardkompatibilitätsgrad angeben, indem Sie die Option **Diese Meldung nicht mehr anzeigen** aktivieren. Bei allen nachfolgenden Projekten wird der angegebene Kompatibilitätsgrad verwendet. Sie können den Standardkompatibilitätsgrad in SSDT unter **Tools** > **Optionen** ändern.  
  
 Zum Upgraden eines Tabellenmodellprojekts legen Sie die **Kompatibilitätsgrad**-Eigenschaft im Fenster **Eigenschaften** des Modells auf **SQL Server 2016 RTM (1200)** fest.  Weitere Informationen finden Sie unter [Upgrade Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md) .  
  
> [!NOTE]  
>  Eine Möglichkeit zum Erstellen eines tabellarischen Modells ist, es basierend auf einer importierten Power Pivot-Arbeitsmappe zu erstellen. Standardmäßig erstellt Power BI Desktop tabellarische Modelle automatisch mit dem Kompatibilitätsgrad 1200. Frühere Versionen von Power Pivot-Arbeitsmappen könnten jedoch den Grad 1100 aufweisen. Wenn Sie eine ältere Arbeitsmappe verwenden, vergessen Sie nicht, die **Kompatibilitätsgrad**-Eigenschaft zu ändern, um sie upzugraden.  
  
## Überprüfen des Kompatibilitätsgrads einer Datenbank in SSMS  
 Klicken Sie in SSMS mit der rechten Maustaste auf den Datenbanknamen > **Eigenschaften** > **Kompatibilitätsgrad**.  
  
## Überprüfen des unterstützten Kompatibilitätsgrads für einen Server in SSMS  
 Klicken Sie in SSMS mit der rechten Maustaste auf den Servernamen > **Eigenschaften** > **Unterstützter Kompatibilitätsgrad**.  
  
 Diese Eigenschaft gibt den höchsten Kompatibilitätsgrad einer auf dem Server ausgeführten Datenbank an.  Der unterstützte Kompatibilitätsgrad ist schreibgeschützt und kann nicht geändert werden.  
  
## Siehe auch  
 [Kompatibilitätsgrad einer mehrdimensionalen Datenbank &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Neuigkeiten in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Importieren aus PowerPivot &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md)   
 [Erstellen eines neuen Tabellenmodellprojekts &#40;Analysis Services&#41;](../../analysis-services/tabular-models/create-a-new-tabular-model-project-analysis-services.md)  
  
  