---
title: Datamining-Projekte | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 543d70fc-34d2-42dd-8d6d-0543109f94d0
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4462aa5a323af4b957fedc5bdbb522705f4f7140
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="data-mining-projects"></a>Data Mining-Projekte
  Ein Data Mining-Projekt ist Teil einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Lösung. Während des Entwurfsprozesses sind die Objekte, die Sie in diesem Projekt erstellen, für Tests und Abfragen im Rahmen einer Arbeitsbereichsdatenbank verfügbar. Wenn Benutzer in der Lage sein sollen, die Objekte im Projekt abzufragen oder zu durchsuchen, müssen Sie das Projekt auf einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bereitstellen, die im mehrdimensionalen Modus ausgeführt wird.  
  
 In diesem Abschnitt werden Ihnen die grundlegenden Informationen bereitgestellt, die Sie benötigen, um Data Mining-Projekte verstehen und erstellen zu können.  
  
 [Erstellen von Data Mining-Projekten](#bkmk_Overview)  
  
 [Objekte in Data Mining-Projekten](#bkmk_Objects)  
  
-   [Datenquellen](#bkmk_DataSources)  
  
-   [Datenquellensichten](#bkmk_DSV)  
  
-   [Miningstrukturen](#bkmk_Structures)  
  
-   [Miningmodelle](#bkmk_Models)  
  
 [Verwenden eines abgeschlossenen Data Mining-Projekts](#bkmk_Complete)  
  
-   [Anzeigen und Untersuchen von Modellen](#bkmk_ViewExplore)  
  
-   [Testen und Validieren von Modellen](#bkmk_Validate)  
  
-   [Erstellen von Vorhersagen](#bkmk_Predict)  
  
 [Programmgesteuerter Zugriff auf Data Mining-Projekte](#bkmk_API)  
  
##  <a name="bkmk_Overview"></a> Erstellen von Data Mining-Projekten  
 In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]erstellen Sie Data Mining-Projekte mithilfe der Vorlage **OLAP- und Data Mining-Projekt**. Mithilfe von AMO können Sie Data Mining-Projekte auch programmgesteuert erstellen. Für einzelne Data Mining-Objekte kann mit der Analysis Services Scripting Language (ASSL) ein Skript erstellt werden. Weitere Informationen finden Sie unter [Datenzugriff auf mehrdimensionale Modelle &#40;Analysis Services – mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md).  
  
 Wenn Sie innerhalb einer vorhandenen Lösung ein Data Mining-Projekt erstellen, werden die Data Mining-Objekte standardmäßig in einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank mit dem gleichen Namen wie die Projektmappendatei bereitgestellt. Sie können diesen Namen und den Zielserver über das Dialogfeld **Projekteigenschaften** ändern. Weitere Informationen finden Sie unter [Konfigurieren von Analysis Services-Projekteigenschaften &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md).  
  
> [!WARNING]  
>  Um das Projekt erfolgreich zu erstellen und bereitzustellen, müssen Sie Zugriff auf eine Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] haben, die im OLAP-/Data Mining-Modus ausführt wird. Sie können Data Mining-Lösungen nicht in einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bereitstellen oder entwickeln, die tabellarische Modelle unterstützt. Sie können außerdem Daten nicht direkt aus einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe oder aus einem tabellarischen Modell heraus verwenden, das den speicherinternen Datenspeicher verwendet. Um zu ermitteln, ob Ihre Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Data Mining unterstützt, lesen Sie den Artikel [Bestimmen des Servermodus einer Analysis Services-Instanz](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
 Innerhalb jedes einzelnen Data Mining-Projekts, das Sie erstellen, müssen Sie die folgenden Schritte ausführen:  
  
1.  Wählen Sie eine *Datenquelle*aus, wie z. B. ein Cube, eine Datenbank oder selbst Excel- oder Textdateien, die die Rohdaten enthält, welche Sie zum Erstellen von Modellen verwenden.  
  
2.  Definieren Sie eine Teilmenge der Daten in der Datenquelle, die für die Analyse verwendet werden soll. Speichern Sie die Teilmenge als *Datenquellensicht*.  
  
3.  Definieren Sie eine *Miningstruktur* , um das Modellieren zu unterstützen.  
  
4.  Fügen Sie der Miningstruktur *Miningmodelle* hinzu, indem Sie einen *Algorithmus* auswählen. Geben Sie an, wie der Algorithmus die Daten verarbeiten soll.  
  
5.  Führen Sie ein Training für die Modelle durch, indem Sie diese mit den ausgewählten Daten oder einer gefilterten Teilmenge der Daten füllen.  
  
6.  Untersuchen, testen und erstellen Sie Modelle neu.  
  
 Wenn das Projekt vollständig ist, können Sie es Benutzern zum Durchsuchen oder Abfragen bereitstellen. Oder Sie stellen einen programmgesteuerten Zugriff auf die Miningmodelle in einer Anwendung zur Verfügung, um Vorhersagen und Analysen zu unterstützen.  
  
  
##  <a name="bkmk_Objects"></a> Objekte in Data Mining-Projekten  
 Sämtliche Data Mining-Projekte enthalten die folgenden vier Typen von Objekten. Sie können über mehrere Objekte sämtlicher unterschiedlicher Typen verfügen.  
  
-   Datenquellen  
  
-   Datenquellensichten  
  
-   Miningstrukturen  
  
-   Miningmodelle  
  
 Ein einzelnes Data Mining-Projekt kann z. B. einen Verweis auf mehrere Datenquellen enthalten. Hierbei kann jede einzelne Datenquelle mehrere Datenquellensichten unterstützen. Andererseits kann auch jede Datenquellensicht mehrere Miningstrukturen unterstützen, die alle eine Vielzahl zugehöriger Miningmodelle aufweisen können.  
  
 Darüber hinaus kann das Projekt Plug-In-Algorithmen, benutzerdefinierte Assemblys oder benutzerdefinierte gespeicherte Prozeduren umfassen. Diese Objekte werden hier jedoch nicht beschrieben. Weitere Informationen finden Sie in der [Dokumentation für Analysis Services-Entwickler](../../analysis-services/analysis-services-developer-documentation.md).  
  
  
###  <a name="bkmk_DataSources"></a> Data Sources  
 Die Datenquelle definiert die Verbindungszeichenfolge und die Authentifizierungsinformationen, die der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Server für den Aufbau einer Verbindung zur Datenquelle verwendet. Die Datenquelle kann mehrere Tabellen oder Sichten enthalten. Sie kann so einfach aufgebaut sein wie eine einzelne Excel-Arbeitsmappe oder eine Textdatei. Sie kann aber auch so komplex sein wie eine analytische Onlineverarbeitungsdatenbank (OLAP) oder eine große relationale Datenbank.  
  
 Ein einzelnes Data Mining-Projekt kann auf mehrere Datenquellen verweisen. Obwohl ein Miningmodell nur eine Datenquelle zur Zeit verwenden kann, weist das Projekt unter Umständen mehrere Modelle auf, die Daten von verschiedenen Datenquellen beziehen.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] unterstützt Daten von vielen externen Anbietern. Außerdem kann SQL Server Data Mining sowohl relationale als auch Cubedaten als Datenquelle verwenden. Wenn Sie jedoch beide Arten von Projekten entwickeln – Modelle auf der Grundlage relationaler Quellen und Modelle auf der Grundlage von OLAP-Cubes –, möchten Sie diese eventuell in separaten Projekten entwickeln und verwalten.  
  
-   In der Regel sollen Modelle, die auf einem OLAP-Cube basieren, innerhalb der OLAP-Entwurfslösung entwickelt werden. Ein Grund hierfür ist, das Modelle auf der Grundlage eines Cubes den Cube verarbeiten müssen, um Daten aktualisieren zu können. Im Allgemeinen sollten Sie Cubedaten nur dann verwenden, wenn diese das hauptsächliche Mittel für Datenspeicherung und -zugriff darstellen oder wenn Sie die Aggregationen, Dimensionen und Attribute benötigen, die über ein mehrdimensionales Projekt erstellt werden.  
  
-   Wenn das Projekt nur relationale Daten verwendet, sollten Sie die relationalen Modelle in einem separaten Projekt erstellen, damit Sie nicht andere Objekte unnötigerweise erneut verarbeiten. In vielen Fällen enthalten die Stagingdatenbank oder das Data Warehouse, die zur Unterstützung der Cube-Erstellung verwendet werden, bereits die Sichten, die zur Ausführung des Data Mining benötigt werden. Außerdem können Sie eher diese Sichten für Data Mining nutzen, anstatt die Aggregationen und die Dimensionen im Cube zu verwenden.  
  
-   Sie können Data Mining-Modelle nicht direkt mit speicherinternen oder [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten erstellen.  
  
 Die Datenquelle identifiziert nur den Server oder den Anbieter sowie den allgemeinen Typ der Daten. Wenn Sie Datenformatierung und Aggregationen ändern müssen, verwenden Sie das Datenquellensichtobjekt.  
  
 Um die Art und Weise zu steuern, mit der Daten aus der Datenquelle verarbeitet werden, können Sie abgeleitete Spalten oder Berechnungen hinzufügen, Aggregate ändern oder Spalten der Daten in der Datenquellensicht umbenennen. (Sie können auch mit Daten-Downstream arbeiten, indem Sie Miningstrukturspalten ändern oder Modellierungsflags und Filter auf der Ebene der Miningmodellspalte verwenden.)  
  
 Wenn eine Datenbereinigung erforderlich ist oder die Daten im Data Warehouse geändert werden müssen, um zusätzliche Variablen zu erstellen, Datentypen zu ändern oder eine alternative Aggregation zu erstellen, müssen Sie unter Umständen zusätzliche Projekttypen zur Unterstützung von Data Mining erstellen. Weitere Informationen über diese verwandten Projekte finden Sie unter [Verwandte Projekte für Data Mining-Lösungen](../../analysis-services/data-mining/related-projects-for-data-mining-solutions.md).  
  
  
###  <a name="bkmk_DSV"></a> Data Source Views  
 Nachdem Sie diese Verbindung zur Datenquelle definiert haben, können Sie eine Sicht erstellen, die die spezifischen Daten identifiziert, die für das Modell relevant sind.  
  
 Über die Datenquellensicht können Sie eine Anpassung der Art und Weise vornehmen, auf die die Daten in der Datenquelle dem Miningmodell bereitgestellt werden. Sie können die Struktur der Daten ändern, um diese relevanter für Ihr Projekt zu machen. Darüber hinaus können Sie ausschließlich bestimmte Arten von Daten auswählen.  
  
 Durch die Verwendung des Datenquellensicht-Editors können Sie z. B. Folgendes erreichen:  
  
-   Erstellen von abgeleiteten Spalten, z. B. Dateparts, Teilzeichenfolgen usw.  
  
-   Aggregatwerte verwenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen wie z. B. GROUP BY (Gruppieren nach).  
  
-   Temporäres Einschränken von Daten oder Beispieldaten  
  
 Weitere Informationen darüber, wie Sie Daten innerhalb einer Datenquellensicht ändern können, finden Sie unter [Datenquellensichten in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
> [!WARNING]  
>  Wenn Sie die Daten filtern möchten, können Sie dies in der Datenquellensicht tun. Sie können aber auch Filter zu den Daten auf der Ebene des Miningmodells erstellen. Da die Filterdefinition mit dem Miningmodell gespeichert wird, erleichtert die Verwendung von Modellfiltern die Bestimmung der Daten, die für das Training des Modells verwendet werden. Darüber hinaus können Sie mehrere zugehörige Modelle mit verschiedenen Filterkriterien erstellen. Weitere Informationen finden Sie unter [Filter für Miningmodelle &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
 Beachten Sie, dass die Datenquellensicht, die Sie erstellen, weitere Daten enthalten kann, die nicht direkt für die Analyse verwendet werden. Sie können z. B. der Datenquellensicht Daten hinzufügen, die für Tests, Vorhersagen oder für Drillthrough verwendet werden. Weitere Informationen zu diesen Nutzungsmöglichkeiten finden Sie unter [Tests und Überprüfung &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md) und [Drillthrough](../../analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
  
###  <a name="bkmk_Structures"></a> Mining Structures  
 Sobald Sie die Datenquelle und die Datenquellensicht erstellt haben, müssen Sie die Spalten jener Daten auswählen, die für Ihr Geschäftsproblem am relevantesten sind, indem Sie die *Miningstrukturen* innerhalb des Projekts definieren. Eine Miningstruktur informiert das Projekt darüber, welche Spalten der Daten aus der Datenquellensicht bei Modellierung, Training und Tests tatsächlich verwendet werden sollen.  
  
 Um eine neue Miningstruktur hinzuzufügen, starten Sie den Data Mining-Assistenten. Dieser Assistent definiert automatisch eine Miningstruktur und führt Sie durch den Prozess der Auswahl der Daten. Außerdem können Sie mit ihm der Struktur optional ein initiales Data Mining-Modell hinzufügen. Innerhalb der Miningstruktur wählen Sie Tabellen und Spalten aus der Datenquellensicht oder von einem OLAP-Cube aus. Sie definieren die Beziehungen unter den Tabellen, wenn die Daten geschachtelte Tabellen umfassen.  
  
 Je nachdem, ob Sie relationale Datenquellen oder analytische Onlineverarbeitungsdatenquellen (OLAP) verwenden, kann die Auswahl der Daten im Data Mining-Assistenten hinsichtlich des äußeren Erscheinungsbildes erhebliche Unterschiede aufweisen.  
  
-   Wenn Sie Daten aus einer relationalen Datenquelle auswählen, ist die Einrichtung einer Miningstruktur einfach: Sie wählen die Spalten von den Daten in der Datenquellensicht aus und stellen zusätzliche Anpassungen wie z. B. Aliase ein. Alternativ können Sie auch festlegen, wie Werte in der Spalte gruppiert oder klassifiziert werden sollen. Weitere Informationen finden Sie unter [Erstellen einer relationalen Miningstruktur](../../analysis-services/data-mining/create-a-relational-mining-structure.md).  
  
-   Wenn Sie Daten von einem OLAP-Cube verwenden, muss sich die Miningstruktur in der gleichen Datenbank wie die OLAP-Lösung befinden.  Um eine Miningstruktur zu erstellen, wählen Sie in der OLAP-Lösung Attribute aus den Dimensionen und verwandten Measures aus. In der Regel werden numerische Werte in den Measures und Kategorievariablen in den Dimensionen gefunden. Weitere Informationen finden Sie unter [Erstellen einer OLAP-Miningstruktur](../../analysis-services/data-mining/create-an-olap-mining-structure.md).  
  
-   Sie können Miningstrukturen auch mithilfe von DMX definieren. Weitere Informationen finden Sie unter [Data Mining-Erweiterungen &#40;DMX&#41; – Datendefinitionsanweisungen](../../dmx/dmx-statements-data-definition.md).  
  
 Nachdem Sie die anfängliche Miningstruktur erstellt haben, können Sie die Strukturspalten kopieren, ändern oder für diese einen Alias verwenden.  
  
 Jede Miningstruktur kann mehrere Miningmodelle enthalten. Nach Abschluss der Aktionen können Sie die Miningstruktur daher erneut öffnen und [Data Mining Designer](../../analysis-services/data-mining/data-mining-designer.md) verwenden, um der Struktur weitere Miningmodelle hinzuzufügen.  
  
 Sie haben auch die Möglichkeit, die Daten in einem Trainingsdataset, das zum Erstellen von Modellen verwendet wird, oder in einem Dataset für zurückgehaltene Daten, das für das Testen oder Validieren der Miningmodelle verwendet wird, zu separieren.  
  
> [!WARNING]  
>  Einige Modelltypen, wie etwa Zeitreihenmodelle, unterstützen die Erstellung von Datasets für zurückgehaltene Daten nicht, da sie für das Training eine kontinuierliche Reihe von Daten benötigen. Weitere Informationen finden Sie unter [Training and Testing Data Sets](../../analysis-services/data-mining/training-and-testing-data-sets.md).  
  
  
###  <a name="bkmk_Models"></a> Mining Models  
 Das Miningmodell definiert den Algorithmus oder die Analysemethode, die Sie auf die Daten anwenden werden. Jeder Miningstruktur fügen Sie ein oder mehrere Miningmodelle hinzu.  
  
 Je nach Anforderungen können Sie in einem einzelnen Projekt viele Modelle kombinieren oder separate Projekte für jeden Modelltyp oder jede analytische Aufgabe erstellen.  
  
 Nachdem Sie eine Struktur und ein Modell erstellt haben, *verarbeiten* Sie jedes Modell, indem Sie die Daten aus der Datenquellensicht an den Algorithmus übergeben, der ein mathematisches Modell der Daten erstellt. Dieser Prozess ist auch bekant als *Trainieren des Modells*. Weitere Informationen finden Sie unter [Anforderungen und Überlegungen zur Verarbeitung &#40;Data Mining&#41;](../../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md).  
  
 Nachdem das Modell verarbeitet wurde, können Sie das Miningmodell entweder visuell untersuchen oder Vorhersageabfragen für das Miningmodell ausführen. Wenn die Daten aus dem Trainingsprozess zwischengespeichert werden, können Sie die *Drillthrough* -Abfragen verwenden, um detaillierte Informationen über die im Modell verwendeten Fälle zurückzugeben.  
  
 Wenn Sie ein Modell für die produktive Umgebung verwenden möchten (z. B. zum Erstellen von Vorhersagen oder zu Untersuchungszwecken für allgemeine Benutzer), können Sie das Modell auf einem anderen Server bereitstellen. Wenn Sie in Zukunft das Modell erneut verarbeiten müssen, so müssen Sie zur gleichen Zeit auch die Definition der zugrunde liegenden Miningstruktur (und notwendigerweise die Definition der Datenquelle und der Datenquellensicht) exportieren.  
  
 Wenn Sie ein Modell bereitstellen, müssen Sie auch sicherstellen, dass die richtigen Verarbeitungsoptionen für die Struktur und das Modell festgelegt werden. Außerdem müssen Sie gewährleisten, dass potenzielle Benutzer über die Berechtigungen verfügen, die sie benötigen, um Abfragen, Sichtmodelle oder Drillthrough für die Struktur oder die Modelldaten ausführen zu können. Weitere Informationen finden Sie unter [Sicherheitsübersicht &#40;Data Mining&#41;](../../analysis-services/data-mining/security-overview-data-mining.md).  
  
  
##  <a name="bkmk_Complete"></a> Verwenden eines abgeschlossenen Data Mining-Projekts  
 Dieser Abschnitt fasst jene Arten zusammen, auf die Sie das abgeschlossene Data Mining-Projekt verwenden können. Sie können Genauigkeitsdiagramme erstellen, Daten untersuchen und überprüfen oder die Data Mining-Muster für Benutzer verfügbar machen.  
  
> [!WARNING]  
>  Die Diagramme, Abfragen und Visualisierungen, die Sie mit Data Mining-Modellen verwenden, werden nicht als Teil des Data Mining-Projekts gespeichert und können nicht bereitgestellt werden. Wenn Sie diese Objekte beibehalten müssen, so müssen Sie entweder den Inhalt speichern, der präsentiert wird, oder für jedes Objekt wie beschrieben ein Skript erstellen.  
  
  
###  <a name="bkmk_ViewExplore"></a> View and Explore Models  
 Nachdem Sie ein Modell erstellt haben, können Sie visuelle Tools und Abfragen verwenden, um die Muster im Modell zu untersuchen und mehr über die zugrunde liegenden Schemata und Statistiken zu erfahren. **stellt im Data Mining-Designer für jeden Miningmodelltyp auf der Registerkarte** Miningmodell-Viewer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Viewer zur Verfügung, die Sie beim Prüfen der Miningmodelle verwenden können.  
  
 Diese Visualisierungen sind temporär und werden ohne Speicherung geschlossen, wenn Sie die Sitzung mit [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]beenden. Wenn Sie daher diese Visualisierungen in eine andere Anwendung zur Präsentation oder weiteren Analyse exportieren müssen, verwenden Sie die auf jeder Registerkarte oder in jedem Bereich der Viewerschnittstelle bereitgestellten Befehle zum **Kopieren** .  
  
 Die Data Mining Add-Ins für Excel stellen ebenfalls eine Visio-Vorlage bereit, die Sie verwenden können, um die Modelle in einem Visio-Diagramm darstellen und kommentieren sowie um das Diagramm mit Visio-Tools ändern zu können. Weitere Informationen finden Sie unter [Microsoft SQL Server 2008 SP2 Data Mining-Add-Ins für Microsoft Office 2007](http://go.microsoft.com/fwlink/?LinkID=123146).  
  
  
###  <a name="bkmk_Validate"></a> Test and Validate Models  
 Nachdem Sie die Modelle verarbeitet haben, können Sie die Ergebnisse analysieren und entscheiden, welche Modelle ihrer Aufgabe am besten gerecht wurden.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bietet verschiedene Diagramme zur Bereitstellung von Tools, die Sie dafür verwenden können, Miningmodelle unmittelbar zu vergleichen und das exakteste oder nützlichste Miningmodell auszuwählen. Zu diesen Tools gehören ein Prognosegütediagramm, ein Gewinndiagramm und eine Klassifikationsmatrix. Sie können diese Diagramme mit ded **Mininggenauigkeitsdiagramm** des Data Mining-Designers generieren.  
  
 Darüber hinaus können Sie den übergreifenden Überprüfungsbericht verwenden, um eine iterative Unterstichprobe Ihrer Daten durchzuführen, um festzustellen, ob das Modell zu einem bestimmten Dataset tendiert. Die vom Bericht gelieferten Statistiken können für den objektiven Vergleich von Modellen und die Bewertung der Qualität Ihrer Trainingsdaten herangezogen werden.  
  
 Beachten Sie, dass diese Berichte und die Diagramme nicht mit dem Projekt oder in der Datenbank ssASnoversion gespeichert werden. Wenn Sie deshalb die Ergebnisse beibehalten oder duplizieren müssen, sollten Sie entweder die Ergebnisse speichern oder mithilfe von DMX oder AMO ein Skript für die Objekte erstellen. Sie können gespeicherte Prozeduren auch für die Kreuzvalidierung verwenden.  
  
 Weitere Informationen finden Sie unter [Tests und Überprüfung &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md).  
  
  
###  <a name="bkmk_Predict"></a> Create Predictions  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] stellt eine Abfragesprache der Data Mining-Erweiterungen (Data Mining Extensions, DMX) bereit, die die Grundlage zum Erstellen von Vorhersagen bildet und auf einfache Weise skriptfähig ist. Um Sie bei der Erstellung von DMX-Vorhersageabfragen zu unterstützen, stellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Abfrage-Generator bereit, der über [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]verfügbar ist. Für den Abfrage-Editor in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]liegt eine Vielzahl von DMX-Vorlagen vor. Wenn Sie mit Vorhersageabfragen noch nicht vertraut sind, empfiehlt es sich, dass Sie den Abfrage-Generator verwenden, der sowohl über den Data Mining-Designer als auch über [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]bereitgestellt wird. Weitere Informationen finden Sie unter [Data Mining Tools](../../analysis-services/data-mining/data-mining-tools.md).  
  
 Die Vorhersagen, die Sie entweder in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] erstellen, werden nicht beibehalten. Wenn die Abfragen komplex sind oder Sie die Ergebnisse reproduzieren müssen, empfiehlt es sich daher, dass Sie die Vorhersageabfragen in DMX-Abfragedateien speichern, Skripts für diese erstellen oder die Abfragen als Teil eines Integration Services-Pakets einbetten.  
  
  
##  <a name="bkmk_API"></a> Programmgesteuerter Zugriff auf Data Mining-Objekte  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] stellt mehrere Tools bereit, mit denen Sie programmgesteuert mit Data Mining-Projekten und den darin enthaltenen Objekten arbeiten können. Die DMX-Sprache stellt Anweisungen bereit, mit denen Sie Datenquellen und Datenquellensichten erstellen sowie Data Mining-Strukturen und -Modelle erstellen, trainieren und verwenden können. Weitere Informationen finden Sie unter [Data Mining-Erweiterungen &#40;DMX&#41; – Referenz](../../dmx/data-mining-extensions-dmx-reference.md).  
  
 Sie können diese Aufgaben auch mit der Analysis Services Scripting Language (ASSL) oder mithilfe von Analysis Management Objects (AMO) ausführen. Weitere Informationen finden Sie unter [Entwickeln mit XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md).  
  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 In den folgenden Themen wird Verwendung des Data Mining-Assistenten beschrieben, um ein Data Mining-Projekt und zugeordnete Objekte zu erstellen.  
  
|Aufgaben|Thema|  
|-----------|------------|  
|Beschreibt, wie mit Miningstrukturspalten gearbeitet wird|[Erstellen einer relationalen Miningstruktur](../../analysis-services/data-mining/create-a-relational-mining-structure.md)|  
|Stellt weitere Informationen darüber bereit, wie neue Miningmodelle hinzugefügt und wie Strukturen und Modelle verarbeitet werden|[Hinzufügen von Miningmodellen zu einer Struktur &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)|  
|Stellt Links für Ressourcen bereit, die Sie bei der Anpassung von Algorithmen unterstützen, welche die Miningmodelle erstellen|[Anpassen von Miningmodellen und -strukturen](../../analysis-services/data-mining/customize-mining-models-and-structure.md)|  
|Stellt Links zu Informationen über jeden der Miningmodell-Viewer bereit|[Data Mining-Modell-Viewer](../../analysis-services/data-mining/data-mining-model-viewers.md)|  
|Informationen zum Erstellen eines Prognosegütediagramms, eines Gewinndiagramms oder einer Klassifikationsmatrix oder zum Testen einer Miningstruktur|[Tests und Überprüfung &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)|  
|Informationen über das Verarbeiten von Optionen und Berechtigungen|[Verarbeiten von Data Mining-Objekten](../../analysis-services/data-mining/processing-data-mining-objects.md)|  
|Bietet weitere Informationen über Analysis Services|[Mehrdimensionale Modelldatenbanken &#40;SSAS&#41;](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining Designer](../../analysis-services/data-mining/data-mining-designer.md)   
 [Erstellen mehrdimensionaler Modelle mit SQL Server-Datentools &#40;SSDT&#41;](../../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)   
 [Arbeitsbereichsdatenbank &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/workspace-database-ssas-tabular.md)  
  
  

