---
title: "Installieren von Analysis Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cd6ac80d-b735-4e3e-a024-489f1409ad33
caps.latest.revision: 20
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 19
---
# Installieren von Analysis Services
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ist ein analytischer Datenbankserver, der tabellarische Modelle, multidimensionale Cubes und Data Mining-Modelle hostet, auf die Sie über Berichte, Tabellenkalkulationen und Dashboards zugreifen können.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] besitzt mehrere Instanzen. Das bedeutet, dass Sie mehr als eine Kopie von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] auf einem einzelnen Computer installieren oder eine alte und eine neue Version parallel ausführen können. Jede von Ihnen installierte Instanz wird in einem von drei Modi entsprechend den Setupeinstellungen ausgeführt: „Mehrdimensional und Data Mining“, „Tabellarisch“ oder „SharePoint“. Wenn Sie mehrere Modi verwenden möchten, benötigen Sie für jeden Modus eine separate Instanz.  
  
 Nach der Installation des Servers in einem bestimmten Modus können Sie ihn zum Hosten von Projektmappen nutzen, die mit dem Modus kompatibel sind. Ein Server im tabellarischen Modus ist beispielsweise erforderlich, um den Zugriff auf Daten im tabellarischen Modell über das Netzwerk zu ermöglichen.  
  
## Aufrufen von Tools und Designern  
 SQL Server-Setup ist nicht mehr für die Installation der Modell-Designer oder Management-Tools zuständig, mit denen Projektmappen entworfen oder Server verwaltet werden. In dieser Version werden Tools separat installiert, und zwar über die folgenden Links:  
  
-   [Herunterladen von SQL Server Management Studio für SQL Server 2016](https://msdn.microsoft.com/en-US/library/mt238290.aspx)  
  
-   [Herunterladen von SQL Server Data Tools für SQL Server 2016](https://msdn.microsoft.com/en-US/library/mt204009.aspx)  
  
 Sie benötigen sowohl Management Studio als auch SQL Server Data Tools zum Arbeiten mit Analysis Services-Instanzen und -Daten. Tools können überall installiert werden. Sie sollten allerdings darauf achten, die Ports auf dem Server zu konfigurieren, bevor Sie versuchen, eine Verbindung herzustellen. Siehe [Konfigurieren der Windows-Firewall, um den Zugriff auf Analysis Services zuzulassen](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
## Installieren mithilfe eines Assistenten  
 Die folgende Liste enthält die Seiten im SQL Server-Installations-Assistenten, die zum Installieren von Analysis Services verwendet werden:  
  
1.  Wählen Sie in der Funktionsstruktur des Setups **Analysis Services** aus.  
  
     ![Setup feature tree showing Analsyis Services](../../../analysis-services/instances/install-windows/media/ssas-setupas.gif "Setup feature tree showing Analsyis Services")  
  
2.  Achten Sie darauf, dass Sie auf der Analysis Services-Konfigurationsseite die Option **Tabellarischer Modus** auswählen, wenn Sie eine tabellarische Instanz wünschen. Andernfalls ist der Standardwert **Mehrdimensionaler und Data Mining-Modus**.  
  
     ![Setup page with Analysis Services config options](../../../analysis-services/instances/install-windows/media/ssas-setupasconfig.png "Setup page with Analysis Services config options")  
  
 Der mehrdimensionale und Data Mining-Modus verwendet MOLAP als Standardspeicher für die in Analysis Services bereitgestellten Modelle. Nach der Bereitstellung auf dem Server können Sie eine Projektmappe für die Verwendung von ROLAP konfigurieren, wenn Abfragen direkt gegen die relationale Datenbank ausgeführt werden sollen, anstatt Abfragedaten in eine mehrdimensionalen Analysis Services-Datenbank zu speichern.  
  
 Der tabellarische Modus verwendet das xVelocity-Modul für Datenanalyse im Arbeitsspeicher (VertiPaq). Dies ist der Standardspeicher für tabellarische Modelle, die Sie in Analysis Services bereitstellen. Nachdem Sie Projektmappen mit einem tabellarischen Modell auf dem Server bereitgestellt haben, können Sie selektiv tabellarische Projektmappen konfigurieren, um DirectQuery-Festplattenspeicher als Alternative zu arbeitsspeichergebundenem Speicher zu verwenden.  
  
 Die Verwaltung des Arbeitsspeichers und E/A-Einstellungen können angepasst werden, um eine bessere Leistung zu erzielen, wenn Sie nicht standardmäßige Speichermodi verwenden. Weitere Informationen finden Sie unter [Server Properties in Analysis Services](../../../analysis-services/server-properties/server-properties-in-analysis-services.md) (Servereigenschaften in Analysis Services).  
  
## Befehlszeilensetup  
 Das SQL Server-Setup enthält einen Parameter (**ASSERVERMODE**), der den Servermodus angibt. Das folgende Beispiel zeigt ein Befehlszeilensetup, bei dem Analysis Services im tabellarischen Servermodus installiert wird.  
  
```  
  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /FEATURES=AS /ASSERVERMODE=TABULAR /INSTANCENAME=ASTabular /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 **INSTANCENAME** muss weniger als 17 Zeichen enthalten.  
  
 Alle Platzhalterkontowerte müssen durch gültige Konten und Kennwörter ersetzt werden.  
  
 Bei **ASSERVERMODE** wird die Groß- und Kleinschreibung berücksichtigt.  Alle Werte müssen in Großbuchstaben angegeben werden. In der folgenden Tabelle werden die gültigen Werte für **ASSERVERMODE** beschrieben.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|MULTIDIMENSIONAL|Dies ist der Standardwert. Wenn Sie **ASSERVERMODE** nicht festlegen, wird der Server im multidimensionalen Servermodus installiert.|  
|POWERPIVOT|Dieser Wert ist optional. Wenn Sie den **ROLE**-Parameter festlegen, wird der Servermodus automatisch auf 1 festgelegt. Hierdurch wird **ASSERVERMODE** optional für eine [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint-Installation. Weitere Informationen finden Sie unter [Installieren von Power Pivot über die Eingabeaufforderung](http://msdn.microsoft.com/de-de/7f1f2b28-c9f5-49ad-934b-02f2fa6b9328).|  
|TABULAR|Dieser Wert ist erforderlich, wenn Sie Analysis Services mit einem Befehlszeilensetup im tabellarischen Modus installieren.|  
  
## Siehe auch  
 [Bestimmen des Servermodus einer Analysis Services-Instanz](../../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Convert an in-memory Tabular Database to DirectQuery in SQL Server Management Studio &#40;SSMS&#41; (Konvertieren einer tabellarischen Datenbank im Arbeitsspeicher in DirectQuery in SQL Server Management Studio [SSMS])](../Topic/Convert%20an%20in-memory%20Tabular%20Database%20to%20DirectQuery%20in%20SQL%20Server%20Management%20Studio%20\(SSMS\).md)   
 [Tabellarische Modellierung &#40;SSAS – tabellarisch&#41;](../Topic/Tabular%20Modeling%20\(SSAS\).md)  
  
  