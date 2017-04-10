---
title: "Konfigurieren des Zeichenfolgenspeichers f&#252;r Dimensionen und Partitionen | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 987f6cfc-da82-4b2e-96ef-a8af88339e5f
caps.latest.revision: 21
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 21
---
# Konfigurieren des Zeichenfolgenspeichers f&#252;r Dimensionen und Partitionen
  Sie haben die Möglichkeit, Zeichenfolgenspeicher neu zu konfigurieren, um Platz für sehr große Zeichenfolgen in Dimensionsattributen oder Partitionen schaffen, die die maximale Dateigröße von 4 GB für Zeichenfolgenspeicher überschreiten. Wenn die Dimensionen oder Partitionen Zeichenfolgenspeicher dieser Größe beinhalten, können Sie die Dateigrößeneinschränkung durch Ändern der Eigenschaft **StringStoresCompatibilityLevel** auf Ebene der Dimension oder Partition für lokale als auch für verknüpfte Objekte (lokal oder remote) umgehen.  
  
 Beachten Sie, dass Sie Zeichenfolgenspeicher genau für jene Objekte erhöhen können, die zusätzlichen Kapazität benötigen. In den meisten mehrdimensionalen Modellen werden Zeichenfolgendaten Dimensionen zugeordnet. Von dieser Einstellung können jedoch auch Partitionen, die Distinct Count Measures enthalten, neben Zeichenfolgen profitieren. Da die Einstellung für Zeichenfolgen gilt, sind numerische Daten nicht betroffen.  
  
 Für diese Eigenschaften gibt es u. a. folgende gültige Werte:  
  
|Wert|Description|  
|-----------|-----------------|  
|**1050**|Gibt die standardmäßige Zeichenfolgenspeicherarchitektur an, für die eine maximale Dateigröße von 4 GB pro Speicher gilt.|  
|**1100**|Gibt den größeren Zeichenfolgenspeicher an, unterstützt bis zu 4 Milliarden eindeutige Zeichenfolgen pro Speicher.|  
  
> [!IMPORTANT]  
>  Um die Zeichenfolgenspeichereinstellungen eines Objekts zu ändern, müssen Sie das Objekt selbst und alle abhängigen Objekte erneut verarbeiten. Die Verarbeitung ist erforderlich, um die Prozedur abzuschließen.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
-   [Informationen zu Zeichenfolgenspeichern](#bkmk_background)  
  
-   [Erforderliche Komponenten](#bkmk_prereq)  
  
-   [Schritt 1: Festlegen der StringStoreCompatiblityLevel-Eigenschaft in SQL Server-Datentools](#bkmk_step1)  
  
-   [Schritt 2: Verarbeiten der Objekte](#bkmk_step2)  
  
##  <a name="bkmk_background"></a> Informationen zu Zeichenfolgenspeichern  
 Der Konfiguration des Zeichenfolgenspeichers ist optional. Das bedeutet, dass sogar neue Datenbanken, die Sie erstellen, die Architektur für Standardzeichenfolgenspeicher verwenden, für die die maximale Dateigröße von 4 GB gilt. Die Architektur für größeren Zeichenfolgenspeicher beeinträchtigt die Leistung geringfügig, ist jedoch bemerkbar. Sie sollten diese Architektur nur verwenden, wenn die maximale Größe von 4 GB für Zeichenfolgenspeicherdateien erreicht bzw. fast erreicht wird.  
  
> [!NOTE]  
>  Diese Einstellung gilt nicht für Data Mining-Modelle. Derzeit ist es weiterhin möglich, dass die Dateigrößenbegrenzung in GB für Modelle gilt, die Data Mining-Strukturen enthalten.  
  
 In einer mehrdimensionalen Datenbank von Analysis Services werden Zeichenfolgen getrennt von numerischen Daten gespeichert, um Optimierungen basierend auf den Eigenschaften der Daten zuzulassen. Zeichenfolgendaten werden in der Regel in Dimensionsattributen gefunden, die Namen oder Beschreibungen darstellen. Zeichenfolgendaten können auch in Distinct Count Measures enthalten sein. Zeichenfolgendaten können auch in Schlüsseln verwendet werden.  
  
 Sie können einen Zeichenfolgenspeicher an der Dateierweiterung (z. B. .asstore-, .bstore-, .ksstore- oder .string-Dateien) erkennen. Standardmäßig gilt für jede dieser Dateien eine maximale Dateigröße von 4 GB. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]können Sie die maximale Dateigröße überschreiben, indem Sie einen alternativen Speichermechanismus angeben, bei dem die Größe des Zeichenfolgenspeichers an die Anforderungen angepasst wird.  
  
 Im Gegensatz zur Architektur für Standardzeichenfolgenspeicher, in der es eine Obergrenze für die Größe der physischen Datei gibt, basiert der größere Zeichenfolgenspeicher auf einer maximalen Anzahl von Zeichenfolgen. Der größere Zeichenfolgenspeicher kann maximal 4 Milliarden eindeutige Zeichenfolgen oder 4 Milliarden Datensätze enthalten, je nachdem, welcher Wert zuerst erreicht wird. Der größere Zeichenfolgenspeicher erstellt Datensätze von gleichmäßiger Größe, wobei jeder Datensatz gleich einer 64-KB-Seite ist. Bei sehr langen Zeichenfolgen, die nicht in einen einzelnen Datensatz passen, liegt die tatsächliche Grenze bei weniger als 4 Milliarden Zeichenfolgen.  
  
##  <a name="bkmk_prereq"></a> Erforderliche Komponenten  
 Sie müssen [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] oder eine neuere Version von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]haben.  
  
 Dimensionen und Partitionen müssen MOLAP-Speicher verwenden.  
  
 Der Kompatibilitätsgrad der Datenbank muss auf 1100 festgelegt werden. Wenn Sie eine Datenbank mithilfe von [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] und der [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] -Version oder einer neueren Version von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]erstellt oder bereitgestellt haben, ist der Kompatibilitätsgrad der Datenbank bereits auf 1100 festgelegt. Wenn Sie eine in einer früheren Version von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] erstellte Datenbank in ssSQL11 oder eine neuere Version verschoben haben, müssen Sie den Kompatibilitätsgrad aktualisieren. Für Datenbanken, die Sie verschieben, aber nicht erneut bereitstellen, können Sie den Kompatibilitätsgrad mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] festlegen. Weitere Informationen finden Sie unter [Kompatibilitätsgrad einer mehrdimensionalen Datenbank &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md).  
  
##  <a name="bkmk_step1"></a> Schritt 1: Festlegen der StringStoreCompatiblityLevel-Eigenschaft in SQL Server-Datentools  
  
1.  Öffnen Sie das Projekt mit den zu ändernden Dimensionen oder Partitionen in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Um den Zeichenfolgenspeicher für Dimensionen zu ändern, öffnen Sie Projektmappen-Explorer. Doppelklicken Sie auf die Dimension, für die Sie den Zeichenfolgenspeicher ändern.  
  
3.  Stellen Sie im Dimensions-Designer im Bereich Attribute sicher, dass der übergeordnete Knoten der Dimension ausgewählt ist (wenn die Dimension z. B. "Kunden" ist, wählen Sie "Kunden" aus und nicht die untergeordneten Attribute).  
  
4.  Legen Sie **StringStoresCompatibilityLevel** im Bereich Eigenschaften im Abschnitt Erweitert auf **1100**fest. Wiederholen Sie diesen Schritt für andere Dimensionen, die einen größeren Speicher erfordern, oder behalten Sie den Wert **1050** für die verbleibenden Dimensionen bei.  
  
5.  Öffnen Sie einen Cube von Projektmappen-Explorer für Partitionen.  
  
6.  Klicken Sie auf die Registerkarte Partitionen.  
  
7.  Erweitern Sie die Partition, wählen Sie die Partition aus, die zusätzliche Speicherkapazität erfordert, und ändern Sie dann die **StringStoresCompatibilityLevel** -Eigenschaft.  
  
8.  Speichern Sie die Datei.  
  
##  <a name="bkmk_step2"></a> Schritt 2: Verarbeiten der Objekte  
 Die neue Speicherarchitektur wird verwendet, nachdem Sie die Objekte verarbeitet haben. Die Verarbeitung der Objekte zeigt auch an, dass das Problem der Speichereinschränkung behoben wurde, da der Fehler, der zuvor bei einer Überlaufbedingung des Zeichenfolgenspeichers gemeldet wurde, nicht mehr auftreten sollte.  
  
-   Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf die soeben geänderte Dimension, und wählen Sie **Verarbeiten** aus.  
  
 Sie müssen die Option Vollständig verarbeiten für jedes Objekt verwenden, das die neue Zeichenfolgenspeicherarchitektur verwendet. Führen Sie vor der Verarbeitung eine Auswirkungsanalyse für die Dimension durch, um festzustellen, ob abhängige Objekte ebenfalls eine erneute Verarbeitung erfordern.  
  
## Siehe auch  
 [Tools und Ansätze zum Verarbeiten &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md)   
 [Verarbeiten von Optionen und Einstellungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)   
 [Speichermodi und Verarbeitung von Partitionen](../Topic/Partition%20Storage%20Modes%20and%20Processing.md)   
 [Speichern von Dimensionen](../Topic/Dimension%20Storage.md)  
  
  