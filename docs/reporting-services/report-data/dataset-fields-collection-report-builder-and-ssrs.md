---
title: Datasetfeldauflistung (Berichts-Generator und SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b3884576-1f7e-4d40-bb7d-168312333bb3
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 271d1b4018890ab23db0254b24cbf7664491b848
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="dataset-fields-collection-report-builder-and-ssrs"></a>Datasetfeldauflistung (Berichts-Generator und SSRS)
  Datasetfelder stellen die Daten aus einer Datenverbindung dar. Ein Feld kann entweder numerische oder nicht numerische Daten darstellen. Dazu zählen z. B. Umsätze, der Gesamtumsatz, Kundennamen, Datenbankbezeichner, URLs, Bilder, räumliche Daten und E-Mail-Adressen. Auf der Entwurfsoberfläche werden Felder als Ausdrücke in Berichtselementen wie z. B. Textfelder, Tabellen und Diagramme angezeigt.  
  
 Ein Bericht hat drei Typen von Feldern und zeigt sie im Berichtsdatenbereich an: Datasetfelder, berechnete Datasetfelder und integrierte Felder.  
  
-   **Datasetfelder.** Die Metadaten, die die Auflistung von Feldern darstellen, die zurückgegeben werden, wenn die Datasetabfrage für die Datenquelle ausgeführt wird.  
  
-   **Berechnete Datasetfelder.** Weitere Felder, die Sie für das Dataset erstellen. Jedes berechnete Feld wird erstellt, indem ein von Ihnen definierter Ausdruck ausgewertet wird.  
  
-   **Integrierte Felder.** Die Metadaten, die eine vom Berichts-Generator gelieferte Auflistung von Feldern darstellen, die Berichtsinformationen, wie zum Beispiel den Berichtsnamen oder den Zeitpunkt der Berichtsverarbeitung, bereitstellen. Weitere Informationen finden Sie unter [Integrierte globale Werte und Benutzerverweise &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).  
  
 Datasetfeldnamen werden als Teil der Berichtsdatasetdefinition gespeichert. Weitere Informationen finden Sie unter [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Fields"></a> Datasetfelder und Abfragen  
 Datasetfelder werden über den Befehl zur Datasetabfrage und über von Ihnen definierte berechnete Felder angegeben. Die Auflistung von Feldern, die Sie im Bericht sehen, hängt von Ihrem Typ des Datasets ab:  
  
-   **Freigegebenes Dataset.** Die Feldauflistung ist die Liste von Feldern für die Abfrage in der Definition des freigegebenen Datasets zu der Zeit, zu der Sie dem Bericht das freigegebene Dataset direkt hinzugefügt haben oder einen Berichtsteil hinzugefügt haben, der das freigegebene Dataset enthielt. Die lokale Feldauflistung ändert sich nicht, wenn sich die freigegebene Datasetdefinition auf dem Berichtsserver ändert. Um die lokale Feldauflistung zu aktualisieren, müssen Sie die Liste für das lokale freigegebene Dataset aktualisieren.  
  
-   **Eingebettetes Dataset.** Die Feldauflistung ist die Liste der Felder, die zurückgegeben werden, wenn die aktuelle Abfrage für die Datenquelle ausgeführt wird.  
  
 Weitere Informationen finden Sie unter [Hinzufügen, Bearbeiten und Aktualisieren von Feldern im Berichtsdatenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).  
  
  
### <a name="calculated-fields"></a>Berechnete Felder  
 Sie geben ein berechnetes Feld manuell an, indem Sie einen Ausdruck erstellen. Sie können berechnete Felder verwenden, um neue Werte zu erstellen, die unter der Datenquelle nicht vorhanden sind. Ein berechnetes Feld kann zum Beispiel einen neuen Wert, eine benutzerdefinierte Sortierreihenfolge für eine Gruppe von Feldwerten oder ein vorhandenes Feld darstellen, das in einen anderen Datentyp konvertiert wird.  
  
 Berechnete Felder sind mit einem Bericht verknüpft und können nicht als Teil eines freigegebenen Datasets gespeichert werden.  
  
 Weitere Informationen finden Sie unter [Hinzufügen, Bearbeiten und Aktualisieren von Feldern im Berichtsdatenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).  
  
  
### <a name="entities-and-entity-fields"></a>Entitäten und Entitätsfelder  
 Wenn Sie mit einer Berichtsmodelldatenquelle arbeiten, geben Sie die Entitäten und Entitätsfelder als Berichtsdaten an. Im Abfrage-Designer für ein Berichtsmodell können Sie verknüpfte Entitäten interaktiv untersuchen und wählen und die Felder auswählen, die Sie in das Berichtsdataset einschließen möchten. Nachdem Sie die Abfrage entworfen haben, können Sie die Auflistung von Entitätsbezeichnern und Entitätsfeldern im Berichtsdatenbereich sehen. Entitätsbezeichner werden automatisch vom Berichtsmodell generiert und werden in der Regel nicht für den Endbenutzer angezeigt.  
  
### <a name="using-extended-field-properties"></a>Verwenden von erweiterten Feldeigenschaften  
 Datenquellen, die mehrdimensionale Abfragen unterstützen, zum Beispiel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], unterstützen auch Feldeigenschaften in Feldern. Feldeigenschaften werden im Resultset einer Abfrage angezeigt, sind im Bereicht **Berichtsdaten** jedoch nicht sichtbar. Sie stehen trotzdem zur Verwendung im Bericht zur Verfügung. Wenn Sie auf eine Eigenschaft für ein Feld verweisen möchten, ziehen Sie das Feld in den Bericht und ändern die Standardeigenschaft **Value** in den Feldnamen der gewünschten Eigenschaft. In einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Cube können Sie zum Beispiel Formate für Werte in den Cubezellen definieren. Der formatierte Wert ist mithilfe der Feldeigenschaft **FormattedValue**verfügbar. Um den Wert direkt zu verwenden, anstatt einen Wert zu verwenden und die Formateigenschaft des Textfelds festzulegen, ziehen Sie das Feld in das Textfeld und ändern den Standardausdruck `=Fields!FieldName.Value` in `=Fields!FieldName.FormattedValue`.  
  
> [!NOTE]  
>  Nicht alle **Field** -Eigenschaften können für alle Datenquellen verwendet werden. Die **Value** - und die **IsMissing** -Eigenschaft werden für alle Datenquellen definiert. Weitere vordefinierte Eigenschaften (zum Beispiel **Key**, **UniqueName**und **ParentUniqueName** für mehrdimensionale Datenquellen) werden nur unterstützt, wenn die Datenquelle diese Eigenschaften bereitstellt. Benutzerdefinierte Eigenschaften werden von einigen Datenanbietern unterstützt. Weitere Informationen finden Sie in den entsprechenden Themen zu erweiterten Feldeigenschaften für den Datenquellentyp unter [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md). Z. B. für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenquelle finden Sie unter [Erweiterte Feldeigenschaften für eine Analysis Services-Datenbank &#40; SSRS &#41; ](../../reporting-services/report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md).  
  
  
##  <a name="Defaults"></a> Grundlegendes zu Standardausdrücken für Felder  
 Bei einem Textfeld kann es sich um ein Textfeld-Berichtselement im Text des Berichts oder um ein Textfeld in einer Zelle eines Tablix-Datenbereichs handeln. Wenn Sie ein Feld mit einem Textfeld verknüpfen, gibt die Position des Textfelds den Standardausdruck für den Feldverweis vor. Im Hauptteil des Berichts muss ein Textfeldwert-Ausdruck ein Aggregat und ein Dataset angeben. Wenn im Bericht nur ein Dataset vorhanden ist, wird dieser Standardausdruck für Sie erstellt. Die Standardaggregatfunktion für numerische Felder ist Sum. Das Standardaggregat für nicht numerische Felder ist First.  
  
 In einem Tablix-Datenbereich hängt der Standardfeldausdruck von den Zeilen- und Gruppenmitgliedschaften des Textfelds ab, dem Sie das Feld hinzufügen. Der Feldausdruck für das Feld Sales lautet `[Sales]`, wenn Sie dieses einem Textfeld in der Detailzeile einer Tabelle hinzufügen. Wenn Sie dasselbe Feld einem Textfeld in einem Gruppenkopf hinzufügen, lautet der Standardausdruck `(Sum[Sales])`. Dies liegt daran, dass der Gruppenkopf zusammenfassende Werte für die Gruppe anzeigt, keine Detailwerte. Beim Ausführen des Berichts wertet der Berichtsprozessor die einzelnen Ausdrücke aus und ersetzt das Ergebnis im Bericht.  
  
 Weitere Informationen zu Ausdrücken finden Sie unter [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
  
##  <a name="DataTypes"></a> Felddatentypen  
 Beim Erstellen eines Datasets kann es sein, dass die Datentypen der Felder einer Datenquelle nicht genau den Datentypen entsprechen, die in einem Bericht verwendet werden. Datentypen durchlaufen in der Regel eine oder zwei Zuordnungsebenen. Gegebenenfalls ordnet die Datenverarbeitungserweiterung bzw. der Datenanbieter die Datentypen der Datenquelle CLR-Datentypen (Common Language Runtime) zu. Die Datentypen, die von den Datenverarbeitungserweiterungen zurückgegeben werden, werden einer Teilmenge der CLR-Datentypen (Common Language Runtime) von [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]zugeordnet.  
  
 Unter der Datenquelle werden die Daten als Datentypen gespeichert, die von der Datenquelle unterstützt werden. Bei Daten in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank muss es sich zum Beispiel um einen der unterstützten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentypen handeln, z. B. **nvarchar** oder **datetime**. Wenn Sie Daten aus einer Datenquelle abrufen, durchlaufen die Daten eine Datenverarbeitungserweiterung oder einen Datenanbieter, die bzw. der dem Datenquellentyp zugeordnet ist. Je nach Datenverarbeitungserweiterung können Daten von den Datentypen, die von der Datenquelle verwendet werden, in Datentypen konvertiert werden, die von der Datenverarbeitungserweiterung unterstützt werden. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verwendet Datentypen, die von der mit [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]installierten CLR (Common Language Runtime) unterstützt werden. Der Datenanbieter ändert die Zuordnung der einzelnen Spalten des Resultsets vom systemeigenen Datentyp in einen CLR (Common Language Runtime)-Datentyp für [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] .  
  
 In den einzelnen Phasen werden die Daten mithilfe der Datentypen dargestellt, die in der folgenden Liste beschrieben sind:  
  
-   **Datenquelle** Die Datentypen, die von der Version des Datenquellentyps unterstützt werden, zu der Sie eine Verbindung herstellen.  
  
     Typische Datentypen für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenquelle sind zum Beispiel **int**, **datetime**und **varchar**. Mit in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] eingeführten Datentypen wurde Unterstützung für **date**, **time**, **datetimetz**und **datetime2**hinzugefügt. Weitere Informationen finden Sie unter [Datentypen (Transact-SQL)](http://go.microsoft.com/fwlink/?linkid=98362).  
  
-   **Datenanbieter oder Datenverarbeitungserweiterung** Die Datentypen, die von der Version des Anbieters der Datenverarbeitungserweiterung unterstützt werden, die Sie beim Herstellen der Verbindung zur Datenquelle auswählen. Datenanbieter, die auf [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] basieren, verwenden von der CLR unterstützte Datentypen. Weitere Informationen zu Datentypen des [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Datenanbieters finden Sie auf der MSDN-Website unter [Datentypzuordnungen (ADO.NET](http://go.microsoft.com/fwlink/?LinkId=112178) ) und [Arbeiten mit Basistypen](http://go.microsoft.com/fwlink/?LinkId=112177) .  
  
     Typische Datentypen, die von [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] unterstützt werden, sind zum Beispiel **Int32** und **String**. Datum und Uhrzeit für Kalender werden von der **DateTime** -Struktur unterstützt. Mit dem [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0 Service Pack 1 wurde die Unterstützung der **DateTimeOffset** -Struktur für Daten mit einem Zeitzonenoffset eingeführt.  
  
    > [!NOTE]  
    >  Der Berichtsserver verwendet die Datenanbieter, die auf dem Berichtsserver installiert und konfiguriert wurden. Berichterstellungsclients im Vorschaumodus verwenden die installierten und konfigurierten Datenverarbeitungserweiterungen auf dem Clientcomputer. Sie müssen den Bericht sowohl in der Berichtsclient- als auch in der Berichtsserverumgebung testen.  
  
-   **Berichtsprozessor** Die Datentypen basieren auf der Version der CLR, die bei der Installation von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]installiert war.  
  
     Die Datentypen, die der Berichtsprozessor für die neuen Datums- und Uhrzeittypen verwendet, die mit [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] eingeführt werden, sind in der folgenden Tabelle aufgeführt:  
  
    |SQL-Datentyp|CLR-Datentyp|Description|  
    |-------------------|-------------------|-----------------|  
    |**Date**|**DateTime**|Nur Datum|  
    |**Time**|**TimeSpan**|Nur Uhrzeit|  
    |**DateTimeTZ**|**DateTimeOffset**|Datum und Uhrzeit mit Zeitzonenoffset|  
    |**DateTime2**|**DateTime**|Datum und Uhrzeit mit Bruchteilen von Millisekunden|  
  
 Weitere Informationen über [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanktypen finden Sie unter [Datentypen (Datenbankmodul)](http://go.microsoft.com/fwlink/?linkid=98362) und [Datums- und Uhrzeitdatentypen und zugehörige Funktionen (Transact-SQL)](http://go.microsoft.com/fwlink/?linkid=98360).  
  
 Weitere Informationen zum Einschließen von Verweisen auf ein Datasetfeld aus einem Ausdruck finden Sie unter [Datentypen in Ausdrücken &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md).  
  
  
##  <a name="MissingFields"></a> Erkennen von fehlenden Feldern zur Laufzeit  
 Wenn der Bericht verarbeitet wird, sind im Resultset für ein Dataset möglicherweise nicht für alle angegebenen Spalten Werte enthalten, da die Spalten in der Datenquelle nicht mehr vorhanden sind. Über die Feldeigenschaft „IsMissing“ können Sie ermitteln, ob zur Laufzeit Werte für ein Feld zurückgegeben wurden. Weitere Informationen finden Sie unter [Verweise auf Datasetfeld-Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-dataset-fields-collection-references-report-builder.md).  
  
  
## <a name="see-also"></a>Siehe auch  
 [Dataseteigenschaften (Dialogfeld), Felder &#40;Berichts-Generator&#41;](http://msdn.microsoft.com/library/75c7e54a-3d20-4c9a-88da-ab36dce2ce42)   
 [Berichtsteile und Datasets im Berichts-Generator](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)   
 [Melden Sie eingebettete Datasets und freigegebene Datasets &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
