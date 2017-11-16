---
title: Sprachen und Sortierungen (Analysis Services) | Microsoft Docs
ms.custom: 
ms.date: 04/20/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- Analysis Services testen
helpviewer_keywords:
- Windows collations [Analysis Services]
- default collations
- languages [Analysis Services]
- sort orders [Analysis Services]
- language identifiers [Analysis Services]
- default languages
- collations [Analysis Services]
ms.assetid: 666cf8a7-223b-4be5-86c0-7fe2bcca0d09
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d2f1ca64cc2c6a3c3d376b47c660598e05227bf8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="languages-and-collations-analysis-services"></a>Sprachen und Sortierungen (Analysis Services)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] unterstützt die Sprachen und Sortierungen, die von [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows-Betriebssystemen bereitgestellt werden. **Language** - und **Collation** -Eigenschaften werden zunächst während der Installation auf Instanzebene festgelegt, können jedoch nachträglich auf unterschiedlichen Ebenen der Objekthierarchie geändert werden.  
  
 In einem mehrdimensionalen Modell (ausschließlich) lassen sich diese Eigenschaften in einer Datenbank oder einem Cube festlegen – Sie können sie auch für Übersetzungen festlegen, die Sie für Objekte innerhalb eines Cubes erstellen. In einem Tabellenmodell werden Sprache und Sortierung vom Betriebssystemhost geerbt.  
  
 Beim Festlegen von **Sprache** und **Sortierung** in einem mehrdimensionalen Modell geben Sie entweder Einstellungen an, die während der Verarbeitung und Abfrageausführung vom Datenmodell verwendet werden, oder Sie statten ein Modell mit mehreren Übersetzungen aus, sodass fremdsprachige Personen in ihrer Muttersprache mit dem Modell arbeiten können. Das explizite Festlegen der Eigenschaften **Sprache** und **Sortierung** für ein Objekt (Datenbank, Modell oder Cube) ist sinnvoll, wenn die Entwicklungsumgebung und der Produktionsserver für verschiedene Gebietsschemas konfiguriert wurden und Sie sicherstellen möchten, dass die Sprache und Sortierung mit der beabsichtigten Zielumgebung übereinstimmen.  
  
##  <a name="bkmk_object"></a> Objekte, die Sprach- und Sortierungseigenschaften unterstützen  
 **Language** - und **Collation** -Eigenschaften werden häufig zusammen verfügbar gemacht – wenn Sie **Language**festlegen können, können Sie auch **Collation**festlegen.  
  
 Sie können **Language** und **Collation** für die folgenden Objekte festlegen:  
  
-   **Instanz**. Alle Projekte, die für die Instanz bereitgestellt werden, übernehmen die Sprache und die Sortierung der Instanz, vorausgesetzt, Sprache und Sortierung sind nicht definiert. Standardmäßig lässt ein mehrdimensionales Modell die Sprache und Sortierung leer. Wenn das Projekt bereitgestellt wird, erhalten die resultierende Datenbank und die Cubes die Sprache und die Sortierung der Instanz.  
  
     Anfänglich werden die Sprach- und Sortierungseigenschaften während des Setups festgelegt, sie können jedoch von einem Administrator in Management Studio überschrieben werden. Einzelheiten dazu finden Sie unter [Ändern der Standardsprache oder -sortierung für die Instanz](#bkmk_defaultLang) .  
  
-   **Datenbank**: Um die Vererbung zu unterbrechen, können Sie Sprache und Sortierung explizit auf der Projektebene festlegen, die von allen Cubes verwendet werden, die in der Datenbank enthalten sind. Sofern nicht anders angegeben, erhalten alle Cubes in der Datenbank die Sprache und die Sortierung, die Sie auf dieser Ebene angeben. Wenn Sie routinemäßig für verschiedene Gebietsschemas codieren und bereitstellen (z. B. die Lösung auf einem chinesischen Computer entwickeln, sie jedoch für einen Server bereitstellen, der im Besitz einer französischen Tochtergesellschaft ist), ist das Festlegen von Sprache und Sortierung auf Datenbankebene der erste und wichtigste Schritt um sicherzustellen, dass die Lösung in der Zielumgebung funktioniert. Der beste Ort zum Festlegen dieser Eigenschaften ist innerhalb des Projekts (über den Befehl **Datenbank bearbeiten** für das Projekt).  
  
-   **Datenbankdimension** Obwohl der Designer die Eigenschaften **Language** und **Collation** für eine Datenbankdimension verfügbar macht, ist das Festlegen von Eigenschaften für dieses Objekt nicht hilfreich. Datenbankdimensionen werden nicht als eigenständige Objekte verwendet, es ist also möglicherweise schwierig, wenn nicht sogar unmöglich, die von Ihnen definierten Eigenschaften zu nutzen. In einem erbt eine Dimension immer **Language** und **Collation** vom übergeordneten Cube. Alle Werte, die Sie ggf. für das eigenständige Datenbank-Dimensionsobjekt festgelegt haben, werden ignoriert.  
  
-   **Cube**: Als primäre Abfragestruktur können Sie die Sprache und Sortierung auf Cubeebene festlegen. Sie möchten beispielsweise mehrere Sprachversionen eines Cubes, wie z. B. eine englische und chinesische Version, innerhalb desselben Projekts erstellen, wobei jeder Cube eine eigene Sprache und Sortierung hat.  
  
     Ganz gleich, welche Sprache und Sortierung Sie in einem Cube festgelegt haben, sie werden von allen Measures und Dimensionen verwendet, die im Cube enthalten sind. Die einzige Möglichkeit, die Sortierungseigenschaften feiner differenziert festzulegen, ist das Erstellen von Übersetzungen für ein Dimensionsattribut. Andernfalls ist, wenn keine Übersetzungen auf Attributebene vorliegen, eine Sortierung pro Cube vorhanden.  
  
 Darüber hinaus können Sie **Language**alleine für ein **Translation** -Objekt festlegen.  
  
 Ein Übersetzungsobjekt wird erstellt, wenn Sie Übersetzungen zu einem Cube oder einer Dimension hinzufügen. **Language** ist Teil der Übersetzungsdefinition. **Collation**hingegen wird auf der Cube- oder einer höheren Ebene festgelegt und von allen Übersetzungen gemeinsam verwendet. Dies zeigt sich im XMLA eines Cubes, der Übersetzungen enthält– hier sehen Sie mehrere Spracheigenschaften (eine für jede Übersetzung), jedoch nur eine Sortierung. Beachten Sie, dass es eine Ausnahme für Übersetzungen von Dimensionsattributen gibt, bei der Sie die Cubesortierung überschreiben können, um eine Attributsortierung anzugeben, die mit der Quellspalte übereinstimmt (das Datenbankmodul unterstützt das Festlegen einer Sortierung für einzelne Spalten, und in der Regel werden einzelne Übersetzungen konfiguriert, um die Elementdaten aus den verschiedenen Quellspalten abzurufen). Für alle anderen Übersetzungen wird andernfalls **Language** alleine ohne begleitende **Collation** verwendet. Weitere Informationen finden Sie unter [Unterstützung für Übersetzungen in Analysis Services](../analysis-services/translation-support-in-analysis-services.md) .  
  
##  <a name="bkmk_lang"></a> Sprachunterstützung in Analysis Services  
 Die Eigenschaft **Sprache** legt das Gebietsschema eines Objekts fest, das während der Verarbeitung, Abfrage und mit **Untertiteln** und **Übersetzungen** zur Unterstützung von mehrsprachigen Szenarios verwendet wird. Gebietsschemas basieren auf einem Sprachbezeichner, z. B. Englisch, und einem Gebiet, wie z. B. USA oder Australien, wodurch Datums- und Uhrzeitdarstellungen weiter verfeinert werden.  
  
 Auf Instanzebene wird die Eigenschaft während der Installation festgelegt und basiert auf der Sprache des Windows Server-Betriebssystems (eine von 37 Sprachen, vorausgesetzt, ein Sprachpaket ist installiert). Sie können die Sprache nicht beim Setup ändern.  
  
 Nach der Installation können Sie die **Sprache** mithilfe der Servereigenschaftenseite in Management Studio oder in der Konfigurationsdatei „msmdsrv.ini“ überschreiben. Sie können unter vielen weiteren Sprachen wählen, darunter alle Sprachen, die vom Windows-Client unterstützt werden. Bei der Festlegung auf Instanzebene auf dem Server bestimmt **Language** das Gebietsschema aller Datenbanken, die später bereitgestellt werden. Wenn Sie beispielsweise **Language** auf Deutsch festlegen, haben alle Datenbanken, die für die Instanz bereitgestellt werden, die Spracheigenschaft 1031, die LCID für Deutsch.  
  
###  <a name="bkmk_lcid"></a> Wert der Spracheigenschaft ist ein Gebietsschemabezeichner (LCID, Locale Identifier)  
 Gültige Werte sind alle LCIDs, die in der Dropdownliste angezeigt werden. In Management Studio und SQL Server Data Tools werden LCIDs als Zeichenfolgenentsprechungen dargestellt. Unabhängig vom Tool werden überall da, wo die **Language** -Eigenschaft verfügbar gemacht wird, dieselben Sprachen angezeigt. Durch eine identische Liste der Sprachen wird sichergestellt, dass Sie Übersetzungen im gesamten Modell konsistent implementieren und testen können.  
  
 Obwohl Analysis Services die Sprachen nach Name aufführt, ist der tatsächlich für die Eigenschaft gespeicherte Wert eine LCID. Wenn Sie eine Spracheigenschaft programmgesteuert oder über die Datei „msmdsrv.ini“ festlegen, müssen Sie den [Gebietsschemabezeichner](http://en.wikipedia.org/wiki/Locale) (locale identifier; LCID) als Wert verwenden. Eine LCID ist ein 32-Bit-Wert, der aus einer Sprach-ID, einer Sortierungs-ID und reservierten Bits besteht, die eine bestimmte Sprache identifizieren. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] verwendet LCIDs, um die ausgewählte Sprache für [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Instanzen und -Objekte anzugeben.  
  
 Sie können die LCID im Hexadezimal- oder Dezimalformat festlegen. Zu den Beispielen für gültige Werte für die Eigenschaft **Sprache** gehören:  
  
-   0x0409 oder 1033 für **Englisch (Vereinigte Staaten)**  
  
-   0x0411 oder 1041 für **Japanisch**  
  
-   0x0407 oder 1031 für **Deutsch (Deutschland)**  
  
-   0x0416 oder 1046 für **Portugiesisch (Brasilien)**  
  
 Eine längere Liste finden Sie unter [Von Microsoft zugewiesene Gebietsschema-IDs](http://msdn.microsoft.com/goglobal/bb964664.aspx). Weitere Informationen finden Sie unter [Codierung und Codepages](http://msdn.microsoft.com/goglobal/bb688114.aspx).  
  
> [!NOTE]  
>  Die **Language** -Eigenschaft bestimmt nicht die Sprache für die Rückgabe von Systemmeldungen oder die in der Benutzeroberfläche angezeigten Zeichenfolgen. Fehler, Warnungen und Meldungen sind in allen von Office und Office 365 unterstützten Sprachen lokalisiert und werden automatisch verwendet, wenn die Clientverbindung eines der unterstützten Gebietsschemas angibt.  
  
##  <a name="bkmk_collations"></a> Sortierungsunterstützung in Analysis Services  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] verwendet ausschließlich Windows- und Binärsortierungen (Versionen _90 und _100). Ältere SQL Server-Sortierungen werden nicht verwendet. Innerhalb eines Cubes wird eine einzelne Sortierung verwendet, mit Ausnahme von Übersetzungen auf Attributebene. Weitere Informationen zum Definieren von Attributübersetzungen finden Sie unter [Unterstützung für Übersetzungen in Analysis Services](../analysis-services/translation-support-in-analysis-services.md).  
  
 Sortierungen steuern die Unterscheidung nach Groß-/Kleinschreibung aller Zeichenfolgen in einem „bikameralen“ Sprachskript, mit Ausnahme von Objektbezeichnern. Wenn Sie in einem Objektbezeichner Groß- und Kleinbuchstaben verwenden, beachten Sie, dass die Unterscheidung nach Groß-/Kleinschreibung von Objektbezeichnern nicht von der Sortierung bestimmt wird, sondern von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Für Objektbezeichner, die im englischen Skript verfasst werden, wird die Groß-/Kleinschreibung unabhängig von der Sortierung nie unterschieden. Für Kyrillisch und andere „bikamerale“ Sprachen gilt das Gegenteil (immer Unterscheidung nach Groß-/Kleinschreibung). Einzelheiten dazu finden Sie unter [Tipps und Best Practices für die Globalisierung &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md) .  
  
 Die Sortierung in Analysis Services ist kompatibel mit dem relationalen Datenbankmodul von SQL Server, vorausgesetzt, Sie behalten die Parität in den Sortieroptionen bei, die Sie für jeden Dienst auswählen. Wenn die relationale Datenbank beispielsweise nach Akzenten unterscheidet, sollten Sie den Cube auf die gleiche Weise konfigurieren. Es können Probleme auftreten, wenn Sortierungseinstellungen voneinander abweichen. Ein Beispiel und empfohlene Problemumgehungen finden Sie unter [Leerzeichen in einer Unicode-Zeichenfolge haben unterschiedliche Verarbeitungsergebnisse basierend auf Sortierung](http://social.technet.microsoft.com/wiki/contents/articles/23979.ssas-processing-error-blanks-in-a-unicode-string-have-different-processing-outcomes-based-on-collation-and-character-set.aspx). Weitere Informationen zur Sortierung und zum Datenbankmodul finden Sie unter [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
###  <a name="bkmk_collationtype"></a> Sortierungstypen  
 Analysis Services unterstützt zwei Sortierungstypen:  
  
-   **Windows-Sortierungen (Versionen _90 und _100)**  
  
     Versionen der Windows-Sortierung sind _90 (eine nicht markierte ältere Version) und die neuere Version _100. Nur die _100-Version zeigt die Versionsnummer im Sortierungsnamen an:  
  
    -   latin1_general  
  
    -   latin1_general_100  
  
     Eine Windows-Sortierung sortiert Zeichen anhand der linguistischen und kulturellen Merkmale der Sprache. In Windows übertrifft die Anzahl der Sortierungen die der damit verwendeten Gebietsschemas (oder Sprachen), da viele Sprachen gemeinsame Alphabete und Regeln für das Sortieren und Vergleichen von Zeichen besitzen. 33 Windows-Gebietsschemas, einschließlich aller portugiesischen und englischen Windows-Gebietsschemas, verwenden z. B. die Latin1-Codepage (1252) und folgen gemeinsamen Regeln für das Sortieren und Vergleichen von Zeichen.  
  
    > [!NOTE]  
    >  Bei der Entscheidung für eine Sortierung sollten Sie die gleiche Sortierung verwenden, die auch von der zugrunde liegenden Datenbank verwendet wird. Wenn Sie die Wahl haben, ist die _100-Version allerdings die neuere und bietet eine sprachlich präzisere kulturelle Sortierregel.  
  
-   **Binäre Sortierungen (BIN oder BIN2)**  
  
     Binäre Sortierungen sortieren nach Unicode-Codepunkten, nicht nach linguistische Werten. Beispiel: Latin1_General_BIN und Japanese_BIN führen zu unterschiedlichen Sortierergebnissen bei Verwendung mit Unicode-Daten. Bei einer linguistischen Sortierung kann sich z. B. das Ergebnis aAbBcCdD ergeben, bei einer binären Sortierung hingegen ABCDabcd, da der Codepunkt aller Großbuchstaben zusammen höher ist als die Codepunkte der Kleinbuchstaben.  
  
###  <a name="bkmk_sortorder"></a> Optionen für die Sortierreihenfolge  
 Sortieroptionen werden verwendet, um die Sortier- und Vergleichsregeln anhand der Unterscheidung nach Groß-/Kleinschreibung, Akzent, Kana und Breite zu verfeinern. Der Standardwert der Konfigurationseigenschaft **Sortierung** für [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ist beispielsweise Latin1_General_AS_CS. Damit wird angegeben, dass die Latin1_General-Sortierung mit einer Sortierreihenfolge verwendet wird, die nach Akzent sowie Groß- und Kleinschreibung unterscheidet.  
  
 Beachten Sie, dass sich BIN und BIN2 und andere Sortieroptionen gegenseitig ausschließen; wenn Sie BIN oder BIN2 verwenden möchten, müssen Sie die Sortieroption für Unterscheidung nach Akzent deaktivieren. Entsprechend sind bei Auswahl von BIN2 die Optionen für Unterscheidung nach Groß-/Kleinschreibung, Nichtunterscheidung nach Groß-/Kleinschreibung. Unterscheidung nach Akzent, Nichtunterscheidung nach Akzent, Unterscheidung nach Kana und Unterscheidung nach Breite nicht verfügbar.  
  
 In der folgenden Tabelle werden Windows-Optionen für die Sortierreihenfolge und verknüpfte Suffixe für [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]beschrieben.  
  
|Sortierreihenfolge (Suffix)|Beschreibung der Sortierreihenfolge|  
|---------------------------|----------------------------|  
|Binär (_BIN) oder BIN2 (_BIN2)|In SQL Server gibt es zwei Arten von binären Sortierungen: die älteren BIN-Sortierungen und die neueren BIN2-Sortierungen. In einer BIN2-Sortierung werden alle Zeichen entsprechend ihrer Codepunkte sortiert. In einer BIN-Sortierung wird nur das erste Zeichen entsprechend seinem Codepunkt sortiert, die anderen Zeichen jedoch nach ihren Bytewerten. (Da die Intel Plattform eine Little-Endian-Architektur aufweist, werden Unicode-Zeichen immer mit vertauschten Bytes gespeichert.)<br /><br /> Bei binären Sortierungen von Unicode-Datentypen wird das Gebietsschema bei Datensortierungen nicht berücksichtigt. Beispielsweise führen „Latin_1_General_BIN“ und „Japanese_BIN“ bei Unicode-Daten zu den gleichen Sortierergebnissen.<br /><br /> Die binäre Sortierreihenfolge unterscheidet nach Groß- und Kleinschreibung und nach Akzent. Die Option Binär ist zudem die schnellste Sortierreihenfolge.|  
|Unterscheidung nach Groß-/Kleinschreibung (_CS)|Unterscheidet zwischen Groß- und Kleinbuchstaben. Wenn diese Option ausgewählt ist, stehen Kleinbuchstaben in der Sortierreihenfolge vor ihren entsprechenden Großbuchstaben. Sie können die Nichtunterscheidung nach Groß-/Kleinschreibung durch Angabe von „_CI“ explizit festlegen. Sortierungsspezifische Einstellungen zur Groß-/Kleinschreibung gelten nicht für Objektbezeichner, wie z. B. die ID einer Dimension, eines Cube und anderer Objekte. Einzelheiten dazu finden Sie unter [Tipps und Best Practices für die Globalisierung &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md) .|  
|Unterscheidung nach Akzent (_AS)|Unterscheidet zwischen Zeichen mit Akzent und Zeichen ohne Akzent. Beispielsweise ist 'a' nicht mit 'ấ' identisch. Wenn diese Option nicht ausgewählt ist, betrachtet [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] die Zeichen mit Akzent und die Zeichen ohne Akzent für Sortierzwecke als identisch. Sie können die Nichtunterscheidung nach Akzent durch Angabe von „_AI“ explizit festlegen.|  
|Unterscheidung nach Kana (_KS)|Unterscheidet zwischen zwei japanischen Kana-Zeichen: Hiragana und Katakana. Wenn diese Option nicht ausgewählt ist, betrachtet [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Hiragana- und Katakana-Zeichen für Sortierzwecke als identisch. Es gibt kein Sortierreihenfolgensuffix für die Sortierung der Kana-Zeichen.|  
|Unterscheidung nach Breite (_WS)|Unterscheidet zwischen einem Single-Byte-Zeichen und demselben Zeichen als Double-Byte-Zeichen. Wenn diese Option nicht ausgewählt ist, betrachtet [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] die Single-Byte- und die Double-Byte-Darstellung desselben Zeichens für Sortierzwecke als identisch. Es gibt kein Sortierreihenfolgensuffix für die Sortierung mit Unterscheidung nach Breite.|  
  
##  <a name="bkmk_defaultLang"></a> Ändern der Standardsprache oder -sortierung für die Instanz  
 Standardsprache und -sortierung werden während des Setups eingerichtet, können jedoch im Rahmen der Konfiguration nach der Installation geändert werden. Das Ändern der Sortierung auf Instanzebene ist nicht trivial und mit den folgenden Anforderungen verbunden:  
  
-   Neustart des Diensts  
  
-   Aktualisieren der Sortierungseinstellungen von vorhandenen Objekten. Sortierungseinstellungen werden geerbt, nachdem das Objekt erstellt wurde. Nachfolgende Änderungen an der Sortierung müssen manuell erfolgen. Einzelheiten dazu finden Sie unter [Ändern von Sprache und Sortierung innerhalb eines Datenmodells mithilfe von XMLA](#bkmk_XMLA) finden Sie Tipps zum Weitergeben von Sortierungsänderungen im gesamten Modell.  
  
-   Erneutes Verarbeiten von Partitionen und Dimensionen, nachdem die Sortierung aktualisiert wurde  
  
 Sie können SQL Server Management Studio oder AMO PowerShell verwenden, um die Standardsprache oder -sortierung auf Serverebene zu ändern. Alternativ können Sie ändern die  **\<Sprache >** und  **\<CollationName >** Einstellungen in der Datei "Msmdsrv.ini" der LCID der Sprache angeben.  
  
1.  Klicken Sie in Management Studio mit der rechten Maustaste auf den Servernamen, und wählen Sie **Eigenschaften**  |  **Sprache/Sortierung** aus.  
  
2.  Wählen Sie die Sortieroptionen. Um entweder **Binär** oder **Binär 2**auszuwählen, deaktivieren Sie zuerst das Kontrollkästchen **Unterscheidung nach Akzent**.  
  
     Beachten Sie, dass Sortierung und Sprache vollständig unabhängige Einstellungen sind. Wenn Sie eine Einstellung ändern, werden die Werte der anderen nicht gefiltert, um gemeinsame Kombinationen anzuzeigen.  
  
3.  Aktualisieren Sie das Datenmodell, um die neue Sortierung zu verwenden (siehe folgender Abschnitt).  
  
4.  Starten Sie den Dienst neu.  
  
##  <a name="bkmk_cube"></a> Ändern von Sprache oder Sortierung für einen Cube  
  
1.  Doppelklicken Sie im Projektmappen-Explorer auf einen Cube, um ihn im Cube-Designer zu öffnen.  
  
2.  Wählen Sie den obersten Knoten im Bereich „Measures“ oder „Dimensionen“ aus. Das Objekt auf der obersten Ebene in beiden Bereichen ist der Cube.  
  
3.  Legen Sie unter „Eigenschaften“ **Language** und **Collation**fest. Die von Ihnen gewählten Werte werden von allen Cubeobjekten verwendet, einschließlich Cubedimensionen und -measures. Die Werte wirken sich auf Verarbeitungs- und Abfragevorgänge aus.  
  
     Die einzige Möglichkeit zum Einbetten von alternativen Sprach- und Sortierungseigenschaften für Objekte innerhalb des Cubes sind Übersetzungen. Weitere Informationen finden Sie unter [Unterstützung für Übersetzungen in Analysis Services](../analysis-services/translation-support-in-analysis-services.md) .  
  
##  <a name="bkmk_XMLA"></a> Ändern von Sprache und Sortierung innerhalb eines Datenmodells mithilfe von XMLA  
 Sprach- und Sortierungseinstellungen werden geerbt, nachdem das Objekt erstellt wurde. Nachfolgende Änderungen an diesen Eigenschaften müssen manuell erfolgen. Eine schnelle Möglichkeit zum Ändern der Sortierung mehrerer Objekte ist die Verwendung eines ALTER-Befehls in einem XMLA-Skript.  
  
 Standardmäßig wird die Sortierung ein Mal auf Datenbankebene festgelegt. Die Vererbung wird im weiteren Verlauf der Objekthierarchie impliziert. Wenn Sie **Collation** für Objekte innerhalb des Cubes explizit festlegen, was für einzelne Dimensionsattribute zulässig ist, wird die Einstellung in der XMLA-Definition angezeigt. Andernfalls existiert nur die Sortierungseigenschaft der obersten Ebene.  
  
 Vor der Verwendung von XMLA zum Ändern eine vorhandenen Datenbank müssen Sie sicherstellen, dass Sie keine Abweichungen zwischen der Datenbank und den Quelldateien einbringen, die zur Erstellung verwendet werden. Beispiel: Sie möchten XMLA verwenden, um schnell die Sprache oder die Sortierung für Tests von Machbarkeitsstudien zu ändern, nehmen dann aber Änderungen an der Quelldatei vor (siehe [Ändern von Sprache oder Sortierung für einen Cube](#bkmk_cube)) und stellen die Lösung mithilfe der bereits vorhandenen Betriebsverfahren erneut bereit.  
  
1.  Klicken Sie in Management Studio mit der rechten Maustaste auf die Datenbank | **Skript für Datenbank als**  |  **ALTER in**  |  **Neues Abfrage-Editor-Fenster**.  
  
2.  Suchen Sie die vorhandene Sprache oder Sortierung, und ersetzen Sie sie durch einen alternativen Wert.  
  
3.  Drücken Sie F5, um das Skript auszuführen.  
  
4.  Verarbeiten Sie den Cube erneut.  
  
##  <a name="bkmk_enablefast1033"></a> Steigern der Leistung für englische Gebietsschemas durch EnableFast1033Locale  
 Wenn Sie die Sprachen-ID English (Vereinigte Staaten), (0x0409 oder 1033), als Standardsprache für die [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Instanz verwenden, können Sie von zusätzlichen Leistungsverbesserungen profitieren, indem Sie die Konfigurationseigenschaft **EnableFast1033Locale** definieren. Es handelt sich hierbei um eine erweiterte Konfigurationseigenschaft, die nur für diese Sprachen-ID zur Verfügung steht. Wenn Sie den Wert dieser Eigenschaft auf **true** festlegen, kann [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] einen schnelleren Algorithmus für Zeichenfolge-Hashingoperationen und Zeichenfolgevergleiche verwenden. Weitere Informationen zum Festlegen der Konfigurationseigenschaften finden Sie unter [Servereigenschaften in Analysis Services](../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
##  <a name="bkmk_gb18030"></a> GB18030-Unterstützung in Analysis Services  
 GB18030 ist ein separater Standard, der in der Volksrepublik China zur Codierung von chinesischen Schriftzeichen verwendet wird. In GB18030 können Zeichen 1, 2 oder 4 Bytes lang sein. In Analysis Services wird bei der Verarbeitung von Daten aus externen Quellen keine Datenkonvertierung vorgenommen. Die Daten werden einfach als Unicode-Daten gespeichert. Zur Abfragezeit wird basierend auf den Client-Betriebssystemeinstellungen eine GB18030-Konvertierung über die Analysis Services-Clientbibliotheken durchgeführt (insbesondere mit dem OLE DB-Anbieter „MSOLAP.dll“), wenn Textdaten in den Abfrageergebnissen zurückgegeben werden. Das Datenbankmodul unterstützt GB18030 ebenfalls. Einzelheiten dazu finden Sie unter [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Globalisierungsszenarien für Analysis Services](../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Globalisierung Tipps und Best Practices &#40; Analysis Services &#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md)   
 [Sortierung und Unicode-Unterstützung](../relational-databases/collations/collation-and-unicode-support.md)  
  
  

