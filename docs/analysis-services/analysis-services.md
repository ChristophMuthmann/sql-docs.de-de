---
title: "Analysis Services | Microsoft Docs"
ms.date: "03/28/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "Analysis Services, Informationen zu Analysis Services – mehrdimensionale Daten"
  - "SSAS"
  - "Analysis Services"
  - "SQL Server Analysis Services, Informationen zu Analysis Services – mehrdimensionale Daten"
  - "SQL Server Analysis Services"
  - "Mehrdimensionale Daten [Analysis Services]"
  - "SSAS, Informationen zu Analysis Services – mehrdimensionale Daten"
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
caps.latest.revision: 60
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 60
---
# Analysis Services
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ist ein analytisches Online-Datenmodul, das in Lösungen für Decision Support und Business Analytics zur Anwendung kommt, und analytische Daten für Geschäftsberichte und Clientanwendungen wie Power BI, Excel, Reporting Services-Berichte und andere Datenvisualisierungstools bereitstellt.  
  
 Ein typischer Workflow für [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] beinhaltet die Erstellung eines multidimensionalen oder tabellarischen Datenmodells, die Bereitstellung des Modells als Datenbank in einer [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Instanz, die Bearbeitung der Datenbank, um Daten oder Metadaten in diese zu laden, das Einrichten der Datenaktualisierung und die Zuweisung der Datenzugriffsberechtigungen durch Endbenutzer. Wenn dieser abgeschlossen ist, kann jede Anwendung, die [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] als Datenquelle unterstützt, auf dieses semantische Mehrzweckdatenmodell zugreifen.  
  
 Die Modelle werden mit Daten aus externen Datensystemen gefüllt. Dies sind normalerweise Data Warehouses, die von einem relationalen SQL Server- oder Oracle-Datenbankmodul gehostet werden. (Tabellarische Modelle unterstützen zusätzliche Datenquellentypen.) Modelle geben Abfrageobjekte wie z. B. Cubes an, aber auch Dimensionen, die in mehreren Cubes verwendet werden können, Berechnungen und KPIs, die Geschäftslogik kapseln, sowie Interaktionen wie Navigations- und Drillthroughverhalten.  
 
## <a name="analysis-services-on-premises-and-in-the-cloud"></a>Analysis Services lokal und in der Cloud
Analysis Services ist jetzt in der Cloud und als Azure-Dienst verfügbar. Azure Analysis Services befindet sich derzeit in der Vorschau und unterstützt tabellarische Modelle auf Kompatibilitätsgrad 1200. DirectQuery, Partitionen, Sicherheit auf Zeilenebene, Bidirektionale Beziehungen und Übersetzungen werden unterstützt. Um mehr über den Dienst zu erfahren, und ihn kostenlos zu testen, wechseln Sie zu [Azure Analysis Services](https://azure.microsoft.com/en-us/services/analysis-services/). 
  
## <a name="server-mode"></a>Servermodus  
 Bei der Installation von Analysis Services mithilfe des [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] -Setups, geben Sie während der Konfiguration einen Servermodus für diese Instanz an.  Jeder Modus umfasst verschiedene Funktionen, die für eine bestimmte Analysis Services-Lösung eindeutig sind.  
  
-   **Mehrdimensionaler und Data Mining-Modus** – Implementieren von OLAP-Modellierungskonstrukten (Cubes, Dimensionen, Measures).  
  
-   **Tabellenmodus** – Implementieren speicherinterner, relationaler Datenmodellkonstrukten (Modell, Tabellen, Spalten).  
  
     Tabellarische Modelle können mit dem Standardkompatibilitätsgrad 1200 erstellt werden und so die neueste Funktionalität nutzen, sie können aber auch mit dem älteren Kompatibilitätsgrad 1103 erstellt werden. Es gibt deutliche Unterschiede zwischen den Kompatibilitätsgraden. Weitere Informationen zum Vergleich der Grade finden Sie unter [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).  
  
-   **Power Pivot-Modus** – Implementieren von [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] - und Excel-Datenmodellen in SharePoint ([!INCLUDE[ssGemini](../includes/ssgemini-md.md)] für SharePoint ist ein Datenmodul der mittleren Ebene, das Datenmodelle lädt, abfragt und aktualisiert, die in SharePoint gehostet werden).  
  
 Eine einzelne Instanz kann mit nur einem Modus konfiguriert werden und kann später nicht geändert werden.  Sie können mehrere Instanzen mit unterschiedlichen Modi auf dem gleichen Server installieren, aber Sie müssen das Setup ausführen und Konfigurationseinstellungen für jede Instanz festlegen.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Funktionen variieren je nach Edition. Weitere Informationen finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](../sql-server/von-den-sql-server-2016-editionen-unterstützte-funktionen.md) 
  
## <a name="authoring-solutions"></a>Erstellen von Projektmappen  
 Verwenden Sie SQL Server Data Tools zum Erstellen eines Modells (siehe [In Analysis Services verwendete Tools und Anwendungen](../analysis-services/tools-and-applications-used-in-analysis-services.md)), und wählen Sie eine der Projektvorlagen für tabellarische oder für mehrdimensionale und Data Mining-Modelle aus. Die Projektvorlage enthält Ordner für alle in einem Modell erforderlichen Objekte. Assistenten helfen dabei, viele grundlegende Elemente zu erstellen, wie z.B. Datenquellen, Datenquellensichten, Dimensionen, Cubes und Rollen.  
  
## <a name="documentation-by-area"></a>Dokumentation nach Bereich  
Die Dokumentation für Analysis Services ist in Abschnitten organisiert, die dem Typ des Projekts entsprechen, die Sie erstellen. Wählen Sie in den folgenden Links, um mehr über jeden Modus oder die einzelnen Funktionsbereiche zu erfahren.  
   
 ![Kleines Dateiordnersymbol](../analysis-services/media/filefolder-small.png "Kleines Dateiordnersymbol") [Neuigkeiten](../analysis-services/what-s-new-in-analysis-services.md)  
  
 ![Kleines Dateiordnersymbol](../analysis-services/media/filefolder-small.png "Kleines Dateiordnersymbol") [Comparing Tabular and Multidimensional Solutions](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)  
  
 ![Kleines Dateiordnersymbol](../analysis-services/media/filefolder-small.png "Kleines Dateiordnersymbol") [Tabellarische Modelle](../analysis-services/tabular-models/tabular-models-ssas.md)  
  
 ![Kleines Dateiordnersymbol](../analysis-services/media/filefolder-small.png "Kleines Dateiordnersymbol") [Mehrdimensionale Modelle](../analysis-services/multidimensional-models/multidimensional-models-ssas.md)  
  
 ![Kleines Dateiordnersymbol](../analysis-services/media/filefolder-small.png "Kleines Dateiordnersymbol") [Data Mining](../analysis-services/data-mining/data-mining-ssas.md)  
  
 ![Kleines Dateiordnersymbol](../analysis-services/media/filefolder-small.png "Kleines Dateiordnersymbol") [PowerPivot für SharePoint](../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
  
 ![Kleines Dateiordnersymbol](../analysis-services/media/filefolder-small.png "Kleines Dateiordnersymbol") [Analysis Services-Instanzverwaltung](../analysis-services/instances/analysis-services-instance-management.md)  
   
 ![Kleines Dateiordnersymbol](../analysis-services/media/filefolder-small.png "Kleines Dateiordnersymbol") [Analysis Services-Lernprogramme](../analysis-services/analysis-services-tutorials-ssas.md)  
  
![Kleines Dateiordnersymbol](../analysis-services/media/filefolder-small.png "Kleines Dateiordnersymbol") [Analysis Services Developer Documentation (Entwicklerhandbuch Analysis Services)](https://msdn.microsoft.com/library/bb500153(SQL.130).aspx)  
 
![Kleines Dateiordnersymbol](../analysis-services/media/filefolder-small.png "Kleines Dateiordnersymbol") [Technische Referenz (SSAS)](../analysis-services/powershell/technical-reference-ssas.md)