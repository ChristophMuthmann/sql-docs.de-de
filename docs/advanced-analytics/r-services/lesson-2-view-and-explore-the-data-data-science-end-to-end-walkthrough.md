---
title: "Lektion 2: Anzeigen und Durchsuchen von Daten (Exemplarische Data Science-Ende-zu-Ende-Vorgehensweise) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: d3835d6d-e68b-486d-81a0-81b717cc6134
caps.latest.revision: 32
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 26
---
# Lektion 2: Anzeigen und Durchsuchen von Daten (Exemplarische Data Science-Ende-zu-Ende-Vorgehensweise)
Durchsuchen von Daten ist ein wichtiger Bestandteil beim Modellieren von Daten und umfasst das Überprüfen der Zusammenfassung von Datenobjekten in Analysen sowie die Visualisierung von Daten. In dieser Lektion werden Sie Datenobjekte durchsuchen und Plots generieren, mit [!INCLUDE[tsql](../../includes/tsql-md.md)] und R-Funktionen, die in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]enthalten sind.  
  
Anschließend generieren Sie Plots zum Visualisieren der Daten mithilfe der neue Funktionen von Paketen, die mit [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]installiert werden.  
  
> [!TIP]  
> Sind Sie bereits ein R-Meister?  
>   
> Da Sie nun alle Daten heruntergeladen und die Umgebung vorbereitet haben, können Sie das vollständige R-Skript in RStudio oder in einer anderen Umgebung ausführen und die Funktionalität selbst ausprobieren. Öffnen Sie einfach die Datei RSQL_Walkthrough.R, markieren Sie einzelne Zeilen und führen Sie aus – oder das gesamte Skript als eine Demo.  
>   
> Weitere Informationen zu RevoScaleR-Funktionen und Tipps zum Arbeiten mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten in R erhalten Sie in diesem Tutorial. Es verwendet genau das gleiche Skript.  
  
## <a name="verify-downloaded-data-using-sql"></a>Überprüfen Sie die heruntergeladenen Daten mit SQL  
Stellen Sie zuerst fest, dass Ihre Daten korrekt geladen wurden.  
  
1.  Stellen Sie eine Verbindung zu Ihrer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz her.  
  
    Sie können eine Vielzahl von Tools zum Verbinden und Anzeigen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbanken verwenden.  
  
    -   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]    
    -   Server-Explorer in Visual Studio  
  
2.  Erweitern Sie die Datenbank, die Sie erstellt haben. Die folgende Abbildung zeigt die neue Datenbank, Tabellen und Funktionen in **Server-Explorer**.  
  
    ![new database objects created by script](../../advanced-analytics/r-services/media/rsql-e2e-ssms-newobjects.PNG "new database objects created by script")  
  
3.  Sie können auch einfache Abfragen auf die Daten anwenden. Klicken Sie beispielsweise in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]mit der rechten Maustaste auf die Tabelle und wählen Sie **Die ersten 1000 Zeilen auswählen** , um diese Abfrage zu generieren und auszuführen:  
  
    ```  
    SELECT TOP 1000 * FROM [dbo].[nyctaxi_sample]  
    ```  
    Wenn keine Daten in der Tabelle nicht angezeigt werden, wechseln Sie im vorherigen Abschnitt zu [Problembehandlung](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md).
      
4.  Um Schema und Datentypen der Daten anzuzeigen, können Sie die System-Verwaltungssichten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwenden.  
  
    ```  
    SELECT TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME, COLUMN_NAME, COLUMN_DEFAULT  
    FROM [TaxiSample].INFORMATION_SCHEMA.COLUMNS  
    WHERE TABLE_NAME = N'nyctaxi_sample';  
    ```  
  
    > [!TIP]  
    > Zum Abrufen von Details wie die Datentabelle erstellt wurde, können Sie auch das Skript `create-db-tb-upload-data.sql`überprüfen.  
  
### <a name="generate-summaries-using-sql"></a>Zusammenfassungen mit SQL generieren  
Eine der Stärken von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und damit eine gute Ergänzung zu R ist die schnelle Verarbeitung satzbasierter Berechnungen.  Der Code, der die Tabelle für diese exemplarische Vorgehensweise erstellt habt, hat auch einen [Columnstore-Index](../Topic/Columnstore%20Indexes%20Guide.md) angewendet, um Berechnungen weiter zu beschleunigen.   
  
```  
SELECT DISTINCT [passenger_count]  
    , ROUND (SUM ([fare_amount]),0) as TotalFares   
    , ROUND (AVG ([fare_amount]),0) as AvgFares  
FROM [dbo].[nyctaxi_sample]  
GROUP BY [passenger_count]   
ORDER BY  AvgFares desc  
```  

In den nächsten Schritten verwenden Sie R, um einige komplexere Zusammenfassungen und Zeichnungen mithilfe der Daten in SQL Server zu generieren.  
  
## <a name="next-steps"></a>Nächste Schritte  
[Anzeigen und Zusammenfassen von Daten mithilfe von R &#40;Lückenlose exemplarische Data Science-Vorgehensweise&#41;](../../advanced-analytics/r-services/view-and-summarize-data-using-r-data-science-end-to-end-walkthrough.md)  
  
[Erstellen von Graphen und Diagrammen mit R &#40;Lückenlose exemplarische Data Science-Vorgehensweise&#41;](../../advanced-analytics/r-services/create-graphs-and-plots-using-r-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>Vorherige Lektion  
[Lektion 1: Vorbereiten der Daten &#40;Lückenlose exemplarische Data Science-Vorgehensweise&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
## <a name="see-also"></a>Siehe auch  
[Beschreibung von Columnstore-Indizes](../Topic/Columnstore%20Indexes%20Guide.md)  
  
  
  
