---
title: Verwenden von sicheren Webdienstmethoden | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- SOAP [Reporting Services], secure connections
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- XML Web service [Reporting Services], SOAP
ms.assetid: 87329299-c2ea-4517-9148-d855726768a9
caps.latest.revision: "36"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a9fdb0fed17a833fef1153ff5ab179116d811ade
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="using-secure-web-service-methods"></a>Verwenden von sicheren Webdienstmethoden
  Es kann sein, dass für bestimmte Berichtsserver-Webdienstmethoden eine sichere Verbindung erforderlich ist, wenn Sie diese aufrufen. Die Methoden, die eine sichere Verbindung benötigen, werden von der Einstellung **SecureConnectionLevel**(sichere Verbindungsebene) in der Datei „RSReportServer.config“ bestimmt. Der Wert der Einstellung ist ein ganzzahliger Wert im gültigen Bereich von 0 und höher. In der folgenden Tabelle werden diese Werte beschrieben.  
  
|Ebene|Description|  
|-----------|-----------------|  
|**0**|Nicht sicher. Aufrufe an die Reporting Services-SOAP-API benötigen keine sichere Verbindung.|  
|Größer als **0**|Sicher. Alle Aufrufe an die Reporting Services-SOAP-API benötigen eine sichere Verbindung.|  
  
 Sie können mithilfe der <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A>-Methode des Webdiensts eine Liste der Webdienstmethoden zurückgeben, die entsprechend der aktuellen Konfiguration des Berichtsservers eine sichere Verbindung benötigen. In einem SSL-Szenario sollten Sie die Liste der von <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> zurückgegebenen Methoden überprüfen und den Schema-Namen der Webdienst-URI entsprechend der aufgerufenen Methode in "https" oder "http" ändern.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Anwendungen mit dem Webdienst und .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Report Server Web Service (Report Server-Webdienst)](../../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
