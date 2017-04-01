---
title: "OData-Quelle | Microsoft Docs"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.DTS.DESIGNER.ODATASOURCE.F1"
ms.assetid: cc9003c9-638e-432b-867e-e949d50cec90
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# OData-Quelle
  Verwenden Sie die OData-Quellkomponente in einem SSIS-Paket, um Daten aus einem Open Data Protocol (OData)-Dienst zu nutzen. Die Komponente unterstützt die OData v3 und v4-Protokolle.  
  
-   Für OData V3-Protokolle unterstützt die Komponente das ATOM- und das JSON-Datenformat.  
  
-   Für OData V4-Protokolle unterstützt die Komponente das ATOM- und das JSON-Datenformat.  
  
> [!NOTE]  
>  Sie können die OData-Quelle auch verwenden, um Daten aus SharePoint-Listen zu lesen. Um alle Listen auf einem SharePoint-Server anzuzeigen, verwenden Sie die folgende URL: http://\<Server>/_vti_bin/ListData.svc. Weitere Informationen zu den URL-Konventionen in SharePoint finden Sie unter [SharePoint Foundation-REST-Schnittstelle](http://msdn.microsoft.com/library/ff521587.aspx).  Die OData-Quelle unterstützt jetzt Microsoft Dynamics AX Online- und Microsoft Dynamics CRM Online-Produkte.
  
## <a name="odata-format"></a>OData-Format  
 Die meisten OData-Dienste geben Ergebnisse in verschiedenen Formaten zurück. Sie können das Format des Resultsets mithilfe der $format-Abfrageoption angeben. Formate wie JSON und JSON Light sind effizienter als ATOM oder XML und erzielen bei der Übertragung großer Datenmengen möglicherweise eine bessere Leistung. In der folgenden Tabelle sind Ergebnisse aus Beispieltests dargestellt. Wie Sie erkennen können, ergab der Wechsel von ATOM zu JSON einen Leistungszuwachs von 30-53% und der Wechsel von ATOM zum neuen JSON Light-Format (verfügbar in WCF Data Services 5.1) einen Leistungszuwachs von 67 %.  
  
|||||  
|-|-|-|-|  
|Zeilen|ATOM|JSON|JSON (Light)|  
|10000|113 Sekunden|74 Sekunden|68 Sekunden|  
|1000000|1110 Sekunden|853 Sekunden|665 Sekunden|  
  
> [!NOTE]  
>  Die SSIS-OData-Quelle verwendet 5.6.1 zum Analysieren von OData V3-Feeds und ODataLib 6.12.0 zum Analysieren von OData V4-Feeds.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Lernprogramm: Verwenden der OData-Quelle](../../integration-services/data-flow/tutorial-using-the-odata-source.md)  
  
-   [Ändern einer OData-Quellabfrage zur Laufzeit](../../integration-services/data-flow/modify-odata-source-query-at-runtime.md)  
  
-   [Quellen-Editor für OData &#40;Seite „Verbindung“&#41;](../../integration-services/data-flow/odata-source-editor-connection-page.md)  
  
-   [Quellen-Editor für OData &#40;Seite Spalten&#41;](../../integration-services/data-flow/odata-source-editor-columns-page.md)  
  
-   [Quellen-Editor für OData &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/odata-source-editor-error-output-page.md)  
  
-   [OData-Quelleneigenschaften](../../integration-services/data-flow/odata-source-properties.md)  
  
## <a name="see-also"></a>Siehe auch  
 [OData-Verbindungs-Manager](../../integration-services/connection-manager/odata-connection-manager.md)  
  
  