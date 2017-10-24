---
title: Installieren von Analysis Services-Datenanbietern (AMO, ADOMD.NET, MSOLAP) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a7aedabc-6af9-4698-a7a4-98f894001476
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bd6aa812228cce132b4180a8537ba853f3ea92a2
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="install-analysis-services-data-providers-amo-adomdnet-msolap"></a>Installieren von Analysis Services-Datenanbietern (AMO, ADOMD.NET, MSOLAP)
  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] ist ein Versionsupdate der Analysis Services-Datenanbieter, die aus ADOMD.Net, AMO und MSOLAP bestehen.  
  
 Für die meisten abfragebasierten Datenzugriffsszenarien können Sie die vorhandenen älteren Versionen von bereits auf Clientsystemen installierten Datenanbietern verwenden, um auf tabellarische und mehrdimensionale Modelle auf einer SQL Server 2016 Analysis Services-Instanz zuzugreifen. Dies schließt tabellarische Modelle ein, die ausschließlich für SQL Server 2016 verfügbare Funktionen verwenden. Im Allgemeinen sollten Clientanwendungen, die Abfragen generieren (wie Excel, Reporting Services oder Tableau), beim Zugriff auf ein Analysis Services-Modell nicht die neuesten Datenanbieter benötigen.  
  
 Modellierungs- und Verwaltungstools stellen eine Ausnahme der Regel dar, zumindest im Hinblick auf die Versionsanforderungen für Datenanbieter. Diese Tools müssen über die Datenanbieter verfügen, die speziell für den Zielserver erstellt wurden, um Objekte auf diesem Server zu bearbeiten. Glücklicherweise beinhalten die im Lieferumfang von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] enthaltenen Tools automatisch Datenanbieter, die mit der aktuellen Version des Servers kompatibel sind.  Das Setup für SQL Server Data Tools für Visual Studio 2015 installiert Datenanbieter für SQL Server 2016 Analysis Services. Ebenso installiert SQL Server 2016 Management Studio, das sowohl AMO als auch ADOMD.Net verwendet, beide Datenanbieter für [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 Benutzerdefinierte Anwendungen oder Skripts, die Analysis Services Management Objects (AMO) verwenden, stellen ein Szenario dar, das die manuelle Installation eines Datenanbieters erfordert. Dieses Release enthält einen überarbeiteten Namespace, der Hauptobjekte wie Server und Datenbank in einen neuen Namespace (Microsoft.AnalysisServices.Core) verschiebt, der Teil der Microsoft.AnalysisServices.dll-Assembly ist. Wenn Sie über benutzerdefinierten Code oder Skripts verfügen, die AMO verwenden, müssen Sie Code neu kompilieren. Außerdem müssen Sie AMO auf jedem Server und jeder Clientarbeitsstation manuell aktualisieren, die eine direkte Verbindung über AMO mit einer SQL Server 2016-Instanz von Analysis Services herstellt.  
  
## <a name="provider-list"></a>Liste der Anbieter  
 In der folgenden Tabelle wird jeder Parameter beschrieben.  
  
||||  
|-|-|-|  
|Anbieter|Filename|Version|  
|Analysis Services Management Objects (AMO)|Microsoft.AnalysisServices.dll|13.0.0.0|  
|Analysis Services Core|Microsoft.AnalysisServices.Core.dll|13.0.0.0|  
|Analysis Services (ADOMD.NET)|Microsoft.AnalysisServices.AdomdClient.dll|13.0.0.0|  
|OLE DB-Anbieter für Analysis Services (MSOLAP)|MSOLAP130.dll|13.0.0.0|  
  
## <a name="download-and-install-data-provider"></a>Herunterladen und Installieren des Datenanbieters  
  
1.  Wechseln Sie zur [Feature Pack-Downloadseite für SQL Server 2016](http://go.microsoft.com/fwlink/?LinkID=398150).  
  
2.  Klicken Sie auf **Herunterladen** , um die Installation einzelner Komponenten zu aktivieren.  
  
3.  Wählen Sie für 64-Bit-Computer alle oder einige der folgenden Komponenten aus (andernfalls wählen Sie die entsprechenden Komponenten für x86):  
  
    -   ENU\x64\SQL_AS_ADOMD.msi  
  
    -   ENU\x64\SQL_AS_AMO.msi  
  
    -   ENU\x64\SQL_AS_OLEDB.msi  
  
4.  Klicken Sie auf **Weiter** , um die Dateien herunterzuladen.  
  
5.  Führen Sie zum Installieren des Anbieters jedes Programm aus. ADO.MD- and AMO-Assemblys werden unter „C:\Windows\assembly\GAC_MSIL“ installiert. Der Analysis Services-OLE DB-Anbieter wird unter „C:\Programme\Microsoft Analysis Services\AS OLEDB\130“ installiert.  
  
## <a name="verify-installation"></a>Überprüfen der Installation  
  
1.  Wechseln Sie im Datei-Explorer zu „C:\Windows\Assembly“.  
  
2.  Klicken Sie mit der rechten Maustaste auf „Microsoft.AnalysisServices“, und wählen Sie **Eigenschaften**aus.  
  
3.  Klicken Sie auf **Version** , um zu bestätigen, dass Sie über den neuesten Build verfügen.  
  
  

