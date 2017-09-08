---
title: "Übersetzungen in mehrdimensionalen Modellen (Analysis Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.dimensiondesigner.deletelanguagefirm.f1
ms.assetid: 5521f8ef-b10a-4861-9df7-1e43e0a1fb3f
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 87f826e36a3fb58cfb1adba2b30a1375e3b84e71
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="translations-in-multidimensional-models-analysis-services"></a>Übersetzungen in mehrdimensionalen Modellen (Analysis Services)
  Sie können Übersetzungen in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] definieren, indem Sie den entsprechenden Designer für das zu übersetzende [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekt verwenden. Durch Definieren einer Übersetzung wird ein **Translation** -Objekt erstellt, das dem entsprechenden [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekt zugewiesen ist. Dieses verfügt über die angegebenen Literalwerte in der angegebenen Sprache für die Eigenschaften des zugewiesenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekts.  
  
## <a name="elements-of-a-multi-lingual-data-model"></a>Elemente eines mehrsprachigen Datenmodells  
 Ein in einer mehrsprachigen Lösung verwendetes Datenmodell benötigt mehr als übersetzte Beschriftungen (Feldnamen und Beschreibungen). Es muss auch Datenwerte bereitstellen, die in verschiedenen Sprachskripts formuliert sind. Für eine mehrsprachige Lösung müssen einzelne Attribute vorhanden sein, die an Spalten in einer externen Datenbank gebunden sind, die die Daten zurückgeben.  
  
 Adventure Works-Beispieldatenbanken (mehrdimensional und das relationale Data Warehouse) veranschaulichen die Übersetzungsmöglichkeiten von Analysis Services. Das Beispielmodell enthält übersetzte Beschriftungen und Beschreibungen. Das relationale Data Warehouse-Beispiel enthält Spalten mit übersetzten Werten, die lokalisierte Attributelemente im Modell bereitstellen.  
  
 So zeigen Sie die im Modell verfügbaren übersetzten Datenwerte an:  
  
1.  Öffnen Sie das mehrdimensionale Adventure Works-Modell im Designer.  
  
2.  Klicken Sie im Projektmappen-Explorer öffnen Datenquellensichten, und doppelklicken Sie auf Adventure Works DW\<Version > .dsv.  
  
3.  Suchen Sie nach dimDate, dimProduct, dimProductCategory oder dimProductSubcateogry. Alle diese Dimensionen enthalten Attribute für übersetzte Elemente für Monat, Tag der Woche, Produktname, Kategoriename usw.  
  
4.  Klicken Sie mit der rechten Maustaste auf ein beliebiges Feld, und wählen Sie **Daten durchsuchen**aus. Für jedes Element werden Übersetzungen in Englisch, Spanisch und Französisch angezeigt.  
  
 Formate für Datum, Uhrzeit und Währung werden nicht durch Übersetzungen implementiert. Um kulturspezifische Formate basierend auf dem Gebietsschema des Clients dynamisch bereitzustellen, verwenden Sie den Währungsumrechnungs-Assistenten und die **FormatString** -Eigenschaft. Weitere Einzelheiten finden Sie unter [Währungsumrechnungen &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md) und [FormatString-Element &#40;ASSL&#41;](../../analysis-services/scripting/properties/formatstring-element-assl.md).  
  
 [Lesson 9: Defining Perspectives and Translations](../../analysis-services/lesson-9-defining-perspectives-and-translations.md) im Analysis Services-Lernprogramm führt Sie durch die Schritte zum Erstellen und Testen von Übersetzungen.  
  
## <a name="defining-translations"></a>Definieren von Übersetzungen  
  
### <a name="add-translations-to-a-cube"></a>Hinzufügen von Übersetzungen zu einem Cube  
 Sie können Übersetzungen zu Cubes, Measuregruppen, Measures, Cubedimensionen, Perspektiven, KPIs, Aktionen, benannten Mengen und berechneten Elementen hinzufügen.  
  
1.  Doppelklicken Sie im Projektmappen-Explorer auf einen Cubenamen, um den Cube-Designer zu öffnen.  
  
2.  Klicken Sie auf die Registerkarte **Übersetzungen** . Alle Objekte, die Übersetzungen unterstützen, werden auf dieser Seite aufgeführt.  
  
3.  Geben Sie für jedes Objekt die Zielsprache (wird intern in eine LCID aufgelöst), die übersetzte Beschriftung und die übersetzte Beschreibung an. Die Sprachenliste ist überall in Analysis Services konsistent, egal, ob Sie die Serversprache in Management Studio festlegen oder die Übersetzungsüberschreibung zu einem einzelnen Attribut hinzufügen.  
  
     Denken Sie daran, dass Sie die Sortierung nicht ändern können. Ein Cube verwendet im Wesentlichen eine Sortierung, selbst wenn Sie mehrere Sprachen durch übersetzte Beschriftungen unterstützen (es gibt eine Ausnahme für Dimensionsattribute, die weiter unten erläutert wird). Wenn die Sprachen nicht ordnungsgemäß unter der freigegebenen Sortierung sortiert werden, müssen Sie Kopien des Cubes erstellen, um den Sortierungsanforderungen gerecht zu werden.  
  
4.  Erstellen Sie das Projekt, und stellen Sie es bereit.  
  
5.  Stellen Sie mithilfe einer Clientanwendung wie Excel eine Verbindung mit der Datenbank her, und ändern Sie dabei die Verbindungszeichenfolge so, dass sie den Gebietsschemabezeichner verwendet. Weitere Einzelheiten finden Sie unter [Tipps und Best Practices für die Globalisierung &#40;Analysis Services&#41;](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md).  
  
### <a name="add-translations-to-a-dimension-and-attributes"></a>Hinzufügen von Übersetzungen zu einer Dimension und Attributen  
 Sie können Übersetzungen zu Datenbankdimensionen, Attributen, Hierarchien und Ebenen innerhalb einer Hierarchie hinzufügen.  
  
 Übersetzte Beschriftungen werden mithilfe Ihrer Tastatur oder durch Kopieren und Einfügen manuell zum Modell hinzugefügt, bei Dimensionsattributelementen können Sie die übersetzten Werte jedoch aus einer externen Datenbank abrufen. Insbesondere die **CaptionColumn** -Eigenschaft eines Attributs kann an eine Spalte in einer Datenquellenansicht gebunden werden.  
  
 Auf Attributebene können Sie Sortierungseinstellungen überschreiben, z. B. können Sie die Unterscheidung nach Breite anpassen oder für ein bestimmtes Attribut eine binäre Sortierung verwenden. In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]wird die Sortierung dort zur Verfügung gestellt, wo Datenbindungen definiert sind. Da Sie eine Dimensionsattributübersetzung an eine andere Quellspalte in der Datenquellensicht binden, ist eine Sortierungseinstellung verfügbar, sodass Sie die Sortierung der Quellspalte angeben können. Weitere Informationen zur Spaltensortierung in der relationalen Datenbank finden Sie unter [Set or Change the Column Collation](../../relational-databases/collations/set-or-change-the-column-collation.md) .  
  
1.  Doppelklicken Sie im Projektmappen-Explorer auf den Dimensionsnamen, um den Dimensions-Designer zu öffnen.  
  
2.  Klicken Sie auf die Registerkarte **Übersetzungen** . Alle Dimensionsobjekte, die Übersetzungen unterstützen, werden auf dieser Seite aufgeführt.  
  
     Geben Sie für jedes Objekt die Zielsprache (wird in eine LCID aufgelöst), die übersetzte Beschriftung und die übersetzte Beschreibung an. Die Sprachenliste ist überall in Analysis Services konsistent, egal, ob Sie die Serversprache in Management Studio festlegen oder die Übersetzungsüberschreibung zu einem einzelnen Attribut hinzufügen.  
  
3.  Um ein Attribut an eine Spalte binden, müssen Sie folgende übersetzte Werte angeben:  
  
    1.  Fügen Sie im Dimensions-Designer unter **Übersetzungen**eine neue Übersetzung hinzu. Wählen Sie die Sprache aus. Auf der Seite wird eine neue Spalte für die übersetzten Werte angezeigt.  
  
    2.  Platzieren Sie den Cursor in einer leeren Zelle neben einem der Attribute. Das Attribut darf nicht der Schlüssel sein, aber alle anderen Attribute sind zulässige Optionen. Eine kleine Schaltfläche mit einem Punkt darin sollte angezeigt werden. Klicken Sie auf die Schaltfläche, um das Dialogfeld **Attributdatenübersetzung**zu öffnen.  
  
    3.  Geben Sie eine Übersetzung für die Beschriftung ein. Diese wird als Datenbeschriftung in der Zielsprache verwendet, z. B. als Feldname in einer PivotTable-Feldliste.  
  
    4.  Wählen Sie die Quellspalte aus, die die übersetzten Werte der Attributelemente bereitstellt. Nur bereits vorhandene Spalten in der an die Dimension gebundene Tabelle oder Abfrage sind verfügbar. Wenn die Spalte nicht vorhanden ist, müssen Sie die Datenquellensicht, die Dimension und den Cube zur Auswahl der Spalte ändern.  
  
    5.  Wählen Sie ggf. die Sortierung und die Sortierreihenfolge.  
  
4.  Erstellen Sie das Projekt, und stellen Sie es bereit.  
  
5.  Stellen Sie mithilfe einer Clientanwendung wie Excel eine Verbindung mit der Datenbank her, und ändern Sie dabei die Verbindungszeichenfolge so, dass sie den Gebietsschemabezeichner verwendet. Weitere Einzelheiten finden Sie unter [Tipps und Best Practices für die Globalisierung &#40;Analysis Services&#41;](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md).  
  
### <a name="add-a-translation-of-the-database-name"></a>Hinzufügen einer Übersetzung des Datenbanknamens  
 Auf Datenbankebene können Sie Übersetzungen für den Datenbanknamen und die Beschreibung hinzufügen. Der übersetzte Datenbankname ist möglicherweise bei Clientverbindungen sichtbar, die die LCID der Sprache angeben, das hängt jedoch vom Tool ab. Bei Anzeige der Datenbank in Management Studio beispielsweise wird der übersetzte Name nicht angezeigt, selbst wenn Sie den Gebietsschemabezeichner für die Verbindung angeben. Die von Management Studio für die Herstellung einer Verbindung mit Analysis Services verwendete API liest die **Language** -Eigenschaft nicht.  
  
1.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Projektnamenamen, und wählen Sie **Datenbank bearbeiten** aus, um den Datenbank-Designer zu öffnen.  
  
2.  Geben Sie unter „Übersetzungen“ die Zielsprache (wird in eine LCID aufgelöst), die übersetzte Beschriftung und die übersetzte Beschreibung an. Die Sprachenliste ist überall in Analysis Services konsistent, egal, ob Sie die Serversprache in Management Studio festlegen oder die Übersetzungsüberschreibung zu einem einzelnen Attribut hinzufügen.  
  
3.  Legen Sie auf der Eigenschaftenseite der Datenbank für **Language** die gleiche LCID fest, die Sie für die Übersetzung angegeben haben. Legen Sie ggf. auch **Collation** fest, wenn der Standardwert nicht mehr sinnvoll ist.  
  
4.  Erstellen Sie die Datenbank, und stellen Sie sie bereit.  
  
## <a name="deleting-translation-objects"></a>Löschen von Übersetzungsobjekten  
 Im Dimension- oder Cube-Designer können Sie mit der rechten Maustaste auf ein Übersetzungsobjekt klicken, um es dauerhaft zu löschen. Sie können ein gelöschtes Objekt nicht wiederherstellen oder wiederverwenden; sehen Sie sich daher die Liste der betroffenen Objekte unbedingt genau an, bevor Sie fortfahren.  
  
## <a name="resolving-translations"></a>Auflösung von Übersetzungen  
 Wenn eine Clientanwendung Informationen in einem bestimmten Sprachbezeichner anfordert, versucht die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz, Daten und Metadaten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekte in den nächstmöglichen Sprachbezeichner aufzulösen. Wenn die Clientanwendung keine Standardsprache und auch nicht den neutralen Gebietsschemabezeichner (0) oder den standardmäßigen Prozesssprachbezeichner (1024) vorgibt, dann verwendet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die Standardsprache für die Instanz, um Daten und Metadaten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekte zurückzugeben.  
  
 Wenn die Clientanwendung einen anderen als den angegebenen Standardsprachbezeichner verwendet, führt die Instanz eine Iteration durch alle verfügbaren Übersetzungen für alle verfügbaren Objekte durch. Wenn der angegebene Sprachbezeichner dem Sprachbezeichner einer Übersetzung entspricht, gibt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] diese Übersetzung zurück. Wenn keine Übereinstimmungen gefunden werden können, versucht [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mit einer der folgenden Methoden, Übersetzungen zurückzugeben, die dem angebenen Sprachbezeichner am ähnlichsten sind:  
  
-   Für die folgenden Sprachbezeichner versucht [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] einen alternativen Sprachbezeichner zu verwenden, wenn eine Übersetzung für den angegebenen Sprachbezeichner nicht definiert ist:  
  
    |Angegebener Sprachbezeichner|Alternativer Sprachbezeichner|  
    |-----------------------------------|-----------------------------------|  
    |3076 - Chinesisch (Hongkong S.A.R., Volksrepublik China)|1028 - Chinesisch (Taiwan)|  
    |5124 - Chinesisch (Macau SAR)|1028 - Chinesisch (Taiwan)|  
    |1028 - Chinesisch (Taiwan)|Standardsprache|  
    |4100 - Chinesisch (Singapur)|2052 - Chinesisch (Volksrepublik China)|  
    |2074 - Kroatisch|Standardsprache|  
    |3098 - Kroatisch (Kyrillisch)|Standardsprache|  
  
-   Für alle anderen angegebenen Sprachbezeichner extrahiert [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die Hauptsprache des angegebenen Sprachbezeichners und ruft den von Windows als beste Übereinstimmung für die Hauptsprache angegebenen Sprachbezeichner zurück. Wenn eine Übersetzung für den ähnlichsten Sprachbezeichner nicht gefunden werden kann, oder wenn der vorgegebene Sprachbezeichner am stärksten mit der Hauptsprache übereinstimmt, wird die Standardsprache verwendet.  
  
## <a name="see-also"></a>Siehe auch  
 [Globalisierungsszenarien für Analysis Services](../../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Sprachen und Sortierungen &#40; Analysis Services &#41;](../../analysis-services/languages-and-collations-analysis-services.md)  
  
  
