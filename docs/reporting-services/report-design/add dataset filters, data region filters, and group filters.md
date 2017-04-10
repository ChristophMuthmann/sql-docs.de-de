---
title: "Hinzuf&#252;gen von Datasetfiltern, Datenbereichsfiltern und Gruppenfiltern (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fcca7243-a702-4725-8e6f-cf118e988acf
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# Hinzuf&#252;gen von Datasetfiltern, Datenbereichsfiltern und Gruppenfiltern (Berichts-Generator und SSRS)
  In einem Bericht ist ein Filter Teil eines Datasets, eines Datenbereichs oder einer Datenbereichsgruppe, den Sie erstellen, um die im Bericht verwendeten Daten zu beschränken. Mithilfe von Filtern können Berichtsdaten gesteuert werden, wenn es nicht möglich ist, die Datasetabfrage zu ändern, z. B. bei Verwendung eines freigegebenen Datasets.  
  
 Mit Filtern können Sie die in einem Bericht angezeigten und verarbeiteten Daten bestimmen. Sie können Filter in beliebiger Kombination für ein Dataset, einen Datenbereich oder eine Gruppe festlegen.  
  
 Weitere Informationen finden Sie unter [Hinzufügen eines Filters zu einem Dataset &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md) und [Beispiele für Filtergleichungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="When"></a> Verwenden von Filtern  
 Legen Sie Filter für Berichtselemente fest, wenn die Daten nicht in der Quelle gefiltert werden können. Verwenden Sie Berichtsfilter z. B., wenn die Datenquelle keine Abfrageparameter unterstützt, wenn Sie gespeicherte Prozeduren ausführen müssen und die Abfrage nicht bearbeiten können oder wenn durch eine parametrisierte Berichtsmomentaufnahme individuelle Daten für verschiedene Benutzer angezeigt werden.  
  
 Berichtsdaten können vor oder nach dem Abrufen für ein Berichtsdataset abgerufen wurden. Ändern Sie die Abfrage für jedes Dataset, wenn Sie Daten vor dem Abrufen filtern möchten. Wenn Sie Daten in der Abfrage filtern, filtern Sie damit die Daten in der Datenquelle. Auf diese Weise wird die Menge der Daten reduziert, die in einem Bericht abgerufen und verarbeitet werden muss. Um Daten nach dem Abrufen zu filtern, erstellen Sie im Bericht Filterausdrücke. Sie können Filterausdrücke für ein Dataset, einen Datenbereich oder eine Gruppe (einschließlich der Detailgruppen) festlegen. Außerdem können Sie Parameter in Filterausdrücke einbinden, um das Filtern von Daten für bestimmte Werte oder Benutzer zu ermöglichen. Sie können z. B. nach einem Wert filtern, der Benutzer identifiziert, die den Bericht anzeigen.  
  
##  <a name="Where"></a> Filterposition  
 Die Position eines Filters wird durch die Ziele vorgegeben, die Sie mit dem Bericht verfolgen. Zur Laufzeit werden Filter vom Berichtsprozessor in der folgenden Reihenfolge angewendet: zuerst auf das Dataset, dann auf den Datenbereich und anschließend auf die Gruppe (in der Reihenfolge von oben nach unten in jeder Gruppenhierarchie). Bei einer Tabelle, Matrix oder Liste werden Filter für Zeilen- und Spaltengruppen sowie für angrenzende Gruppen unabhängig voneinander angewendet. Bei Diagrammen werden Filter für Kategorie- und Reihengruppen unabhängig voneinander angewendet. Wenn der Berichtsprozessor die Filter anwendet, werden alle Filtergleichungen in der Reihenfolge angewendet, in der sie für die einzelnen Berichtselemente auf der Seite **Filter** im Dialogfeld **Eigenschaften** definiert sind. Dies entspricht der Kombination der Filter durch Boolesche AND-Operationen.  
  
 Die folgende Liste zeigt die unterschiedlichen Auswirkungen von Filtern, die für verschiedene Berichtselemente festgelegt werden:  
  
-   **Für das Dataset** : Legen Sie einen Filter für das Dataset fest, wenn ein oder mehrere Datenbereiche, die an ein einzelnes Dataset gebunden sind, auf dieselbe Weise gefiltert werden sollen. Beispiel: Legen Sie den Filter für das Dataset fest, das sowohl an eine Tabelle mit Verkaufsdaten als auch an ein Diagramm, in dem dieselben Daten angezeigt werden, gebunden ist.  
  
-   **Für den Datenbereich** : Legen Sie einen Filter für den Datenbereich fest, wenn von einem oder mehreren Datenbereichen, die an ein einzelnes Dataset gebunden sind, verschiedene Sichten des Datasets bereitgestellt werden sollen. Beispiel: Legen Sie den Filter für einen Tabellendatenbereich fest, in dem die zehn umsatzstärksten Läden angezeigt werden sollen, und für einen anderen Tabellendatenbereich, in dem im selben Bericht die zehn umsatzschwächsten Läden enthalten sein sollen.  
  
-   **Für die Zeilen- oder Spaltengruppen in einem Tablix-Datenbereich** : Legen Sie einen Filter für eine Gruppe fest, wenn Sie bestimmte Werte für einen Gruppenausdruck ein- bzw. ausschließen möchten, um zu steuern, welche Werte in der Tabelle, Matrix oder Liste angezeigt werden.  
  
-   **Für die Detailgruppe in einem Tablix-Datenbereich** : Legen Sie einen Filter für die Detailgruppe fest, wenn für einen Datenbereich mehrere Detailgruppen vorhanden sind und jede Detailgruppe einen anderen Satz Daten aus dem Dataset anzeigen soll.  
  
-   **Für die Reihen- oder Kategoriegruppen in einem Diagrammdatenbereich** : Legen Sie einen Filter für eine Reihen- oder Kategoriegruppe fest, wenn Sie bestimmte Werte für einen Gruppierungsausdruck ein- oder ausschließen möchten, um die im Diagramm angezeigten Werte zu steuern.  
  
 Zurück zum Anfang  
  
##  <a name="FilterEquations"></a> Grundlegendes zur Filtergleichung  
 Zur Laufzeit konvertiert der Berichtsprozessor den Wert in den angegebenen Datentyp und vergleicht dann anhand des festgelegten Operators Ausdruck und Wert. In der folgenden Liste werden die einzelnen Bestandteile der Filtergleichung beschrieben:  
  
-   **Ausdruck** : Definiert das Filterelement. Im Allgemeinen handelt es sich hierbei um ein Datasetfeld.  
  
-   **Datentyp** : Legt den Datentyp fest, der bei der Auswertung der Filtergleichung durch den Berichtsprozessor zur Laufzeit verwendet werden soll. Bei dem gewählten Datentyp muss es sich um einen vom Berichtsdefinitionsschema unterstützten Datentyp handeln.  
  
-   **Operator** : Definiert, wie die beiden Teile der Filtergleichung miteinander verglichen werden.  
  
-   **Wert** : Legt den im Vergleich verwendeten Ausdruck fest.  
  
 In den folgenden Abschnitten werden die einzelnen Bestandteile der Filtergleichung vorgestellt.  
  
### Ausdruck  
 Wenn die Filtergleichung zur Laufzeit vom Berichtsprozessor ausgewertet wird, müssen Ausdruck und Wert denselben Datentyp aufweisen. Der Datentyp des unter **Ausdruck** ausgewählten Felds wird durch die Datenverarbeitungserweiterung oder den Datenanbieter, über den die Daten aus der Datenquelle abgerufen werden, vorgegeben. Der Datentyp des unter **Wert** eingegebenen Ausdrucks wird durch [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Standards vorgegeben. Die verfügbaren Datentypen sind abhängig von den für eine Berichtsdefinition unterstützten Datentypen. Die Werte aus der Datenbank werden ggf. vom Datenanbieter in einen CLR-Typ konvertiert.  
  
### Datentyp  
 Damit der Berichtsprozessor zwei Werte vergleichen kann, müssen diese Werte denselben Datentyp aufweisen. Die folgende Tabelle zeigt die Zuordnung zwischen CLR-Datentypen und Berichtsdefinitionsdatentypen. Die aus einer Datenquelle abgerufenen Daten werden u. U. in einen Datentyp konvertiert, der sich vom Typ der Berichtsdaten unterscheidet.  
  
|**Datentyp des Berichtsdefinitionsschemas**|**CLR-Typ(en)**|  
|--------------------------------------------|-----------------------|  
|**Boolean**|**Boolean**|  
|**DateTime**|**DateTime**, **DateTimeOffset**|  
|**Integer**|**Int16**, **Int32**, **UInt16**, **Byte**, **SByte**|  
|**Float**|**Single**, **Double**, **Decimal**|  
|**Text**|**String**, **Char**, **GUID**, **Timespan**|  
  
 Falls Sie einen Datentyp angeben müssen, können Sie im Value-Teil des Ausdrucks Ihre eigene Konvertierung festlegen.  
  
### Operator  
 Die folgende Tabelle enthält die Operatoren, die in Filtergleichungen verwendet werden können, und beschreibt, welche Elemente zur Auswertung der Filtergleichung vom Berichtsprozessor verwendet werden.  
  
|Operator|Aktion|  
|--------------|------------|  
|**Equal, Like, NotEqual, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual**|Vergleicht den Ausdruck mit einem Wert.|  
|**TopN, BottomN**|Vergleicht den Ausdruck mit einem **Integer** -Wert.|  
|**TopPercent, BottomPercent**|Vergleicht den Ausdruck mit einem **Integer** - oder einem **Float** -Wert.|  
|**Zwischen**|Prüft, ob der Ausdruck zwischen zwei Werten (einschließlich) liegt.|  
|**In**|Prüft, ob der Ausdruck in einem Satz von Werten enthalten ist.|  
  
### Wert  
 Der Value-Ausdruck legt den abschließenden Teil der Filtergleichung fest. Der Berichtsprozessor konvertiert den ausgewerteten Ausdruck in den festgelegten Datentyp und wertet dann die gesamte Filtergleichung aus, um zu ermitteln, ob die unter Ausdruck angegebenen Daten den Filter passieren dürfen.  
  
 Wenn der Ausdruck in einen Datentyp konvertiert werden soll, bei dem es sich nicht um einen Standard-CLR-Datentyp handelt, müssen Sie den Ausdruck so ändern, dass explizit in einen Datentyp konvertiert wird. Sie können hierfür die im Dialogfeld **Ausdruck** unter **Allgemeine Funktionen**, **Konvertierung**aufgelisteten Konvertierungsfunktionen verwenden. Beispiel: Das Feld `ListPrice` repräsentiert Daten, die mit einem **money**-Datentyp in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenquelle gespeichert sind. Die Datenverarbeitungserweiterung gibt den Feldwert als <xref:System.Decimal>-Datentyp zurück. Wenn Sie einen Filter festlegen möchten, durch den nur Werte über **€ 50000,00** in der Berichtswährung verwendet werden, konvertieren Sie den Wert mit dem Ausdruck `=CDec(50000.00)`in einen Dezimalwert.  
  
 Dieser Wert kann auch einen Parameterverweis enthalten, mit dem Benutzer interaktiv einen Filterwert auswählen können.  
  
 Zurück zum Anfang  
  
## Siehe auch  
 [Ausdrucksverwendungen in Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Berichtsparameter &#40;Berichts-Generator und Berichts-Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
  