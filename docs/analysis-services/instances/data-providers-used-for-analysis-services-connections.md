---
title: "F&#252;r Analysis Services-Verbindungen verwendete Datenanbieter | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 128f6dde-409d-4c12-9820-3305bab57b75
caps.latest.revision: 19
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 18
---
# F&#252;r Analysis Services-Verbindungen verwendete Datenanbieter
  Analysis Services stellt drei Datenanbieter für den Server- und Datenzugriff bereit. Alle Anwendungen, die eine Verbindung mit Analysis Services herstellen, verwenden dazu einen dieser Anbieter. Die beiden Anbieter ADOMD.NET und AMO (Analysis Services Management Objects) sind verwaltete Datenanbieter. Der Analysis Services OLE DB-Anbieter (MSOLAP DLL) ist ein systemeigener Datenanbieter.  
  
 In Organisationen, in denen mehrere Analysis Services-Versionen ausgeführt werden, müssen auf Benutzerarbeitsstationen, die eine Verbindung mit Analysis Services-Daten herstellen, u. U. neuere Versionen der Datenanbieter installiert werden. Damit Verbindungen mit neueren Analysis Services-Versionen hergestellt werden können, sind Datenanbieter derselben Hauptversion erforderlich. Um eine Verbindung mit [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]herzustellen, muss jede Arbeitsstation beispielsweise über einen Datenanbieter derselben Version verfügen. Obwohl die von Excel für Verbindungen benötigten Datenanbieter installiert werden, kann dieser Anbieter im Vergleich zu den verwendeten Analysis Services-Instanzen veraltet sein.  
  
 Dieses Thema enthält die folgenden Abschnitte:  
  
 [Ermitteln der Serverversion](#bkmk_ServVers)  
  
 [Ermitteln der Version von Analysis Services-Datenanbietern](#bkmk_LibUpdate)  
  
 [Herunterladen einer neueren Version des Datenanbieters](#bkmk_downloadsite)  
  
 [Analysis Services OLE DB-Anbieter](#bkmk_OLE)  
  
 [ADOMD.NET](#bkmk_ADOMD)  
  
 [AMO](#blkmk_AMO)  
  
##  <a name="bkmk_ServVers"></a> Ermitteln der Serverversion  
 Wenn Sie die Version der Analysis Services-Instanz kennen, können Sie leichter feststellen, ob für die unternehmensweiten Arbeitsstationen neuere Versionen der Datenanbieter installiert werden müssen.  
  
-   Stellen Sie in SQL Server Management Studio eine Verbindung mit der Analysis Services-Instanz her. Sie können Versionsinformationen unter **Servereigenschaften** > **Allgemein** > **Version**aufrufen.  
  
 Die Hauptbuildnummer der ersten Version von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ist 13.0.1601.5.  
  
  
##  <a name="bkmk_LibUpdate"></a> Ermitteln der Version von Analysis Services-Datenanbietern  
 Datenanbieter werden mit Analysis Services sowie von Clientanwendungen installiert, die routinemäßig Verbindungen mit Analysis Services-Datenbanken herstellen, z. B. Excel.  
  
 Mit Office 2010 werden Datenanbieter von SQL Server 2008 installiert. Mit Office 2013 werden Datenanbieter von SQL Server 2012 usw. installiert. Wenn Sie mehrere Office- oder SQL Server-Versionen verwenden und die Verfügbarkeit von Verbindungen oder Funktionen nicht Ihren Erwartungen entspricht, müssen Sie ggf. eine neuere Version der Datenanbieter installieren. Von jedem Datenanbieter können mehrere Hauptversionen parallel auf demselben Computer ausgeführt werden.  
  
#### Ermitteln der Dateiversion des OLE DB-Anbieters  
  
1.  Navigieren Sie zu „\Programme\Microsoft Analysis Services\AS OLEDB\130“.  
  
2.  Klicken Sie mit der rechten Maustaste auf **msolap130.dll** > **Eigenschaften** > **Details**.  
  
 Wenn Sie die Datei an diesem Ort nicht finden oder wenn der Ordnerpfad AS OLEDB\110 oder AS OLEDB\90 enthält, verwenden Sie eine ältere Bibliothek und müssen jetzt eine neuere Version (AS OLEDB\11) installieren, um eine Verbindung mit [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]herzustellen.  
  
#### Ermitteln der Dateiversion von ADOMD.NET und AMO  
  
1.  Wechseln Sie zu C:\Windows\Assembly.  
  
2.  Klicken Sie mit der rechten Maustaste auf Microsoft.AnalysisServices.AdomdClient, und klicken Sie auf **Eigenschaften**. Klicken Sie auf **Version**.  
  
     Klicken Sie für AMO mit der rechten Maustaste auf Microsoft.AnalysisServices.  
  
##  <a name="bkmk_downloadsite"></a> Herunterladen einer neueren Version des Datenanbieters  
 Die auf dem Clientcomputer installierte Version sollte mit der Hauptversion des Servers übereinstimmen, der die Daten bereitstellt. Wenn die Serverinstallation neuer als die auf den Arbeitsstationen im Netzwerk installierten Datenanbieter ist, müssen Sie u. U. neuere Bibliotheken installieren.  
  
#### Suchen der Datenanbieter auf der Downloadwebsite  
  
1.  Wechseln Sie zum [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkID=296473).  
  
2.  Erweitern Sie **Installationsanweisungen**. ADOMD.NET, der OLE DB-Anbieter und AMO sind in der Liste enthalten. Jede Bibliothek ist als 32- und 64-Bit-Version verfügbar. Server und neuere Arbeitsstationen, auf denen ein 64-Bit-Betriebssystem ausgeführt wird, erfordern die 64-Bit-Version.  
  
##  <a name="bkmk_OLE"></a> Analysis Services OLE DB-Anbieter  
 Der Analysis Services OLE DB-Anbieter ist der systemeigene Anbieter für Analysis Services-Datenbankverbindungen. MSOLAP wird indirekt von ADOMD.NET und AMO verwendet, wodurch Verbindungsanforderungen an den Datenanbieter delegiert werden. Sie können den OLE DB-Anbieter auch direkt im Anwendungscode aufrufen, beispielsweise wenn die Verwendung einer verwalteten API für die Lösung nicht infrage kommt.  
  
 Der Analysis Services OLE DB-Anbieter wird von SQL Server-Setup, Excel und anderen Anwendungen, die häufig für den Zugriff auf Analysis Services-Datenbanken verwendet werden, automatisch installiert. Sie können ihn auch manuell installieren, indem Sie ihn aus dem Download Center herunterladen. Der Anbieter befindet sich standardmäßig im Ordner \Programme\Microsoft Analysis Services. Der Anbieter muss auf jeder Arbeitsstation installiert werden, die für den Zugriff auf Analysis Services-Daten verwendet wird.  
  
 Die mit [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] gelieferte Version des Analysis Services OLE DB-Anbieters lautet MSOLAP130.dll. Einige der letzten Vorgängerversionen waren MSOLAP110.dll (für SQL Server 2008 und 2008 R2) und MSOLAP90.dll (für SQL Server 2005).  
  
 OLE DB-Anbieter werden häufig in Verbindungszeichenfolgen angegeben. In einer Analysis Services-Verbindungszeichenfolge wird mit einer anderen Benennung auf den OLE DB-Anbieter verwiesen: MSOLAP.\<Version>>.dll  
  
 MSOLAP.5.dll ist der aktuelle Analysis Services OLE DB-Anbieter, der mit Excel 2013 installiert wird. Auf Arbeitsstationen mit älteren Excel-Versionen sind häufig frühere Versionen wie MSOLAP.4.dll oder MSOLAP.3.dll zu finden. Einige Analysis Services-Funktionen, wie das [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Add-In, erfordern bestimmte Versionen des OLE DB-Anbieters. Weitere Informationen finden Sie unter [Verbindungszeichenfolgen-Eigenschaften &#40;Analysis Services&#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md).  
  
##  <a name="bkmk_ADOMD"></a> ADOMD.NET  
 ADOMD.NET ist ein verwalteter Datenanbieter, der zum Abfragen von Analysis Services-Daten verwendet wird. Excel verwendet ADOMD.NET beim Herstellen einer Verbindung mit einem bestimmten Analysis Services-Cube. Die in Excel angezeigte Verbindungszeichenfolge bezieht sich auf eine ADOMD.NET-Verbindung.  
  
 ADOMD.NET wird von SQL Server-Setup installiert und von SQL Server-Clientanwendungen für Verbindungen mit Analysis Services genutzt. Mit Office wird diese Bibliothek zur Unterstützung von Datenverbindungen von Excel aus installiert. Wenn Sie die Bibliothek in benutzerdefiniertem Code verwenden, können Sie ADOMD.NET wie alle anderen in SQL Server enthaltenen Datenanbieter neu verteilen. Sie können ADOMD.NET auch herunterladen und manuell installieren, um die neuere Version zu erhalten (Informationen hierzu finden Sie unter [Ermitteln der Version von Analysis Services-Datenanbietern](#bkmk_LibUpdate) in diesem Thema).  
  
 Um die Dateiversion zu überprüfen, suchen Sie ADOMD.NET im globalen Assemblycache unter `Microsoft.AnalysisServices.AdomdClient`.  
  
 Beim Herstellen einer Verbindung mit einer Datenbank sind die Verbindungszeichenfolgen-Eigenschaften für alle drei Bibliotheken weitgehend identisch. Nahezu jede Verbindungszeichenfolge, die Sie für ADOMD.NET (<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>) definieren, funktioniert auch für AMO und den Analysis Services OLE DB-Anbieter. Weitere Informationen finden Sie unter [Verbindungszeichenfolgen-Eigenschaften &#40;Analysis Services&#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md).  
  
 Weitere Informationen zum programmgesteuerten Herstellen einer Verbindung finden Sie unter [Establishing Connections in ADOMD.NET](../Topic/Establishing%20Connections%20in%20ADOMD.NET.md).  
  
##  <a name="blkmk_AMO"></a> AMO  
 AMO ist ein verwalteter Datenanbieter, der für die Serververwaltung und Datendefinition verwendet wird. Beispielsweise verwendet SQL Server Management Studio AMO, um Verbindungen mit Analysis Services herzustellen.  
  
 AMO wird von SQL Server-Setup installiert und von SQL Server-Clientanwendungen für Verbindungen mit Analysis Services genutzt. Sie können es auch herunterladen und manuell installieren, wenn Sie AMO im benutzerdefinierten Code verwenden (Informationen hierzu finden Sie unter [Ermitteln der Version von Analysis Services-Datenanbietern](#bkmk_LibUpdate) in diesem Thema). AMO ist im globalen Assemblycache als `Microsoft.AnalysisServices`enthalten.  
  
 Eine Verbindung mit AMO ist normalerweise sehr einfach gehalten und besteht z.B. aus „data source=\<Servername>“. Nachdem eine Verbindung hergestellt wurde, verwenden Sie die API, um mit Datenbankauflistungen und Hauptobjekten zu arbeiten. Sowohl SSDT als auch SSMS verwenden AMO, um eine Verbindung mit einer Analysis Services-Instanz herzustellen.  
  
 Weitere Informationen zum programmgesteuerten Herstellen einer Verbindung finden Sie unter [Programming AMO Fundamental Objects](../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-fundamental-objects.md).  
  
## Siehe auch  
 [Verbindung mit Analysis Services herstellen](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  