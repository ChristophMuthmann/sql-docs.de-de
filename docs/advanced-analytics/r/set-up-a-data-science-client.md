---
title: Einrichten eines Data Science-Clients | Microsoft-Dokumentation
ms.custom: 
ms.date: 02/10/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d15ee956-918f-40e0-b986-2bf929ef303a
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0661b2fcf9b23d3c81cb0d80f0424d87dbde7ef8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-up--a-data-science-client"></a>Einrichten eines Data Science-Clients
  Nachdem Sie durch Installieren von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] R Services (In-Database) **eine Instanz von**konfiguriert haben, möchten Sie wahrscheinlich eine R-Entwicklungsumgebung einrichten, die zur Remoteausführung und Bereitstellung eine Verbindung mit dem Server herstellen kann. 
  
  Diese Umgebung muss die ScaleR-Pakete und optional eine Client-Entwicklungsumgebung beinhalten.
  
 ## <a name="where-to-get-scaler"></a>ScaleR abrufen 
  
  Ihre Clientumgebung sollte Microsoft R Open sowie zusätzliche RevoScaleR-Pakete enthalten, die eine verteilte Ausführung von R auf SQL Server unterstützt.  Diese Pakete können auf unterschiedliche Weise installiert werden:
  
+ Installieren Sie [Microsoft R Client](http://aka.ms/rclient/download). Weitere Setup-Anweisungen sind hier enthalten: [Erste Schritte mit Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-get-started)
+ Installieren Sie Microsoft R Server. Sie können Microsoft R Server von SQL Server-Setup oder mit den neuen eigenständigen Windows Installer abrufen. Weitere Informationen finden Sie unter [Erstellen eines eigenständigen R Servers](../../advanced-analytics/r-services/create-a-standalone-r-server.md) oder [Introduction to R Server (Einführung in R Server)](https://msdn.microsoft.com/microsoft-r/rserver).

Wenn Sie über einen R Server-Lizenzvertrag verfügen, empfehlen wir die Verwendung von Microsoft R Server (eigenständig), um Einschränkungen für R bei der Verarbeitung von Threads und Daten im Arbeitsspeicher zu vermeiden.


## <a name="how-to-set-up-the-r-development-environment"></a>Einrichten der Entwicklungsumgebung R

Sie können jede R-Entwicklungsumgebung Ihrer Wahl verwenden, die mit Windows kompatibel ist. 

+ R-Tools für Visual Studio unterstützt die Integration in Microsoft R Open
+ RStudio ist eine beliebte kostenlose Umgebung  

Nach der Installation müssen Sie die Umgebung neu konfigurieren, um die Microsoft R Open-Bibliotheken standardmäßig zu verwenden, oder Sie werden keinen Zugriff auf die ScaleR-Bibliotheken haben. Weitere Informationen finden Sie unter [Erste Schritte mit Microsoft R Client](http://msdn.microsoft.com/microsoft-r/r-client-get-started).
 
## <a name="more-resources"></a>Weitere Ressourcen
  
 Eine ausführliche exemplarische Vorgehensweise zum Herstellen einer Verbindung zu einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz für die Remoteausführung von R-Code wird im folgenden Lernprogramm beschrieben: [Tieferer Einblick in Data Science: Verwenden der RevoScaleR-Pakete](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md).  
 

Weitere Informationen zum Verwenden von Microsoft R Client und den ScaleR-Pakete mit SQL Server finden Sie unter [Erste Schritte mit ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started#).  
  
## <a name="see-also"></a>Siehe auch  
 [Einrichten von SQL Server R Services &#40;In-Database&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  

