---
title: Erteilen von benutzerdefiniertem Zugriff auf dimensiondaten (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f6a10ec3bab74c2bd5c540b1816d77c2dcbd104c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="grant-custom-access-to-dimension-data-analysis-services"></a>Erteilen eines benutzerdefinierten Zugriffs auf Dimensiondaten (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Nach der Aktivierung des Lesezugriffs auf einen Cube können Sie zusätzliche Berechtigungen festlegen, die den Zugriff auf Dimensionselemente ausdrücklich zulassen oder verweigern (einschließlich der Measures, die in der Measuredimension enthalten sind, die alle in einem Cube verwendeten Measures enthält). Wenn Sie beispielsweise mehrere Kategorien von Resellern haben, möchten Sie möglicherweise Berechtigungen festlegen, um Daten für einen bestimmten Unternehmenstyp auszuschließen. In der folgenden Abbildung ist die Vorher-und-Nachher-Auswirkung des Verweigerns des Zugriffs auf den Unternehmenstyp "Warehouse" in der Dimension "Reseller" dargestellt.  
  
 ![PivotTables mit und ohne Dimensionselement](../../analysis-services/multidimensional-models/media/ssas-permsdimdenied.png "PivotTables mit und ohne Dimensionselement")  
  
 Standardmäßig können Sie Daten aus einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Cube lesen und verfügen automatisch über Leseberechtigungen für alle Measures und Dimensionselemente, die diesem Cube zugeordnet sind. Zwar mag dieses Verhalten für viele Szenarien ausreichen, aber manchmal erfordern Sicherheitsanforderungen eine stärker segmentierte Autorisierungsstrategie mit unterschiedlichen Zugriffsstufen für verschiedene Benutzer für dieselbe Dimension.  
  
 Sie können den Zugriff einschränken, indem Sie auswählen, für welche Elemente der Zugriff zugelassen (AllowedSet) oder verweigert (DeniedSet) wird. Dafür aktivieren oder deaktivieren Sie Dimensionselemente, die in die Rolle eingeschlossen oder davon ausgeschlossen werden.  
  
 Die Standarddimensionssicherheit ist die einfachste: Sie wählen einfach aus, welche Dimensionsattribute und Attributhierarchien in die Rolle eingeschlossen oder daraus ausgeschlossen werden. Die erweiterte Sicherheit ist komplexer und erfordert Kenntnisse im MDX-Skripting. Beiden Ansätze werden im Folgenden beschrieben.  

> [!NOTE]  
>  Die folgenden Anweisungen setzen eine Clientverbindung voraus, die Abfragen in MDX ausgibt. Wenn der Client DAX verwendet, wie z.B. Power View in Power BI, ist die Dimensionssicherheit in den Abfrageergebnissen nicht ersichtlich. Weitere Informationen finden Sie unter [Grundlegendes zu Power View für mehrdimensionale Modelle](understanding-power-view-for-multidimensional-models.md) .
      
## <a name="prerequisites"></a>Erforderliche Komponenten  
 Nicht alle Measures oder Dimensionselemente können in benutzerdefinierten Zugriffsszenarien verwendet werden. Eine Verbindung schlägt fehl, wenn eine Rolle den Zugriff auf ein Standardmeasure oder -element oder auf Measures einschränkt, die Teil von Measureausdrücken sind.  
  
 **Prüfen Sie, ob Hindernisse für die Dimensionssicherheit vorhanden sind: Standardmeasures, Standardelemente und in Measureausdrücken verwendete Measures.**  
  
1.  Klicken Sie in SQL Server Management Studio mit der rechten Maustaste auf einen Cube, und wählen Sie **Skript für Cube als** | **ALTER in** | **Neues Abfrage-Editor-Fenster**.  
  
2.  Suchen Sie nach **DefaultMeasure**. Sie sollten eins für den Cube und eins für jede Perspektive finden. Wenn Sie die Dimensionssicherheit definieren, sollten Sie vermeiden, den Zugriff auf Standardmeasures einzuschränken.  
  
3.  Suchen Sie als Nächstes nach **MeasureExpression**. Ein Measureausdruck ist ein Measure, das auf einer Berechnung basiert, wobei die Berechnung oft weitere Measures beinhaltet. Vergewissern Sie sich, dass das Measure, das Sie einschränken möchten, nicht in einem Ausdruck verwendet wird. Alternativ fahren Sie fort, und schränken Sie den Zugriff ein. Stellen Sie dabei nur sicher, dass Sie auch alle Referenzen auf dieses Measure im gesamten Cube ausschließen.  
  
4.  Abschließend suchen Sie nach **DefaultMember**. Notieren Sie alle Attribute, die als Standardelement eines Attributs dienen. Vermeiden Sie, Einschränkungen für diese Attribute festzulegen, wenn Sie die Dimensionssicherheit einrichten.  
  
## <a name="basic-dimension-security"></a>Standarddimensionssicherheit  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]her, erweitern Sie im Objekt-Explorer das **Rollen** -Element für die entsprechende Datenbank, und klicken Sie dann auf eine Datenbankrolle (oder erstellen Sie eine neue Datenbankrolle).  
  
     Die sollte bereits über Lesezugriff für den Cube verfügen. Weitere Informationen finden Sie unter [Erteilen von Cube- oder Modellberechtigungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md) .  
  
2.  Wählen Sie unter **Dimensionsdaten** | **Standard**die Dimension aus, für die Sie Berechtigungen festlegen.  
  
3.  Wählen Sie die Attributhierarchie aus. Es werden nicht alle Attribute zur Verfügung stehen. Nur die Attribute mit **AttributeHierarchyEnabled** werden in der Liste **Attributhierarchie** angezeigt.  
  
4.  Wählen Sie aus, für welche Elemente der Zugriff zugelassen oder verweigert wird. Standardmäßig wird der Zugriff über die Option **Alle Elemente auswählen** zugelassen. Wir schlagen vor, dass Sie diese Standardeinstellung beibehalten und dann einzelne Elemente löschen, die für die Windows-Benutzer- und -Gruppenkonten im Bereich **Mitgliedschaften** über diese Rolle nicht sichtbar sein sollten. Der Vorteil ist, dass neue Elemente, die in zukünftigen Verarbeitungsvorgängen hinzugefügt werden, automatisch für Personen verfügbar sind, die eine Verbindung über diese Rolle herstellen.  
  
     Alternativ können Sie über die Option **Auswahl aufheben** den Zugriff insgesamt widerrufen und dann auswählen, welche Elemente zugelassen werden. Bei zukünftigen Verarbeitungsvorgängen sind neue Elemente erst sichtbar, wenn Sie die Dimensionsdatensicherheit manuell bearbeiten und den Zugriff darauf zulassen.  
  
5.  Klicken Sie optional auf **Erweitert** , um **Sichtbare Gesamtwerte** für diese Attributhierarchie zu aktivieren. Mit dieser Option werden Aggregation auf der Basis der durch die Rolle verfügbaren Elemente neu berechnet.  
  
    > [!NOTE]  
    >  Beim Zuweisen von Berechtigungen, die Dimensionselemente entfernen, werden aggregierte Gesamtwerte nicht automatisch neu berechnet. Nehmen wir an, das Element **Alle** einer Attributhierarchie gibt die Anzahl 200 zurück, bevor Berechtigungen angewendet werden. Nach der Anwendung von Berechtigungen, die den Zugriff auf einige Elemente verweigern, gibt **Alle** immer noch 200 zurück, obwohl viel weniger für den Benutzer sichtbare Elementwerte vorhanden sind. Um Missverständnisse bei den Consumern Ihres Cubes zu vermeiden, können Sie das Element **Alle** als Aggregat nur für die Elemente konfigurieren, zu denen Rollenmitglieder gehören, statt als Aggregat für alle Elemente der Attributhierarchie. Zum Aufrufen dieses Verhaltens können Sie auf der Registerkarte **Erweitert** die Option **Sichtbare Gesamtwerte** aktivieren, wenn Sie die Dimensionssicherheit konfigurieren. Nach der Aktivierung wird das Aggregat zum Abfragezeitpunkt berechnet, statt von vorab berechneten Aggregationen abgerufen zu werden. Dies kann eine spürbare Auswirkung auf die Abfrageleistung und sollte nur verwendet werden, wenn es notwendig ist.  
  
## <a name="hiding-measures"></a>Ausblenden von Measures  
 Stellen Sie in [Erteilen von benutzerdefiniertem Zugriff auf Zellendaten &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)wurde erläutert, dass zum vollständigen Ausblenden aller visuellen Aspekte eines Measures – nicht nur seiner Zellendaten – Berechtigungen für Dimensionselemente erforderlich sind. In diesem Abschnitt wird erklärt, wie Sie den Zugriff auf die Objektmetadaten eines Measures verweigern.  
  
1.  Scrollen Sie unter **Dimensionsdaten** | **Standard**in der Liste der Dimensionen, bis Sie die Cubedimensionen erreichen. Wählen Sie dann **Measuredimension**aus.  
  
2.  Deaktivieren Sie in der Liste der Measures das Kontrollkästchen für Measures, die für Benutzer nicht angezeigt werden sollten, die eine Verbindung über diese Rolle herstellen.  
  
> [!NOTE]  
>  Überprüfen Sie die Voraussetzungen, um zu erfahren, wie Sie Measures erkennen, die die Rollensicherheit durchbrechen.  
  
## <a name="advanced-dimension-security"></a>Erweiterte Dimensionssicherheit  
 Wenn Sie über MDX-Kenntnisse verfügen, besteht ein weiterer Ansatz darin, MDX-Ausdrücke zu schreiben, mit denen die Kriterien festgelegt werden, für welche Elemente der Zugriff zugelassen oder verweigert wird. Klicken Sie auf **Rolle erstellen** | **Dimensionsdaten** | **Erweitert** , um das Skript bereitzustellen.  
  
 Zum Schreiben der MDX-Anweisung können Sie den MDX-Generator verwenden. Informationen dazu finden Sie unter [MDX-Generator &#40;Analysis Services – Mehrdimensionale Daten&#41;](http://msdn.microsoft.com/library/fecbf093-65ea-4e1b-b637-f04876f1cb0f). Die Registerkarte **Erweitert** enthält die folgenden Optionen:  
  
 **Attribut**  
 Wählen Sie das Attribut aus, für das Sie Einstellungen der Elementsicherheit verwalten möchten.  
  
 **Zulässige Elementgruppe**  
 Die Eigenschaft AllowedSet kann zu keinen Elementen (Standard), allen Elementen oder einigen Elementen aufgelöst werden. Wenn Sie das Zugreifen auf ein Attribut zulassen und keine Elemente der zulässigen Gruppe definieren, wird Zugriff auf alle Elemente gewährt. Wenn Sie den Zugriff auf ein Attribut zulassen und eine bestimmte Gruppe an Attributelementen definieren, sind nur die ausdrücklich zulässigen Elemente sichtbar.  
  
 Die Erstellung von AllowedSet wirkt sich wellenartig aus, wenn das Attribut Teil einer Hierarchie mit mehreren Ebenen ist. Nehmen wir beispielsweise an, eine Rolle gewährt den Zugriff auf den Staat Washington (gehen Sie von einem Szenario aus, in dem die Rolle Berechtigungen für die Vertriebsabteilung eines Unternehmens im Staat Washington gewährt). Für Personen, die eine Verbindung über diese Rolle herstellen, werden bei Anfragen, die Vorgänger (USA) oder Nachfolger (Seattle und Redmond) enthalten, nur Elemente in einer Kette angezeigt, die den Staat Washington enthält. Da andere Staaten ausdrücklich nicht zulässig sind, ist die Wirkung dieselbe, als wären sie verweigert.  
  
> [!NOTE]  
>  Wenn Sie eine leere Menge definieren ({}) von Attributelementen, werden keine Elemente des Attributs für die Datenbankrolle sichtbar werden. Eine fehlende zulässige Gruppe wird nicht als leere Gruppe interpretiert.  
  
 **Verweigerte Elementgruppe**  
 Die Eigenschaft DeniedSet kann zu keinen Elementen, allen Elementen (Standard) oder einigen Attributelementen aufgelöst werden. Wenn die verweigerte Gruppe nur eine bestimmte Gruppe von Attributelementen enthält, wird der Datenbankrolle der Zugriff nur auf diese bestimmten Elemente sowie auf Nachfolger verweigert, wenn sich das Attribut in einer Hierarchie mit mehreren Ebenen befindet. Denken Sie an das Beispiel der Vertriebsabteilung im Staat Washington. Wenn Washington in DeniedSet platziert wird, werden den Personen, die eine Verbindung über diese Rolle herstellen, alle Staaten außer Washington und seinen Nachfolgerattributen angezeigt.  
  
 Erinnern Sie sich aus dem vorherigen Abschnitt, dass die verweigerte Gruppe eine feste Auflistung ist. Wenn die Verarbeitung nachfolgend neue Elemente einführt, denen der Zugriff ebenfalls verweigert werden sollte, müssen Sie diese Rolle bearbeiten, um diese Elemente zur Liste hinzuzufügen.  
  
 **Standardelement**  
 Die Eigenschaft DefaultMember bestimmt das Dataset, das an einen Client zurückgegeben wird, wenn ein Attribut nicht ausdrücklich in eine Abfrage eingeschlossen ist. Wenn das Attribut nicht explizit eingeschlossen ist, verwendet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eines der folgenden Standardelemente für das Attribut:  
  
-   Wenn die Datenbankrolle ein Standardelement für das Attribut definiert, verwendet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dieses Standardmitglied.  
  
-   Wenn die Datenbankrolle kein Standardelement für das Attribut definiert, verwendet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dieses Standardmitglied, das für das Attribut selbst definiert wurde. Wenn Sie keine anderen Festlegungen treffen, ist das Standardelement für ein Attribut das **Alle** -Element (es sei denn, das Attribut ist als nicht aggregierbar definiert).  
  
 Beispiel: Eine Datenbankrolle gibt **Männlich** als Standardelement für das Attribut **Geschlecht** an. Wenn eine Abfrage nicht ausdrücklich sowohl das Attribut **Geschlecht** einschließt als auch ein anderes Element für dieses Attribut angibt, gibt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ein Dataset zurück, das lediglich männliche Kunden einschließt. Weitere Informationen zum Festlegen des Standardelements finden Sie unter [Definieren eines Standardelements](../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md).  
  
 **Sichtbarer Gesamtwert aktivieren**  
 Die VisualTotals-Eigenschaft gibt an, ob die angezeigten aggregierten Zellenwerte gemäß allen Zellenwerten oder nur gemäß den Zellenwerten berechnet werden, die für die Datenbankrolle sichtbar sind.  
  
 Standardmäßig ist die VisualTotals-Eigenschaft deaktiviert (auf **False**festgelegt). Diese Standardeinstellung maximiert die Leistung, da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] das Gesamtergebnis aller Zellenwerte schnell berechnen kann, ohne Zeit für das Auswählen der zu berechnenden Zellenwerte aufwenden zu müssen.  
  
 Das Deaktivieren der VisualTotals-Eigenschaft kann jedoch zum Sicherheitsproblem werden, wenn ein Benutzer die aggregierten Zellenwerte verwenden kann, um Werte für Attributelemente abzuleiten, auf die die Datenbankrolle des Benutzers keinen Zugriff hat. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verwendet beispielsweise die Werte für drei Attributelemente, um einen aggregierten Zellenwert zu berechnen. Die Datenbankrolle verfügt über die Zugriffsrechte zum Anzeigen zwei dieser drei Attributelemente. Mithilfe des aggregierten Zellenwertes wäre ein Mitglied dieser Datenbankrolle in der Lage, den Wert für das dritte Attributelement abzuleiten.  
  
 Durch Festlegen der VisualTotals-Eigenschaft auf **True** lässt sich dieses Risiko ausschließen. Wenn Sie die VisualTotals-Eigenschaft aktivieren, kann eine Datenbankrolle aggregierte Gesamtergebnisse nur für Dimensionselemente anzeigen, für die die Rolle die entsprechende Berechtigung aufweist.  
  
 **Check**  
 Klicken Sie, um die auf dieser Seite definierte MDX-Syntax zu testen.  
  
## <a name="see-also"></a>Siehe auch  
 [Erteilen von Cube- oder Modellberechtigungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)   
 [Erteilen von benutzerdefiniertem Zugriff auf Zellendaten &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)   
 [Erteilen von Berechtigungen für Datamining-Strukturen und Modelle &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [Erteilen von Berechtigungen für ein Datenquellenobjekt & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md)  
  
  
