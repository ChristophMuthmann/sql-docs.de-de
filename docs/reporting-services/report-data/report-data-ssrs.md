---
title: "Berichtsdaten (SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e22b7c24-edab-42d6-82f6-95068e1c6043
caps.latest.revision: 16
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 16
---
# Berichtsdaten (SSRS)
  Berichtsdaten können aus mehreren Datenquellen in Ihrer Organisation stammen. Der erste Schritt beim Entwerfen eines Berichts ist das Erstellen von Datenquellen und Datasets, die die zugrunde liegenden Berichtsdaten darstellen. Jede Datenquelle enthält Datenverbindungsinformationen. Jedes Dataset enthält einen Abfragebefehl, der den Satz von Feldern definiert, der als Daten aus einer Datenquelle verwendet werden soll. Sie können die Daten jedes Datasets visuell darstellen, indem Sie einen Datenbereich hinzufügen, z. B. eine Tabelle, eine Matrix, ein Diagramm oder eine Karte. Wenn der Bericht verarbeitet wird, wird Datenquelle abgefragt, und jeder Datenbereich nach Bedarf erweitert, um die Abfrageergebnisse für das Dataset anzuzeigen.  
  
##  <a name="BkMk_ReportDataTerms"></a> Begriffe  
  
-   **Datenverbindung.** Wird auch als *Datenquelle*. Eine Datenverbindung umfasst einen Namen und Verbindungseigenschaften, die vom Verbindungstyp abhängen. Programmbedingt enthält eine Datenverbindung keine Anmeldeinformationen. Eine Datenverbindung gibt nicht an, welche Daten aus der externen Datenquelle abgerufen werden sollen. Geben Sie hierzu beim Erstellen eines Datasets eine Abfrage an.  
  
-   **Datenquellendefinition.** Eine Datei, die die XML-Darstellung einer Berichtsdatenquelle enthält. Wenn ein Bericht veröffentlicht wird, werden seine Datenquellen unabhängig von der Berichtsdefinition auf dem Berichtsserver oder der SharePoint-Website als Datenquellendefinitionen gespeichert. Ein Berichtsserveradministrator kann z. B. die Verbindungszeichenfolge oder die Anmeldeinformationen aktualisieren. Auf einem systemeigenen Berichtsserver lautet der Dateityp RDS. Auf einer SharePoint-Website lautet der Dateityp RSDS.  
  
-   **Verbindungszeichenfolge.** Eine Verbindungszeichenfolge ist eine Zeichenfolgenversion der Verbindungseigenschaften, die zum Herstellen einer Verbindung mit einer Datenquelle erforderlich sind. Verbindungseigenschaften unterscheiden sich je nach Datenverbindungstyp. Beispiele finden Sie unter [Data Connections, Data Sources, and Connection Strings in Report Builder](../Topic/Data%20Connections,%20Data%20Sources,%20and%20Connection%20Strings%20in%20Report%20Builder.md).  
  
-   **Freigegebene Datenquelle.** Eine auf einem Berichtsserver oder einer SharePoint-Website verfügbare Datenquelle, die von mehreren Berichten verwendet wird.  
  
-   **Eingebettete Datenquelle.** Wird auch als *berichtsspezifische Datenquelle* bezeichnet. Eine Datenquelle, die in einem Bericht definiert und nur von diesem Bericht verwendet wird.  
  
-   **Anmeldeinformationen.** Anmeldeinformationen sind die Authentifizierungsinformationen, die für den Zugriff auf externe Daten bereitgestellt werden müssen.  
  
##  <a name="BkMk_ReportDataTips"></a> Tipps zum Angeben von Berichtsdaten  
 Die folgenden Informationen helfen Ihnen beim Entwerfen Ihrer Berichtsdaten-Strategie.  
  
-   **Datenquellen** Datenquellen können veröffentlicht werden und unabhängig von Berichten auf einem Berichtsserver oder einer SharePoint-Website verwaltet werden. Für jede Datenquelle können Sie oder der Datenbankbesitzer Verbindungsinformationen an einem Ort verwalten. Anmeldeinformationen für Datenquellen werden sicher auf dem Berichtsserver gespeichert; Kennwörter werden nicht in die Verbindungszeichenfolge aufgenommen. Sie können eine Datenquelle von einem Testserver an einen Produktionsserver umleiten. Sie können eine Datenquelle deaktivieren, um alle Berichte anzuhalten, die sie verwenden.  
  
-   **Datasets** Datasets können veröffentlicht werden und unabhängig von Berichten oder den freigegebenen Datenquellen, von denen sie abhängen, verwaltet werden. Sie oder der Datenbankbesitzer können optimierte Abfragen zur Verfügung stellen, die die Berichtsautoren dann verwenden können. Wenn Sie die Abfrage ändern, verwenden alle Berichte, die das freigegebene Dataset nutzen, die aktualisierte Abfrage. Zur Steigerung der Leistung können Sie die Zwischenspeicherung von Datasets aktivieren. Sie können die Zwischenspeicherung von Abfragen für eine bestimmte Zeit planen oder einen freigegebenen Zeitplan verwenden.  
  
-   **Daten, die von Berichtsteilen verwendet werden** Berichtsteile können Daten einbeziehen, von denen sie abhängen. Weitere Informationen zu Berichtsteilen finden Sie unter [Berichtsteile im Berichts-Designer &#40;SSRS&#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md).  
  
-   **Filtern von Daten** Berichtsdaten können in der Abfrage oder im Bericht gefiltert werden. Sie können kaskadierende Parameter mithilfe von Datasets und Abfragevariablen erstellen und so den Benutzern die Möglichkeit geben, die Auswahl von Tausenden von Möglichkeiten auf eine überschaubare Zahl einzugrenzen. Sie können Daten in einer Tabelle oder in einem Diagramm auf Grundlage von Parameterwerten oder anderen Werten, die Sie angeben, filtern.  
  
-   **Parameter** Dataset-Abfragebefehle, die Abfragevariablen einschließen, erstellen automatisch übereinstimmende Berichtsparameter. Parameter können aber auch manuell erstellt werden. Wenn Sie einen Bericht anzeigen, zeigt die Berichtssymbolleiste die Parameter an. Benutzer können Werte auswählen, um Berichtsdaten zu überprüfen oder deren Auftreten zu melden. Sie können Berichtsdaten für bestimmte Zielgruppen anpassen, indem Sie Sätze von Berichtsparametern mit anderen Standardwerten erstellen, die mit derselben Berichtsdefinition verknüpft sind, oder das integrierte **UserID**-Feld verwenden. Weitere Informationen finden Sie unter [Berichtsparameter &#40;Berichts-Generator und Berichts-Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md) und [Integrierte Sammlungen in Ausdrücken &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder-and-ssrs.md).  
  
-   **Datenwarnungen** Nach der Veröffentlichung eines Berichts können Sie Warnungen auf Grundlage der Berichtsdaten erstellen, und die Zusendung einer E-Mail veranlassen, wenn die Daten den angegebenen Regeln entsprechen.  
  
-   **Daten gruppieren und aggregieren** Berichtsdaten können in der Abfrage oder im Bericht gruppiert oder aggregiert werden. Wenn Sie Werte in der Abfrage aggregieren, können Sie weiterhin im Rahmen des Sinnvollen Werte im Bericht kombinieren.  Weitere Informationen finden Sie unter [Filtern, Gruppieren und Sortieren von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md) und [Aggregate-Funktion &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/aggregate-function-report-builder-and-ssrs.md).  
  
-   **Daten sortieren** Berichtsdaten können in der Abfrage oder im Bericht sortiert werden. In Tabellen können Sie zudem eine interaktive Sortierschaltfläche hinzufügen, mit der die Benutzer selbst über die Sortierreihenfolge entscheiden können.  
  
-   **Ausdrucksbasierte Daten:** Da die meisten Berichtseigenschaften ausdrucksbasiert sein und Ausdrücke Verweise auf Datasetfelder und Berichtsparameter enthalten können, können Sie leistungsstarke Ausdrücke schreiben, um die Berichtsdaten und ihre Darstellung zu steuern. Sie können einem Benutzer die Möglichkeit geben, die Datenanzeige durch Definieren von Parametern zu steuern.  
  
-   **Daten aus einem Dataset anzeigen** Daten aus einem Dataset werden in der Regel in einem oder mehreren Datenbereichen angezeigt, z. B. einer Tabelle und einem Diagramm.  
  
-   **Daten aus mehreren Datasets anzeigen**  . Sie können Ausdrücke in einem Datenbereich auf Grundlage eines Datasets schreiben, die nach Werten oder Aggregaten in anderen Datasets suchen. Sie können Unterberichte auf Grundlage eines Datasets in eine Tabelle aufnehmen, um Daten aus einer anderen Datenquelle anzuzeigen.  
  
 Die folgende Liste kann Ihnen dabei helfen, die Quellen von Daten für einen Bericht zu definieren.  
  
-   Dabei müssen Sie sich entscheiden, ob Sie eingebettete oder freigegebene Datenquellen und Datasets verwenden möchten. Arbeiten Sie mit Besitzern der Datenquellen zusammen, um eine Authentifizierungs- und Autorisierungstechnologie zu implementieren und zu verwenden, die für Ihre Organisation geeignet ist.  
  
-   Beachten Sie dabei bitte die Architektur der Softwaredatenschichten Ihrer Organisation und die potenziellen Probleme, die sich aus Datentypen ergeben können. Achten Sie darauf, wie sich Datenerweiterungen und Datenverarbeitungserweiterungen auf Abfrageergebnisse auswirken können. Je nach Datenquelle, Datenanbieter und den in der Berichtsdefinitionsdatei (.rdl) gespeicherten Datentypen stehen unterschiedliche Datentypen zur Verfügung.  
  
-   Achten Sie auf die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Client/Server-Architekturen und -Tools. Im Berichts-Designer erstellen Sie z. B. Berichte auf einem Clientcomputer, der integrierte Datenquellentypen verwendet. Wenn Sie einen Bericht veröffentlichen, müssen der Berichtsserver oder die SharePoint-Website die Datenquellentypen unterstützen.  Weitere Informationen finden Sie unter [Von Reporting Services unterstützte Datenquellen &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
-   Datenquellen und Datasets werden in einem Bericht erstellt und von einem Clienterstellungstool auf einem Berichtsserver oder einer SharePoint-Website veröffentlicht. Datenquellen können auf dem Berichtsserver direkt erstellt werden. Nach der Veröffentlichung können Sie Anmeldeinformationen und andere Eigenschaften auf dem Berichtsserver konfigurieren. Weitere Informationen finden Sie unter [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) und [Reporting Services-Tools](../../reporting-services/tools/reporting-services-tools.md).  
  
-   Die verfügbaren Datenquellen hängen davon ab, welche [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Datenerweiterungen installiert sind. Je nach Clienterstellungstool, Berichtsserverversion und Berichtsserverplattform kann sich die Unterstützung für Datenquellen unterscheiden. Weitere Informationen finden Sie unter [Von Reporting Services unterstützte Datenquellen &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
-   Die Anmeldeinformationen für Datenquellen sind unterschiedlich je nach Datenquellentyp und je nachdem, ob Sie die Berichte auf Ihrem Client, auf dem Berichtsserver oder auf einer SharePoint-Website anzeigen. Weitere Informationen finden Sie unter [Festlegen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../../reporting-services/security/set permissions for report server items on a sharepoint site.md) und [Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md) und zu Anmeldeinformationen zu speziellen Tools in [Reporting Services-Tools](../../reporting-services/tools/reporting-services-tools.md).  
  
## Verwandte Aufgaben  
 Auf das Erstellen von Datenverbindungen bezogene Tasks, die Daten aus externen Quellen, Datasets und Abfragen hinzufügen.  
  
|||  
|-|-|  
|**Allgemeine Aufgaben**|**Links**|  
|Erstellen von Datenverbindungen|[Datenverbindungen, Datenquellen und Verbindungszeichenfolgen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)|  
|Erstellen von Datasets und Abfragen|[Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)|  
|Verwalten von Datenquellen nach der Veröffentlichung|[Verwalten von Berichtsdatenquellen](../../reporting-services/report-data/manage-report-data-sources.md)|  
|Verwalten von freigegebenen Datasets nach der Veröffentlichung|[Verwalten von freigegebenen Datasets](../../reporting-services/report-data/manage-shared-datasets.md)|  
|Erstellen und Verwalten von Datenwarnungen|[Reporting Services-Datenwarnungen](../../reporting-services/reporting-services-data-alerts.md)|  
|Zwischenspeichern von freigegebenen Datasets|[Zwischenspeichern von freigegebenen Datasets &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)|  
|Festlegen des Zeitpunkts für das Vorladen des Caches mit freigegebenen Datasets|[Zeitpläne](../../reporting-services/subscriptions/schedules.md)|  
|Hinzufügen von Datenerweiterungen|[Implementieren von Datenverarbeitungserweiterungen](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)|  
  
## Verwandte Inhalte  
  