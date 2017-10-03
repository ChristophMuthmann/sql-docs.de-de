---
title: Installieren von Analysis Services | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 04/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cd6ac80d-b735-4e3e-a024-489f1409ad33
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 084223d83c3786610dbce145f27a4c18a6409769
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="install-sql-server-analysis-services"></a>Installieren von SQL Server Analysis Services
  SQL Server Analysis Services ist ein analytischer Datenbankserver, der hostet tabellarische Modelle, multidimensionale Cubes und Datamining-Modelle, die Sie über Berichte, Kalkulationstabellen und Dashboards zugreifen können.  
  
 Analysis Services ist mit mehreren Instanzen, was bedeutet, dass Sie die mehr als eine Kopie auf einem einzelnen Computer zu installieren oder neue und alte Versionen-Seite-an-Seite ausführen können. Jede von Ihnen installierte Instanz wird in einem von drei Modi entsprechend den Setupeinstellungen ausgeführt: „Mehrdimensional und Data Mining“, „Tabellarisch“ oder „SharePoint“. Wenn Sie mehrere Modi verwenden möchten, benötigen Sie für jeden Modus eine separate Instanz.  
  
 Nach der Installation des Servers in einem bestimmten Modus können Sie ihn zum Hosten von Projektmappen nutzen, die mit dem Modus kompatibel sind. Ein Server im tabellarischen Modus ist beispielsweise erforderlich, um den Zugriff auf Daten im tabellarischen Modell über das Netzwerk zu ermöglichen.  
  
## <a name="get-tools-and-designers"></a>Aufrufen von Tools und Designern  
 SQL Server-Setup ist nicht mehr für die Installation der Modell-Designer oder Management-Tools zuständig, mit denen Projektmappen entworfen oder Server verwaltet werden. In dieser Version werden Tools separat installiert, und zwar über die folgenden Links:  
  
-   [Herunterladen von SQL Server Management Studio (SSMS)](../../../ssms/download-sql-server-management-studio-ssms.md)  
  
-   [Herunterladen von SQL Server Data Tools (SSDT)](../../../ssdt/download-sql-server-data-tools-ssdt.md)  
  
 Sie benötigen sowohl SSMS und SSDT zum Arbeiten mit Analysis Services-Instanzen und Daten. Tools können überall installiert werden, aber Achten Sie darauf, dass Sie Ports auf dem Server zu konfigurieren, bevor Sie versuchen, eine Verbindung herzustellen. Siehe [Konfigurieren der Windows-Firewall, um den Zugriff auf Analysis Services zuzulassen](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) .  
  
## <a name="install-using-a-wizard"></a>Installieren mithilfe eines Assistenten  
 Die folgende Liste enthält die Seiten im SQL Server-Installations-Assistenten, die zum Installieren von Analysis Services verwendet werden:  
  
1.  Wählen Sie in der Funktionsstruktur des Setups **Analysis Services** aus.  
  
     ![Setup-Funktionsstruktur mit Funktionsstruktur Services](../../../analysis-services/instances/install-windows/media/ssas-setupas.gif "Setup-Funktionsstruktur Funktionsstruktur Dienste anzeigen")  
  
2.  Wählen Sie einen Modus, auf der Seite "Analysis Services-Konfiguration". Im tabellarischer Modus ist die Standardeinstellung...  
  
     ![Setupseite mit Analysis Services-Konfigurationsoptionen](../../../analysis-services/instances/install-windows/media/ssas-setupasconfig.png "Setupseite mit Analysis Services-Konfigurationsoptionen")  
  
  Der tabellarische Modus verwendet das xVelocity in-Memory-Modul (VertiPaq), das ist der Standardspeicher für tabellarische Modelle. Nach dem Sie tabellarische Modelle auf dem Server bereitstellen, können Sie selektiv tabellarische Projektmappen Verwendung von DirectQuery-Festplattenspeicher als Alternative zu arbeitsspeichergebundenem Speicher konfigurieren.  
 
 Mehrdimensionale und Data Mining-Modus verwendet MOLAP als Standardspeicher für Modelle in Analysis Services bereitgestellt. Nach der Bereitstellung auf dem Server können Sie eine Projektmappe für die Verwendung von ROLAP konfigurieren, wenn Abfragen direkt gegen die relationale Datenbank ausgeführt werden sollen, anstatt Abfragedaten in eine mehrdimensionalen Analysis Services-Datenbank zu speichern.  
  

  
 Die Verwaltung des Arbeitsspeichers und E/A-Einstellungen können angepasst werden, um eine bessere Leistung zu erzielen, wenn Sie nicht standardmäßige Speichermodi verwenden. Weitere Informationen finden Sie unter [Server Properties in Analysis Services](../../../analysis-services/server-properties/server-properties-in-analysis-services.md) (Servereigenschaften in Analysis Services).  
  
## <a name="command-line-setup"></a>Befehlszeilensetup  
 Das SQL Server-Setup enthält einen Parameter (**ASSERVERMODE**), der den Servermodus angibt. Das folgende Beispiel zeigt ein Befehlszeilensetup, bei dem Analysis Services im tabellarischen Servermodus installiert wird.  
  
```  
  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /FEATURES=AS /ASSERVERMODE=TABULAR /INSTANCENAME=ASTabular /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 **INSTANCENAME** muss weniger als 17 Zeichen enthalten.  
  
 Alle Platzhalterkontowerte müssen durch gültige Konten und Kennwörter ersetzt werden.  
  
 Bei**ASSERVERMODE** wird die Groß- und Kleinschreibung berücksichtigt.  Alle Werte müssen in Großbuchstaben angegeben werden. In der folgenden Tabelle werden die gültigen Werte für **ASSERVERMODE**beschrieben.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|TABULAR|Dies ist der Standardwert. Wenn Sie nicht festlegen **ASSERVERMODE**, der Server im tabellarischen Modus installiert ist.|
|MULTIDIMENSIONAL|Dieser Wert ist optional.|  
|POWERPIVOT|Dieser Wert ist optional. Wenn Sie den **ROLE** -Parameter festlegen, wird der Servermodus automatisch auf 1 festgelegt. Hierdurch wird **ASSERVERMODE** optional für eine [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint-Installation. Weitere Informationen finden Sie unter [Installieren von Power Pivot über die Eingabeaufforderung](http://msdn.microsoft.com/en-us/7f1f2b28-c9f5-49ad-934b-02f2fa6b9328).|  
  
  
## <a name="see-also"></a>Siehe auch  
 [Bestimmen des Servermodus einer Analysis Services-Instanz](../../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Tabellenmodellierung (SSAS – tabellarisch)](https://msdn.microsoft.com/library/hh212945(v=sql.110).aspx)  
  
  

