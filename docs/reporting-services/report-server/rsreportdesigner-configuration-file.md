---
title: "RSReportDesigner-Konfigurationsdatei | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Berichts-Designer [Reporting Services], Konfigurationsdatei"
  - "RSReportDesigner-Konfigurationsdatei"
ms.assetid: fdcc9c58-3bad-45b3-ba8e-c7816d64f14c
caps.latest.revision: 47
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 47
---
# RSReportDesigner-Konfigurationsdatei
  In der Datei RSReportDesigner.config werden Einstellungen zu Rendering- und Datenverarbeitungserweiterungen gespeichert, die in Berichts-Designer verfügbar sind. Die Informationen zu Datenverarbeitungserweiterungen werden im **Data** -Element gespeichert. Die Informationen zu Renderingerweiterungen werden im **Render** -Element gespeichert. Das **Designer** -Element zählt die in Berichts-Designer verwendeten Abfrage-Generatoren auf.  
  
 Berichts-Designer verwendet integrierte Berichtsserverfunktionen für die Berichtsvorschau. Zur Unterstützung der lokalen serverseitigen Verarbeitung für Vorschauvorgänge können serverbezogene Einstellungen angegeben werden. Weitere Informationen zu den Konfigurationseinstellungen für den Berichtsserver finden Sie unter [RsReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).  
  
## Dateispeicherort  
 Diese Datei befindet sich unter \Programme\Microsoft Visual Studio 8\Common7\IDE\PrivateAssemblies.  
  
## Bearbeitungsrichtlinien  
 Ändern Sie die Einstellungen in dieser Datei nur, wenn Sie eine benutzerdefinierte Erweiterung bereitstellen bzw. entfernen, das Zwischenspeichern während der Vorschau deaktiviert haben oder nach einem Service Pack-Upgrade eine neue Datenverarbeitungserweiterung registrieren.  
  
 Wenn Sie Renderingerweiterungseinstellungen anpassen, sind spezifische Anweisungen zum Bearbeiten von Konfigurationsdateien verfügbar. Weitere Informationen finden Sie unter [Anpassen der Parameter für Renderingerweiterungen in der Datei „RSReportServer.config“](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md).  
  
 Allgemeine Anleitungen zum Bearbeiten von Konfigurationsdateien finden Sie unter [Ändern einer Reporting Services-Konfigurationsdatei &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
## Beispiel für eine Konfigurationsdatei  
 Das folgende Beispiel veranschaulicht das Format der Datei RSReportDesigner.config.  
  
```  
<Configuration>  
  <Add Key="SecureConnectionLevel" Value="0" />  
  <Add Key="InstanceName" Value="Microsoft.ReportingServices.PreviewServer" />  
  <Add Key="SessionCookies" Value="true" />  
  <Add Key="SessionTimeoutMinutes" Value="3" />  
  <Add Key="PolicyLevel" Value="rspreviewpolicy.config" />  
  <Add Key="CacheDataForPreview" Value="true" />  
  <Extensions>  
    <Render> . . . </Render>  
    <Data> . . . </Data>  
    <Designer> . . . </Designer>  
```  
  
## Konfigurationseinstellungen  
  
|Einstellung|Description|  
|-------------|-----------------|  
|**SecureConnectionLevel**|Der Sicherheitsgrad der Webdienstverbindung. Gültige Werte sind 0 bis 3, wobei 0 die geringste Sicherheit bietet. Weitere Informationen finden Sie unter [Using Secure Web Service Methods](../../reporting-services/report-server-web-service/net-framework/using-secure-web-service-methods.md).|  
|**InstanceName**|Ein Bezeichner für den Vorschauserver. Ändern Sie diesen Wert nicht.|  
|**SessionCookies**|Gibt an, ob der Berichtsserver Sitzungsinformationen mithilfe von Browsercookies verwaltet. Gültige Werte sind **true** und **false**. Der Standardwert ist **true**. Wenn Sie diesen Wert auf false festlegen, werden Sitzungsdaten in der **reportservertempdb** -Datenbank gespeichert.|  
|**SessionTimeoutMinutes**|Gibt an, für welchen Zeitraum ein Sitzungscookie gültig ist. Der Standardwert ist 3 Minuten.|  
|**PolicyLevel**|Gibt die Sicherheitsrichtlinien-Konfigurationsdatei an. Der gültige Wert ist Rspreviewpolicy.config. Weitere Informationen finden Sie unter [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|  
|**CacheDataForPreview**|Ist der Wert auf **True**festgelegt, speichert Berichts-Designer Daten in einer Cachedatei auf dem lokalen Computer. Gültige Werte sind **TRUE** (Standardwert) und **FALSE**. Weitere Informationen finden Sie unter [Previewing Reports](../../reporting-services/reports/previewing-reports.md).|  
|**Render**|Zählt die Renderingerweiterungen auf, die für Berichts-Designer zur Vorschau verfügbar sind. Die für die Vorschau verwendeten Renderingerweiterungen sollten mit den Renderingerweiterungen identisch sein, die mit dem Berichtsserver installiert werden.<br /><br /> **Name** gibt die Renderingerweiterung an. Wenn Sie eine Renderingerweiterung per Code aufrufen, verwenden Sie diesen Wert zur Angabe einer bestimmten Erweiterung.<br /><br /> **Type** gibt den vollqualifizierten Namen der Erweiterungsklasse an sowie den Namen der Bibliothek, durch Trennzeichen getrennt.<br /><br /> **Visible** gibt an, ob der Name auf einer Benutzeroberfläche angezeigt wird. Dieser Wert kann **TRUE** (Standardwert) oder **FALSE** sein. Bei **True**wird der Name auf Benutzeroberflächen angezeigt.|  
|**Daten**|Zählt die Datenverarbeitungserweiterungen auf, die für Berichts-Designer zum Herstellen einer Verbindung zu Datenquellen verfügbar sind, die wiederum Daten für Berichte bereitstellen. Die in Berichts-Designer verwendeten Datenverarbeitungserweiterungen sollten mit den Datenverarbeitungserweiterungen identisch sein, die mit dem Berichtsserver installiert werden. Informationen zum Hinzufügen oder Entfernen benutzerdefinierter Erweiterungen finden Sie unter [Deploying a Data Processing Extension](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md).<br /><br /> **Name** gibt die Datenverarbeitungserweiterung an.<br /><br /> **Type** gibt den vollqualifizierten Namen der Erweiterungsklasse an sowie den Namen der Bibliothek, durch Trennzeichen getrennt.|  
|**Designer**|Zählt die Abfrage-Generatoren auf, die für Berichts-Designer verfügbar sind. Abfrage-Generatoren bieten eine Benutzeroberfläche zum Erstellen von Abfragen, die in Berichten verwendete Daten abrufen. Die Abfrage-Generatoren für verschiedene Datenverarbeitungserweiterungen können voneinander abweichen. Standardmäßig bietet Reporting Services eine grafische Datentool-Benutzeroberfläche für alle Datenverarbeitungserweiterungen, die im Lieferumfang des Produkts enthalten sind. Wenn Sie allerdings Datenverarbeitungsanwendungen erstellen oder Datenverarbeitungsanwendungen von Drittanbietern verwenden, werden möglicherweise andere Abfrage-Generator-Oberflächen angewendet.|  
|**PreviewProcessingServiceStartupTimeoutSeconds**|Gibt den Zeitraum an, der auf das Starten des Vorschauverarbeitungsdienst gewartet wird, bevor eine Fehlermeldung angezeigt wird. Der Standardwert ist 15 Sekunden.|  
  
## Siehe auch  
 [Reporting Services-Konfigurationsdateien](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Abfrageentwurfstools &#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md)  
  
  