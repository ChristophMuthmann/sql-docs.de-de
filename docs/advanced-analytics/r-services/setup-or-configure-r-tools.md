---
title: "Einrichten oder Konfigurieren von R-Tools | Microsoft Docs"
ms.custom: ""
ms.date: "01/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7c04ae30-d391-4369-9742-d2b275e14c0d
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# Einrichten oder Konfigurieren von R-Tools
  Microsoft R Server bietet Basis R-Bibliotheken, die Skalierung von R-Pakete und standard R-Tools, die Sie benötigen zum Entwickeln und Testen von R-Code. Wenn Sie eine dedizierte R-Entwicklungsumgebung verwenden möchten, gibt es jedoch mehrere verfügbar, einschließlich zahlreiche kostenlose Tools.  
  
## <a name="basic-r-tools"></a>Grundlegende R-Tools  
 Zusätzliche Tools sind in einer Installation von Microsoft R Server, nicht erforderlich, da alle standard-R-tools sind in enthalten eine *basieren Installation* von R werden standardmäßig installiert.

-   **RTerm**: ein Befehlszeilentool zum Ausführen von R-Skripts 
  
-   **RGui.exe**: einen einfachen interaktive-Editor für R. Die Befehlszeilenargumente sind für RGui.exe und RTerm identisch. 
  
-   **RScript**: ein Befehlszeilentool zum Ausführen von R-Skripts im Batchmodus ausgeführt.  

Standardmäßig werden diese Tools in den folgenden Ordnern installiert:
- SQLServer 2016: `C:\Program Files\Microsoft SQL Server\130\R_SERVER\bin\x64`  
- SQL Server vNext: `C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64`  

> [!TIP]  
>  Benötigen Sie weitere Hilfe? Dokumentation für die R-Tools finden Sie in den Ordner "Setup": `C:\Program Files\Microsoft SQL Server\R_SERVER\doc` und `C:\Program Files\Microsoft SQL Server\R_SERVER\doc\manual`.  
>   
>  Oder öffnen Sie einfach **"rgui.exe"**, klicken Sie auf **Hilfe**, und wählen Sie eine der Optionen.  

## <a name="microsoft-r-client"></a>Microsoft R Client

Microsoft R-Client ist kostenlos, mit dem Sie die R-Lösungen zu entwickeln, die einfach in Microsoft R Server oder in SQL Server R Services ausgeführt werden können.

In der Regel installieren eine andere R-Entwicklungsumgebung, z. B. R-Tools für Visual Studio oder RStudio, und klicken Sie dann angeben, dass der Microsoft-R-Client als ausführbare Datei R verwendet werden. Dies ermöglicht Ihnen vollständigen Zugriff auf die "revoscaler"-Paket und anderen Funktionen von Microsoft R Server.

Sie können auch vertrauten Tools z. B. "rgui.exe" und RTerm Ausführen von Skripts oder das Schreiben und ad-hoc-R-Code ausführen.

[Installieren Sie Microsoft R-Client](https://msdn.microsoft.com/microsoft-r/r-client-install)
  
##  <a name="a-namebkmkrtoolsa-r-tools-for-visual-studio"></a> R-Tools für Visual Studio  

 Der Einfachheit halber beim Arbeiten mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbanken in Betracht [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] als Ihre Entwicklungsumgebung. [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] ist ein kostenloses add-in für Visual Studio, die in allen Editionen von Visual Studio funktioniert. Visual Studio bietet auch Unterstützung für die Integration von Python und f#.  

Weitere Informationen finden Sie unter [VisualStudio.com](https://www.visualstudio.com/vs/rtvs/).

 Dieser Abschnitt enthält Anweisungen zur Installation [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] die kostenlose Community-Edition von Visual Studio verwenden.  
  
#### <a name="install-visual-studio"></a>Installieren von Visual Studio  
  
1.  Die kostenlose Community-Edition von Visual Studio steht zum Download auf dieser Seite: [Visual Studio-Community](http://visualstudio.com/products/visual-studio-community-vs.aspx)  
  
2.  Wenn der Download abgeschlossen ist, klicken Sie auf **Ausführen** und wählen Sie die zu installierenden Komponenten.  
  
     Wenn Sie eine benutzerdefinierte Installation tun, beachten Sie, dass die Microsoft Web Developer-Komponenten erforderlich sind.  
  
3.  Wählen Sie die **Allgemeine** festgelegt wird. Bei der Installation [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)], stehen Ihnen die Toption so ändern Sie ein Layout für die Entwicklung von R angepasst.  

#### <a name="add-the-r-tools"></a>Hinzufügen von R-Tools

Nach der Installation von Visual Studio werden Erweiterungen für R, Python und viele weitere Sprachen über die **Optionen** Menü.

4. Klicken Sie auf der Menüleiste auf Extras, und wählen Sie dann **Erweiterungen und Updates**.

5. Gegen Ende der Installation erkennt R-Tools die Versionen der R-Laufzeit, die auf dem Computer verfügbar sind, und gefragt, ob Sie Ihre Entwicklungsumgebung für das Verwenden der R-Laufzeit für Microsoft R Server oder der R-Laufzeit für Microsoft R-Client ändern möchten.

Wenn Setup das R-Server-Laufzeitmodul nicht Sie verwenden möchten erkennen, können Sie ändern sie manuell zu einem beliebigen Zeitpunkt mithilfe der **Optionen** Menü. Weitere Informationen finden Sie unter [Konfigurieren der IDE](https://msdn.microsoft.com/microsoft-r/r-client-get-started#step-2-configure-your-ide).

## <a name="rstudio"></a>RStudio

Wenn Sie es vorziehen, verwenden Sie RStudio, diese weitere Schritte ausführen, die "revoscaler"-Bibliotheken zu verwenden:
- Installieren Sie Microsoft R Server oder Microsoft R-Client auf, um die erforderlichen Pakete und Bibliotheken zu erhalten.
- Aktualisieren Sie den R-Pfad, um die entsprechenden R-Laufzeit verwenden.

Weitere Informationen finden Sie unter [Konfigurieren der IDE](https://msdn.microsoft.com/microsoft-r/r-client-get-started#step-2-configure-your-ide).


## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie einen eigenständigen R-Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md)   
 [Erste Schritte mit Microsoft R Server &#40; Eigenständige &#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  