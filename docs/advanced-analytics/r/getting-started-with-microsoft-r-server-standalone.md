---
title: "Erste Schritte mit Microsoft R Server (Eigenständig) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52347d0d-ce60-4bb8-98d2-6163e87716b0
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fc7874c6900474c7c2f3d927183616b2f5e69699
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="getting-started-with-microsoft-r-server-standalone"></a>Erste Schritte mit Microsoft R Server (eigenständig)
  Mit Microsoft R Server (eigenständig) können Sie die beliebte Open Source-R-Sprache in Ihrem Unternehmen einführen, um leistungsfähige Analyselösungen und die Integration mit anderen Unternehmensanwendungen zu ermöglichen.  

  
## <a name="install-microsoft-r-server"></a>Installieren von Microsoft R Server 

Wie Sie Microsoft R Server installieren, hängt davon ab, ob Sie SQL Server-Daten in Ihrer Anwendung verwenden müssen. Wenn dies der Fall ist, sollten Sie mit SQL Server-Setup installieren. Wenn Sie keine SQL Server-Daten verwenden oder R-Code in der Datenbank ausführen müssen, können Sie entweder SQL Server-Setup oder den neuen eigenständigen Installer verwenden.
 
 
+ Installieren Sie den Microsoft R Server (Eigenständig) aus dem SQL Server-Setup. Eine separate Instanz der R-Binärdateien für den R Server wird erstellt, und die Instanz über die Supportrichtlinien für die SQL Server Enterprise Edition wird lizenziert. Weitere Informationen finden Sie unter [Erstellen eines eigenständigen R Servers](../../advanced-analytics/r-services/create-a-standalone-r-server.md).  

+ Verwenden Sie den neuen eigenständigen Windows Installer, um eine neue Instanz des Microsoft R Servers zu erstellen, die die Supportrichtlinien von Microsoft Modern Software Lifecycle verwendet. Weitere Informationen finden Sie unter [Run Microsoft R Server for Windows (Ausführen von Microsoft R Server für Windows)](https://msdn.microsoft.com/microsoft-r/rserver-install-windows).

+ Wenn Sie über eine vorhandene Instanz von R Servern (Eigenständig) oder R-Diensten verfügen, die Sie aktualisieren möchten, müssen Sie auch den Windows-basierten Installer für das Update herunterladen und ausführen. Weitere Informationen finden Sie unter [Run Microsoft R Server for Windows (Ausführen von Microsoft R Server für Windows)](https://msdn.microsoft.com/microsoft-r/rserver-install-windows).
  
## <a name="install-additional-r-tools"></a>Installieren zusätzlicher R-Tools  

 Wir empfehlen den kostenlosen [Microsoft R Client](http://aka.ms/rclient/download) (Download).  

 Mit Ihrer bevorzugten R-Entwicklungsumgebung können Sie auch Lösungen für SQL Server-R-Services oder Microsoft R Server entwickeln. Weitere Informationen finden Sie unter [Setup or Configure R Tools (Einrichten oder Konfigurieren von R-Tools)](../../advanced-analytics/r-services/setup-or-configure-r-tools.md). 
 

### <a name="location-of-r-server-binaries"></a>Speicherort der R Server-Binärdateien

Abhängig von der Methode, die Sie verwenden, um Microsoft R Server zu installieren, unterscheidet sich der Standardspeicherort. Bevor Sie beginnen, Ihre bevorzugte Entwicklungsumgebung zu verwenden, vergewissern Sie sich, wo Sie die R-Bibliotheken installiert haben:

+ Microsoft R Server, installiert mit dem neuen Windows Installer

  `C:\Program Files\Microsoft\R Server\R_SERVER`

+ R Server (Eigenständig), installiert mit SQL Server-Setup

  `C:\Program Files\Microsoft SQL Server\130\R_SERVER`

+ R Services (In-Database)

  `C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES`
      
## <a name="start-using-r-on-microsoft-r-server"></a>Starten Sie mit R in Microsoft R Server  

 Nachdem Sie die Serverkomponenten eingerichtet und Ihre R-IDE konfiguriert haben, um die R Server-Binärdateien zu verwenden, können Sie mit der Entwicklung der Projektmappe mit den neuen APIs, wie z.B. das RevoScaleR-Paket, MicrosoftML und olapR, beginnen.
    
Zum Einstieg in R Server finden Sie unter diesem Handbuch in der MSDN Library weitere Informationen: [R Server – Getting Started (R Server – Erste Schritte)](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node)   
  
-   [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started): Untersuchen Sie diese Sammlung von verteilbaren analytischen Funktionen, die eine hohe Leistung und Skalierung für R-Lösungen bereitstellen. Enthält parallelisierbare Versionen von vielen der beliebtesten R-Modellierpakete wie K-Means-Clustering, Entscheidungsstrukturen, Entscheidungswälder und Tools für die Datenbearbeitung. Weitere Informationen finden Sie unter [Explore R and ScaleR in 25 Functions (Erkunden von R und ScaleR in 25 Funktionen)](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started-tutorial).  
    
- [MicrosoftML](https://msdn.microsoft.com/library/mt790482.aspx): Das MicrosoftML-Paket ist eine Reihe von neuen bei Microsoft entwickelten Algorithmen für maschinelles Lernen und Transformationen, die schnell und skalierbar sind. Weitere Informationen finden Sie unter [MicrosoftML functions (Microsoft ML-Funktionen)](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml).
  


  
## <a name="see-also"></a>Siehe auch  
 [Erste Schritte mit SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  

