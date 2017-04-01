---
title: "Reporting Services (SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
  - "reporting-services-sharepoint"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "Berichte [Reporting Services]"
  - "SSRS"
  - "Berichte [Reporting Services], Informationen zu Berichten"
  - "Reporting Services"
  - "SQL Server Reporting Services"
ms.assetid: b8d18d3d-9db0-43e7-8286-7b46cc3a37ed
caps.latest.revision: 70
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# Reporting Services (SSRS)
  Mit einer Reihe von direkt einsatzbereiten Tools und Diensten, die von SQL Server Reporting Services (SSRS) bereitgestellt werden, können Sie mobile und paginierte Berichte lokal erstellen, bereitstellen und verwalten. 
  
 ![SQL Server Reporting Services all together](../reporting-services/media/ss-reporting-services-all-together.png "SQL Server Reporting Services all together")  
## <a name="what-is-sql-server-reporting-services-ssrs"></a>Was ist SQL Server Reporting Services (SSRS)?

SQL Server Reporting Services ist eine Lösung, die Kunden auf ihrer eigenen Infrastruktur bereitstellen, um Berichte zu erstellen, zu veröffentlichen und zu verwalten und schließlich auf unterschiedliche Weise an die gewünschten Benutzer zu übermitteln, etwa durch Anzeigen der Berichte im Webbrowser, auf mobilen Geräten oder als E-Mails in den Postfächern.

Für SQL Server 2016 wird in Reporting Services eine aktualisierte Sammlung von Produkten bereitgestellt:

* **„Herkömmlich“ paginierte Berichte** sind auf den neuesten Stand gebracht, sodass Sie modern aussehende Berichte erstellen können, wozu Sie aktualisierte Tools und neue Funktionen nutzen. 
* **Neue mobile Berichte** mit einem ansprechenden Layout, das sich entsprechend den verschiedenen Geräten und den verschiedenen Arten anpasst, wie Sie diese Geräte halten. 
* **Ein modernes Webportal**, das Sie in jedem modernen Browser anzeigen können. In dem neuen Portal können Sie mobile und paginierte Berichte sowie neue KPIs organisieren und anzeigen. Außerdem können Sie Excel-Arbeitsmappen und Power BI Desktop-Berichte im Portal speichern. 

Lesen Sie weiter, um weitere Informationen zu jedem Aspekt zu erhalten.
  
### <a name="whats-new-in-reporting-services"></a>Neuigkeiten bei Reporting Services

Mit diesen Quellen informieren wir Sie über neue Funktionen in SQL Server 2016 Reporting Services. 
* [Neuigkeiten bei Reporting Services](../reporting-services/neues-in-sql-server-reporting-services-ssrs.md)
* [SQL Server Reporting Services Team Blog (Blog des SQL Server Reporting Services-Teams)](https://blogs.msdn.microsoft.com/sqlrsteamblog/)
* Der [YouTube-Kanal „Guy in a Cube“](https://www.youtube.com/channel/UCFp1vaKzpfvoGai0vE5VJ0w)
  
## <a name="paginated-reports"></a>Paginierte Berichte

![SSRS - paginierte Berichte](../reporting-services/media/ssrs-paginated-reports.png)

Reporting Services ist mit „herkömmlichen“ paginierten Berichten im Dokumentstil verknüpft, in denen, je mehr Daten vorliegen, der jeweilige Bericht umso mehr Zeilen in den Tabellen und umso mehr Seiten hat. Dies ist großartig für das Erstellen von zu druckenden pixelgenauen Dokumenten mit festem Layout, z. B. PDF- und Word-Dateien. 

Diese BI-Kernarbeitslast gibt es nach wie vor, weshalb wir sie modernisiert haben. Sie können nun modern aussehende Berichte mit aktualisierten Funktionen erstellen, wozu Sie den [Berichts-Generator](../reporting-services/report-builder/report-builder-in-sql-server-2016.md) oder den [Berichts-Designer in SQL Server Data Tools (SSDT)](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md) verwenden. 

* Wir haben die Standardstile und -farbpaletten aktualisiert, d. h., Sie erstellen Berichte standardmäßig mit einem neuen minimalistischen Stil.
* Wir haben den Bereich „Parameter“ aktualisiert, sodass Sie Parameter nach Wunsch beliebig anordnen können.
* Sie können in neue Formate, etwa PowerPoint, exportieren. Reporting Services-Visualisierungen in PowerPoint sind lebendig und können bearbeitet werden, sie sind nicht einfach Screenshots.
* Sie können eine hybride Power BI/Reporting Services-Umgebung erstellen: Statt Ihre lokalen Reporting Services-Berichte in Power BI neu zu erstellen, können Sie visuelle Objekte aus diesen Berichten an Ihre Power BI-Dashboards anheften. Anschließend können Sie alle Elemente an einem Ort in Ihrem Power BI-Dashboard überwachen.
 
## <a name="mobile-reports"></a>Mobile Berichte

![SSRS - Mobile Berichte](../reporting-services/media/ssrs-mobile-reports.png)

Mobile Geräte haben zu einem anderen Arbeitsverhalten geführt, was bedeutet, dass Menschen von heute andere Anforderungen an Berichte haben. Die Berichtsdarstellung mit festem Layout funktioniert nicht sehr gut für Tablets und Smartphones. Eine Darstellung, die für einen breiten PC-Bildschirm konzipiert ist, ergibt nicht die optimale Darstellung auf einem kleinen Smartphonebildschirm, der nicht nur kleiner ist, sondern auch eine Ausrichtung im Hoch- oder Querformat hat.

Für diese sehr verschiedene Bildschirmformfaktoren benötigen Sie kein festes Layout, sondern ein reagierendes Layout, das sich an diese verschiedenen Geräten und die unterschiedlichen Arten anpasst, wie Sie diese halten. Dafür haben wir einen neuen Berichtstyp hinzugefügt: mobile Berichte, die auf der Datazen-Technologie basieren, die wir vor über einem Jahr erworben und in das Produkt integriert haben. Sie können Ihre vorhandene Datazen Berichte über den [SQL Server Migration Assistant for Datazen](https://www.microsoft.com/download/details.aspx?id=53128) zu Reporting Services migrieren. 

Sie erstellen diese mobilen Berichte in der neuen App [Publisher für mobile Berichte](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md). Dann können Sie in den systemeigenen [Power BI-Apps für mobile Geräte](https://powerbi.microsoft.com/documentation/powerbi-power-bi-apps-for-mobile-devices/) für Windows 10, iOS, Android und HTML5 auf die Daten, die Sie in Power BI in der Cloud haben, sowie Ihre lokalen SQL Server 2016 Reporting Services-Daten zugreifen. Während Sie Visualisierungen erstellen, generiert Publisher für mobile Berichte automatisch Beispieldaten für jede Visualisierung, sodass Sie sehen können, wie die Visualisierung mit Ihren Daten aussieht und welche Art von Daten in jeder Visualisierung gut funktioniert.

## <a name="web-portal"></a>Webportal

![SSRS - Webportal](../reporting-services/media/ssrs-web-portal.png)

Für Endbenutzer des einheitlichen Modus von Reporting Services ist die „Eingangstür“ ein modernes Webportal, das Sie in jedem modernen Browser anzeigen können. Sie können auf alle diese mobilen und paginierten Berichte im neuen Portal sowie auf neue KPIs zugreifen. Sie können Ihre Favoriten kennzeichnen, und Sie können den Inhalt verwalten, wenn Sie diese Rolle haben. 

Sie können Ihr eigenes benutzerdefiniertes Branding auf Ihr Webportal anwenden. Und Sie können KPIs direkt im Webportal erstellen. KPIs können wichtige Geschäftsmetriken auf einen Blick im Browser zum Vorschein bringen, ohne dass ein Bericht geöffnet werden muss. 

Das neue Webportal ist eine vollständig neu geschriebene Version des Berichts-Managers. Es ist nun eine auf Standards basierende Einzelseiten-HTML5-App, für die moderne Browser optimiert sind: Edge, Internet Explorer 10 und 11, Chrome, Firefox, Safari und alle weiteren wichtigen Browser.

Das Webportal unterstützt weiterhin die herkömmlichen Ordnerhierarchie, sodass Sie den Inhalt strukturieren können. Der Inhalt wird nach Typ strukturiert: mobile Berichte, KPIs, paginierte Berichte sowie Power BI Desktop-Berichte, Excel-Arbeitsmappen, freigegebene Datasets und freigegebene Datenquellen, die als Bausteine für Berichte verwendet werden können. Sie können diese hier sicher speichern und verwalten.

Und Sie können im neuen Webportal weiterhin Berichtsverarbeitung planen, bei Bedarf auf Berichte zugreifen sowie veröffentlichte Berichte abonnieren.

Weitere Informationen zum [Reporting Services-Webportal](../reporting-services/web-portal-ssrs-native-mode.md).
  
## <a name="reporting-services-in-sharepoint-integrated-mode"></a>Reporting Services im integrierten SharePoint-Modus  

Sie veröffentlichen Berichte in Reporting Services im integrierten SharePoint-Modus. Sie können die Verarbeitung von Berichten planen, nach Bedarf auf Begriffe zugreifen, veröffentlichte Berichte abonnieren und Berichten in andere Programme wie Microsoft Excel exportieren. Erstellen Sie Datenwarnungen für Berichte, die auf einer SharePoint-Website veröffentlicht werden, und lassen Sie sich bei Berichtsdatenänderungen per E-Mail benachrichtigen.  

Weitere Informationen über [Reporting Services-Berichtsserver im integrierten SharePoint-Modus](../reporting-services/report-server-sharepoint/reporting-services-report-server-sharepoint-mode.md).
 
## <a name="includessrsnoversiontokenssrsnoversionmdmd-programming-features"></a>[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]-Programmierfeatures  
 Nutzen Sie [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]-Programmierfeatures, um Ihre Berichterstellungsfunktionen zu erweitern und anzupassen. Dabei wird mit APIs die Daten- und Berichtsverarbeitung in benutzerdefinierte Anwendungen integriert und erweitert.
 
 Weitere Informationen finden Sie in der [Reporting Services-Entwicklerdokumentation](../reporting-services/reporting-services-developer-documentation.md). 
  
## <a name="browse-content-by-area"></a>Durchsuchen von Inhalt nach Bereich  
* [Abwärtskompatibilität](../reporting-services/abwärtskompatibilität-reporting-services.md) 
* [Reporting Services-Berichtsserver](../reporting-services/report-server-sharepoint/reporting-services-berichtsserver.md)  
* [Das Webportal](../reporting-services/web-portal-ssrs-native-mode.md)
* [Reporting Services-Berichte &#40;SSRS&#41;](../reporting-services/reports/reporting-services-reports-ssrs.md)  
* [Berichtsdaten &#40;SSRS&#41;](../reporting-services/report-data/report-data-ssrs.md)  
* [Berichts-Generator in SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
* [Publisher für mobile Berichte von SQL Server](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
* [KPIs in Reporting Services](../reporting-services/working-with-kpis-in-reporting-services.md)
* [Reporting Services-Tools](../reporting-services/tools/reporting-services-tools.md)  
  
## <a name="see-also"></a>Siehe auch  
* [Installieren von Reporting Services](../reporting-services/install-windows/install-reporting-services.md)
* [Installieren des Berichts-Generators](../reporting-services/install-windows/install-report-builder.md)   
* [Herunterladen von SQL Server Data Tools (SSDT)](http://go.microsoft.com/fwlink/?LinkID=616714)
  
  