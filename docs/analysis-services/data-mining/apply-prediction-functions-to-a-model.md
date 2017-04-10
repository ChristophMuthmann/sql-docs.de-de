---
title: "Anwenden von Vorhersagefunktionen auf ein Modell | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Miningmodellvorhersage [Analysis Services], Auswählen von Miningmodellen"
ms.assetid: cf9a97e2-c249-441b-af12-c977c1a91c44
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 17
---
# Anwenden von Vorhersagefunktionen auf ein Modell
  Zum Erstellen einer Vorhersageabfrage in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining müssen Sie zuerst das Miningmodell auswählen, auf dem die Abfrage basieren soll. Sie können jedes Miningmodell auswählen, das im aktuellen Projekt vorhanden ist.  
  
 Nachdem Sie ein Modell ausgewählt haben, fügen Sie der Abfrage eine *Vorhersagefunktion* hinzu. Eine Vorhersagefunktion kann verwendet werden, um eine Vorhersage zu erhalten. Aber Sie können auch Vorhersagefunktionen hinzufügen, die damit zusammenhängenden Statistiken zurückgeben, z. B. die Wahrscheinlichkeit des vorhergesagten Wert oder Informationen, die beim Generieren der Vorhersage verwendet wurden.  
  
 Vorhersagefunktionen können die folgenden Typen von Werten zurückgeben:  
  
-   Den Namen des vorhersagbaren Attributs und den vorhergesagten Wert  
  
-   Statistiken zur Verteilung und der Varianz der vorhergesagten Werte  
  
-   Die Wahrscheinlichkeit eines angegebenen Ergebnisses oder von allen möglichen Ergebnissen  
  
-   Die obersten oder untersten Ergebnisse oder Werte  
  
-   Werte, die einem bestimmten Knoten, Objekt oder Attribut zugeordnet sind  
  
 Der Typ der Vorhersagefunktionen, die verfügbar sind, hängt vom Typ des Modells ab, mit dem Sie arbeiten. Beispielsweise können Vorhersagefunktionen, die auf Entscheidungsstrukturmodelle angewendet werden, Regeln und Knotenbeschreibungen zurückgeben. Vorhersagefunktionen für Zeitreihenmodelle können die Verzögerung und andere für Zeitreihen spezifische Informationen zurückgeben.  
  
 Eine Liste der Vorhersagefunktionen, die für fast alle Modelltypen unterstützt werden, finden Sie unter [Allgemeine Vorhersagefunktionen &#40;DMX&#41;](../../dmx/general-prediction-functions-dmx.md).  
  
 Beispiele zum Abfragen eines bestimmten Typs von Miningmodell finden Sie im Algorithmusreferenzthema unter [Data Mining-Algorithmen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
### Auswählen eines Miningmodells für die Vorhersage  
  
1.  Klicken Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mit der rechten Maustaste auf das Modell, und wählen Sie **Vorhersageabfrage erstellen** aus.  
  
     - oder -  
  
     Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf die Registerkarte **Miningmodellvorhersage**und anschließend auf **Modell auswählen** in der Tabelle  **Miningmodell** .  
  
2.  Wählen Sie im Dialogfeld **Miningmodell auswählen** ein Miningmodell aus, und klicken Sie dann auf **OK**.  
  
     Sie können jedes Modell in der aktuellen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank auswählen. Damit eine Abfrage mithilfe eines Modells in einer anderen Datenbank erstellt werden kann, müssen Sie entweder ein neues Abfragefenster im Kontext dieser Datenbank öffnen oder die Projektmappendatei öffnen, die das Modell enthält.  
  
### Hinzufügen von Vorhersagefunktionen zu einer Abfrage  
  
1.  Konfigurieren Sie im **Generator für Vorhersageabfragen**die für die Vorhersage verwendeten Eingabedaten, und zwar entweder durch das Bereitstellen von Werten im Dialogfeld **SINGLETON-Abfrageeingabe** oder indem Sie einer externen Datenquelle das Modell zuordnen.  
  
     Weitere Informationen finden Sie unter [Auswählen und Zuordnen von Eingabedaten für eine Vorhersageabfrage](../../analysis-services/data-mining/choose-and-map-input-data-for-a-prediction-query.md).  
  
    > [!WARNING]  
    >  Es ist nicht erforderlich, dass Sie Eingaben bereitstellen, um Vorhersagen zu generieren. Liegt keine Eingabe vor, gibt der Algorithmus im Allgemeinen den am wahrscheinlichsten vorhergesagten Wert über alle möglichen Eingaben zurück.  
  
2.  Klicken Sie auf die Spalte **Quelle** , und wählen Sie einen Wert aus der Liste aus:  
  
    |||  
    |-|-|  
    |**\<Name des Modells>**|Aktivieren Sie diese Option, um Werte vom Miningmodell in die Ausgabe einzuschließen. Sie können nur vorhersagbaren Spalten hinzufügen.<br /><br /> Wenn Sie eine Spalte aus dem Modell hinzufügen, ist das zurückgegebene Ergebnis die nicht unterschiedliche Liste der Werte in dieser Spalte.<br /><br /> Die Spalten, die Sie mit dieser Option hinzufügen, sind im SELECT-Teil der resultierenden DMX-Anweisung enthalten.|  
    |**Vorhersagefunktion**|Aktivieren Sie diese Option, um eine Liste von Vorhersagefunktionen zu durchsuchen.<br /><br /> Dem SELECT-Teil der resultierenden DMX-Anweisung werden die von Ihnen ausgewählten Werte oder die Funktionen hinzugefügt.<br /><br /> Die Liste der Vorhersagefunktionen wird durch den von Ihnen ausgewählten Modelltyp weder gefiltert noch eingeschränkt. Wenn Sie sich nicht sicher sind, ob die Funktion vom aktuellen Modelltyp unterstützt wird, können Sie demzufolge der Liste einfach die Funktion hinzufügen und anzeigen, ob ein Fehler vorliegt.<br /><br /> Listenelemente, denen $ (z. B. $ADJUSTEDPROBABILITY) vorangestellt werden, stellen Spalten von der geschachtelten Tabelle dar, die ausgegeben wird, wenn Sie die Funktion **PredictHistogram** verwenden. Dies sind Verknüpfungen, mit denen Sie eine einzelne Spalte, aber keine geschachtelte Tabelle zurückgeben können.|  
    |**Benutzerdefinierter Ausdruck**|Aktivieren Sie diese Option, um einen benutzerdefinierten Ausdruck einzugeben und der Ausgabe dann einen Alias zuzuweisen.<br /><br /> Dem SELECT-Teil der resultierenden DMX-Vorhersageabfrage wird der benutzerdefinierte Ausdruck hinzugefügt.<br /><br /> Diese Option ist nützlich, wenn Sie Text für die Ausgabe mit jeder Zeile hinzufügen, VB-Funktionen oder benutzerdefinierte gespeicherte Prozeduren aufrufen möchten.<br /><br /> Informationen zum Verwenden von VBA- und Excel-Funktionen von DMX aus finden Sie unter [VBA-Funktionen in MDX und DAX](../../mdx/vba-functions-in-mdx-and-dax.md).|  
  
3.  Wechseln Sie, nachdem Sie jede Funktion oder jeden Ausdruck hinzugefügt haben, zur DMX-Ansicht, um zu sehen, wie die Funktion in der DMX-Anweisung hinzugefügt wurde.  
  
    > [!WARNING]  
    >  Der Generator für Vorhersageabfragen überprüft die DMX erst, wenn Sie auf **Ergebnisse**klicken. Sie werden öfters feststellen, dass der vom Abfrage-Generator erzeugte Ausdruck kein gültiger DMX-Wert ist. Dies liegt normalerweise an einer Spalte, die sich nicht auf die vorhersagbare Spalte bezieht, oder an dem Versuch, eine Spalte in einer geschachtelten Tabelle vorherzusagen, die eine untergeordnete SELECT-Anweisung erfordert. Hierkönnen Sie zur DMX-Ansicht wechseln und die Anweisung weiterhin bearbeiten.  
  
### Beispiel: Erstellen einer Abfrage für ein Clusteringmodell  
  
1.  Wenn Sie über kein Clustermodell für das Erstellen dieser Beispielabfrage verfügen, erstellen Sie das Modell [TM_Clustering] mithilfe des [Tutorials zu Data Mining-Grundlagen](../Topic/Basic%20Data%20Mining%20Tutorial.md).  
  
2.  Klicken Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mit der rechten Maustaste auf das Modell, [TM_Clustering]. und wählen Sie **Vorhersageabfrage erstellen** aus.  
  
3.  Klicken Sie im Menü **Miningmodell** auf **SINGLETON-Abfrage**.  
  
4.  Legen Sie im Dialogfeld **SINGLETON-Abfrageeingabe** die folgenden Werte als Eingaben fest:  
  
    -   Geschlecht = M  
  
    -   Arbeitsweg = 8–16 Kilometer (5–10 Meilen)  
  
5.  Wählen Sie im Abfrageraster für **Quelle** „TM_Clustering-Miningmodell“ aus, und fügen Sie die Spalte „[Bike Buyer]“ hinzu.  
  
6.  Wählen Sie **Vorhersagefunktion**als **Quelle**aus, und fügen Sie die Funktion **Cluster**hinzu.  
  
7.  Wählen Sie **Vorhersagefunktion** für **Quelle** aus, fügen Sie die Funktion **PredictSupport** hinzu, und ziehen Sie die Modellspalte „[Bike Buyer]“ in das Feld **Kriterium/Argument**. Geben Sie in der Spalte **Alias** die Zeichenfolge **Support** ein.  
  
     Kopieren Sie den Ausdruck, der die Vorhersagefunktion und den Spaltenverweis vom Feld **Kriterium/Argument** darstellt.  
  
8.  Wählen Sie für **Quelle**die Option **Benutzerdefinierter Ausdruck**aus, geben Sie einen Alias ein, und verweisen Sie dann in Excel mit der folgenden Syntax auf die CEILING-Funktion:  
  
    ```  
    Excel![CEILING](<arguments) as <return type>  
    ```  
  
     Fügen Sie den Spaltenverweis als Argument zur Funktion ein.  
  
     Der folgende Ausdruck gibt beispielsweise den CEILING vom Unterstützungswert zurück:  
  
    ```  
    EXCEL!CEILING(PredictSupport([TM_Clustering].[Bike Buyer]),2)  
    ```  
  
     Geben Sie in der Spalte **Alias** die Zeichenfolge CEILING ein.  
  
9. Klicken Sie auf **Zur Abfragetextsicht wechseln** , um die generierte DMX-Anweisung zu überprüfen. Klicken Sie dann auf **Zur Abfrageergebnissicht wechseln** , um die Spaltenausgabe durch die Vorhersageabfrage zu sehen.  
  
     In der folgenden Tabelle werden die erwarteten Ergebnisse angezeigt:  
  
    |Bike Buyer|$Cluster|Alias|CEILING|  
    |----------------|--------------|-------------|-------------|  
    |0|Cluster 8|954|953.948638926372|  
  
 Wenn Sie an anderen Stellen weitere Klauseln in der Anweisung hinzufügen möchten, – wenn Sie beispielsweise eine WHERE-Klausel hinzufügen möchten – können Sie es nicht mit dem Raster hinzufügen, sondern müssen zuerst zur DMX-Ansicht wechseln.  
  
## Siehe auch  
 [Data Mining-Abfrage](../../analysis-services/data-mining/data-mining-queries.md)  
  
  