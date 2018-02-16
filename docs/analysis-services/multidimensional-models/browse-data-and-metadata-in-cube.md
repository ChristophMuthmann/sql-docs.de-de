---
title: Durchsuchen von Daten und Metadaten in Cube | Microsoft Docs
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
ms.assetid: 5faf2a9d-df39-465f-9c81-a00d5cd63f5a
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0159070eb0405e49f9813828aa82b1483008b61f
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="browse-data-and-metadata-in-cube"></a>Durchsuchen von Daten und Metadaten in Cube
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Klicken Sie im Cube-Designer auf die Registerkarte **Browser** , um Cubedaten zu durchsuchen. Sie können diese Ansicht verwenden, um die Struktur eines Cubes zu untersuchen und die Daten, die Berechnung, die Formatierung und die Sicherheit der Datenbankobjekte zu überprüfen. Sie können schnell einen Cube untersuchen, während dieser von Endbenutzern in Berichterstellungstools oder anderen Clientanwendungen angezeigt wird. Wenn Sie Cubedaten durchsuchen, können Sie unterschiedliche Dimensionen anzeigen, einen Drilldown in Elemente ausführen und die Dimensionen in Slices aufteilen.  
  
 Bevor Sie einen Cube durchsuchen, müssen Sie ihn verarbeiten und erneut eine Verbindung damit herstellen. Nach der Verarbeitung öffnen Sie im Cube-Designer die Registerkarte **Browser** . Klicken Sie auf der Symbolleiste auf die Schaltfläche Verbindung wiederherstellen, um die Verbindung zu aktualisieren.  
  
 Die Registerkarte **Browser** verfügt über drei Bereiche: Metadaten, Filter und Daten. Verwenden Sie den Bereich Metadaten, um die Struktur des Cubes im Strukturformat zu untersuchen. Verwenden Sie den Bereich **Filter** oben auf der Registerkarte Browser, um einen beliebigen Teilcube zu definieren, den Sie durchsuchen möchten. Verwenden Sie den Bereich Daten, um das Resultset anzuzeigen und einen Drilldown durch Dimensionshierarchien auszuführen.  
  
## <a name="setting-up-the-browser"></a>Einrichten des Browsers  
 Um die Suche in einem Cube vorzubereiten, können Sie eine gewünschte Perspektive oder Übersetzung angeben. Fügen Sie dem Bereich Daten Measures und Dimensionen hinzu, und geben Sie im Bereich Filter Filter an.  
  
##### <a name="specifying-a-perspective"></a>Angeben einer Perspektive  
 Verwenden Sie die Liste **Perspektive** , um eine für den Cube definierte Perspektive auszuwählen. Perspektiven werden im Cube-Designer auf der Registerkarte **Perspektiven** definiert. Um zu einer anderen Perspektive zu wechseln, wählen Sie eine beliebige Perspektive aus der Liste aus.  
  
##### <a name="specifying-a-translation"></a>Angeben einer Übersetzung  
 Verwenden Sie die Liste **Sprache** , um eine für den Cube definierte Übersetzung auszuwählen. Übersetzungen werden im Cube-Designer auf der Registerkarte **Übersetzungen** definiert. Auf der Registerkarte **Browser** werden anfänglich Beschriftungen für die Standardsprache angezeigt, die über die **Language** -Eigenschaft für den Cube angegeben wird. Um zu einer anderen Sprache zu wechseln, wählen Sie eine beliebige Sprache aus der Liste aus.  
  
##### <a name="formatting-the-data-pane"></a>Formatieren des Bereichs "Daten"  
 Sie können Beschriftungen und Zellen im Bereich Daten formatieren. Klicken Sie mit der rechten Maustaste auf die ausgewählten Zellen oder die Beschriftungen, die Sie formatieren möchten, und klicken Sie dann auf **Befehle und Optionen**. Abhängig von der Auswahl werden im Dialogfeld **Befehle und Optionen** Einstellungen für **Format**, **Filtern und Gruppieren**, **Bericht**und **Verhalten**angezeigt.  
  
## <a name="setting-up-the-data"></a>Einrichten der Daten  
  
##### <a name="adding-or-removing-measures"></a>Hinzufügen oder Entfernen von Measures  
 Ziehen Sie die Measures, die durchsucht werden sollen, aus dem Bereich Metadaten auf den Detailbereich im Bereich Daten, der dem großen leeren Bereich unten rechts im Arbeitsbereich entspricht. Während Sie zusätzliche Measures ziehen, werden diese als Spalten hinzugefügt. Eine vertikale Linie gibt an, wo jedes zusätzliche Measure abgelegt wird. Wenn Sie den Ordner **Measures** ziehen, werden automatisch alle Measures im Detailbereich abgelegt.  
  
 Um ein Measure aus dem Detailbereich zu entfernen, ziehen Sie es entweder aus dem Datenbereich heraus, oder klicken Sie mit der rechten Maustaste darauf, und klicken Sie dann im Kontextmenü auf **Löschen** .  
  
##### <a name="adding-or-removing-dimensions"></a>Hinzufügen oder Entfernen von Dimensionen  
 Ziehen Sie die Hierarchien oder Dimensionen in die Zeilen- oder Filterbereiche.  
  
 Wenn Sie mehrere Dimensionen verwenden möchten, verwenden Sie In Excel analysieren. In Excel analysieren ist eine Verknüpfung, durch die Excel gestartet wird, wenn die Anwendung auf demselben Computer wie [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]installiert ist. In Excel wird eine Arbeitsmappe geöffnet, die eine vorhandene Verbindung zur aktuellen Datenbank und eine PivotTable-Feldliste enthält, in die Measures und Dimensionen vorab geladen wurden. Weitere Informationen finden Sie unter [Analysieren in Excel &#40;Registerkarte „Browser“, Cube-Designer, Analysis Services – mehrdimensionale Daten&#41;](http://msdn.microsoft.com/library/890ed457-137e-44ac-9b2c-83344a1b8fc9).  
  
 Um eine Dimension zu entfernen, ziehen Sie sie entweder aus dem Datenbereich heraus, oder klicken Sie mit der rechten Maustaste darauf, und klicken Sie dann im Kontextmenü auf **Löschen**.  
  
##### <a name="adding-or-removing-filters"></a>Hinzufügen oder Entfernen von Filtern  
 Zum Hinzufügen eines Filters können Sie eine der beiden folgenden Methoden verwenden:  
  
-   Erweitern Sie eine Dimension im Bereich Metadaten, und ziehen Sie dann eine Hierarchie in den Bereich Filter.  
  
     \- oder –  
  
-   In der **Dimension** Spalte die **Filter** Bereich, klicken Sie auf  **\<Dimension auswählen >** wählen Sie eine Dimension aus der Liste, und klicken Sie auf  **\<Hierarchie auswählen >** in der **Hierarchie** Spalte, und wählen Sie eine Hierarchie aus der Liste.  
  
 Nachdem Sie die Hierarchie angegeben haben, geben Sie den Operator und den Filterausdruck an. In der folgenden Tabelle werden die Operatoren und die Filterausdrücke beschrieben.  
  
|Operator|Filterausdruck|Description|  
|--------------|-----------------------|-----------------|  
|Gleich|Ein oder mehrere Elemente|Werte müssen gleich einem angegebenen Element sein.<br /><br /> (Stellt für andere Attributhierarchien als Über-/Unterordnungshierarchien die Auswahl mehrerer Elemente und für sonstige Hierarchien die Auswahl einzelner Elemente bereit.)|  
|Ungleich|Ein oder mehrere Elemente|Die Werte dürfen nicht gleich einem angegebenen Element sein.<br /><br /> (Stellt für andere Attributhierarchien als Über-/Unterordnungshierarchien die Auswahl mehrerer Elemente und für sonstige Hierarchien die Auswahl einzelner Elemente bereit.)|  
|In|Eine oder mehrere benannte Mengen|Werte müssen in einer angegebenen benannten Menge enthalten sein.<br /><br /> (Wird nur für Attributhierarchien unterstützt.)|  
|Nicht in|Eine oder mehrere benannte Mengen|Werte dürfen nicht in einer angegebenen benannten Menge enthalten sein.<br /><br /> (Wird nur für Attributhierarchien unterstützt.)|  
|Bereich (inklusiv)|Eine oder zwei begrenzende Elemente eines Bereichs|Werte müssen gleich den begrenzenden Elementen sein oder dazwischen liegen. Wenn die begrenzenden Elemente gleich sind oder nur ein Element angegeben ist, wird kein Bereich erstellt, und alle Werte sind zulässig.<br /><br /> (Wird nur für Attributhierarchien unterstützt. Die Bereichswerte müssen sich auf einer Hierarchieebene befinden. Unbegrenzte Bereiche werden derzeit nicht unterstützt.)|  
|Bereich (exklusiv)|Eine oder zwei begrenzende Elemente eines Bereichs|Werte müssen zwischen den begrenzenden Elementen liegen. Wenn die begrenzenden Elemente gleich sind oder nur ein Element angegeben ist, müssen die Werte größer oder kleiner als das begrenzende Element sein.<br /><br /> (Wird nur für Attributhierarchien unterstützt. Die Bereichswerte müssen sich auf einer Hierarchieebene befinden. Unbegrenzte Bereiche werden derzeit nicht unterstützt.)|  
|MDX|Ein MDX-Ausdruck, der eine Elementgruppe zurückgibt.|Werte müssen in der Gruppe berechneter Elemente liegen. Bei Auswahl dieser Option wird das Dialogfeld **Generator für berechnete Elemente** zum Erstellen von MDX-Ausdrücken angezeigt.|  
  
 Bei benutzerdefinierten Hierarchien, in denen mehrere Elemente in einem Filterausdruck angegeben sein können, müssen sich alle angegebenen Elemente auf derselben Ebene befinden und dasselbe übergeordnete Element haben. Diese Einschränkung gilt nicht für Über-/Unterordnungshierarchien.  
  
## <a name="working-with-data"></a>Arbeiten mit Daten  
  
##### <a name="drilling-down-into-a-member"></a>Ausführen von Drilldowns in ein Element  
 Um einen Drilldown in ein bestimmtes Element auszuführen, klicken Sie auf das Pluszeichen (+) neben dem Element, oder doppelklicken Sie auf das Element.  
  
##### <a name="slicing-through-cube-dimensions"></a>Aufteilen von Cubedimensionen in Slices  
 Um die Cubedaten zu filtern, klicken Sie in der Spaltenüberschrift der obersten Ebene auf das Dropdown-Listenfeld. Sie können die Hierarchie erweitern und ein Element auf einer beliebigen Ebene auswählen oder löschen, um es mit allen seinen untergeordneten Elementen ein- oder auszublenden. Deaktivieren Sie das Kontrollkästchen neben **(Alle)** , um alle Elemente in der Hierarchie auszublenden.  
  
 Nachdem Sie diesen Filter für Dimensionen festgelegt haben, können Sie ihn aktivieren oder deaktivieren, indem Sie mit der rechten Maustaste auf eine beliebige Stelle im Datenbereich klicken und dann auf **Automatisch filtern**klicken.  
  
##### <a name="filtering-data"></a>Filtern von Daten  
 Sie können den Filterbereich verwenden, um einen Teilcube zu definieren, der durchsucht werden soll. Sie können einen Filter hinzufügen, indem Sie entweder auf eine Dimension im Bereich Filter klicken oder eine Dimension im Bereich Metadaten erweitern und dann eine Hierarchie in den Bereich Filter ziehen. Geben Sie dann einen **Operator** und einen **Filterausdruck**an.  
  
##### <a name="performing-actions"></a>Ausführen von Aktionen  
 Eine Überschrift oder eine Zelle im Bereich Daten, für die eine Aktion ausgeführt wird, ist mit einem Dreieck gekennzeichnet. Die Zelle könnte sich auf eine Dimension, eine Ebene, ein Element oder eine Cubezelle beziehen. Bewegen Sie den Zeiger über das Überschriftenobjekt, um eine Liste verfügbarer Aktionen zu sehen. Klicken Sie auf das Dreieck in der Zelle, um ein Menü anzuzeigen und den zugehörigen Prozess zu starten.  
  
 Aus Sicherheitsgründen werden auf der Registerkarte **Browser** nur die folgenden Aktionen unterstützt:  
  
-   URL  
  
-   Rowset  
  
-   Drillthrough ausführen  
  
 Aktionen in der Befehlszeile, Anweisungen und proprietäre Aktionen werden nicht unterstützt. URL-Aktionen sind so sicher wie die Webseite, mit der sie verknüpft sind.  
  
##### <a name="viewing-member-properties-and-cube-cell-information"></a>Anzeigen von Elementeigenschaften und Cubezelleninformationen  
 Um Informationen zu einem Dimensionsobjekt oder einem Zellenwert anzuzeigen, bewegen Sie den Zeiger über die Zelle.  
  
##### <a name="showing-or-hiding-empty-cells"></a>Ein- oder Ausblenden leerer Zellen  
 Sie können leere Zellen im Datenraster ausblenden, indem Sie mit der rechten Maustaste auf eine beliebige Stelle im Datenbereich klicken und dann auf **Leere Zellen anzeigen**klicken.  
  
  
