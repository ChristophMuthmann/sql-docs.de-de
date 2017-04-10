---
title: "Technical Preview von Power BI-Berichten in SSRS - Versionshinweise | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4c2f20d7-a9f9-47e3-8dc3-c544a14457e0
caps.latest.revision: 5
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Reporting Services-Versionshinweise
 ||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]** Januar 2017 Technical Preview von Power BI-Berichten in SQL Server Reporting Services|

Dieses Thema beschreibt die Einschränkungen und Probleme mit der Technical Preview von Power BI-Berichten in SQL Server Reporting Services.

- Informationen über die Neuerungen in dieser Version finden Sie unter [Neues bei Reporting Services](../reporting-services/neues-in-sql-server-reporting-services-ssrs.md).

 **Probieren Sie es aus:**    
   -   [![Vom Microsoft Download Center herunterladen](../analysis-services/media/download.png)](https://go.microsoft.com/fwlink/?linkid=839351) Laden Sie die Technical Preview von Power BI-Berichten in SQL Server Reporting Services, und Power BI Desktop (SQL Server Reporting Services), aus dem **[Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=839351)** herunter.


## <a name="january--2017"></a>Januar 2017

### <a name="report-server"></a>Berichtsserver

- HTTPS wird jetzt unterstützt. Dies war in der Technical Preview-VM, die im Oktober 2016 freigegeben wurde, nicht verfügbar. Weitere Informationen finden Sie unter [Konfigurieren von SSL-Verbindungen auf einem Berichtsserver im einheitlichen Modus](../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md).
   - HTTPS ist erforderlich, um das PowerPoint Web-Viewer-Add-In zu verwenden und um Power BI-Berichten innerhalb dieses bereitzustellen.
- Horizontales Skalieren wird jetzt unterstützt. Dies war in der Technical Preview-VM, die im Oktober 2016 freigegeben wurde, nicht verfügbar. Weitere Informationen finden Sie unter [Konfigurieren eines Berichtsservers im einheitlichen Modus für Bereitstellungen für horizontales Skalieren](../reporting-services/install-windows/configure a native mode report server scale-out deployment.md).

### <a name="power-bi-reports"></a>Power BI-Berichte

- Power BI-Berichte müssen mit Power BI Desktop (SQL Server Reporting Services) erstellt werden, um mit SQL Server Reporting Services zu arbeiten. Sie können Power BI Desktop (SQL Server Reporting Services) aus dem Evaluation Center herunterladen.
- Power BI-Berichte unterstützen nur die aktive Verbindungen mit Analysis Services (tabellarische oder mehrdimensionale).
- Keine Unterstützung für benutzerdefinierte visuelle Elemente.
- Keine Unterstützung für benutzerdefinierte R-Elemente.