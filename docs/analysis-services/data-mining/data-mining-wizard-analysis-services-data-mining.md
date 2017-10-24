---
title: "Datamining-Assistenten (Analysis Services – Datamining) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dimensions [Analysis Services], data mining
- OLAP [Analysis Services], mining models
- Data Mining Wizard
- relational mining models [Analysis Services]
ms.assetid: d5fea90f-5f38-4639-8851-7707f6606a12
caps.latest.revision: 57
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ee0b59c9035d6801bbe7a87d8589e7c337c6c9c2
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="data-mining-wizard-analysis-services---data-mining"></a>Data Mining-Assistent (Analysis Services - Data Mining)
  Der Data Mining-Assistent in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] wird immer dann gestartet, wenn Sie einem Data Mining-Projekt eine neue Miningstruktur hinzufügen. Der Assistent hilft Ihnen, eine Datenquelle auszuwählen und eine Datenquellenansicht einzurichten, mit der die für die Analyse verwendeten Daten definiert werden. Anschließend hilft er Ihnen, ein erstes Modell zu erstellen.  
  
 In der abschließenden Phase des Assistenten können Sie die Daten optional in Training und Testsätze unterteilen und Funktionen wie Drillthrough aktivieren.  
  
## <a name="what-to-know-before-you-start"></a>Wissenswertes vor dem Start  
 Die folgenden Dinge sollten Sie wissen, bevor Sie den Assistenten starten.  
  
-   Werden die Data Mining-Struktur und die -Modelle von einer relationalen Datenbank aus oder von einem vorhandenen Cube in einer OLAP-Datenbank erstellt?  
  
-   Welche Spalten enthalten die Schlüssel, die einen Falldatensatz eindeutig identifizieren?  
  
-   Welche Spalten oder Attribute möchten Sie für die Vorhersage verwenden? Welche Spalten oder Attribute sind als Eingabe für die Analyse gut geeignet?  
  
-   Welchen Algorithmus sollten Sie verwenden? Die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bereitgestellten Algorithmen haben unterschiedliche Eigenschaften und erzeugen verschiedene Ergebnisse. Glücklicherweise sind Sie nicht auf ein Modell für alle Datensätze beschränkt, Sie können daher nach Bedarf verschiedene Modelle hinzufügen.  
  
-   Müssen Sie in der Lage sein, die Modelle auf einem einheitlichen Dataset zu testen? In diesem Fall erwägen Sie, die Option zu verwenden, um einige Daten für Tests zu reservieren. Sie können einen Prozentsatz auswählen und diesen bei Bedarf durch eine angegebene Anzahl von Zeilen nach oben begrenzen.  
  
##  <a name="BKMK_Using_DM_Wizard"></a> Starten des Data Mining-Assistenten  
 Es muss eine Projektmappe in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] geöffnet sein, die mindestens ein Data Mining- oder OLAP-Projekt enthält, um den Data Mining-Assistenten verwenden zu können.  
  
-   Wenn die Projektmappe für Data Mining bereit ist, können Sie im Projektmappen-Explorer einfach mit der rechten Maustaste auf den Knoten **Miningstrukturen** klicken und **Neue Miningstruktur** auswählen, um den Assistenten zu starten.  
  
-   Wenn die Projektmappe keine vorhandenen Projekte enthält, können Sie ein neues Data Mining-Projekt hinzufügen. Wählen Sie im Menü **Datei** die Option **Neu**aus, und klicken Sie dann auf **Projekt**. Wählen Sie die Vorlage für multidimensionale Projekte bzw. Data Mining-Projekte von Analysis Services aus ****.  
  
-   Sie können auch Metadaten aus einer vorhandenen Data Mining-Projektmappe mithilfe des Analysis Services-Import-Assistenten abrufen. Sie können jedoch die zu importierenden einzelnen Objekte nicht auswählen. Die gesamte Datenbank wird importiert, und zwar einschließlich sämtlicher Cubes, Datenquellensichten usw. Die durch den Import neu erstellte Projektmappe wird automatisch so konfiguriert, dass sie die lokale Standarddatenbank verwendet. Sie müssen dies möglicherweise in eine andere Instanz ändern, bevor Sie die Objekte verarbeiten oder durchsuchen können. Wenn Sie aus einer früheren Version von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]importieren, müssen Sie die Verweise auf Anbieter möglicherweise aktualisieren.  
  
 Anschließend müssen Sie die Miningstruktur und ein zugeordnetes Data Mining-Modell erstellen. Sie können auch nur die Miningstruktur erstellen und später Modelle hinzufügen. Es ist jedoch im Allgemeinen am einfachsten, zuerst ein Testmodell zu erstellen.  
  
###  <a name="BKMK_Relational"></a>Vergleich der relationalen und OLAP-Miningmodelle  
 Sie sollten sich entscheiden, ob Sie eine relationale Datenquelle verwenden oder ob Ihr Modell auf multidimensionalen Daten (OLAP) basieren soll.  
  
 Im Data Mining-Assistenten gibt es an dieser Stelle zwei Möglichkeiten, je nachdem, ob Ihre Datenquelle relational oder in einem Cube ist: Abgesehen vom Datenauswahlprozess ist alles andere gleich – die Auswahl des Algorithmus, die Möglichkeit, ein Dataset mit zurückgehaltenen Daten hinzuzufügen usw. Die Auswahl der Cubedaten ist jedoch ein wenig komplexer als die Verwendung von relationalen Daten. (Sie erhalten am Ende auch einige zusätzliche Optionen, wenn Sie ein Modell auf Grundlage eines Cubes erstellen.)  
  
 Eine detaillierte exemplarische Vorgehensweise jeder Option finden Sie in den folgenden Themen:  
  
 [Erstellen einer relationalen Miningstruktur](../../analysis-services/data-mining/create-a-relational-mining-structure.md)  
 Hilft Ihnen bei der Entscheidungsfindung, wenn Sie ein relationales Data Mining-Modell erstellen.  
  
 [Erstellen einer OLAP-Miningstruktur](../../analysis-services/data-mining/create-an-olap-mining-structure.md)  
 Beschreibt die zusätzlichen Optionen und die Auswahlmöglichkeiten, wenn Daten von einem OLAP-Cube ausgewählt werden.  
  
> [!NOTE]  
>  Für ein Data Mining ist es nicht erforderlich, dass Sie einen Cube oder eine OLAP-Datenbank haben. Sofern Ihre Daten nicht bereits in einem Cube gespeichert sind oder Sie OLAP-Dimensionen oder die Ergebnisse von OLAP-Aggregationen oder -Berechnungen auswerten möchten, empfehlen wir die Verwendung einer relationalen Tabelle oder Datenquelle für das Data Mining.  
  
### <a name="choosing-an-algorithm"></a>Auswählen eines Algorithmus  
 Anschließend müssen Sie sich entscheiden, welcher Algorithmus für die Verarbeitung Ihrer Daten verwendet werden soll. Es kann schwierig sein, eine Entscheidung zu treffen. Jeder in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bereitgestellte Algorithmus verfügt über unterschiedliche Funktionen und führt zu unterschiedlichen Ergebnissen. Sie können experimentieren und verschiedene Modelle ausprobieren, bevor Sie das angemessenste Modell für Ihre Daten und Ihr Geschäftsproblem bestimmen. Im folgenden Thema finden Sie eine Erklärung der Aufgaben, für die jeder Algorithmus am besten geeignet ist.  
  
 [Data Mining-Algorithmen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
 Sie können mehrere Modelle mit unterschiedlichen Algorithmen erstellen oder die Parameter der Algorithmen ändern, um verschiedene Modelle zu erstellen. Sie werden in Bezug auf die Auswahl des Algorithmus nicht eingeschränkt, und es ist eine gute Übung, um mehrere unterschiedliche Modelle für die gleichen Daten zu erstellen.  
  
### <a name="define-the-data-used-for-modeling"></a>Definieren der für Modellierung verwendeten Daten  
 Zusätzlich zur Auswahl der Daten von einer Quelle müssen Sie angeben, welche der Tabellen in der Datenquellensicht die *Falldaten*enthält. Die Falltabelle wird verwendet, um das Data Mining-Modell zu erlernen. Sie sollte die zu analysierenden Entitäten enthalten, beispielsweise Kunden und deren demografische Informationen. Jeder Fall muss eindeutig sein und durch einen *Fallschlüssel*identifizierbar sein.  
  
 Zusätzlich zum Bestimmen der Falltabelle können Sie *geschachtelte Tabellen* in die Daten einbeziehen. Eine geschachtelte Tabelle enthält in der Regel zusätzliche Informationen zu den Entitäten in der Falltabelle, etwa von dem Kunden vorgenommene Transaktionen oder Attribute, die eine n:1-Beziehung zu der Entität aufweisen. Eine mit der Falltabelle **Kunden** verknüpfte geschachtelte Tabelle könnte beispielsweise eine Liste der von jedem Kunden erworbenen Produkte enthalten. In einem Modell, das Datenverkehr zu einer Website analysiert, könnte die geschachtelte Tabelle die Sequenzen von Seiten enthalten, die der Benutzer besucht hat. Weitere Informationen finden Sie unter [Geschachtelte Tabellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/nested-tables-analysis-services-data-mining.md).  
  
### <a name="additional-features"></a>Zusätzliche Funktionen  
 Vom Data Mining-Assistenten werden diese zusätzlichen Funktionen bereitgestellt, um Ihnen dabei zu helfen, die richtigen Daten auszuwählen und die Datenquellen ordnungsgemäß zu konfigurieren:  
  
-   **Automatische Erkennung von Datentypen:**Der Assistent untersucht die Eindeutigkeit und die Verteilung von Spaltenwerten und empfiehlt anschließend den besten Datentyp sowie einen Verwendungstyp für die Daten. Sie können diese Vorschläge überschreiben, indem Sie Werte aus einer Liste auswählen.  
  
-   **Vorschläge für Variablen**: Sie können auf ein Dialogfeld klicken und einen Analyzer starten, der Korrelationen zwischen den in einem Modell einbezogenen Spalten berechnet und bestimmt, ob alle Spalten basierend auf der bisherigen Konfiguration des Modells wahrscheinliche Vorhersagen des Ausgabeattributs sind. Sie können diese Vorschläge überschreiben, indem Sie andere Werte eingeben.  
  
-   **Funktionsauswahl**: Von den meisten Algorithmen werden Spalten, die gute Indikatoren sind, automatisch erkannt und bevorzugt verwendet. Die *Funktionsauswahl* wird auf Spalten angewendet, die zu viele Werte enthalten, um die Kardinalität der Daten zu reduzieren und um die Chancen zu erhöhen, ein aussagekräftiges Muster zu finden. Sie können das Verhalten der Funktionsauswahl beeinflussen, indem Sie Modellparameter verwenden.  
  
-   **Automatische Aufteilung des Cubes**: Wenn das Miningmodell auf einer OLAP-Datenquelle basiert, besteht automatisch die Möglichkeit, das Modell mit Cubeattributen in Slices aufzuteilen. Dies ist praktisch, um Modelle auf Grundlage der Teilmengen von Cubedaten zu erstellen.  
  
### <a name="completing-the-wizard"></a>Abschließen des Assistenten  
 Der letzte Schritt im Assistenten besteht aus der Benennung der Miningstruktur und dem damit verbundenen Miningmodell. Je nachdem welchen Modelltyp Sie erstellt haben, stehen Ihnen die folgenden wichtigen Optionen zur Verfügung;  
  
-   Wenn Sie **Drillthrough zulassen**auswählen, wird die Möglichkeit zum *Drillthrough* im Modell aktiviert. Mit Drillthrough können Benutzer, die die entsprechenden Berechtigungen haben, die Quelldaten analysieren, die beim Erstellen des Modells verwendet wurden.  
  
-   Wenn Sie ein OLAP-Modell erstellen, können Sie die Option **Neuen Data Mining-Cube erstellen**oder **Data Mining-Dimension erstellen**auswählen. Die beiden Optionen erleichtern es, das fertige Modell zu durchsuchen und einen Drillthrough auf die zugrunde liegenden Daten auszuführen.  
  
 Nachdem Sie den Data Mining-Assistenten abgeschlossen haben, ändern Sie mit dem Data Mining-Designer die Miningstruktur und die -modelle, um die Genauigkeit des Modells sowie die Charakteristika der Struktur und der Modelle anzuzeigen, oder Vorhersagen mithilfe der Modelle durchzuführen.  
  
 [Zurück zum Anfang](#BKMK_Using_DM_Wizard)  
  
## <a name="related-content"></a>Verwandte Inhalte  
 Weitere Informationen über die nötigen Entscheidungen bei der Erstellung eines Data Mining-Modells sind den folgenden Links zu entnehmen:  
  
 [Data Mining-Algorithmen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
 [Inhaltstypen &#40;Data Mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md)  
  
 [Datentypen &#40;Data Mining&#41;](../../analysis-services/data-mining/data-types-data-mining.md)  
  
 [Funktionsauswahl &#40;Data Mining&#41;](../../analysis-services/data-mining/feature-selection-data-mining.md)  
  
 [Fehlende Werte &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md)  
  
 [Miningmodell-Drillthrough](../../analysis-services/data-mining/drillthrough-on-mining-models.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining-Tools](../../analysis-services/data-mining/data-mining-tools.md)   
 [Data Mining-Projektmappen](../../analysis-services/data-mining/data-mining-solutions.md)  
  
  

