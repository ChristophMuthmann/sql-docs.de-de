---
title: Programmieren AMO-OLAP-von erweiterten Objekten | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- programming [AMO]
- Analysis Management Objects, OLAP
- OLAP [AMO]
- AMO, OLAP
ms.assetid: b75f35a7-32df-4f22-983d-324aa98e15a9
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dedfe7e17d6f8fd0be0bb769b9891880a83b2eba
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="programming-amo-olap-advanced-objects"></a>Programmieren von erweiterten AMO OLAP-Objekten
  In diesem Thema werden die Programmierdetails von erweiterten OLAP-Objekten in Analysis Management Objects (AMO) erläutert. Dieses Thema enthält folgende Abschnitte:  
  
-   [Aktionsobjekte](#Action)  
  
-   [KPI-Objekte](#KPI)  
  
-   [Perspective-Objekte](#Persp)  
  
-   [ProactiveCaching-Objekte](#PC)  
  
-   [Übersetzungsobjekte](#Transl)  
  
##  <a name="Action"></a>Aktionsobjekte  
 Aktionsklassen werden verwendet, um beim Durchsuchen von bestimmten Bereichen des Cubes eine aktive Antwort zu erstellen. Aktionsobjekte können mithilfe von AMO definiert werden, sie werden jedoch von der Clientanwendung verwendet, die die Daten durchsucht. Aktionen können von anderen Typen sein, und sie müssen entsprechend ihrem Typ erstellt werden. Folgende Aktionen stehen zur Verfügung:  
  
-   Drillthroughaktionen geben die Zeilen zurück, die die zugrunde liegenden Daten der ausgewählten Zellen des Cubes darstellen, in dem die Aktion ausgeführt wird.  
  
-   Berichtsaktionen geben einen Bericht von [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] zurück, der mit dem ausgewählten Abschnitt des Cubes verbunden ist, in dem die Aktion ausgeführt wird.  
  
-   Standardaktionen geben das Aktionselement zurück (URL, HTML, DataSet, RowSet und sonstige Elemente), das mit dem ausgewählten Abschnitt des Cubes verbunden ist, in dem die Aktion ausgeführt wird.  
  
 Für die Erstellung eines Aktionsobjekts sind folgende Schritte erforderlich:  
  
1.  Erstellen Sie das abgeleitete Aktionsobjekt, und füllen Sie die grundlegenden Attribute auf.  
  
     Folgende grundlegende Attribute stehen zur Verfügung: Typ der Aktion, Zieltyp oder Abschnitt des Cubes, Ziel oder spezifischer Bereich des Cubes, in dem die Aktion verfügbar ist, Beschriftung und Beschriftung als MDX-Ausdruck.  
  
2.  Füllen Sie die spezifischen Attribute des Aktionstyps auf.  
  
     Die Attribute unterscheiden sich für die drei Aktionstypen, weitere Informationen zu Parametern finden Sie im folgenden Codebeispiel.  
  
3.  Fügen Sie die Aktion der Cubeauflistung hinzu, und aktualisieren Sie den Cube. Die Aktion ist kein aktualisierbares Objekt.  
  
 Für den Test der Aktion ist eine andere Programmanwendung erforderlich. Sie können Ihre Aktion in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] testen. Sie müssen zuerst installieren [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] Beispiele finden Sie unter [Verarbeiten eines mehrdimensionalen Modells &#40; Analysis Services &#41; ](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 Der folgende Beispielcode repliziert drei unterschiedliche Aktionen aus dem Analysis Services-Projektbeispiel für Adventure Works. Sie können die Aktionen unterscheiden, da die von Ihnen anhand des folgenden Beispiels eingeführten mit "My" beginnen.  
  
```  
static public void CreateActions(Cube cube)  
{  
    #region Adding a drillthrough action  
    // Verify That action exists and drop it  
    if (cube.Actions.ContainsName("My Reseller Details"))  
        cube.Actions.Remove("My Drillthrough Action",true);  
  
    //Create a Drillthrough action  
    DrillThroughAction dtaction = new DrillThroughAction("My Reseller Details", "My Drillthrough Action");  
  
    //Define the Action  
    dtaction.Type = ActionType.DrillThrough;  
    dtaction.TargetType = ActionTargetType.Cells;  
    dtaction.Target = "MeasureGroupMeasures(\"Reseller Sales\")";  
    dtaction.Caption = "My Drillthrough...";  
    dtaction.CaptionIsMdx = false;  
  
    #region create drillthrough action specifics  
    //Adding Drillthrough columns  
    //Adding Measure columns to the drillthrough  
    MeasureGroup mg = cube.MeasureGroups.FindByName("Reseller Sales");  
    MeasureBinding mb1 = new MeasureBinding();  
    mb1.MeasureID = mg.Measures.FindByName( "Reseller Sales Amount").ID;  
    dtaction.Columns.Add(mb1);  
  
    MeasureBinding mb2 = new MeasureBinding();  
    mb2.MeasureID = mg.Measures.FindByName("Reseller Order Quantity").ID;  
    dtaction.Columns.Add(mb2);  
  
    MeasureBinding mb3 = new MeasureBinding();  
    mb3.MeasureID = mg.Measures.FindByName("Reseller Unit Price").ID;  
    dtaction.Columns.Add(mb3);  
  
    //Adding Dimension Columns to the drillthrough  
    CubeAttributeBinding cb1 = new CubeAttributeBinding();  
    cb1.CubeID = cube.ID;  
    cb1.CubeDimensionID = cube.Dimensions.FindByName("Reseller").ID;  
    cb1.AttributeID = "Reseller Name";  
    cb1.Type = AttributeBindingType.All;  
    dtaction.Columns.Add(cb1);  
  
    CubeAttributeBinding cb2 = new CubeAttributeBinding();  
    cb2.CubeID = cube.ID;  
    cb2.CubeDimensionID = cube.Dimensions.FindByName("Product").ID;  
    cb2.AttributeID = "Product Name";  
    cb2.Type = AttributeBindingType.All;  
    dtaction.Columns.Add(cb2);  
    #endregion  
  
    //Add the defined action to the cube  
    cube.Actions.Add(dtaction);  
    #endregion  
  
    #region Adding a Standard action  
    // Verify That action exists and drop it  
    if (cube.Actions.ContainsName("My City Map"))  
        cube.Actions.Remove("My Action", true);  
  
    //Create a Drillthrough action  
    StandardAction stdaction = new StandardAction("My City Map", "My Action");  
  
    //Define the Action  
    stdaction.Type = ActionType.Url;  
    stdaction.TargetType = ActionTargetType.AttributeMembers;  
    stdaction.Target = "[Geography].[City]";  
    stdaction.Caption = "\"My View Map for \" + [Geography].[City].CurrentMember.Member_Caption + \"...\"";  
    stdaction.CaptionIsMdx = true;  
  
    #region create standard action specifics  
    stdaction.Expression = "\"http://maps.msn.com/home.aspx?plce1=\" + " +  
        "[Geography].[City].CurrentMember.Name + \",\" + " +  
        "[Geography].[State-Province].CurrentMember.Name + \",\" + " +  
        "[Geography].[Country].CurrentMember.Name + " +  
        "\"&regn1=\" + " +  
        "Case " +  
            "When [Geography].[Country].CurrentMember Is " +  
                    "[Geography].[Country].&[Australia] " +  
                "Then \"3\" " +  
            "When [Geography].[Country].CurrentMember Is " +  
                    "[Geography].[Country].&[Canada] " +  
                "Or [Geography].[Country].CurrentMember Is " +  
                    "[Geography].[Country].&[United States] " +  
                "Then \"0\" " +  
                "Else \"1\" " +  
        "End ";  
    #endregion  
  
    //Add the defined action to the cube  
    cube.Actions.Add(stdaction);  
  
    #endregion  
  
    #region Adding a Reporting action  
    // Verify That action exists and drop it  
    if (cube.Actions.ContainsName("My Sales Reason Comparisons"))  
        cube.Actions.Remove("My Report Action", true);  
  
    //Create a Report action  
    ReportAction rsaction = new ReportAction("My Sales Reason Comparisonsp", "My Report Action");  
  
    //Define the Action  
    rsaction.Type = ActionType.Report;  
    rsaction.TargetType = ActionTargetType.AttributeMembers;  
    rsaction.Target = "[Product].[Category]";  
    rsaction.Caption = "\"My Sales Reason Comparisons for \" + [Product].[Category].CurrentMember.Member_Caption + \"...\"";  
    rsaction.CaptionIsMdx = true;  
  
    #region create Report action specifics  
    rsaction.ReportServer = "MyRSSamplesServer";  
    rsaction.Path = "ReportServer?/AdventureWorks Sample Reports/Sales Reason Comparisons";  
    rsaction.ReportParameters.Add("ProductCategory", "UrlEscapeFragment( [Product].[Category].CurrentMember.UniqueName )");  
    rsaction.ReportFormatParameters.Add("rs:Command", "Render");  
    rsaction.ReportFormatParameters.Add("rs:Renderer", "HTML5");  
    #endregion  
  
    //Add the defined action to the cube  
    cube.Actions.Add(rsaction);  
  
    #endregion  
}  
```  
  
##  <a name="KPI"></a>KPI-Objekte  
 Ein Key Performance Indicator (KPI) ist eine Auflistung von Berechnungen, die einer Measuregruppe in einem Cube zugeordnet sind und zur Auswertung der Geschäftserfolge verwendet werden. <xref:Microsoft.AnalysisServices.Kpi>-Objekte können mithilfe von AMO definiert werden, sie werden jedoch von der Clientanwendung verwendet, die die Daten durchsucht.  
  
 Erstellen einer <xref:Microsoft.AnalysisServices.Kpi> Objekt erfordert die folgenden Schritte aus:  
  
1.  Erstellen Sie das <xref:Microsoft.AnalysisServices.Kpi>-Objekt, und füllen Sie die grundlegenden Attribute auf.  
  
     Folgende grundlegende Attribute stehen zur Verfügung: Beschreibung, Anzeigeordner, zugeordnete Measuregruppe und Wert. Der Anzeigeordner teilt der Clientanwendung mit, wo sich der KPI befindet, damit er vom Endbenutzer gefunden werden kann. Die zugeordnete Measuregruppe gibt die Measuregruppe an, auf die sich alle MDX-Berechnungen beziehen. Der Wert zeigt den tatsächlichen Wert des Performance Indicators als MDX-Ausdruck an.  
  
2.  Definieren des KPI-Indikators: Ziel, Status und Trend.  
  
     Indikatoren sind MDX-Ausdrücke, die zu einem Wert zwischen -1 und 1 ausgewertet werden sollten. Der Wertebereich für die Indikatoren wird jedoch von der durchsuchenden Anwendung definiert.  
  
3.  Beim Durchsuchen von KPIs in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] werden Werte kleiner als -1 wie -1 und Werte größer als 1 wie 1 behandelt.  
  
4.  Definieren Sie Grafiken.  
  
     Grafiken sind Zeichenfolgenwerte, die in der Clientanwendung als Referenz verwendet werden, um den richtige Satz von Bildern für die Anzeige zu identifizieren. Die Grafikzeichenfolge definiert auch das Verhalten der Anzeigefunktion. Normalerweise wird der Bereich in eine ungerade Anzahl von Status aufgeteilt, von ungültig bis gut, und jedem Status wird ein Bild aus dem Satz zugeordnet.  
  
     Wenn Sie zum Durchsuchen Ihrer KPIs [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] verwenden, wird der Indikatorbereich in Abhängigkeit von den Namen in drei oder fünf Status aufgeteilt. Zudem gibt es Namen, bei denen sich die Bereiche umkehren, d. h., -1 ist "Gut", und 1 ist "Ungültig". In [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] werden die drei Status folgendermaßen bezeichnet:  
  
    -   Ungültig = -1 bis -0,5  
  
    -   OK = -0,4999 bis 0,4999  
  
    -   Gut = 0,50 bis 1  
  
     In [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], fünf Status innerhalb des Bereichs lauten wie folgt:  
  
    -   Ungültig = -1 bis -0,75  
  
    -   Risiko = -0,7499 bis -0,25  
  
    -   OK = -0,2499 bis 0,2499  
  
    -   Steigend = 0,25 bis 0,7499  
  
    -   Gut = 0,75 bis 1  
  
 In der folgenden Tabelle sind Verwendung, Name und die Anzahl der Status aufgeführt, die dem Bild zugeordnet sind.  
  
|Bildverwendung|Bildname|Anzahl von Status|  
|-----------------|----------------|----------------------|  
|Status|Formen|3|  
|Status|Verkehrsampel|3|  
|Status|Straßenschilder|3|  
|Status|Messgerät|3|  
|Status|Umgekehrter Maßstab|5|  
|Status|Thermometer|3|  
|Status|Zylinder|3|  
|Status|Gesichter|3|  
|Status|Varianzpfeil|3|  
|Trend|Standardpfeil|3|  
|Trend|Statuspfeil|3|  
|Trend|Umgekehrter Statuspfeil|5|  
|Trend|Gesichter|3|  
  
1.  Fügen Sie den KPI der Cubeauflistung hinzu, und aktualisieren Sie den Cube, da der KPI kein aktualisierbares Objekt ist.  
  
 Für den Test der KPI ist eine andere Programmanwendung erforderlich. Sie können Ihren KPI in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] testen.  
  
 Der folgende Beispielcode erstellt einen KPI im Ordner "Financial Perpective/Grow Revenue" für den AdventureWorks-Cube, der im Analysis Services-Projektbeispiel für AdventureWorks enthalten ist.  
  
```  
static public void CreateKPIs(Cube cube)  
{  
    Kpi kpi = cube.Kpis.Add("My Internet Revenue", "My Internet Revenue");  
    kpi.Description = "(My) Revenue achieved through direct sales via Interner";  
    kpi.DisplayFolder = "\\Financial Perspective\\Grow Revenue";  
    kpi.AssociatedMeasureGroupID = "Internet Sales";  
    kpi.Value = "[Measures].[Internet Sales Amount]";  
    #region Goal  
    kpi.Goal = "Case" +  
               "     When IsEmpty" +  
               "          (" +  
               "            ParallelPeriod" +  
               "            (" +  
               "              [Date].[Fiscal Time].[Fiscal Year]," +  
               "              1," +  
               "              [Date].[Fiscal Time].CurrentMember" +  
               "            )" +  
               "          )" +   
               "     Then [Measures].[Internet Sales Amount]" +  
               "     Else 1.10 *" +  
               "          (" +  
               "            [Measures].[Internet Sales Amount]," +  
               "            ParallelPeriod" +  
               "            (" +  
               "              [Date].[Fiscal Time].[Fiscal Year]," +  
               "              1," +  
               "              [Date].[Fiscal Time].CurrentMember" +  
               "            )" +  
               "          ) " +  
               " End";  
    #endregion  
    #region Status  
    kpi.Status = "Case" +  
                 "   When KpiValue( \"Internet Revenue\" ) / KpiGoal ( \"Internet Revenue\" ) >= .95 " +  
                 "   Then 1 " +  
                 "   When KpiValue( \"Internet Revenue\" ) / KpiGoal ( \"Internet Revenue\" ) <  .95 " +  
                 "        And  " +  
                 "        KpiValue( \"Internet Revenue\" ) / KpiGoal ( \"Internet Revenue\" ) >= .85 " +  
                 "   Then 0 " +  
                 "   Else -1 " +  
                 "End";  
    #endregion  
    #region Trend  
    kpi.Trend = "Case " +  
                "    When VBA!Abs " +  
                "         ( " +  
                "           KpiValue( \"Internet Revenue\" ) -  " +  
                "           ( " +  
                "             KpiValue ( \"Internet Revenue\" ), " +  
                "             ParallelPeriod " +  
                "             (  " +  
                "               [Date].[Fiscal Time].[Fiscal Year], " +  
                "               1, " +  
                "               [Date].[Fiscal Time].CurrentMember " +  
                "             ) " +  
                "           ) / " +  
                "           ( " +  
                "             KpiValue ( \"Internet Revenue\" ), " +  
                "             ParallelPeriod " +  
                "             (  " +  
                "               [Date].[Fiscal Time].[Fiscal Year], " +  
                "               1, " +  
                "               [Date].[Fiscal Time].CurrentMember " +  
                "             ) " +  
                "           )   " +  
                "         ) <=.02  " +  
                "    Then 0 " +  
                "    When KpiValue( \"Internet Revenue\" ) -  " +  
                "         ( " +  
                "           KpiValue ( \"Internet Revenue\" ), " +  
                "           ParallelPeriod " +  
                "           (  " +  
                "             [Date].[Fiscal Time].[Fiscal Year], " +  
                "             1, " +  
                "             [Date].[Fiscal Time].CurrentMember " +  
                "           ) " +  
                "         ) / " +  
                "         ( " +  
                "           KpiValue ( \"Internet Revenue\" ), " +  
                "           ParallelPeriod " +  
                "           (  " +  
                "             [Date].[Fiscal Time].[Fiscal Year], " +  
                "             1, " +  
                "             [Date].[Fiscal Time].CurrentMember " +  
                "           ) " +  
                "         )  >.02 " +  
                "    Then 1 " +  
                "    Else -1 " +  
                "End";  
    #endregion  
    kpi.TrendGraphic = "Standard Arrow";  
    kpi.StatusGraphic = "Cylinder";  
}.  
```  
  
##  <a name="Persp"></a>Perspective-Objekte  
 <xref:Microsoft.AnalysisServices.Perspective>-Objekte können mithilfe von AMO definiert werden, sie werden jedoch von der Clientanwendung verwendet, die die Daten durchsucht.  
  
 Erstellen einer <xref:Microsoft.AnalysisServices.Perspective> Objekt erfordert die folgenden Schritte aus:  
  
1.  Erstellen Sie das <xref:Microsoft.AnalysisServices.Perspective>-Objekt, und füllen Sie die grundlegenden Attribute auf.  
  
     Im Folgenden finden Sie eine Liste der grundlegenden Attribute: Name, Standardmeasure, Beschreibung und Anmerkungen.  
  
2.  Fügen Sie alle Objekte aus dem übergeordneten Cube hinzu, die für den Endbenutzer sichtbar sein sollen.  
  
     Fügen Sie Cubedimensionen (Attribute und Hierarchien), Measuregruppen (Measure und Measuregruppe), Aktionen, KPIs und Berechnungen hinzu.  
  
3.  Fügen Sie die Perspektive der Cubeauflistung hinzu, und aktualisieren Sie den Cube, da die Perspektive kein aktualisierbares Objekt ist.  
  
 Für den Test der Perspektive ist eine andere Programmanwendung erforderlich. Sie können Ihre Perspektive in testen [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
 Das folgende Codebeispiel erstellt eine Perspektive mit dem Namen "Direct Sales" für den bereitgestellten Cube.  
  
```  
static public void CreatePerspectives(Cube cube)  
{  
    Perspective perspective = cube.Perspectives.Add("Direct Sales", "Direct Sales");  
    CubeDimension dim1 = cube.Dimensions.GetByName("Date");  
    PerspectiveDimension pdim1 = perspective.Dimensions.Add(dim1.DimensionID);  
    pdim1.Attributes.Add("Date");  
    pdim1.Attributes.Add("Calendar Year");  
    pdim1.Attributes.Add("Fiscal Year");  
    pdim1.Attributes.Add("Calendar Quarter");  
    pdim1.Attributes.Add("Fiscal Quarter");  
    pdim1.Attributes.Add("Calendar Month Number");  
    pdim1.Attributes.Add("Fiscal Month Number");  
    pdim1.Hierarchies.Add("Calendar Time");  
    pdim1.Hierarchies.Add("Fiscal Time");  
  
    CubeDimension dim2 = cube.Dimensions.GetByName("Product");  
    PerspectiveDimension pdim2 = perspective.Dimensions.Add(dim2.DimensionID);  
    pdim2.Attributes.Add("Product Name");  
    pdim2.Attributes.Add("Product Line");  
    pdim2.Attributes.Add("Model Name");  
    pdim2.Attributes.Add("List Price");  
    pdim2.Attributes.Add("Size");  
    pdim2.Attributes.Add("Weight");  
    pdim2.Hierarchies.Add("Product Model Categories");  
    pdim2.Hierarchies.Add("Product Categories");  
  
    PerspectiveMeasureGroup pmg = perspective.MeasureGroups.Add("Internet Sales");  
    pmg.Measures.Add("Internet Sales Amount");  
    pmg.Measures.Add("Internet Order Quantity");  
    pmg.Measures.Add("Internet Unit Price");  
  
    pmg = perspective.MeasureGroups.Add("Reseller Sales");  
    pmg.Measures.Add("Reseler Sales Amount");  
    pmg.Measures.Add("Reseller Order Quantity");  
    pmg.Measures.Add("Reseller Unit Price");  
  
    PerspectiveAction pact = perspective.Actions.Add("Drillthrough Action");  
  
    PerspectiveKpi pkpi = perspective.Kpis.Add("Internet Revenue");  
    Cube.Update();  
}  
```  
  
##  <a name="PC"></a>ProactiveCaching-Objekte  
 <xref:Microsoft.AnalysisServices.ProactiveCaching>Objekte können mithilfe von AMO definiert werden.  
  
 Erstellen einer <xref:Microsoft.AnalysisServices.ProactiveCaching> Objekt erfordert die folgenden Schritte aus:  
  
1.  Erstellen Sie das <xref:Microsoft.AnalysisServices.ProactiveCaching>-Objekt.  
  
     Es müssen keine grundlegenden Attribute definiert werden.  
  
2.  Fügen Sie Cachespezifikationen hinzu.  
  
|Spezifikation|Beschreibung|  
|-------------------|-----------------|  
|AggregationStorage|Der Speichertyp für Aggregationen.<br /><br /> Gilt nur für Partitionen. Für Dimensionen muss **Regular.**verwendet werden.|  
|SilenceInterval|Minimale Zeit, die der Cache vorhanden ist, bevor das MOLAP-Imaging beginnt.|  
|Latenzzeit|Die Zeit zwischen der frühesten Benachrichtigung und dem Zeitpunkt, an dem die MOLAP-Images zerstört werden.|  
|SilenceOverrideInterval|Die Zeit nach einer ersten Benachrichtigung, nach der das MOLAP-Imaging unbedingt zum Einsatz kommt.|  
|ForceRebuildInterval|Die Zeit (beginnend, nachdem ein neues MOLAP-Image gelöscht wurde), nach der MOLAP-Imaging unbedingt startet (ohne Benachrichtigung).|  
|OnlineMode|Zeitpunkt, zu dem das MOLAP-Image verfügbar ist.<br /><br /> Dies kann entweder **Immediate** oder **OnCacheComplete**lauten.|  
  
1.  Fügen Sie das <xref:Microsoft.AnalysisServices.ProactiveCaching>-Objekt der übergeordneten Auflistung hinzu. Sie müssen das übergeordnete Element aktualisieren, da <xref:Microsoft.AnalysisServices.ProactiveCaching> kein aktualisierbares Objekt ist.  
  
 Das folgende Codebeispiel erstellt eine <xref:Microsoft.AnalysisServices.ProactiveCaching> Objekt in allen Partitionen der Internet Sales-Measuregruppe im Adventure Works-Cube in einer angegebenen Datenbank.  
  
```  
static public void SetProactiveCachingSettings(Database db)  
{  
    ProactiveCaching pc;  
    if (db.Cubes.ContainsName("Adventure Works") && db.Cubes.FindByName("Adventure Works").MeasureGroups.ContainsName("Internet Sales"))  
    {  
        ProactiveCachingTablesBinding pctb;  
        TableNotification tn;  
  
        MeasureGroup mg = db.Cubes.FindByName("Adventure Works").MeasureGroups.FindByName("Internet Sales");  
        foreach(Partition part in mg.Partitions)  
        {  
            pc = new ProactiveCaching();  
            pc.AggregationStorage = ProactiveCachingAggregationStorage.MolapOnly;  
            pc.SilenceInterval = TimeSpan.FromSeconds(10);  
            pc.Latency = TimeSpan.FromSeconds(-1);  
            pc.SilenceOverrideInterval = TimeSpan.FromMinutes(10);  
            pc.ForceRebuildInterval = TimeSpan.FromSeconds(-1);  
            pc.Enabled = true;  
            pc.OnlineMode = ProactiveCachingOnlineMode.OnCacheComplete;  
            pctb = new ProactiveCachingTablesBinding();  
            pctb.NotificationTechnique = NotificationTechnique.Server;  
            tn = new TableNotification("[FactInternetSales]", "dbo");  
            pctb.TableNotifications.Add( tn);  
            pc.Source = pctb;  
  
            part.ProactiveCaching = pc;  
            part.Update();  
        }  
    }  
}  
```  
  
##  <a name="Transl"></a>Übersetzungsobjekte  
 Übersetzungsobjekte können mithilfe von AMO definiert werden, sie werden jedoch von der Clientanwendung verwendet, die die Daten durchsucht. Übersetzungsobjekte sind einfach zu codierende Objekte. Übersetzungen für Objektbeschriftungen werden von Paaren von Gebietsschemabezeichnern und übersetzten Beschriftungen bereitgestellt. Für alle Beschriftungen können mehrere Übersetzungen aktiviert werden. Übersetzungen können bereitgestellt werden, für die meisten [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Objekte, z. B. Dimensionen, Attribute, Hierarchien, Cubes, Measuregruppen, Measures und andere.  
  
 Im folgenden Codebeispiel wird eine spanische Übersetzung für den Namen des Attributs "Product Name" bereitgestellt.  
  
```  
static public void CreateTranslations(Database db)  
{  
    //Spanish Tranlations for Product Category in Product Dimension  
    Dimension dim = db.Dimensions["Product"];  
    DimensionAttribute atr = dim.Attributes["Product Name"];  
    Translation tran = atr.Translations.Add(3082);  
    tran.Caption = "Nombre Producto";  
  
    dim.Update(UpdateOptions.ExpandFull);  
  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.AnalysisServices>   
 [Einführung in AMO-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [AMO-OLAP-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-olap-classes.md)   
 [Logische Architektur &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Datenbankobjekte &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [Verarbeiten eines mehrdimensionalen Modells &#40; Analysis Services &#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Installieren von Sample Data and Projects für Analysis Services-mehrdimensionale Modellierung-Lernprogramm](../../../analysis-services/install-sample-data-and-projects.md)  
  
  

