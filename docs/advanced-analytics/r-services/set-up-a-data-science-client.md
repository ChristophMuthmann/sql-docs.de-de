---
title: "Einrichten eines Data Science-Clients | Microsoft Docs"
ms.custom: ""
ms.date: "02/10/2017"
ms.prod: "r-server"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d15ee956-918f-40e0-b986-2bf929ef303a
caps.latest.revision: 14
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# Einrichten eines Data Science-Clients
  Nachdem Sie durch Installieren von **R Services (In-Database)** eine Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] konfiguriert haben, möchten Sie wahrscheinlich eine R-Entwicklungsumgebung einrichten, die zur Remoteausführung und Bereitstellung eine Verbindung mit dem Server herstellen kann. 
  
  Ihre Clientumgebung sollte Microsoft R Open sowie zusätzliche RevoScaleR-Pakete enthalten, die eine verteilte Ausführung von R auf SQL Server unterstützen.  Diese Pakete können auf unterschiedliche Weise installiert werden:
  
+ Installieren Sie [Microsoft R Client](http://aka.ms/rclient/download).
+ Installieren Sie Microsoft R Server. Sie können Microsoft R Server über SQL Server-Setup oder über ein eigenständiges Installationsprogramm erhalten. Weitere Informationen finden Sie unter [Erstellen eines eigenständigen R Servers](../../advanced-analytics/r-services/create-a-standalone-r-server.md) oder [Introduction to R Server (Einführung in R Server)](https://msdnstage.redmond.corp.microsoft.com/en-us/microsoft-r/rserver?branch=r-server-nov16-dev).

 Weitere Informationen zur Verwendung von Microsoft R Client für die Verbindung mit SQL Server mithilfe der ScaleR-Pakete finden Sie unter [ScaleR Getting Started (Erste Schritte mit ScaleR)](https://msdn.microsoft.com/microsoft-r/scaler-getting-started#).  
  
 Eine ausführliche exemplarische Vorgehensweise zum Herstellen einer Verbindung zu einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz für die Remoteausführung von R-Code wird im folgenden Lernprogramm beschrieben: [Tieferer Einblick in Data Science: Verwenden der RevoScaleR-Pakete](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Einrichten von SQL Server R Services &#40;In-Database&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  