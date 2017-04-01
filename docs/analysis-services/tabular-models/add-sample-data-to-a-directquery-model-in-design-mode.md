---
title: "Hinzuf&#252;gen von Beispieldaten zu einem DirectQuery-Modell im Entwurfsmodus | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1af1e823-85aa-4319-a93f-98b35f7c7322
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Hinzuf&#252;gen von Beispieldaten zu einem DirectQuery-Modell im Entwurfsmodus
 Im DirectQuery-Modus werden Tabellenpartitionen entweder zum Erstellen von Beispieldatenteilmengen verwenden, die während des Modellentwurfs genutzt werden, oder zum Erstellen von Alternativen einer vollständigen Datenansicht.
 
 Bei der Bereitstellung eines DirectQuery-Tabellenmodells ist nur eine Partition pro Tabelle erlaubt, und diese Partition muss bei Bedarf eine vollständige Datenansicht sein. Bei jeder zusätzlichen Partition handelt es sich entweder um einen Ersatz für eine vollständige Datenansicht oder um Beispieldaten. In diesem Thema wird das Erstellen einer Beispielpartition mit einer Teilmenge von Daten beschrieben.
 
 Standardmäßig enthält die Arbeitsdatenbank des Modells keine Daten, wenn ein Tabellenmodell im DirectQuery-Modus in SSDT erstellt wird. Es gibt eine Standardpartition für jede Tabelle, und diese Partition übermittelt alle Abfragen an die Datenquelle. 
  
Sie können jedoch eine kleinere Menge an Beispieldaten der Arbeitsdatenbank Ihres Modells hinzufügen, die zur Entwurfszeit verwendet wird. Beispieldaten werden über eine Abfrage auf eine Beispielpartition angegeben, die nur während des Entwurfs verwendet wird. Sie werden mit dem Modell im Arbeitsspeicher zwischengespeichert. Dies hilft Ihnen bei der Überprüfung von Modellierungsentscheidungen, ohne dabei die Datenquelle zu beeinträchtigen. Sie können Ihre Modellierungsentscheidungen mit dem Beispieldataset überprüfen, wenn Sie es mit **In Excel analysieren** in SQL Server Data Tools (SSDT) verwenden, oder es aus anderen Clientanwendungen stammt, die eine Verbindung mit Ihrer Arbeitsbereichsdatenbank herstellen können.  
  
> [!TIP]  
>  Selbst im DirectQuery-Modus bei einem leeren Modell können Sie sich immer für jede Tabelle ein kleines eingebautes Rowset anzeigen lassen. Klicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] auf **Tabelle** > **Tabelleneigenschaften**, um das Dataset mit 50 Zeilen anzuzeigen.  
  
## Erstellen einer Beispielpartition
 Diese Anleitungen gelten für tabellarische Modelle, mit dem Kompatibilitätsgrad 1200 erstellt oder auf diesen upgegradet werden. Modelle mit niedrigeren Kompatibilitätsgraden verwenden verschiedene Eigenschaften zum Abrufen zwischengespeicherter Daten. Zusätzliche Beschreibungen finden Sie unter [Aktivieren des DirectQuery-Modus in SSMS](../../analysis-services/tabular-models/enable-directquery-mode-in-ssms.md).  
  
1.  Klicken Sie in SQL Server Data Tools unter „Diagramm“ oder „Datenansicht“ auf eine Faktentabelle, um deren Eigenschaftenseite zu öffnen. Faktentabellen geben die aggregierten numerischen Daten und die Measures in Ihrem Modell an. Sie verfügen möglicherweise über mehr als eine Faktentabelle.  
  
2.  Klicken Sie auf **Tabelle** > **Eigenschaften**, um das Dialogfeld „Partitionsverwaltung“ zu öffnen.  
  
    Beachten Sie, dass die Standardpartition **(Direct Query) \<Tabellenname>** ist. Dies ist die vollständige Datenansicht. Löschen Sie diese Partition nicht! Diese Partition wird verwendet, wenn das Modell bereitgestellt wird.  
  
4.  Wählen Sie die Partition aus, und klicken Sie anschließend auf **Kopieren**.  

    Dadurch wird eine Kopie der Standardpartition erstellt. Diese Kopie enthält jedoch Beispieldaten, die Sie in einer Abfrage angeben. Beispiel:
  
     ![ssas_tabularproject_copypartition](../../analysis-services/tabular-models/media/ssas-tabularproject-copypartition.jpg "ssas_tabularproject_copypartition")  
  
5.  Wählen Sie die kopierte Partition aus, und klicken Sie anschließend auf die Schaltfläche **SQL-Abfrage-Editor**, um einen Filter hinzuzufügen. Reduzieren Sie die Größe Ihrer Beispieldaten während der Erstellung des Modells. Wenn Sie z.B. **FactInternetSales** aus AdventureWorksDW auswählen, kann Ihr Filter wie Folgt aussehen:  
  
    ```  
    SELECT [dbo].[FactInternetSales].* FROM [dbo].[FactInternetSales]  
    JOIN DimSalesTerritory as ST  
    ON ST.SalesTerritoryKey = FactInternetSales.SalesTerritoryKey  
    WHERE ST.SalesTerritoryGroup='North America';  
    ```  
  
6.  Klicken Sie auf **Überprüfen**, um die Syntaxfehler zu überprüfen.  
  
     Beachten Sie, dass im DirectQuery-Modus zusätzliche zu den Schaltflächen **Neu**, **Kopieren** und **Löschen** im Dialogfeld der Partition auch eine Umschaltfläche existiert, die alternativ **Als Beispiel festlegen** oder **Als DirectQuery festlegen** liest.  
  
     Nur eine Partition kann die DirectQuery-Partition sein. Sie können dies steuern, indem Sie eine Partition auswählen, die für die Tabelle definiert ist und anschließend auf **Als Beispiel festlegen** klicken.  
  
7.  Verarbeiten der Tabelle.  
  


  
  