---
title: "Analysieren in Excel (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2f17b4df-eea2-48c7-a1f2-a3fb7748c15f
caps.latest.revision: 19
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 19
---
# Analysieren in Excel (SSAS – tabellarisch)
  Die Funktion In Excel analysieren in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]erleichtert Entwicklern tabellarischer Modelle die schnelle Analyse von Modellprojekten während der Entwicklung. Über die Funktion In Excel analysieren wird Microsoft Excel geöffnet; sie stellt eine Datenquellenverbindung mit der Arbeitsbereichsdatenbank des Modells her und fügt automatisch eine PivotTable in das Arbeitsblatt ein. Objekte der Arbeitsbereichsdatenbank (Tabellen, Spalten und Measures) sind als Felder in der PivotTable-Feldliste enthalten. Objekte und Daten können dann innerhalb des Kontexts des effektiven Benutzers oder der Rolle und Perspektive angezeigt werden.  
  
 In diesem Thema wird davon ausgegangen, dass Sie bereits mit Microsoft Excel, PivotTables und PivotCharts vertraut sind. Weitere Informationen zur Verwendung von Excel finden Sie in der Excel-Hilfe.  
  
 Abschnitte in diesem Thema:  
  
-   [Vorteile](#bkmk_benefits)  
  
-   [Verwandte Aufgaben](#bkmk_rt)  
  
##  <a name="bkmk_benefits"></a> Vorteile  
 Die Funktion In Excel analysieren bietet Modellentwicklern die Möglichkeit, die Effizienz eines Modellprojekts unter Verwendung der verbreiteten Datenanalyseanwendung Microsoft Excel zu testen. Um die Funktion „In Excel analysieren“ zu verwenden, muss Microsoft Office 2003 oder höher auf demselben Computer wie [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]installiert sein.  
  
> [!NOTE]  
>  Wenn Office nicht auf demselben Computer wie [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]installiert ist, können Sie Excel auf einem anderen Computer verwenden, um eine Verbindung mit der Arbeitsbereichsdatenbank als Datenquelle herzustellen. Sie können dem Arbeitsblatt dann manuell eine PivotTable hinzufügen.  
  
 Durch die Funktion In Excel analysieren wird Excel geöffnet und eine neue Excel-Arbeitsmappe (.xls) erstellt. Eine Datenverbindung von der Arbeitsmappe zur Modellarbeitsbereichsdatenbank wird erstellt. Dem Arbeitsblatt wird eine leere PivotTable hinzugefügt, und die PivotTable-Feldliste wird mit Modellobjektmetadaten aufgefüllt. Sie können der PivotTable anschließend Anzeigedaten und Slicer hinzufügen.  
  
 Wenn die Funktion In Excel analysieren mit der Standardeinstellung verwendet wird, entspricht das aktuell angemeldete Benutzerkonto dem effektiven Benutzer. Dieses Konto ist in der Regel ein Administrator und verfügt über keinerlei Einschränkungen für die Modellierung von Objekten oder Daten. Sie können jedoch einen anderen effektiven Benutzernamen oder eine Rolle angeben. Auf diese Weise können Sie ein Modellprojekt in Excel innerhalb des Kontexts eines spezifischen Benutzers bzw. einer spezifischen Rolle durchsuchen. Für das Festlegen des effektiven Benutzers stehen folgende Optionen zur Verfügung:  
  
 **Aktueller Windows-Benutzer**  
 Verwendet das Benutzerkonto, unter dem Sie gerade angemeldet sind.  
  
 **Anderer Windows-Benutzer**  
 Verwendet einen angegebenen Windows-Benutzernamen anstatt den Namen des aktuell angemeldeten Benutzers. Zur Verwendung eines anderen Windows-Benutzers ist kein Kennwort erforderlich. Objekte und Daten können nur in Excel innerhalb des Kontexts des effektiven Benutzernamens angezeigt werden. In Excel können keine Änderungen an Modellobjekten oder -daten vorgenommen werden.  
  
 **Rolle**  
 Eine Rolle wird verwendet, um Benutzerberechtigungen für die Objektmetadaten und die Daten zu definieren. Rollen werden normalerweise für einen bestimmten Windows-Benutzer oder eine Windows-Benutzergruppe definiert. Bestimmte Rollen können zusätzliche Filter auf Zeilenebene einschließen, die in einer DAX-Formel definiert sind. Wenn Sie die Funktion In Excel analysieren verwenden, können Sie optional eine zu verwendende Rolle auswählen. Objektmetadaten und Datensichten werden durch Berechtigungen und Filter eingeschränkt, die für die Rolle definiert sind. Weitere Informationen finden Sie unter [Erstellen und Verwalten von Rollen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md).  
  
 Zusätzlich zum effektiven Benutzer oder der Rolle können Sie eine Perspektive angeben. Perspektiven ermöglichen Modellentwicklern die Definition von Modellobjekt- und Datensichten für bestimmte Geschäftsszenarien. Standardmäßig wird keine Perspektive verwendet. Um eine Perspektive mit In Excel analysieren zu verwenden, müssen Perspektiven bereits mit dem Dialogfeld Perspektiven in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]definiert worden sein. Wenn eine Perspektive angegeben wird, enthält die PivotTable-Liste nur die in der Perspektive ausgewählten Objekte. Weitere Informationen finden Sie unter [Erstellen und Verwalten von Perspektiven &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md).  
  
##  <a name="bkmk_rt"></a> Verwandte Aufgaben  
  
|**Thema**|**Description**|  
|---------------|---------------------|  
|[Analysieren eines Tabellenmodells in Excel &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/analyze-a-tabular-model-in-excel-ssas-tabular.md)|In diesem Thema wird Folgendes beschrieben: Öffnen von Excel über die Funktion In Excel analysieren im Modell-Designer, Erstellen einer Datenquellenverbindung mit der Arbeitsbereichsdatenbank des Modells und Hinzufügen einer PivotTable zum Arbeitsblatt.|  
  
## Siehe auch  
 [Analysieren eines Tabellenmodells in Excel &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/analyze-a-tabular-model-in-excel-ssas-tabular.md)   
 [Rollen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/roles-ssas-tabular.md)   
 [Perspektiven &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)  
  
  