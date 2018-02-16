---
title: Erstellen eines Cubes mit einer Datenquellensicht | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bec845a1-d10c-4d45-9acf-0a302adfee47
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1a78f2353c7d6afa88adc0bd76c4031b9224363b
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="create-a-cube-using-a-data-source-view"></a>Erstellen eines Cubes mithilfe einer Datenquellensicht
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Verwenden Sie diese Methode zum Erstellen eines neuen Cubes, wenn Sie beabsichtigen, eine vorhandene Datenquellensicht zu verwenden. Mit dieser Methode geben Sie die Datenquellensicht an und wählen Fakten- und Dimensionstabellen aus, die Sie in der Datenquellensicht verwenden möchten. Anschließend wählen Sie die Dimensionen und Measures aus, die Sie in den Cube einschließen möchten.  
  
 Um einen Cube mit einer Datenquelle zu erstellen, klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf **Cubes** und wählen **Neuer Cube**aus. Der Cube-Assistent wird geöffnet.  
  
## <a name="selecting-the-build-method"></a>Auswählen der Erstellungsmethode  
 Klicken Sie auf der Seite **Erstellungsmethode auswählen** des Assistenten auf **Cube mithilfe einer Datenquelle erstellen**.  
  
 Wenn Sie das Kontrollkästchen **Automatisch erstellen** aktivieren, analysiert der Assistent die Datenquellensicht, um den Cube und die zugehörigen Dimensionen für Sie zu konfigurieren. Der Assistent identifiziert die Fakten- und Dimensionstabellen, wählt Measures aus, die in den Cube eingeschlossen werden sollen, und erstellt Hierarchien. Auf jeder Seite des Assistenten können Sie die vom Assistenten bei Auswahl von **Automatisch erstellen** getroffenen Auswahlen überprüfen und ändern. Wenn Sie **Automatisch erstellen**nicht aktivieren, nehmen Sie all diese Auswahlen manuell vor.  
  
 Bei Auswahl von **Automatisch erstellen**können Sie auf einer beliebigen Seite des Assistenten auf **Fertig stellen** klicken, um zur letzten Seite zu wechseln und für die verbleibenden Assistentenseiten die Standardkonfigurationen zu akzeptieren. Auf der letzten Seite des Assistenten können Sie die Struktur des Cubes überprüfen, bevor Sie den Assistenten beenden.  
  
 Wenn Sie **Automatisch erstellen**nicht aktivieren, müssen Sie die Fakten- und Dimensionstabellen selbst auswählen. Der Assistent erstellt alle Dimensionen, die Sie zur Erstellung auswählen, die benutzerdefinierten Hierarchien in den Dimensionen müssen jedoch mithilfe des Dimensions-Designers manuell erstellt werden. Diese Anforderung macht möglicherweise keinen Unterschied, wenn Sie die Dimensionen, die Sie im Cube verwenden möchten, bereits vor dem Ausführen des Cube-Assistenten erstellt haben.  
  
## <a name="selecting-the-data-source-view"></a>Auswählen der Datenquellensicht  
 Wenn Sie eine vorhandene Datenquelle zum Erstellen eines Cubes verwenden, besteht der erste Schritt darin, die Datenquellensicht anzugeben, auf der der Cube basieren soll. Wählen Sie auf der Seite **Datenquellensicht auswählen** des Assistenten eine vorhandene Datenquellensicht aus. Im Vorschaufenster können Sie die Tabellen in einer ausgewählten Datenquellensicht anzeigen. Um das Schema für eine ausgewählte Datenquellensicht anzuzeigen, klicken Sie auf **Durchsuchen**.  
  
 Wenn die zu verwendende Datenquellensicht nicht aufgelistet ist, klicken Sie im Cube-Assistenten auf **Abbrechen**und öffnen den Datenquellensicht-Assistenten. Sie können auch im Menü **Datei** auf **Neues Element** hinzufügen klicken, um eine vorhandene Datenquellensicht aus einer anderen Datenbank (oder von einem anderen Speicherort) hinzuzufügen. Weitere Informationen zum Erstellen einer Datenquellensicht finden Sie unter [Datenquellensichten in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
> [!NOTE]  
>  Eine Datenquellensicht muss mindestens eine Tabelle enthalten, damit sie auf dieser Seite aufgeführt wird. Sie können keinen Cube auf Grundlage einer Datenquellensicht erstellen, die keine Tabellen aufweist.  
  
## <a name="identify-fact-and-dimension-tables"></a>Identifizieren von Fakten- und Dimensionstabellen  
 Verwenden Sie im Cube-Assistenten die Seite **Fakten- und Dimensionstabellen identifizieren** , um die Fakten- und Dimensionstabellen auszuwählen, die zum Erstellen des Cubes erforderlich sind. Wenn Sie das Kontrollkästchen **Automatisch erstellen** zum Erstellen des Cubes aktiviert haben, sind beim ersten Öffnen dieser Seite die vom Assistenten erkannten Fakten- oder Dimensionstabellen ausgewählt. Wenn der Assistent eine Tabelle erkennt, die sowohl eine Faktentabelle als auch eine Dimensionstabelle darstellt, werden beide Spalten ausgewählt. Wenn der Assistent eine Tabelle erkennt, die keines von beiden ist, wird keine Spalte ausgewählt. Wenn Sie keine Tabelle für den Cubeentwurf benötigen, deaktivieren Sie die Kontrollkästchen **Fakt** und **Dimension** .  
  
 Falls Sie das Kontrollkästchen **Automatisch erstellen** nicht aktiviert haben, müssen Sie alle Auswahlen manuell vornehmen. Verwenden Sie die Registerkarte **Tabellen** oder **Diagramm** :  
  
-   Auf der Registerkarte **Tabellen** werden die Tabellen im Tabellenformat aufgelistet. Aktivieren Sie das Kontrollkästchen in der Spalte **Fakt** oder **Diagramm** .  
  
-   Auf der Registerkarte **Diagramm** wird das Schema der Datenquellensicht angezeigt. Die Tabellen sind farblich codiert, um Fakten oder Dimensionen anzugeben. Klicken Sie auf eine beliebige Tabelle im Schema, und klicken Sie dann auf **Fakt** oder **Dimension** , um die Einstellung für diese Tabelle zu aktivieren oder zu deaktivieren. Verwenden Sie zum Ändern der Vergrößerung die Schaltfläche **Zoom** .  
  
> [!NOTE]  
>  Auf der Registerkarte **Diagramm** können Sie das Assistentenfenster vergrößern oder maximieren, um das Schema anzuzeigen.  
  
 Wenn die Datenquellensicht eine Zeitdimensionstabelle enthält, wählen Sie sie in der Liste **Zeitdimensionstabelle** aus. Wenn keine vorhanden sind, lassen Sie  **\<None >** ausgewählten. Dies ist das Standardelement in der Liste. Durch Auswahl einer Tabelle als Zeitdimensionstabelle wird sie auch auf den Registerkarten **Tabellen** und **Diagramm** als Dimensionstabelle ausgewählt.  
  
## <a name="defining-time-periods"></a>Definieren von Zeiträumen  
 Wenn Sie beim Auswählen von Tabellentypen eine Zeitdimensionstabelle angegeben haben, verwenden Sie die Seite **Zeiträume definieren** des Assistenten, um die Spalten in der Tabelle anzugeben, die Standardzeiträumen entsprechen. Suchen Sie die Standardzeiträume unter **Zeiteigenschaftsname**. Wählen Sie für jede Zeile, die in der Zeitdimensionstabelle über eine entsprechende Spalte verfügt, unter **Zeittabellenspalten**die richtige Spalte aus. Der Assistent verwendet die von Ihnen angegebenen Zuordnungen, um Attribute zu erstellen und Zeithierarchien vorzuschlagen, die für die Daten geeignet sind. Durch diese Zuordnungen wird auch die Eigenschaft **Typ** für die entsprechenden Attribute in der neuen Zeitdimension festgelegt. Der Assistent erstellt dann auf Grundlage einer Zeitdimensionstabelle eine Zeitdimension.  
  
 Nachdem Sie den Cube erstellt haben, können Sie dem Cube mithilfe des Business Intelligence-Assistenten Zeitintelligenzerweiterungen hinzufügen. Zu diesen Erweiterungen zählen die Sichten Zeitraum bis Datum, Gleitender Durchschnitt und Zeitraumvergleich.  
  
## <a name="selecting-dimensions"></a>Auswählen von Dimensionen  
 Mithilfe der Seite **Dimensionen auswählen** des Assistenten können Sie dem Cube vorhandene Dimensionen hinzufügen. Diese Seite wird nur angezeigt, wenn bereits gemeinsame Dimensionen vorhanden sind, die Dimensionstabellen im neuen Cube entsprechen.  
  
 Um vorhandene Dimensionen hinzuzufügen, wählen Sie mindestens eine Dimension aus der Liste **Gemeinsame Dimensionen** aus, und klicken Sie auf die Schaltfläche mit dem Pfeil nach rechts (**>**), um sie in die Liste **Cubedimensionen** zu verschieben. Klicken Sie auf die Schaltfläche mit dem Doppelpfeil (**>>**), um alle Dimensionen in der Liste zu verschieben.  
  
 Wenn eine vorhandene Dimension entgegen Ihrer Erwartung nicht in der Liste angezeigt wird, können Sie auf **Zurück** klicken und die Tabellentypeinstellungen für mindestens eine Tabelle ändern. Eine vorhandene Dimension muss sich auch auf mindestens eine der Faktentabellen im Cube beziehen, damit sie in der Liste **Gemeinsame Dimensionen** angezeigt wird.  
  
## <a name="selecting-measures"></a>Auswählen von Measures  
 Wählen Sie auf der Assistentenseite **Measures auswählen** die Measures aus, die Sie in den Cube einschließen möchten. Jede als Faktentabelle gekennzeichnete Tabelle wird in dieser Liste als Measuregruppe angezeigt, und jede numerische Nichtschlüsselspalte wird in der Liste als Measure angezeigt. Standardmäßig wird jedes Measure in jeder Measuregruppe ausgewählt. Sie können das Kontrollkästchen neben den Measures deaktivieren, die Sie nicht in den Cube einschließen möchten. Um alle Measures einer Measuregruppe aus dem Cube zu entfernen, deaktivieren Sie das Kontrollkästchen **Measuregruppen/Measures** .  
  
 Die Namen der Measures, die unter **Measuregruppen/Measures** aufgeführt sind, entsprechen Spaltennamen. Sie können auf die Zelle klicken, die einen Namen enthält, um den Namen zu bearbeiten.  
  
 Um Daten für ein beliebiges Measure anzuzeigen, klicken Sie mit der rechten Maustaste auf eine Measurezeile in der Liste und klicken dann auf **Beispieldaten anzeigen**. Dadurch wird der **Datenstichproben-Viewer** geöffnet, und es werden maximal die ersten 1000 Datensätze aus der entsprechenden Faktentabelle angezeigt.  
  
## <a name="reviewing-new-dimensions"></a>Prüfen neuer Dimensionen  
 Verwenden Sie die Assistentenseite **Neue Dimensionen prüfen** , um die Strukturen aller vom Assistenten erstellten Dimensionen zu überprüfen. Auf dieser Seite des Assistenten sind die Dimensionen in der Strukturansicht **Neue Dimensionen** aufgeführt. Zum Überprüfen der Dimensionen stehen folgende Methoden zur Verfügung:  
  
-   Erweitern Sie eine beliebige Dimension, um deren Attribute und Hierarchien anzuzeigen.  
  
-   Erweitern Sie den Ordner **Attribute** unter einer beliebigen Dimension, um die Attribute in der Dimension anzuzeigen.  
  
-   Erweitern Sie den Ordner **Hierarchie** unter einer beliebigen Dimension, um die Hierarchien in der Dimension anzuzeigen.  
  
-   Erweitern Sie eine beliebige Hierarchie, um deren Ebenen anzuzeigen.  
  
> [!NOTE]  
>  Sie können das Assistentenfenster vergrößern oder maximieren, damit die Struktur besser zu sehen ist.  
  
 Um ein Objekt in der Struktur aus dem Cube zu entfernen, deaktivieren Sie das Kontrollkästchen daneben. Wenn das Kontrollkästchen neben einem Objekt deaktiviert wird, werden auch alle Objekte unterhalb des Objekts entfernt. Da Abhängigkeiten zwischen Objekten erzwungen werden, werden auch alle vom Attribut abhängigen Hierarchieebenen entfernt, wenn Sie ein Attribut entfernen. Wenn Sie beispielsweise ein Kontrollkästchen neben einer Hierarchie deaktivieren, werden die Kontrollkästchen neben allen Ebenen in der Hierarchie ebenfalls deaktiviert und sowohl die Ebenen als auch die Hierarchien entfernt. Das Schlüsselattribut einer Dimension kann nicht entfernt werden.  
  
 Sie können eine beliebige Dimension, den Attribut, die Hierarchie oder Ebene umbenennen, entweder durch Klicken auf den Namen oder durch Rechtsklick auf den Namen und klicken Sie dann auf das Kontextmenü auf klicken **umbenennen \<Objekt >**, wobei  **\< Objekt >** ist **Dimension**, **Attribut**, oder **Ebene**.  
  
 Es muss nicht unbedingt eine 1:1-Beziehung zwischen der Anzahl der auf der Assistentenseite **Fakten- und Dimensionstabellen identifizieren** definierten Dimensionstabellen und der Anzahl der auf dieser Seite des Assistenten aufgeführten Dimensionen bestehen. Abhängig von den Beziehungen zwischen den Tabellen in der Datenquellensicht kann der Assistent zwei oder mehr Tabellen verwenden, um eine Dimension zu erstellen (wie z. B. für ein Schneeflockenschema erforderlich).  
  
## <a name="completing-the-cube-wizard"></a>Abschließen des Cube-Assistenten  
 Auf der Seite **Assistenten abschließen** des Assistenten können Sie die Measuregruppen, Measures und Dimensionen im neuen Cube anzeigen. Geben Sie im Feld **Cubename** einen Namen für den Cube ein. Wenn der Cube Ihren Vorstellungen entspricht, klicken Sie auf **Fertig stellen**. Andernfalls klicken Sie auf **Zurück** , um zu einer vorherigen Assistentenseite zu wechseln und Änderungen vorzunehmen.  
  
  
