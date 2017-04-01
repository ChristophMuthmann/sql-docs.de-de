---
title: "Designer f&#252;r SharePoint-Listenabfragen (Berichts-Generator) | Microsoft Docs"
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
f1_keywords: 
  - "10016"
ms.assetid: b8a3122c-8008-4950-b515-937636d7967f
caps.latest.revision: 7
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 7
---
# Designer f&#252;r SharePoint-Listenabfragen (Berichts-Generator)
  Berichts-Generator und Berichts-Designer enthalten sowohl einen grafischen Abfrage-Designer als auch einen textbasierten Abfrage-Designer. Mit diesen Designern erstellen Sie Abfragen, um die Daten anzugeben, die für ein Berichtsdataset aus einer SharePoint-Website abgerufen werden sollen. Verwenden Sie den grafischen Abfrage-Designer zum Durchsuchen der Metadaten der SharePoint-Liste, interaktiven Erstellen einer Abfrage und Anzeigen der Ergebnisse der Abfrage. Verwenden Sie den textbasierten Abfrage-Designer, um die vom grafischen Abfrage-Designer erstellte Abfrage anzuzeigen, eine Abfrage zu ändern oder die Abfragebefehle einzugeben. Sie können auch eine vorhandene Abfrage aus einer Datei oder einem Bericht importieren.  
  
> [!IMPORTANT]  
>  Benutzer greifen auf Datenquellen zu, wenn sie Abfragen erstellen und ausführen. Sie sollten minimale Berechtigungen für die Datenquellen gewähren, z. B. nur Leseberechtigungen.  
  
## Grafischer Abfrage-Designer  
 Im grafischen Abfrage-Designer können Sie die SharePoint-Website durchsuchen und den Befehl zum Abrufen der SharePoint-Listendaten für ein Dataset interaktiv erstellen. Sie wählen die Felder aus, die im Dataset enthalten sein sollten, und geben optional Filter an, die die Daten im Dataset begrenzen. Sie können angeben, dass Filter als Parameter verwendet werden und den Wert des Filters zur Laufzeit bereitstellen.  
  
 SharePoint-Listen enthalten viele spezifische SharePoint-Felder, die für Berichte u. U. nicht sinnvoll sind. Der Abfrage-Designer enthält eine Option zum Ausblenden dieser Felder, sodass Sie die gewünschten Felder einfacher und schneller bestimmen können.  
  
 Der grafische Abfrage-Designer ist in drei Bereiche aufgeteilt:  
  
-   Im Bereich "Durchsuchen" wählen Sie die zu verwendenden Listenelemente und Felder aus.  
  
-   Im Bereich "Entwurf" erstellen Sie die Abfrage.  
  
-   Im Bereich "Ergebnisse" zeigen Sie die Abfrageergebnisse an.  
  
 Die folgende Abbildung zeigt den grafischen Abfrage-Designer bei der Verwendung mit SharePoint-Listen.  
  
 ![rsQD_Relational_Graphical_SharePoint](../../reporting-services/report-data/media/rsqd-relational-graphical-sharepoint.gif "rsQD_Relational_Graphical_SharePoint")  
  
 Die folgende Tabelle beschreibt die Funktion jedes Bereichs.  
  
 [SharePoint-Listen](#DatabaseView)  
 Zeigt SharePoint-Listen und die Felder in jedem Element in der Liste an.  
  
 [Ausgewählte Felder](#SelectedFields)  
 Zeigt eine Liste der SharePoint-Listenfeldnamen aus den ausgewählten Elementen im Bereich "SharePoint-Listen" an. Diese Felder werden zur Feldauflistung für das Berichtsdataset.  
  
 [Angewendete Filter](#AppliedFilters)  
 Zeigt eine Liste von Feldern und Filterkriterien für Tabellen oder Sichten in der Datenbanksicht an.  
  
 [Abfrageergebnisse](#QueryResults)  
 Zeigt Beispieldaten für das Resultset für die automatisch generierte Abfrage an.  
  
###  <a name="DatabaseView"></a> Bereich "SharePoint-Listen"  
 Im Bereich "SharePoint-Listen" werden die Metadaten für Datenbankobjekte angezeigt, zu deren Anzeige Sie berechtigt sind. Diese Berechtigungen werden durch die Datenquellenverbindung und die Anmeldeinformationen bestimmt. In der hierarchischen Sicht werden Datenbankobjekte nach Datenbankschema angeordnet angezeigt. Erweitern Sie den Knoten für jedes Schema, um Tabellen, Sichten, gespeicherte Prozeduren und Tabellenwertfunktionen anzuzeigen. Erweitern Sie die Tabelle oder Sicht, um die einzelnen Spalten anzuzeigen.  
  
###  <a name="SelectedFields"></a> Bereich Ausgewählte Felder  
 Im Bereich "Ausgewählte Felder" werden die Listenelementfelder angezeigt, die Sie für SharePoint-Listenelemente auswählen. Die Felder, die in diesem Bereich angezeigt werden, werden zur Feldauflistung für das Berichtsdataset. Nachdem Sie ein Dataset und eine Abfrage erstellt haben, verwenden Sie den Berichtsdatenbereich, um die Feldauflistung für ein Berichtsdataset anzuzeigen. Diese Felder stellen die Daten dar, die Sie in Tabellen, Diagrammen und anderen Berichtselementen bei der Anzeige eines Berichts anzeigen können.  
  
 Aktivieren oder deaktivieren Sie im Bereich "SharePoint-Listen" die Kontrollkästchen für die Tabellen- oder Sichtfelder, um diesem Bereich Felder hinzuzufügen bzw. Felder zu entfernen.  
  
###  <a name="AppliedFilters"></a> Bereich Angewendete Filter  
 Im Bereich "Angewendete Filter" werden die Kriterien angezeigt, mit denen die Anzahl von Datenzeilen begrenzt wird, die zur Laufzeit abgerufen werden. In diesem Bereich angegebene Kriterien werden verwendet, um eine [!INCLUDE[tsql](../../includes/tsql-md.md)] -WHERE-Klausel zu generieren. Wenn Sie die Parameteroption auswählen, wird automatisch ein Berichtsparameter erstellt. Mit Berichtsparametern, die auf Abfrageparametern basieren, kann ein Benutzer Werte für die Abfrage angeben, um die Daten in dem Bericht zu steuern.  
  
 Die folgenden Spalten werden angezeigt:  
  
-   **Feldname** Zeigt den Namen des Felds an, für das die Kriterien angewendet werden sollen.  
  
-   **Operator** Zeigt den Operator an, der im Filterausdruck verwendet werden soll.  
  
-   **Wert** Zeigt den Wert an, der im Filterausdruck verwendet werden soll.  
  
-   **Parameter** Zeigt die Option an, mit der ein Abfrageparameter der Abfrage hinzugefügt werden kann. Verwenden Sie die Dataseteigenschaften, um die Beziehung zwischen Abfrageparameter und Berichtsparameter anzuzeigen.  
  
###  <a name="QueryResults"></a> Bereich Abfrageergebnisse  
 Im Bereich Abfrageergebnisse werden die Ergebnisse für die automatisch generierte Abfrage angezeigt, die mit den Auswahlen in den anderen Bereichen angegeben wird. Die Spalten im Resultset entsprechen den Feldern, die Sie im Bereich Ausgewählte Felder angeben. Die Zeilendaten werden mit den Filtern begrenzt, die Sie im Bereich Angewendete Filter angeben.  
  
 Diese Daten stellen Werte aus der Datenquelle zum Zeitpunkt der Abfrageausführung dar. Die Daten werden nicht in der Berichtsdefinition gespeichert. Die eigentlichen Daten in dem Bericht werden bei der Verarbeitung des Berichts abgerufen.  
  
 Die Sortierreihenfolge im Resultset wird von der Reihenfolge bestimmt, in der die Daten aus der Datenquelle abgerufen werden. Die Sortierreihenfolge kann geändert werden, indem die Abfrage geändert wird oder nachdem die Daten für den Bericht abgerufen wurden.  
  
### Symbolleiste für den grafischen Abfrage-Designer  
 Die Symbolleiste des relationalen Abfrage-Designers stellt die folgenden Schaltflächen bereit, mit denen Sie eine Abfrage angeben oder die Ergebnisse der Abfrage anzeigen können.  
  
|Schaltfläche|Description|  
|------------|-----------------|  
|**Als Text bearbeiten**|Wechselt zum textbasierten Abfrage-Designer, um die automatisch generierte Abfrage anzuzeigen oder die Abfrage zu ändern.|  
|**Importieren**|Importiert eine vorhandene Abfrage aus einer Datei oder einem Bericht. Die Dateitypen SQL und RDL werden unterstützt.|  
|**Abfrage ausführen**|Führen Sie die Abfrage aus. Das Resultset wird im Bereich mit den Abfrageergebnissen angezeigt.|  
|**Verborgene Felder anzeigen**|Blendet die Felder ein oder aus, die automatisch von SharePoint erstellt, normalerweise aber nicht in Berichten verwendet werden (z. B. "ProgId" und "Level" für SharePoint-Linkelemente). Durch das Ausblenden dieser Felder wird die Feldliste verkürzt, sodass sie einfacher zu verwenden ist.|  
  
## Siehe auch  
 [Abfrage-Designer &#40;Berichts-Generator&#41;](../Topic/Query%20Designers%20\(Report%20Builder\).md)  
  
  