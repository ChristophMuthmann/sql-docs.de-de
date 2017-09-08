---
title: Einrichten oder Konfigurieren von R-Tools | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7c04ae30-d391-4369-9742-d2b275e14c0d
caps.latest.revision: 9
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a3baf97a960d7e8f950bb6e9cd251550f4c4b942
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="setup-or-configure-r-tools"></a>Einrichten oder Konfigurieren von R-Tools
  Microsoft R Server bietet alle R-Basisbibliotheken, die besten ScaleR-Pakete und R-Standardtools, die Sie benötigen, um R-Code zu entwickeln und testen. Wenn Sie jedoch eine dedizierte R-Entwicklungsumgebung verwenden möchten, gibt es mehrere verfügbare, einschließlich viele kostenlose Tools.  
  
## <a name="basic-r-tools"></a>Grundlegende R-Tools  
 Zusätzliche Tools sind in einer Installation von Microsoft R Server nicht erforderlich, da alle standardmäßigen R-Tools in einer *Basisinstallation* von R standardmäßig installiert werden.

-   **RTerm**: ein Befehlszeilentool zum Ausführen von R-Skripts. 
  
-   **RGui.exe**: einen einfachen interaktiven Editor für R. Die Befehlszeilenargumente sind identisch für RGui.exe und RTerm. 
  
-   **RScript**: ein Befehlszeilentool zum Ausführen von R-Skripts im Batchmodus.  

Sie finden diese Tools am Speicherort der R-Bibliothek. Dies variiert abhängig davon, ob Sie nur SQL Server R Services installiert, oder auch R Server (eigenständig) installiert haben. Weitere Informationen finden Sie unter [Was installiert wird und wo R-Pakete zu finden sind](https://msdn.microsoft.com/library/mt695941(sql.130).aspx#Anchor_1)

Suchen Sie anschließend im Ordner `..\R_SERVER\bin\x64`.  

> [!TIP]  
>  Benötigen Sie Hilfe mit den R-Tools? Dokumentation ist im Setupordner enthalten: `C:\Program Files\Microsoft SQL Server\R_SERVER\doc` und `C:\Program Files\Microsoft SQL Server\R_SERVER\doc\manual`.  
>   
>  Oder öffnen Sie einfach **Referenzbenutzeroberfläche**, klicken Sie auf **Hilfe**, und wählen Sie eine der Optionen aus.  

## <a name="microsoft-r-client"></a>Microsoft R Client

Microsoft R Client ist eine kostenlose Version, mit der Sie R-Lösungen herunterladen können, die problemlos in Microsoft R Server oder in SQL Server R Services ausgeführt werden können. Diese Option unterstützt Datenanalysten, die keinen Zugriff auf Entwicklungslösungen von R Server (verfügbar in der Enterprise Edition) haben, die ScaleR verwenden. 

Bei Verwendung einer anderen R-Entwicklungsumgebung, z.B. R-Tools für Visual Studio oder RStudio zur Nutzung von ScaleR, müssen Sie angeben, dass der Microsoft R Client als ausführbare R-Datei verwendet wird. Dadurch erhalten Sie Vollzugriff auf das RevoScaleR-Paket und andere Funktionen von Microsoft R Server, obwohl die Leistung beschränkt sind.

Sie können auch die Tools in R-Client nutzen, z.B. RGui und RTerm, um Skripts auszuführen oder Ad-hoc-R-Code zu schreiben und auszuführen.

[Installieren von Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-install)
  
##  <a name="bkmk_RTools"></a> R-Tools für Visual Studio  

 Für die problemlose Arbeit mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbanken sollten Sie die Verwendung von [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] als Entwicklungsumgebung in Betracht ziehen. [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] ist ein kostenloses Add-In für Visual Studio, das in allen Editionen von Visual Studio funktioniert. Visual Studio bietet auch Unterstützung für die Integration von Python und F#.  

 Installationsanweisungen finden Sie unter [zum Installieren von R-Tools für Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation).

> [!TIP]
> Überprüfen Sie vor der Installation von neuen Paketen, ob die R-Laufzeit standardmäßig verwendet wird. Andernfalls kann es leicht geschehen, dass Sie neue R-Pakete an einem Standardspeicherort für die Bibliothek installieren und sie dann nicht von einem R Server aus finden!


## <a name="rstudio"></a>RStudio

Wenn Sie RStudio verwenden möchten, sind einige zusätzliche Schritte erforderlich, um die RevoScaleR-Bibliotheken zu verwenden:
- Installieren Sie Microsoft R Server oder Microsoft R Client, um die erforderlichen Pakete und Bibliotheken zu erhalten.
- Aktualisieren Sie den R-Pfad, um die R-Laufzeit zu verwenden.

Weitere Informationen finden Sie unter [Konfigurieren der IDE](https://msdn.microsoft.com/microsoft-r/r-client-get-started#step-2-configure-your-ide).


## <a name="see-also"></a>Siehe auch  
 [Erstellen eines eigenständigen R Servers](../../advanced-analytics/r-services/create-a-standalone-r-server.md)   
 [Erste Schritte mit Microsoft R Server &#40;eigenständig&#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  

