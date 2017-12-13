---
title: Erstellen eine neue OLAP-Miningstruktur | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], OLAP
- mining structures [Analysis Services], creating
- OLAP [Analysis Services], mining models
ms.assetid: 368f4273-a016-4748-bcb6-505a3e745af3
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ede498333c2fa7c1967d62e2d403d09a6d50acde
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="create-a-new-olap-mining-structure"></a>Erstellen einer neuen OLAP-Miningstruktur
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Sie können Data Mining-Assistenten in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eine Miningstruktur erstellen, die Daten aus einem mehrdimensionalen Modell verwendet. Miningmodelle, die auf OLAP-Cubes basieren, können die Spalte und Werte in Faktentabellen, Dimensionen und Measuregruppen als Attribute für die Analyse verwenden.  
  
### <a name="to-create-a-new-olap-mining-structure"></a>So erstellen Sie eine neue OLAP-Miningstruktur  
  
1.  Klicken Sie im Projektmappen-Explorer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]mit der rechten Maustaste auf den Ordner **Miningstrukturen** in einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt. Klicken Sie anschließend auf **Neue Miningstruktur** , um den Data Mining-Assistenten zu öffnen.  
  
2.  Klicken Sie auf der Seite **Willkommen** auf **Weiter**.  
  
3.  Wählen Sie auf der Seite **Definitionsmethode auswählen** die Option **Aus vorhandenem Cube**aus, und klicken Sie dann auf **Weiter**.  
  
     Wenn Sie einen Fehler mit der Meldung Eine Liste der unterstützten Data Mining-Algorithmen kann nicht abgerufen werden erhalten, öffnen Sie das Dialogfeld **Projekteigenschaften** , und überprüfen Sie, ob Sie den Namen einer Analysis Services-Instanz angegeben haben, die mehrdimensionale Modelle unterstützt. Sie können keine Miningmodelle für eine Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] erstellen, die Tabellenmodellierung unterstützt.  
  
4.  Legen Sie auf der Seite **Data Mining-Struktur erstellen** fest, ob Sie nur eine Miningstruktur oder eine Miningstruktur und ein verknüpftes Miningmodell erstellen möchten. Im Allgemeinen ist es einfacher, gleichzeitig ein Miningmodell zu erstellen, damit Sie aufgefordert werden können, erforderliche Spalten einzuschließen.  
  
     Zum Erstellen eines Miningmodells wählen Sie den Data Mining-Algorithmus aus, den Sie verwenden wollen, und klicken Sie dann auf **Weiter**. Weitere Informationen zur Auswahl des Algorithmus finden Sie unter[Data Mining-Algorithmen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
5.  Suchen Sie auf der Seite **Quellcubedimension auswählen** unter **Quellcubedimension auswählen**die Dimension, die den Großteil der Falldaten enthält.  
  
     Wenn Sie zum Beispiel Kundengruppierungen identifizieren möchten, können Sie die Customer-Dimension auswählen. Wenn Sie Käufe im Rahmen von Transaktionen analysieren, können Sie ggf. die Dimension Internet Sales Order Details verwenden. Sie sind nicht auf die Verwendung ausschließlich der Daten in dieser Dimension beschränkt, doch die Daten sollten wichtige Attribute enthalten, die Sie in der Analyse verwenden möchten.  
  
     Klicken Sie auf **Weiter**.  
  
6.  Wählen Sie auf der Seite **Fallschlüssel auswählen** unter **Attribute**das Attribut aus, das der Schlüssel der Miningstruktur sein soll, und klicken Sie dann auf **Weiter**.  
  
     In der Regel ist das Attribut, das als Schlüssel für die Miningstruktur verwendet wird, auch ein Schlüssel für die Dimension und wird vorab ausgewählt.  
  
7.  Wählen Sie auf der Seite **Spalten auf Fallebene auswählen** unter **Verknüpfte Attribute und Measures**die Attribute und Measures aus, die Werte enthalten, die Sie der Miningstruktur als Falldaten hinzufügen möchten. Klicken Sie auf **Weiter**.  
  
8.  Legen Sie auf der Seite **Verwendung der Miningmodellspalte angeben** unter **Miningmodellstruktur**zuerst die vorhersagbare Spalte fest, und wählen Sie anschließend die als Eingaben zu verwendenden Spalten aus.  
  
    -   Aktivieren Sie das Kontrollkästchen in der äußersten linken Spalte, um die Daten in die Miningstruktur einzuschließen. Sie können Spalten in die Struktur einschließen, die Sie zur Referenz, aber nicht für Analysezwecke verwenden.  
  
    -   Aktivieren Sie das Kontrollkästchen in der Spalte **Eingabe** , um das Attribut als Variable in der Analyse zu verwenden.  
  
    -   Aktivieren Sie das Kontrollkästchen in der Spalte **Vorhersagen** nur für vorhersagbare Attribute.  
  
     Spalten, die Sie als Schlüssel festgelegt haben, können nicht für Eingaben oder Vorhersagen verwendet werden.  
  
     Klicken Sie auf **Weiter**.  
  
9. Auf der Seite **Verwendung der Miningmodellspalte angeben** können Sie der Miningstruktur auch geschachtelte Tabellen hinzufügen bzw. daraus entfernen. Verwenden Sie dazu die Optionen **Geschachtelte Tabellen hinzufügen** und **Geschachtelte Tabellen**.  
  
     In einem OLAP-Miningmodell ist eine geschachtelte Tabelle ein anderer Datensatz innerhalb des Cubes, der eine 1:n-Beziehung mit der Dimension besitzt, die die Fallattribute darstellt. Wenn das Dialogfeld geöffnet wird, werden daher vorab Measuregruppen ausgewählt, die bereits mit der als Falltabelle ausgewählten Dimension verknüpft sind. An dieser Stelle wählen Sie eine andere Dimension aus, die zusätzliche Informationen enthält, die für die Analyse hilfreich sind.  
  
     Wenn Sie zum Beispiel Kunden analysieren, würden Sie als Falltabelle die [Customer]-Dimension verwenden. Für die geschachtelte Tabelle können Sie die Gründe hinzufügen, die von Kunden bei einem Kauf angegeben wurden. Diese Option ist in der Dimension [Sales Reason] enthalten.  
  
     Wenn Sie geschachtelte Daten hinzufügen, müssen Sie zwei zusätzliche Spalten angeben:  
  
    -   Der Schlüssel der geschachtelten Tabelle: Der Schlüssel sollte vorab auf der Seite **Schlüssel der geschachtelten Tabelle auswählen**ausgewählt werden.  
  
    -   Die Attribute oder für die Analyse zu verwendenden Attribute: Die Seite **Geschachtelte Tabellenspalten auswählen**enthält eine Liste der Measures und Attribute in der Auswahl der geschachtelten Tabellen.  
  
        -   Überprüfen Sie für jedes Attribut, das Sie ins Modell einschließen, das Feld in der linken Spalte.  
  
        -   Wenn Sie das Attribut nur zu Analysezwecken verwenden möchten, aktivieren Sie das Kontrollkästchen **Eingabe**.  
  
        -   Wenn Sie die Spalte als eines der vorhersagbaren Attribute für das Modell einschließen möchten, wählen Sie die Option **Vorhersagen**aus.  
  
        -   Jedes Element, das Sie in die Struktur einschließen, aber nicht als Eingabe oder vorhersagbares Attribut angeben, wird der Struktur mit dem Kennzeichen **Ignore**hinzugefügt, d. h., dass die Daten beim Erstellen des Modells verarbeitet, jedoch nicht in der Analyse verwendet werden, sondern nur zu Drillthroughzwecken zur Verfügung stehen. Dies kann hilfreich sein, wenn Sie Details wie z. B. Kundennamen einschließen möchten, ohne sie jedoch in der Analyse zu verwenden.  
  
     Klicken Sie auf **Fertig stellen** , um den Teil des Assistenten zu schließen, in dem geschachtelte Tabellen verwendet werden. Sie können den Vorgang wiederholen, um mehrere geschachtelte Spalten hinzuzufügen.  
  
10. Legen Sie auf der Seite **Inhalt und Datentyp der Spalten angeben** unter **Miningmodellstruktur**den Inhalts- und den Datentyp für jede Spalte fest.  
  
    > [!NOTE]  
    >  OLAP-Miningmodelle unterstützen nicht die **Erkennen** -Funktion, mit der automatisch erkannt wird, ob eine Spalte kontinuierliche oder diskrete Daten enthält.  
  
     Klicken Sie auf **Weiter**.  
  
11. Auf der Seite **Quellcube in Slices aufteilen** können Sie die Daten filtern, die zum Erstellen der Miningstruktur verwendet werden.  
  
     Durch Aufteilen des Cubes können Sie die Daten für die Erstellung des Modells beschränken. Zum Beispiel können Sie separate Modelle für jeden Bereich erstellen, indem Sie die Hierarchien "Geografie" und  
  
    -   **Dimension**aufteilen. Wählen Sie eine verknüpfte Dimension in der Dropdownliste aus.  
  
    -   **Hierarchie**: Wählen Sie die Ebene der Dimensionshierarchie aus, auf der Sie den Filter anwenden möchten. Beispiel: Wenn Sie die Aufteilung bei der Dimension [Geography] vornehmen, würden Sie z.B. eine Hierarchieebene wie [Region Country Name] auswählen.  
  
    -   **Operator**: Wählen Sie einen Operator in der Liste aus.  
  
    -   **Filterausdruck**: Geben Sie einen Wert oder Ausdruck ein, den Sie als Filterbedingung festlegen möchten, oder wählen Sie in der Dropdownliste einen Wert in der Liste der Elemente auf der angegebenen Ebene der Hierarchie aus.  
  
         Beispiel: Wenn Sie als Dimension [Geography] und [Region Country Name] als Hierarchieebene ausgewählt haben, enthält die Dropdownliste alle gültigen Länder, die Sie als Filterbedingung verwenden können. Sie können mehrere Optionen auswählen. Infolgedessen werden die Daten in der Miningstruktur auf Cubedaten aus diesen geografischen Bereichen beschränkt.  
  
    -   **Parameter**: Ignorieren Sie dieses Kontrollkästchen. Dieses Dialogfeld unterstützt mehrere Cubefilteszenarien, und diese Option ist nicht für die Erstellung einer Miningstruktur relevant.  
  
     Klicken Sie auf **Weiter**.  
  
12. Geben Sie auf der Seite **Daten in Trainings- und Testsätze aufteilen** einen Prozentsatz für die Miningstrukturdaten an, die für das Testen reserviert werden sollen, oder geben Sie die maximale Anzahl von Testfällen an. Klicken Sie auf **Weiter**.  
  
     Wenn Sie beide Werte angeben, wird der jeweils niedrigste Wert verwendet.  
  
13. Geben Sie auf der Seite **Assistenten abschließen** einen Namen für die neue OLAP-Miningstruktur und das ursprüngliche Miningmodell an.  
  
14. Klicken Sie auf **Fertig stellen**.  
  
15. Auf der Seite **Assistenten abschließen** haben Sie auch die Möglichkeit, ein Miningmodell und/oder einen Cube zu erstellen, der die Miningmodelldimension verwendet. Diese Optionen werden nur für Modelle unterstützt, die mit den folgenden Algorithmen erstellt werden:  
  
    -   Microsoft Clustering-Algorithmus  
  
    -   Microsoft Decision Trees-Algorithmus  
  
    -   Microsoft Association Rules-Algorithmus  
  
     **Miningmodelldimension erstellen**: Aktivieren Sie dieses Kontrollkästchen, und geben Sie einen Namen für die Miningmodelldimension an. Wenn Sie diese Option verwenden, wird eine neue Dimension innerhalb des ursprünglichen Cubes erstellt, mit dem die Miningstruktur erstellt wurde. Sie können diese Dimension verwenden, um einen Drilldown und weitere Analysen auszuführen. Da sich die Dimension innerhalb des Cubes befindet, wird die Dimension automatisch der Falldatendimension zugeordnet.  
  
     **Cube mithilfe der Miningmodelldimension erstellen**: Aktivieren Sie dieses Kontrollkästchen, und geben Sie einen Namen für den neuen Cube an. Wenn Sie diese Option verwenden, wird ein neuer Cube erstellt, der sowohl die vorhandenen Dimensionen, die beim Erstellen der Struktur verwendet wurden, als auch die neue Data Mining-Dimension mit den Ergebnissen aus dem Modell beinhaltet.  
  
## <a name="see-also"></a>Siehe auch  
 [Tasks und Anweisungen für Miningstrukturen](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
