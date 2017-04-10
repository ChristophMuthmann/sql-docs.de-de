---
title: "Beziehungen (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 21e0144a-3cfd-4bc7-87ff-bb7d1800ed2f
caps.latest.revision: 27
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 27
---
# Beziehungen (SSAS – tabellarisch)
  In tabellarischen Modellen ist eine Beziehung eine Verbindung, die Sie zwischen zwei Tabellen mit Daten erstellen. Die Beziehung legt fest, wie die Daten in den beiden Tabellen korreliert werden sollen. Eine Customers-Tabelle und eine Orders-Tabelle können z. B. verknüpft werden, um den Kundennamen anzuzeigen, der jeder Bestellung zugeordnet ist.  
  
 Wenn Sie Daten mithilfe des Tabellenimport-Assistenten aus derselben Datenquelle importieren, werden Beziehungen, die bereits in den für den Import ausgewählten Tabellen (in der Datenquelle) vorhanden sind, im Modell neu erstellt. Sie können erkannte und neu erstellte Beziehungen automatisch anzeigen, indem Sie den Modell-Designer in der Diagrammsicht oder das Dialogfeld "Beziehungen verwalten" verwenden. Sie können auch manuell neue Beziehungen zwischen Tabellen erstellen. Verwenden Sie dazu den Modell-Designer in der Diagrammsicht oder das Dialogfeld "Beziehung erstellen" oder "Beziehungen verwalten".  
  
 Nach dem Definieren von Beziehungen zwischen Tabellen, entweder automatisch während des Imports oder durch manuelle Erstellung, können Sie Daten mit den verknüpften Spalten und Suchwerten in verknüpften Tabellen filtern.  
  
> [!TIP]  
>  Wenn das Modell viele Beziehungen enthält, unterstützt Sie die Diagrammsicht dabei, die Beziehungen zwischen Tabellen besser darzustellen und neue Beziehungen zu erstellen.  
  
 Abschnitte in diesem Thema:  
  
-   [Vorteile](#what)  
  
-   [Anforderungen für Beziehungen](#requirements)  
  
-   [Inferenz von Beziehungen](#detection)  
  
-   [Erkennen von Beziehungen beim Importieren von Daten](#bkmk_detection)  
  
-   [Manuelles Erstellen von Beziehungen](#bkmk_manually_create)  
  
-   [Doppelte Werte und andere Fehler](#bkmk_dupl_errors)  
  
-   [Verwandte Aufgaben](#bkmk_related_tasks)  
  
##  <a name="what"></a> Vorteile  
 Eine Beziehung ist eine Verbindung zwischen zwei Datentabellen, die auf mindestens einer Spalte in jeder Tabelle basiert. Um zu verstehen, warum Beziehungen nützlich sind, stellen Sie sich vor, dass Sie in Ihrem Unternehmen die Daten für Kundenbestellungen verfolgen möchten. Sie könnten alle Daten in einer einzelnen Tabelle verfolgen, die über eine Struktur wie die folgende verfügt:  
  
|CustomerID|Name|EMail|DiscountRate|OrderID|OrderDate|Product|Quantity|  
|----------------|----------|-----------|------------------|-------------|---------------|-------------|--------------|  
|1|Ashton|chris.ashton@contoso.com|.05|256|2010-01-07|Compact Digital|11|  
|1|Ashton|chris.ashton@contoso.com|.05|255|2010-01-03|SLR Camera|15|  
|2|Jaworski|michal.jaworski@contoso.com|.10|254|2010-01-03|Budget Movie-Maker|27|  
  
 Dieser Ansatz kann umgesetzt werden, bedeutet aber, dass viele redundante Daten gespeichert werden müssen, z. B. die Kunden-E-Mail-Adresse für jede Bestellung. Speicher ist zwar billig, aber wenn sich die E-Mail-Adresse eines Kunden ändert, müssen Sie sicherstellen, dass jede Zeile für diesen Kunden aktualisiert wird. Eine Lösung für dieses Problem ist, die Daten in mehrere Tabellen aufzuteilen und zwischen diesen Tabellen Beziehungen zu definieren. Dieser Ansatz wird in *relationalen Datenbanken* wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet. Eine Datenbank, die Sie in ein Modell importieren, könnte die Bestelldaten z. B. mit drei verknüpften Tabellen darstellen:  
  
### Customers  
  
|[CustomerID]|Name|EMail|  
|--------------------|----------|-----------|  
|1|Ashton|chris.ashton@contoso.com|  
|2|Jaworski|michal.jaworski@contoso.com|  
  
### CustomerDiscounts  
  
|[CustomerID]|DiscountRate|  
|--------------------|------------------|  
|1|.05|  
|2|.10|  
  
### Orders  
  
|[CustomerID]|OrderID|OrderDate|Product|Quantity|  
|--------------------|-------------|---------------|-------------|--------------|  
|1|256|2010-01-07|Compact Digital|11|  
|1|255|2010-01-03|SLR Camera|15|  
|2|254|2010-01-03|Budget Movie-Maker|27|  
  
 Wenn Sie diese Tabellen aus derselben Datenbank importieren, kann der Tabellenimport-Assistent die Beziehungen zwischen den Tabellen anhand der Spalten ermitteln, die in eckigen Klammern stehen, und diese Beziehungen im Modell-Designer reproduzieren. Weitere Informationen finden Sie unter " [Automatische Erkennung und Inferenz von Beziehungen](#detection) " in diesem Thema. Wenn Sie Tabellen aus mehreren Quellen importieren, können Sie Beziehungen manuell erstellen, wie in [Erstellen einer Beziehung zwischen zwei Tabellen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md) beschrieben.  
  
### Spalten und Schlüssel  
 Beziehungen basieren auf den Spalten in jeder Tabelle, die die gleichen Daten enthalten. Die Tabellen "Customers" und "Orders" können z. B. miteinander verknüpft werden, da beide eine Spalte enthalten, in der eine Kundennummer (CustomerID) gespeichert ist. Im Beispiel sind die Spaltennamen identisch, dies ist jedoch keine Voraussetzung. Eine Spalte kann beispielsweise den Namen "CustomerID" und die andere "CustomerNumber" besitzen, sofern alle Zeilen in der Tabelle "Orders" eine ID enthalten, die auch in der Tabelle "Customers" gespeichert ist.  
  
 In einer relationalen Datenbank gibt es mehrere Typen von *Schlüsseln*, die in der Regel nur Spalten mit besonderen Eigenschaften sind. Die folgenden vier Schlüsseltypen können in relationalen Datenbanken verwendet werden:  
  
-   *Primärschlüssel*: Identifiziert eine Zeile in einer Tabelle eindeutig, z.B. CustomerID in der Customers-Tabelle.  
  
-   *Alternativschlüssel* (oder *Kandidatenschlüssel*): Eine eindeutige Spalte, die nicht mit dem Primärschlüssel identisch ist. In einer Tabelle für Mitarbeiter kann beispielsweise eine Mitarbeiter-ID und eine Sozialunterstützungsnummer gespeichert werden, die beide eindeutig sind.  
  
-   *Fremdschlüssel*: Eine Spalte, die auf eine eindeutige Spalte in einer anderen Tabelle verweist, z.B. die CustomerID-Spalte in der Orders-Tabelle, die auf CustomerID in der Customers-Tabelle verweist.  
  
-   *Zusammengesetzter Schlüssel*: Ein Schlüssel, der aus mehr als einer Spalte besteht. Zusammengesetzte Schlüssel werden in Tabellenmodellen nicht unterstützt. Weitere Informationen finden Sie unter "Zusammengesetzte Schlüssel und Suchspalten" in diesem Thema.  
  
 In Tabellenmodellen wird der Primärschlüssel oder Alternativschlüssel als *verknüpfte Suchspalte*oder einfach als *Suchspalte*bezeichnet. Wenn eine Tabelle sowohl über einen Primärschlüssel als auch einen Alternativschlüssel verfügt, können Sie beide als Suchspalte verwenden. Der Fremdschlüssel wird als *Quellspalte* oder nur als *Spalte*bezeichnet. In unserem Beispiel wird zwischen CustomerID in der Orders-Tabelle (die Spalte) und CustomerID (die Suchspalte) in der Customers-Tabelle eine Beziehung definiert. Wenn Sie Daten aus einer relationalen Datenbank importieren, wählt der Modell-Designer standardmäßig den Fremdschlüssel aus einer Tabelle und den entsprechenden Primärschlüssel aus der anderen Tabelle aus. Sie können jedoch jede Spalte verwenden, die über eindeutige Werte für die Suchspalte verfügt.  
  
### Typen von Beziehungen  
 Die Beziehung zwischen Customers und Orders ist eine *1:n-Beziehung*. Jeder Kunde kann mehrere Bestellungen haben, aber eine Bestellung kann nicht mehrere Kunden haben. Die anderen Typen von Beziehungen sind *1:1* und *m:n*. Zwischen der CustomerDiscounts-Tabelle, in der ein einzelner Diskontsatz für jeden Kunden definiert ist, und der Customers-Tabelle besteht eine 1:1-Beziehung. Ein Beispiel für eine m:n-Beziehung ist eine direkte Beziehung zwischen der Products-Tabelle und der Customer-Tabelle, bei der ein Kunde viele Produkte kaufen und ein Produkt von vielen Kunden gekauft werden kann. Der Modell-Designer unterstützt keine m:n-Beziehungen in der Benutzeroberfläche. Weitere Informationen finden Sie unter „[m:n-Beziehungen](#bkmk_many_to_many)“ in diesem Thema.  
  
 In der folgenden Tabelle werden die Beziehungen zwischen den drei Tabellen angezeigt:  
  
|Beziehung|Typ|Suchspalte|Spalte|  
|------------------|----------|-------------------|------------|  
|Customers-CustomerDiscounts|1:1|Customers.CustomerID|CustomerDiscounts.CustomerID|  
|Customers-Orders|1:n|Customers.CustomerID|Orders.CustomerID|  
  
### Beziehungen und Leistung  
 Nach dem Erstellen einer Beziehung muss der Modell-Designer normalerweise alle Formeln neu berechnen, die Spalten aus den Tabellen in der neu erstellten Beziehung verwenden. Die Verarbeitung nimmt, je nach Datenmenge und Komplexität der Beziehungen, einige Zeit in Anspruch.  
  
##  <a name="requirements"></a> Anforderungen für Beziehungen  
 Beim Erstellen von Beziehungen müssen im Modell-Designer mehrere Anforderungen beachtet werden:  
  
### Nur eine aktive Beziehung zwischen zwei Tabellen  
 Mehrere Beziehungen können zu mehrdeutigen Abhängigkeiten zwischen Tabellen führen. Um genaue Berechnungen zu erstellen, benötigen Sie einen einzelnen Pfad von einer Tabelle zur nächsten Tabelle. Daher kann es zwischen jedem Tabellenpaar nur eine aktive Beziehung geben. Beispiel: In AdventureWorks DW 2012 enthält die Tabelle DimDate eine Spalte DateKey, die mit drei verschiedenen Spalten in der Tabelle FactInternetSales verknüpft ist: OrderDate, DueDate und ShipDate. Wenn Sie versuchen, diese Tabellen zu importieren, wird die erste Beziehung erfolgreich erstellt, bei den darauf folgenden Beziehungen, die dieselbe Spalte verwenden, wird jedoch der folgende Fehler ausgelöst:  
  
 \* Beziehung: table[Spalte 1]-> table[Spalte 2]   – Status: Fehler   – Ursache: Zwischen den Tabellen <Tabelle1> und <Tabelle2> kann keine Beziehung erstellt werden. Zwischen zwei Tabellen kann nur eine direkte oder indirekte Beziehung vorhanden sein.  
  
 Wenn Sie zwei Tabellen mit mehreren Beziehungen zueinander haben, müssen Sie mehrere Kopien der Tabelle importieren, die die Suchspalte enthält, und dann eine Beziehung zwischen jedem Tabellenpaar erstellen.  
  
 Es kann viele inaktive Beziehungen zwischen Tabellen geben. Der zwischen Tabellen zu verwendende Pfad wird vom Berichtserstellungsclient zur Abfragezeit angegeben.  
  
### Eine Beziehung pro Quellspalte  
 Eine Quellspalte kann nicht an mehreren Beziehungen beteiligt sein. Wenn Sie eine Spalte bereits als Quellspalte in einer Beziehung verwendet haben, diese Spalte jedoch mit einer anderen zugehörigen Suchspalte in einer anderen Tabelle verknüpfen möchten, erstellen Sie eine Kopie der Spalte, und verwenden Sie diese Spalte für die neue Beziehung.  
  
 Mithilfe einer DAX-Formel in einer berechneten Spalte kann problemlos eine Kopie einer Spalte mit exakt gleichen Werten erstellt werden. Weitere Informationen finden Sie unter [Erstellen einer berechneten Spalte &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/create-a-calculated-column-ssas-tabular.md).  
  
### Eindeutiger Bezeichner für jede Tabelle  
 Jede Tabelle muss eine einzelne Spalte enthalten, die jede Zeile in dieser Tabelle eindeutig identifiziert. Diese Spalte wird oft als Primärschlüssel bezeichnet.  
  
### Eindeutige Suchspalten  
 Die Datenwerte in der Suchspalte müssen jedoch eindeutig sein. Die Spalte darf also keine Duplikate enthalten. In tabellarischen Modellen entsprechen NULL-Werte und leere Zeichenfolgen einem Leerzeichen, das einem eindeutigen Datenwert entspricht. Das bedeutet, dass die Suchspalte nicht mehrere NULL-Werte enthalten darf.  
  
### Kompatible Datentypen  
 Die Datentypen in der Quellspalte und Suchspalte müssen kompatibel sein. Weitere Informationen zu Datentypen finden Sie unter [Unterstützte Datentypen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/data-types-supported-ssas-tabular.md).  
  
### Zusammengesetzte Schlüssel und Suchspalten  
 Sie können zusammengesetzte Schlüssel nicht in einem Tabellenmodell verwenden. Es muss immer eine Spalte vorhanden sein, die jede Zeile in der Tabelle eindeutig identifiziert. Wenn Sie versuchen, Tabellen mit einer vorhandenen Beziehung auf Grundlage eines zusammengesetzten Schlüssels zu importieren, ignoriert der Tabellenimport-Assistent diese Beziehung, da sie in einem Tabellenmodell nicht erstellt werden kann.  
  
 Wenn Sie im Modell-Designer eine Beziehung zwischen zwei Tabellen erstellen möchten und mehrere Spalten die Primär- und Fremdschlüssel definieren, müssen Sie die Werte kombinieren, um vor dem Erstellen der Beziehung eine einzelne Schlüsselspalte zu erstellen. Sie können dies vor dem Importieren von Daten durchführen, oder Sie können den Schritt im Modell-Designer ausführen, indem Sie eine berechnete Spalte erstellen.  
  
###  <a name="bkmk_many_to_many"></a> m:n-Beziehungen  
 Tabellarische Modelle unterstützen keine m:n-Beziehungen und im Modell-Designer können keine *Verknüpfungstabellen* hinzugefügt werden. Sie können jedoch DAX-Funktionen verwenden, um m:n-Beziehungen zu modellieren.  
  
 Sie können auch versuchen, mit einem bidirektionalen Kreuzfilter das gleiche Ziel zu erreichen. Manchmal können die Anforderungen einer m:n-Beziehung mittels Kreuzfilter erfüllt werden, die einen Filterkontext über mehrere Tabellenbeziehungen übertragen. Weitere Informationen finden Sie unter [Bidirektionale Kreuzfilter für tabellarische Modelle in SQL Server 2016 Analysis Services](../../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md).  
  
### Selbstjoins und Schleifen  
 Selbstjoins sind in Tabellenmodelltabellen nicht zulässig. Ein Selbstjoin ist eine rekursive Beziehung einer Tabelle mit sich selbst. Selbstjoins werden oft verwendet, um Über-/Unterordnungshierarchien zu definieren. Sie könnten z.B. eine Employees-Tabelle mit sich selbst verknüpfen, um eine Hierarchie zu erzeugen, die die Managementkette in einem Unternehmen anzeigt.  
  
 Im Modell-Designer können in einem Modell keine Schleifen zwischen Beziehungen erstellt werden. Anders gesagt sind folgende Beziehungen unzulässig.  
  
 Tabelle 1, Spalte a zu Tabelle 2, Spalte f  
  
 Tabelle 2, Spalte f zu Tabelle 3, Spalte n  
  
 Tabelle 3, Spalte n zu Tabelle 1, Spalte a  
  
 Wenn Sie versuchen, eine Beziehung zu erstellen, die die Erstellung einer Schleife bedingt, wird ein Fehler ausgelöst.  
  
##  <a name="detection"></a> Inferenz von Beziehungen  
 In einigen Fällen werden Beziehungen zwischen Tabellen automatisch verkettet. Wenn Sie beispielsweise eine Beziehung zwischen den beiden ersten unten aufgeführten Tabellenpaaren erstellen, wird abgeleitet, dass auch zwischen den Tabellen des dritten Tabellenpaars eine Beziehung besteht, die dann automatisch erstellt wird.  
  
 Products und Category -- manuell erstellt  
  
 Category und SubCategory -- manuell erstellt  
  
 Products und SubCategory -- Beziehung wird abgeleitet  
  
 Damit Beziehungen automatisch verkettet werden, müssen die Beziehungen in eine Richtung zeigen, so wie oben gezeigt. Wenn ursprünglich z. B. Beziehungen zwischen Sales und Products und Sales und Customers bestehen, wird keine Beziehung abgeleitet. Das liegt daran, dass die Beziehung zwischen Products und Customers eine m:n-Beziehung ist.  
  
##  <a name="bkmk_detection"></a> Erkennen von Beziehungen beim Importieren von Daten  
 Wenn Sie aus einer relationalen Datenquellentabelle importieren, erkennt der Tabellenimport-Assistent vorhandene Beziehungen in den entsprechenden Quelltabellen auf Grundlage der Quellschemadaten. Wenn verknüpfte Tabellen importiert werden, werden die entsprechenden Beziehungen im Modell dupliziert.  
  
##  <a name="bkmk_manually_create"></a> Manuelles Erstellen von Beziehungen  
 Während die meisten Beziehungen zwischen Tabellen in einer einzelnen relationalen Datenquelle automatisch erkannt und im Tabellenmodell erstellt werden, gibt es auch viele Instanzen, bei denen Beziehungen zwischen Modelltabellen manuell erstellt werden müssen.  
  
 Wenn das Modell Daten aus mehreren Quellen enthält, müssen Beziehungen wahrscheinlich manuell erstellt werden. Zum Beispiel können Sie Customers-, CustomerDiscounts- und Orders-Tabellen aus einer relationalen Datenquelle importieren. Beziehungen, die zwischen diesen Tabellen an der Quelle vorhanden sind, werden automatisch im Modell erstellt. Anschließend fügen Sie möglicherweise eine andere Tabelle aus einer anderen Quelle hinzu, zum Beispiel importieren Sie Bereichsdaten aus einer Geografietabelle in eine Microsoft Excel-Arbeitsmappe. Sie können dann manuell eine Beziehung zwischen einer Spalte in der Customers-Tabelle und einer Spalte in der Geografietabelle erstellen.  
  
 Um Beziehungen in einem Tabellenmodell manuell zu erstellen, können Sie den Modell-Designer in der Diagrammsicht oder das Dialogfeld "Beziehungen verwalten" verwenden. In der Diagrammsicht werden Tabellen mit den bestehenden Beziehungen in einem grafischen Format angezeigt. Sie können auf eine Spalte in einer Tabelle klicken und den Cursor in eine andere Tabelle ziehen, um problemlos in der richtigen Reihenfolge eine Beziehung zwischen den Tabellen zu erstellen. Im Dialogfeld "Beziehungen verwalten" werden Beziehungen zwischen Tabellen in einem einfachen Tabellenformat angezeigt. So erfahren Sie, wie Sie Beziehungen manuell erstellen können: [Erstellen einer Beziehung zwischen zwei Tabellen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md).  
  
##  <a name="bkmk_dupl_errors"></a> Doppelte Werte und andere Fehler  
 Wenn Sie eine Spalte auswählen, die nicht in der Beziehung verwendet werden kann, wird ein rotes X neben der Spalte angezeigt. Sie können den Mauszeiger auf das Fehlersymbol bewegen, um eine Meldung anzuzeigen, die weitere Informationen zum Problem enthält. Beispiele für Probleme, die es unmöglich machen können, eine Beziehung zwischen den ausgewählten Spalten zu erstellen, sind:  
  
|Problem oder Meldung|Lösung|  
|------------------------|----------------|  
|Die Beziehung kann nicht erstellt werden, weil beide ausgewählte Spalten doppelte Werte enthalten.|Um eine gültige Beziehung zu erstellen, muss mindestens eine Spalte des ausgewählten Paars ausschließlich eindeutige Werte enthalten.<br /><br /> Sie können entweder die Spalten bearbeiten, um Duplikate zu entfernen, oder Sie können die Reihenfolge der Spalten umkehren, sodass die Spalte, die die eindeutigen Werte enthält, als **Verknüpfte Suchspalte**verwendet wird.|  
|Die Spalte enthält eine NULL oder einen leeren Wert.|Datenspalten können nicht über einen NULL-Wert miteinander verknüpft werden. Für jede Zeile muss in beiden Spalten, die in einer Beziehung verwendet werden, ein Wert enthalten sein.|  
  
##  <a name="bkmk_related_tasks"></a> Verwandte Aufgaben  
  
|Thema|Description|  
|-----------|-----------------|  
|[Erstellen einer Beziehung zwischen zwei Tabellen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)|Beschreibt, wie Sie manuell eine Beziehung zwischen zwei Tabellen erstellen.|  
|[Löschen von Beziehungen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/delete-relationships-ssas-tabular.md)|Beschreibt das Löschen einer Beziehung und welche Auswirkungen dies haben kann.|  
|[Bidirektionale Kreuzfilter für tabellarische Modelle in SQL Server 2016 Analysis Services](../../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)|Beschreibt bidirektionale Kreuzfilter für verknüpfte Tabellen. Wenn die Tabellen verknüpft und bidirektionale Kreuzfilter definiert sind, kann der Filterkontext einer Tabellenbeziehung beim Abfragen einer zweiten Tabellenbeziehung verwendet werden.|  
  
## Siehe auch  
 [Tabellen und Spalten &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [Importieren von Daten &#40;SSAS – tabellarisch&#41;](../Topic/Import%20Data%20\(SSAS%20Tabular\).md)  
  
  