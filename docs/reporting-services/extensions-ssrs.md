---
title: Erweiterungen (SSRS) | Microsoft Docs
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
ms.assetid: 2bb0fdca-1837-49f5-b542-61826bab0b46
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d8ec3b39a36a6020a6655e7c7e7c2a589266f3fc
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="extensions-ssrs"></a>Erweiterungen (SSRS)
  Der Berichtsserver in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] verwendet Erweiterungen, um die Eingabe- und Ausgabetypen zu modularisieren, die für die Authentifizierung, die Datenverarbeitung, das Berichtsrendering und die Berichtsübermittlung akzeptiert werden. Dadurch wird für vorhandene [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Installationen die Verwendung neuer Softwarestandards in der Branche erleichtert, z. B. ein neues Authentifizierungsschema, oder ein benutzerdefinierter Datenquellentyp. Der Berichtsserver unterstützt benutzerdefinierte Authentifizierungserweiterungen, Datenverarbeitungserweiterungen, Berichtsverarbeitungserweiterungen, Renderingerweiterungen und Übermittlungserweiterungen, und die Erweiterungen, die den Benutzern zur Verfügung stehen, sind in der Konfigurationsdatei "RSReportServer.config" konfigurierbar. Sie können z. B. die Exportformate, die der Berichts-Viewer verwenden darf, einschränken. Ein Berichtsserver erfordert mindestens eine Authentifizierungserweiterung, Datenverarbeitungserweiterung und Renderingerweiterung. Übermittlungserweiterungen und Berichtsverarbeitungserweiterungen sind zwar optional, jedoch erforderlich, wenn Sie die Berichtsverteilung oder benutzerdefinierte Steuerelemente unterstützen möchten.  
  
 In diesem Thema werden die Erweiterungen beschrieben, die in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]unmittelbar verfügbar sind.  
  
## <a name="security-extensions"></a>Sicherheitserweiterungen  
 Sicherheitserweiterungen werden zum Authentifizieren und Autorisieren von Benutzern und Gruppen bei einem Berichtsserver verwendet. Die Standardsicherheitserweiterung basiert auf der Windows-Authentifizierung. Sie können auch eine benutzerdefinierte Sicherheitserweiterung erstellen, um die Standardsicherung zu ersetzen, wenn das Bereitstellungsmodell einen anderen Authentifizierungsansatz erfordert (wenn z. B. eine formularbasierte Authentifizierung zur Internet- oder Extranetbereitstellung erforderlich ist). Pro [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Installation kann nur eine Sicherheitserweiterung verwendet werden. Sie können die standardmäßige Sicherheitserweiterung der Windows-Authentifizierung ersetzen. Sie können sie allerdings nicht zusammen mit der benutzerdefinierten Sicherheitserweiterung verwenden.  
  
## <a name="data-processing-extensions"></a>Datenverarbeitungserweiterungen  
 Datenverarbeitungserweiterungen werden zum Abfragen einer Datenquelle verwendet und geben ein vereinfachtes Rowset zurück. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] verwendet unterschiedliche Erweiterungen zur Interaktion mit unterschiedlichen Arten von Datenquellen. Sie können die Erweiterungen verwenden, die in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]enthalten sind, oder eigene Erweiterungen entwickeln. Datenverarbeitungserweiterungen für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], Oracle, [!INCLUDE[SAP_DPE_BW_1](../includes/sap-dpe-bw-1-md.md)], Hyperion Essbase, Teradata, OLE DB und ODBC-Datenquellen stehen zur Verfügung. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] kann zudem mit sämtlichen [!INCLUDE[vstecado](../includes/vstecado-md.md)] -Datenanbietern zusammenarbeiten. Datenverarbeitungserweiterungen verarbeiten Abfrageanforderungen von der Berichtsprozessorkomponente in folgenden Schritten:  
  
-   Öffnen einer Verbindung zu einer Datenquelle.  
  
-   Analysieren einer Abfrage und Zurückgeben einer Liste von Feldnamen.  
  
-   Ausführen einer Abfrage für die Datenquelle und Zurückgeben eines Rowsets.  
  
-   Gegebenenfalls Übergeben der Parameter an eine Abfrage.  
  
-   Iteration durch das Rowset und Abrufen der Daten.  
  
 Einige Erweiterungen können auch die folgenden Tasks ausführen:  
  
-   Analysieren einer Abfrage und Zurückgeben einer Liste der in der Abfrage verwendeten Parameternamen.  
  
-   Analysieren einer Abfrage und Zurückgeben der Liste der für die Gruppierung verwendeten Felder.  
  
-   Analysieren einer Abfrage und Zurückgeben der Liste der für die Sortierung verwendeten Felder.  
  
-   Bereitstellen eines Benutzernamens und Kennworts für die Verbindung mit der Datenquelle.  
  
-   Übergeben von Parametern mit mehreren Werten an eine Abfrage.  
  
-   Iteration durch Zeilen und Abrufen von erweiterten Metadaten.  
  
## <a name="rendering-extensions"></a>Renderingerweiterungen  
 Durch Renderingerweiterungen werden Daten und Layoutinformationen aus dem Berichtsprozessorformat in ein gerätespezifisches Format umgewandelt. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] stehen sieben Renderingerweiterungen zur Verfügung: HTML, Excel, CSV, XML, Image, PDF und [!INCLUDE[msCoName](../includes/msconame-md.md)] Word.  
  
-   **HTML-Renderingerweiterung** Wenn Sie einen Bericht von einem Berichtsserver über einen Webbrowser anfordern, verwendet der Berichtsserver die HTML-Renderingerweiterung, um den Bericht zu rendern. Die HTML-Renderingerweiterung generiert HTML stets mit UTF-8-Codierung. Weitere Informationen finden Sie unter [Rendern in das HTML-Format &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-builder/rendering-to-html-report-builder-and-ssrs.md) und [Browserunterstützung für Reporting Services und Power View](../reporting-services/browser-support-for-reporting-services-and-power-view.md).  
  
-   **Excel-Renderingerweiterung** Die Excel-Renderingerweiterung rendert Berichte, die in [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 97 oder höher angezeigt und geändert werden können. Diese Renderingerweiterung erstellt Dateien in BIFF (Binary Interchange File Format). BIFF ist das ursprüngliche Dateiformat für Excel-Daten. Berichte, die in [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] gerendert werden, unterstützen alle für ein beliebiges Arbeitsblatt verfügbaren Funktionen. Weitere Informationen finden Sie unter [Exporting to Microsoft Excel &#40;Report Builder and SSRS&#41;](../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md) (Exportieren nach Microsoft Excel (Berichts-Generator und SSRS)).  
  
-   **CSV-Renderingerweiterung** Die durch Trennzeichen getrennte CSV-Renderingerweiterung (Comma-Separated Value) rendert Berichte in durch Komma getrennte Nur-Text-Dateien ohne jede Formatierung. Benutzer können diese Dateien im Anschluss mit einer Tabellenkalkulationsanwendung, wie [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)], oder einem anderen Programm zum Lesen von Textdateien öffnen. Weitere Informationen finden Sie unter [Exportieren als CSV-Datei &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md).  
  
-   **XML-Renderingerweiterung** Die XML-Renderingerweiterung rendert Berichte in XML-Dateien. Diese XML-Dateien können dann von anderen Programmen gespeichert oder gelesen werden. Sie können auch eine XSLT-Transformation verwenden, um den Bericht in ein anderes XML-Schema zu verwandeln, das von einer anderen Anwendung verwendet wird. Der von der XML-Renderingerweiterung generierte XML-Code ist UTF-8-codiert. Weitere Informationen finden Sie unter [Exportieren nach XML &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-builder/exporting-to-xml-report-builder-and-ssrs.md).  
  
-   **Bild-Renderingerweiterung** Die Bild-Renderingerweiterung rendert Berichte in Bitmaps oder Metadateien. Die Erweiterung kann Berichte in den folgenden Formaten rendern: BMP, EMF, GIF, JPEG, PNG, TIFF und WMF. Standardmäßig wird das Bild in TIFF gerendert, das mit dem standardmäßigen Image Viewer des Betriebssystems (z. B. Windows Bild- und Faxanzeige) angezeigt werden kann. Sie können das Bild vom Viewer aus an einen Drucker senden. Durch Verwenden der Bildrenderingerweiterung zum Rendern des Berichts wird sichergestellt, dass der Bericht auf jedem Client gleich dargestellt wird. (Wenn ein Benutzer einen Bericht in HTML anzeigt, kann die Darstellung des Berichts in Abhängigkeit von der vom Benutzer verwendeten Browserversion, den Browsereinstellungen des Benutzers und den verfügbaren Schriftarten variieren.) Die Bildrenderingerweiterung rendert den Bericht auf dem Server, sodass allen Benutzern dasselbe Bild angezeigt wird. Da der Bericht auf dem Server gerendert wird, müssen alle im Bericht verwendeten Schriftarten auf dem Server installiert sein. Weitere Informationen finden Sie unter [Exportieren in eine Bilddatei &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-builder/exporting-to-an-image-file-report-builder-and-ssrs.md).  
  
-   **PDF-Renderingerweiterung** Die PDF-Renderingerweiterung rendert Berichte in PDF-Dateien, die mit Adobe Acrobat 6.0 oder höher geöffnet und angezeigt werden können. Weitere Informationen finden Sie unter [Exportieren als PDF-Datei &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-builder/exporting-to-a-pdf-file-report-builder-and-ssrs.md).  
  
-   **Word-Renderingerweiterung** Die [!INCLUDE[msCoName](../includes/msconame-md.md)] Word-Renderingerweiterung rendert einen Bericht als Word-Dokument, das mit [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Word 2000 oder höher kompatibel ist. Weitere Informationen finden Sie unter [Exportieren nach Microsoft Word &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md).  
  
## <a name="report-processing-extensions"></a>Berichtsverarbeitungserweiterungen  
 Berichtsverarbeitungserweiterungen können hinzugefügt werden, um die benutzerdefinierte Berichtsverarbeitung für Berichtselemente zu ermöglichen, die nicht in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]enthalten sind. Standardmäßig kann ein Berichtsserver Tabellen, Diagramme, Matrizen, Listen, Textfelder, Bilder und alle anderen Berichtselemente verarbeiten. Wenn Sie spezielle Funktionen zu einem Bericht hinzufügen möchten, die bei der Berichtsausführung die benutzerdefinierte Verarbeitung erforderlich machen (z.B. wenn Sie eine [!INCLUDE[msCoName](../includes/msconame-md.md)] MapPoint-Karte einbetten möchten), können Sie hierfür eine Berichtsverarbeitungserweiterung erstellen.  
  
## <a name="delivery-extensions"></a>Übermittlungserweiterungen  
 In der Anwendung für die Hintergrundverarbeitung kommen Übermittlungserweiterungen zur Bereitstellung von Berichten an unterschiedlichen Orten zum Einsatz. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] verfügt über eine Übermittlungserweiterung für E-Mails und eine für die Dateifreigabe. Mit der E-Mail-Übermittlungserweiterung kann über SMTP (Simple Mail Transport Protocol) eine E-Mail-Nachricht gesendet werden, die entweder den Bericht selbst oder eine URL zum Bericht enthält. Kurznachrichten ohne eine URL oder Bericht können auch an Pager, Telefone oder andere Geräte gesendet werden. Die Dateifreigabe-Übermittlungserweiterung speichert Berichte in einem freigegebenen Ordner im Netzwerk. Sie können einen Speicherort, ein Renderingformat, einen Dateinamen und Optionen zum Überschreiben für die erstellte Datei angeben. Sie können die Dateifreigabeübermittlung zum Archivieren von gerenderten Berichten verwenden und im Rahmen einer Strategie zum Arbeiten mit sehr umfangreichen Berichten. Übermittlungserweiterungen werden in Zusammenhang mit Abonnements verwendet. Beim Erstellen eines Abonnements kann der Benutzer eine der verfügbaren Übermittlungserweiterungen auswählen, um die Art der Berichtsübermittlung zu bestimmen.  
  
  
