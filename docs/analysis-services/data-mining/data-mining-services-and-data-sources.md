---
title: Datamining-Dienste und Datenquellen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b26fd6e3-7d87-4f66-ab47-5303b51b87da
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 78e67d346c451c258e806e6f888aef096e7d4256
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="data-mining-services-and-data-sources"></a>Data Mining-Dienste und Datenquellen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Für Data Mining ist eine Verbindung zu einer Instanz von SQL Server Analysis Services erforderlich. Daten von einem Cube sind für Data Mining nicht erforderlich, und die Verwendung relationaler Quellen wird empfohlen. Data Mining verwendet jedoch vom [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Modul bereitgestellte Komponenten.  
  
 Dieses Thema enthält Informationen, die erforderlich sind, wenn Sie eine Verbindung zu einer lokalen oder Remoteinstanz von SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] herstellen, um Data Mining-Modelle zu erstellen, zu verarbeiten, bereitzustellen oder abzufragen.  
  
## <a name="data-mining-services"></a>Data Mining-Dienste  
 Die Serverkomponente von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ist die Anwendung msmdsrv.exe, die normalerweise als Windows-Dienst ausgeführt wird. Diese Anwendung besteht aus Sicherheitskomponenten, einer XMLA-Überwachungskomponente (XML for Analysis), einer Abfrageverarbeitungskomponente und zahlreichen internen Komponenten, die die folgenden Funktionen ausführen:  
  
-   Analysieren von Anweisungen, die von Client empfangen werden  
  
-   Verwalten von Metadaten  
  
-   Behandeln von Transaktionen  
  
-   Verarbeiten von Berechnungen  
  
-   Speichern von Dimensions- und Zellendaten  
  
-   Erstellen von Aggregationen  
  
-   Planen von Abfragen  
  
-   Zwischenspeichern von Objekten  
  
-   Verwalten von Serverressourcen  
  
### <a name="xmla-listener"></a>XMLA-Überwachung  
 Die XMLA-Überwachungskomponente verarbeitet die gesamte XMLA-Kommunikation zwischen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] und den zugehörigen Clients. Mithilfe der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] **Port** in der Datei msmdsrv.ini können Sie einen Port angeben, der von einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] überwacht wird. Wird in dieser Datei der Wert 0 angegeben, wird der Standardport von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] überwacht. Falls nicht anders angegeben, verwendet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die folgenden TCP-Standardports:  
  
|Port|Description|  
|----------|-----------------|  
|2383|Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|2382|Redirector für andere Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|Dynamische Zuweisung beim Serverstart.|Benannte Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
  
 Weitere Informationen zum Steuern der von diesem Dienst verwendeten Ports finden Sie unter [Konfigurieren der Windows-Firewall, um den Zugriff auf Analysis Services zuzulassen](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
## <a name="connecting-to-data-sources"></a>Herstellen einer Verbindung mit Datenquellen  
 Bei jedem Erstellen oder Aktualisieren einer Data Mining-Struktur oder -Modells verwenden Sie Daten, die von einer Datenquelle definiert sind. Die Datenquelle enthält nicht die Daten, die Excel-Arbeitsmappen, Textdateien und SQL Server-Datenbanken enthalten könnten. Sie definiert nur die Verbindungsinformationen.  Eine Datenquellensicht (Data Source View, DSV) dient oben auf dieser Quelle als Abstraktionsebene, ändert oder ordnet die Daten zu, die aus der Quelle abgerufen werden.  
  
 Es ginge über dieses Thema hinaus, die Verbindungsanforderungen für jede dieser Quellen zu beschreiben. Weitere Informationen finden Sie in der Dokumentation für den Anbieter. Sie sollten im Allgemeinen jedoch die folgenden Anforderungen von Analysis Services beachten, wenn Sie mit Anbietern interagieren:  
  
-   Da Data Mining ein von einem Server bereitgestellter Dienst ist, muss die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz auf die Datenquelle zugreifen können.  Es gibt zwei Aspekte zuzugreifen: Speicherort und Identität.  
  
     **Speicherort** bedeutet, wenn Sie ein Modell mithilfe der nur auf Ihrem Computer gespeicherten Daten erstellen und dieses Modell dann auf einem Server bereitstellen, könnte das Modell nicht verarbeitet werden, da die Datenquelle nicht gefunden werden kann. Zum Beheben dieses Problem könnten Sie Daten in die gleiche SQL Server-Instanz übertragen, in der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ausgeführt wird, oder indem Sie Dateien zu einem freigegebenen Speicherort verschieben.  
  
     **Identität** bedeutet, dass die Dienste auf [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in der Lage sein müssen, die Datendatei oder die Datenquelle mit den entsprechenden Anmeldeinformationen zu öffnen. Als Sie beispielsweise das Modell erstellt haben, standen Ihnen möglicherweise unbegrenzte Berechtigungen zum Anzeigen der Daten zur Verfügung, der Benutzer, der die Modelle auf dem Server verarbeitet and aktualisiert, kann möglicherweise nur eingeschränkt oder nicht auf die Daten zugreifen. Dies wiederum kann zu Fehlern bei der Verarbeitung führen oder die Inhalte des Modells beeinträchtigen. Das Konto, das zum Verbinden zur Remotedatenquelle verwendet wird, muss mindestens über Leseberechtigungen auf die Daten verfügen.  
  
-   Wenn Sie ein Modell verschieben, sind die gleichen Anforderungen gültig: Sie müssen entsprechenden Zugriff zum Speicherort der alten Datenquelle einrichten, müssen die Datenquellen kopieren oder müssen eine neue Datenquelle konfigurieren. Sie müssen zudem Anmeldedaten und Rollen übertragen oder Berechtigungen einrichten, damit Data Mining-Objekte am neuen Speicherort verarbeitet und aktualisiert werden können.  
  
## <a name="configuring-permissions-and-server-properties"></a>Konfigurieren von Berechtigungen und Servereigenschaften  
 Data Mining erfordert zusätzliche Berechtigungen für eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank. Die meisten Data Mining-Eigenschaften können im [Dialogfeld „Eigenschaften für Analysis-Server“ &#40;Analysis Services&#41;](http://msdn.microsoft.com/library/b01ec658-c191-49c9-a6cb-549b21a368ab) festgelegt werden.  
  
 Weitere Informationen zu den Eigenschaften, die Sie konfigurieren können, finden Sie unter [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 Die folgenden Servereigenschaften sind im Hinblick auf Data Mining besonders relevant:  
  
-   **AllowAdHocOpenRowsetQueries** : Steuert den Ad-hoc-Zugriff auf OLE DB-Anbieter, die direkt in den Serverspeicherbereich geladen werden.  
  
    > [!IMPORTANT]  
    >  Zur Erhöhung der Sicherheit wird empfohlen, diese Eigenschaft auf **false**festzulegen. Der Standardwert ist **false**. Auch wenn diese Eigenschaft auf **false**festgelegt ist, können Benutzer dennoch weiterhin SINGLETON-Abfragen erstellen und OPENQUERY für zulässige Datenquellen verwenden.  
  
-   **AllowedProvidersInOpenRowset** : Gibt den Anbieter an, wenn Ad-hoc-Zugriff aktiviert ist. Sie können mehrere Anbieter angeben, indem Sie eine durch Trennzeichen getrennte Liste von Programm-IDs eingeben.  
  
-   **MaxConcurrentPredictionQueries** : Steuert die durch Vorhersagen verursachte Last auf dem Server. Mit dem Standardwert 0 sind unbegrenzte Abfragen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise sowie maximal fünf gleichzeitige Abfragen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard möglich. Abfragen über diesem Limit werden serialisiert und können zu einem Timeout führen.  
  
 Der Server bietet zusätzliche Eigenschaften, die die Verfügbarkeit der Data Mining-Algorithmen, einschließlich Einschränkungen der Algorithmen, und die Standardwerte für alle Data Mining-Dienste steuern. Es gibt jedoch keine Einstellungen, mit denen Sie den Zugriff speziell auf Data Mining-gespeicherte Prozeduren steuern können. Weitere Informationen finden Sie unter [Data Mining Properties](../../analysis-services/server-properties/data-mining-properties.md).  
  
 Sie können auch Eigenschaften festlegen, mit denen Sie den Server optimieren und die Sicherheit für die Clientverwendung kontrollieren können. Weitere Informationen finden Sie unter [Feature Properties](../../analysis-services/server-properties/feature-properties.md).  
  
> [!NOTE]  
>  Weitere Informationen dazu, welche Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Plug-In-Algorithmen unterstützen, finden Sie unter [Von den SQL Server 2012-Editionen unterstützte Funktionen](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473).  
  
## <a name="programmatic-access-to-data-mining-objects"></a>Programmgesteuerter Zugriff auf Data Mining-Objekte  
 Mit den folgenden Objektmodellen können Sie eine Verbindung zu einer Analysis Services-Datenbank herstellen und mit Data Mining-Objekten arbeiten.  
  
 **ADO** : Verwendet OLE DB zur Herstellung einer Verbindung mit einem Analysis Services-Server. Wenn Sie ADO verwenden, wird der Client auf Schemarowsetabfragen und DMX-Anweisungen beschränkt.  
  
 **ADO.NET** : Interagiert mit SQL Server-Anbietern besser als mit anderen Anbietern. Verwendet Datenadapter, um dynamische Rowsets zu speichern. Verwendet das Datasetobjekt, das einen Cache der als Datentabellen gespeicherten Serverdaten darstellt. Diese Tabellen können aktualisiert oder im XML-Format gespeichert werden.  
  
 **ADOMD.NET** : Ein verwalteter Datenanbieter, der zur Verwendung mit Data Mining und OLAP optimiert ist. ADOMD.NET ist schneller und speichereffizienter als ADO.NET. Mit ADOMD.NET können Sie auch Metadaten über Serverobjekte abrufen. ADOMD.NET wird für Clientanwendungen empfohlen, außer .NET ist nicht verfügbar.  
  
 **Server-ADOMD** : Objektmodell für den direkten Zugriff auf Analysis Services-Objekte auf dem Server. Wird von Analysis Services-gespeicherten Prozeduren verwendet; nicht für die Clientverwendung.  
  
 **AMO:** Verwaltungsschnittstelle für Analysis Services, die Entscheidungsunterstützungsobjekte (DSO) ersetzt. Beim Verwenden von AMO erfordern Vorgänge wie die Iteration von Objekten höhere Berechtigungen als bei Verwendung anderer Schnittstellen. Der Grund hierfür liegt darin, dass AMO direkt auf Metadaten zugreift, wohingegen ADOMD.NET und andere Schnittstellen nur auf die Datenbankschemas zugreifen.  
  
### <a name="browse-and-query-access-to-servers"></a>Durchsuchen und Abfragezugriff auf Server  
 Sie können alle Arten von Vorhersagen mit einer Instanz von Analysis Services im OLAP-/Data Mining-Modus ausführen. Es gelten jedoch folgende Einschränkungen:  
  
-   Wenn Sie Server-ADOMD verwenden, können Sie mit DMX auf den Server zugreifen, ohne eine Verbindung herzustellen. Anschließend können Sie die Ergebnisse direkt in eine Datentabelle kopieren. Server-ADOMD kann jedoch nicht ohne Remote-Instanzen verwendet werden. Sie können nur den lokalen Server abfragen.  
  
-   ADO.NET unterstützt keine benannten Parameter für Data Mining. Sie müssen ADOMD.NET verwenden.  
  
-   Mit ADOMD.NET können Sie eine gesamte Tabelle zur Verwendung als Parameter übergeben. Daher können Sie die Daten auf dem Client oder Daten verwenden, die für den Server nicht verfügbar sind. Möglich ist auch die Verwendung von gestalteten Tabellen als Vorhersageeingabe.  
  
### <a name="using-data-mining-stored-procedures"></a>Verwenden von Data Mining-gespeicherten Prozeduren  
 Gespeicherte Prozeduren werden häufig zum Kapseln von Abfragen zur Wiederverwendung verwendet. Der Client kann CALL verwenden, um gespeicherte Prozeduren auszuführen, einschließlich gespeicherte Systemprozeduren von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Wenn die Prozedur ein Dataset zurückgibt, erhält der Client ein Dataset oder eine Datentabelle mit einer geschachtelten Tabelle, die die Zeilen enthält. Wenn Sie jedoch eine Abfrage für den Modellinhalt erstellen, gibt die Abfrage das ganze Modell zurück. Damit nicht zu viele Zeilen zurückgegeben werden, können Sie gespeicherte Prozeduren schreiben, indem Sie das ADOMD+-Objektmodell verwenden.  
  
 Um eine servergespeicherte Prozedur zu schreiben, müssen Sie auf den Microsoft.AnalysisServices.AdomdServer-Namespace verweisen. Weitere Informationen zum Erstellen und Verwenden von gespeicherten Prozeduren finden Sie unter [User Defined Functions and Stored Procedures](../../analysis-services/multidimensional-models-adomd-net-server/user-defined-functions-and-stored-procedures.md).  
  
> [!NOTE]  
>  Gespeicherte Prozeduren können nicht verwendet werden, um die Sicherheit auf Datenserverobjekten zu ändern. Wenn Sie eine gespeicherte Prozedur ausführen, wird der aktuelle Kontext des Benutzers verwendet, um den Zugriff auf alle Serverobjekte zu bestimmen. Daher müssen Benutzer über entsprechende Berechtigungen für Datenbankobjekte verfügen, auf die sie zugreifen.  
  
## <a name="see-also"></a>Siehe auch  
 [Physische Architektur &#40;Analysis Services – mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-physical-architecture.md)   
 [Physische Architektur &#40; Analysis Services – Datamining &#41;](../../analysis-services/data-mining/physical-architecture-analysis-services-data-mining.md)   
 [Verwaltung von Datamining-Lösungen und-Objekten](../../analysis-services/data-mining/management-of-data-mining-solutions-and-objects.md)  
  
  
