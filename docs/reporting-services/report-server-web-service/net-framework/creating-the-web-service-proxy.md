---
title: Erstellen den Webdienstproxy | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Report Server Web service, proxies
- proxies [Reporting Services]
- XML Web service [Reporting Services], proxies
- Web service [Reporting Services], proxies
- Web references [Reporting Services]
ms.assetid: b1217843-8d3d-49f3-a0d2-d35b0db5b2df
caps.latest.revision: 44
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: 1c39d81ec9a1d2cd24f01b9dccfed13e8560a770
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="creating-the-web-service-proxy"></a>Erstellen des Webdienstproxys
  Ein Client und ein Webdienst können über SOAP-Nachrichten kommunizieren, die die Eingabe- und Ausgabeparameter als XML-Datei einkapseln. Eine Proxyklasse ordnet XML-Elementen Parameter zu und sendet dann die SOAP-Nachrichten über ein Netzwerk. So sorgt die Proxyklasse dafür, dass Sie nicht auf der SOAP-Ebene mit dem Webdienst kommunizieren müssen. Außerdem können Sie die Webdienstmethoden in jeder Entwicklungsumgebung aufrufen, die SOAP- und Webdienstproxys unterstützt.  
  
 Es gibt zwei Möglichkeiten, eine Proxyklasse hinzuzufügen, bei der Entwicklung Projekt mithilfe der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]: mit dem WSDL-Tool in der [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], und durch das Hinzufügen eines Webverweises in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]. In den folgenden Abschnitten wird dieser Betreff detaillierter erläutert.  
  
## <a name="adding-the-proxy-using-the-wsdl-tool"></a>Hinzufügen des Proxys über das WSDL-Tool  
 Das [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]-SDK enthält das WSDL-Tool (Web Services Description Language, Wsdl.exe), mit dem Sie einen Webdienstproxy für die Verwendung in der [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]-Entwicklungsumgebung generieren können. Die gängigste Methode, um einen Clientproxy in Sprachen zu erstellen, die Webdienste unterstützen (derzeit c# und [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) ist die Verwendung des WSDL-Tools.  
  
 **Das Projekt mit Wsdl.exe eine Proxyklasse hinzu**  
  
1.  Verwenden Sie Wsdl.exe über eine Eingabeaufforderung, um eine Proxyklasse zu erstellen, und geben Sie (mindestens) die URL zum Berichtsserver-Webdienst an  
  
     Beispielsweise gibt die folgende Anweisung der Eingabeaufforderung eine URL für den Verwaltungsendpunkt des Berichtsserver-Webdiensts an.  
  
    ```  
    wsdl /language:CS /n:"Microsoft.SqlServer.ReportingServices2010" http://<Server Name>/reportserver/reportservice2010.asmx?wsdl  
    ```  
  
     Das WSDL-Tool akzeptiert zum Generieren eines Proxys mehrere Eingabeaufforderungsargumente. Das vorhergehende Beispiel gibt die Sprache C# an, außerdem einen vorgeschlagenen Namespace für die Verwendung im Proxy (um Namenskonflikte zu verhindern, wenn Sie mehr als einen Webdienst-Endpunkt verwenden), und generiert eine C#-Datei mit dem Namen ReportingService2010.cs. Wenn im Beispiel [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] angegeben worden wäre, wäre eine Proxydatei mit dem Namen ReportingService2010.vb generiert worden. Diese Datei wird in dem Verzeichnis erstellt, von dem Sie den Befehl ausführen.  
  
2.  Kompilieren Sie die Proxyklasse in eine Assemblydatei (mit der Erweiterung .dll), und verweisen Sie im Projekt darauf, oder fügen Sie die Klasse als Projektelement hinzu.  
  
    > [!NOTE]  
    >  Wenn Sie eine Proxyklasse manuell zum Projekt hinzufügen, müssen Sie einen Verweis zu System.Web.Services.dll hinzufügen. Wenn Sie den Proxy mithilfe eines Webverweises in Visual Studio .NET hinzufügen, wird der Verweis automatisch für Sie erstellt. Weitere Informationen finden Sie später in diesem Kapitel unter "Hinzufügen eines Proxys mit einem Webverweis in Visual Studio".  
  
     Nachdem Sie die Proxyklasse als Element zu Ihrem Projekt hinzugefügt haben, wird die zugehörige Datei im Projektmappen-Explorer angezeigt.  
  
3.  Um den Dienst programmgesteuert aufzurufen, erstellen Sie eine Instanz der Proxyklasse.  
  
     Im folgenden Codebeispiel wird die Syntax zum Erstellen einer Instanz der <xref:ReportService2010.ReportingService2010>-Proxyklasse in einem Projekt gezeigt:  
  
```vb  
Dim service As New ReportingService2010()  
```  
  
```csharp  
ReportingService2010 service = new ReportingService2010();  
  
```  
  
 Weitere Informationen zum Tool Wsdl.exe, einschließlich der kompletten Syntax, finden Sie unter "Web Services Description Language Tool" in der [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK-Dokumentation. Eine vollständige Erläuterung zu Webdienstproxys finden Sie unter "Erstellen eines XML-Webdienstproxys" in der [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK-Dokumentation.  
  
## <a name="adding-the-proxy-using-a-web-reference-in-visual-studio"></a>Hinzufügen eines Proxys mit einem Webverweis in Visual Studio  
 Über einen Webverweis kann ein Projekt einen oder mehrere Webdienste verwenden. [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] bietet Benutzern die Möglichkeit, Webdienstverweise mit einigen einfachen Schritten zu Projekten hinzuzufügen.  
  
 **So fügen Sie zu einem Projekt einen Webverweis hinzu**  
  
1.  In **Projektmappen-Explorer**, wählen Sie das Projekt, das den Webdienst beansprucht.  
  
2.  Auf der **Projekt** Menü klicken Sie auf **Webverweis hinzufügen**.  
  
     Die **Webverweis hinzufügen** Dialogfeld wird geöffnet.  
  
3.  In der **URL** Feld, geben Sie den vollständigen Pfad zu den Report Server-Webdienst.  
  
     Eine vereinfachte URL für den Berichtsausführungsendpunkt des Berichtsserver-Webdiensts kann folgendermaßen aussehen:  
  
    ```  
    http://<Server Name>/reportserver/reportexecution2005.asmx  
    ```  
  
     Die URL enthält die Domäne, in der der Berichtsserver-Webdienst bereitgestellt wird, den Namen des Ordners, der den Dienst enthält, und den Namen der Ermittlungsdatei für den Dienst. Eine vollständige Beschreibung der verschiedenen URL-Elemente, finden Sie unter [den Zugriff auf die SOAP-API](../../../reporting-services/report-server-web-service/accessing-the-soap-api.md).  
  
     Eine Beschreibung der vom Webdienst zur Verfügung gestellten Methoden und Eigenschaften befindet sich im Browserbereich auf der linken Seite.  
  
    > [!NOTE]  
    >  Weitere Informationen zu den Elementen, die mit der Berichtsserver-Webdienst verknüpft ist, finden Sie unter [Webdienstmethoden für Berichtsserver](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md).  
  
4.  Überprüfen Sie, dass das Projekt den Berichtsserver-Webdienst verwenden kann und dass Sie über die entsprechende Zugriffsberechtigung für den Berichtsserver verfügen.  
  
5.  In der **Webverweisname** Feld, geben Sie einen Namen, die Sie verwenden den Code in der Berichtsserver-Webdienst programmgesteuert zugreifen.  
  
6.  Wählen Sie die **Verweis hinzufügen** Schaltfläche, um einen Verweis in der Anwendung an den Webdienst zu erstellen.  
  
     Der neue Verweis wird im **Projektmappen-Explorer** unter den Knoten Webverweise für das aktive Projekt mit dem Namen gemäß der **Webverweisname** Feld.  
  
7.  In **Projektmappen-Explorer**, erweitern Sie den Ordner Webverweise, um den Namespace für die Webverweisklassen beachten, die für die Elemente in Ihrem Projekt zur Verfügung stehen.  
  
     Nach dem Hinzufügen zu Ihrem Projekt eines Webverweis, werden die zugehörigen Dateien in einem Ordner im Ordner Webverweise von angezeigt **Projektmappen-Explorer**.  
  
 Nachdem Sie den Webverweis hinzugefügt haben, erstellen Sie mit folgender Syntax eine Instanz der Proxyklasse:  
  
```vb  
Dim rs As New myNamespace.myReferenceName.ReportExecutionService()  
rs.Url = "http://<Server Name>/reportserver/reportexecution2005.asmx?wsdl"  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
```  
  
```csharp  
myNamespace.myReferenceName.ReportExecutionService rs = new myNamespace.myReferenceName.ReportExecutionService();  
rs.Url = "http://<Server Name>/reportserver/reportexecution2005.asmx?wsdl"  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
```  
  
 Sie können auch hinzufügen eine **mit** (**Import** in [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) Richtlinie auf den Berichtsserver-Webdienst-Dienstverweis. Wenn Sie diese Direktive verwenden, müssen die Typen im Namespace nicht vollqualifiziert sein. Hierfür fügen Sie dieser Datei den folgenden Code hinzu:  
  
```vb  
Import myNamespace.myReferenceName  
```  
  
```csharp  
using myNamespace.myReferenceName;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Berichtsserver-Webdienst](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Erstellen von Anwendungen mit dem Webdienst und .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Technische Referenz &#40; SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  

