---
title: "Beispiele für URLs für Elemente auf einem Berichtsserver - SharePoint-Modus | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 54cb861a-8cec-445c-875d-599fb9bd1973
caps.latest.revision: 5
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 53c07f85e9ec0bfca627b8ff941eddfde03336df
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="url-examples-for-items-on-a-report-server---sharepoint-mode"></a>Beispiele für URLs für Elemente auf einem Berichtsserver - SharePoint-Modus
  Wenn Sie Berichte und verwandte Elemente in einer SharePoint-Bibliothek veröffentlichen möchten, können Sie den Inhalt mithilfe der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Erstellungstools, wie dem Berichts-Designer, veröffentlichen oder den Inhalt mithilfe von SharePoint-Websiteaktionen hochladen.  
  
 Im einheitlichen Modus werden für SharePoint-Websites andere Webadressen als für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver verwendet. SharePoint-Websitehierarchien enthalten die SharePoint-Webanwendung, eine Stammwebsite, optionale Unterwebsites und Bibliotheken. Ihnen muss das Verfahren zum Erstellen einer URL-Adresse bekannt sein, die den SharePoint-Server sowie den Speicherort in der SharePoint-Websitehierarchie angibt, an dem Sie einen Bericht oder verknüpfte Elemente veröffentlichen möchten.  
  
 Zu einem Bericht gehörende Elemente umfassen u. a. freigegebene Datenquellen, Unterberichte, Drillthroughberichten und Ressourcen wie webbasierte Bilddateien. In einem Bericht, der in einer SharePoint-Bibliothek veröffentlicht wurde, müssen diese zugehörigen Elemente mit ihrem Speicherort in der SharePoint-Bibliothek angegeben werden.  
  
 Die Beispiele in diesem Thema helfen Ihnen, URLs zu Berichten und verwandten Elementen in den Berichtslösungen zu erstellen.  
  
## <a name="site-hierarchy"></a>Websitehierarchie  
 Wenn Sie einen Berichtsserver so konfigurieren, dass er im integrierten SharePoint-Modus ausgeführt wird, wird die SharePoint-Webhierarchie zum Adressieren von Elementen verwendet, die auf einem Berichtsserver verarbeitet und verwaltet werden.  
  
 Die folgenden Elemente der Webhierarchie können zum Zugreifen auf und Sichern von Berichtsserverinhalten verwendet werden. Andere Objekte wie Listen und Seiten werden für den Zugriff auf Berichtsserverinhalte nicht verwendet und daher in der folgenden Tabelle nicht beschrieben.  
  
|Objekt|Description|  
|------------|-----------------|  
|SharePoint-Webanwendung|Eine SharePoint-Webanwendung kann als eigenständiger Server oder als Teil einer Farm installiert werden, die eine Auflistung von virtuellen Servern enthält. Eine Webanwendung besitzt eine URL (z. B. `http:*//servername*`) und kann mehrere Websites enthalten.|  
|Website|Bei einer Website handelt es sich entweder um eine übergeordnete Website für eine Webanwendung oder um eine Unterwebsite.|  
|SharePoint-Bibliothek|Eine Bibliothek enthält Dokumente oder Ordner. Eine Bibliothek bzw. ein Ordner in einer Bibliothek stellt das einzige Websiteobjekt dar, in dem Berichte, Berichtsmodelle, freigegebene Datenquellen und externe Bilder gespeichert werden können.|  
|Element|Berichtsserverelemente, auf die Sie in einer URL verweisen können, enthalten eine Berichtsdefinition für einen Bericht oder Unterbericht, ein Berichtsmodell, eine freigegebene Datenquelle oder ein externes Bild.|  
  
## <a name="url-syntax-and-rules"></a>URL-Syntax und -Regeln  
 Jedes Berichtsserverelement in einer Bibliothek wird durch eine vollqualifizierte URL identifiziert, die ein Protokollpräfix, einen Servernamen, eine Website, eine Bibliothek, einen Dateinamen und eine Dateinamenerweiterung für den Dateityp enthält.  
  
### <a name="url-for-a-sharepoint-server"></a>URL für einen SharePoint-Server  
 Wenn Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ein Berichtsserver- oder Berichtsmodellprojekt für den Berichtsserver bereitstellen, müssen Sie eine URL für den SharePoint-Server verwenden.  
  
 Öffnen Sie zum Suchen des zu verwendenden Servernamens einen Browser, und suchen Sie die SharePoint-Bibliothek, in der Sie einen Bericht veröffentlichen möchten. Der Servername wird z. B. sofort nach dem Protokollpräfix angezeigt `http:*//servername*`.  
  
 Die Verwendung des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -URL-Proxyendpunkts wird nicht unterstützt. Ein Proxyendpunkt enthält eine Portnummer, z. B. `http:*//servername:8080/reportserver*`.  
  
### <a name="url-for-a-sharepoint-server-site-or-subsite"></a>URL für eine SharePoint-Serverwebsite oder -Unterwebsite  
 Wenn Sie einen Bericht oder eine Berichtsdatenquelle bereitstellen, müssen Sie eine URL zu einer SharePoint-Website und ggf. -Unterwebsite verwenden. In der URL der Namen der Website wird unmittelbar nach dem Server, z. B. `http://*servername/site*` oder `http://*servername/site/subsite*`.  
  
 In einer [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007- oder [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] -Webanwendung entsprechen die Website und die Unterwebsite häufig den Registerkarten auf der Hauptwebsite. Klicken Sie zum Suchen des Website- oder Unterwebsitenamens auf **Homepage**und anschließend auf **Gesamter Websiteinhalt**. Führen Sie einen Bildlauf ganz nach unten durch, und suchen Sie nach **Websites und Arbeitsbereiche**. Im folgenden Abschnitt sind die Websites aufgeführt.  
  
### <a name="url-for-a-sharepoint-library"></a>URL für eine SharePoint-Bibliothek  
 Wenn Sie einen Bericht oder ein verknüpftes Element in einer SharePoint-Bibliothek bereitstellen, müssen Sie eine URL zur SharePoint-Bibliothek verwenden. Die URL für eine Bibliothek unterscheidet sich je nach verwendeter SharePoint-Version.  
  
 Auf [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 oder [!INCLUDE[SPF2010](../../includes/spf2010-md.md)], die Bibliothek z. B. nach dem Servernamen angezeigt `http://*servername/*Shared Documents`.  
  
 In [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007 oder [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]wird die Bibliothek nach der Website und der Unterwebsite angezeigt. Beispiel: `http://*servername/site/*Documents`.  
  
 Öffnen Sie zum Suchen der Pfadinformationen für eine neue SharePoint-Bibliothek oder für eine unbekannte Website einen Browser, und suchen Sie die SharePoint-Bibliothek, in der Sie die Berichte veröffentlichen möchten. Wenn die Bibliothek leer ist, laden Sie eine beliebige Datei hoch. Klicken Sie mit der rechten Maustaste auf die Datei, und wählen Sie **Eigenschaften** aus, um das Fenster **Eigenschaften** zu öffnen. Die Adresse der Datei enthält die URL-Werte, die Sie für einen Veröffentlichungsvorgang benötigen.  
  
### <a name="fully-qualified-urls-for-items-on-a-sharepoint-site"></a>Vollqualifizierte URLs für Elemente auf einer SharePoint-Website  
 Elemente, die in einer SharePoint-Bibliothek gespeichert sind, werden stets über eine vollqualifizierte URL, die mit der Web-Anwendung startet adressiert (`http://*server*`) als Stammknoten, und endet mit dem Namen der Datei, die Sie verweisen.  
  
 Dateinamen in der URL müssen eine Dateinamenerweiterung aufweisen.  
  
 In Berichten, die Sie auf einer SharePoint-Website veröffentlichen, können Sie für abhängige Elemente keine relativen URLs verwenden. Beispielsweise können Sie keine relative URL verwenden, um auf eine freigegebene Datenquelle, auf ein Berichtsmodell oder auf einen Unterbericht zu verweisen. Sie müssen für jedes Element stets die vollqualifizierte URL zu einer SharePoint-Bibliothek angeben. Es kann nicht vorhergesagt werden, wo sich eine abhängige Datei befindet, da keine vordefinierte Hierarchie für die Websites zur Verfügung steht, die Sie zum Analysieren eines URL-Formats verwenden können.  
  
 Wenn Sie einen Bericht veröffentlichen oder hochladen, der abhängige Elemente enthält, müssen Sie die Verweise auf die abhängigen Elemente nach der Veröffentlichung des Berichts festlegen. Verweise, die im Vorschaumodus im Berichts-Designer wie vorgesehen verwendet werden konnten, sind nach der Veröffentlichung des Berichts nicht notwendigerweise auch funktionsfähig. Weitere Informationen finden Sie unter [Veröffentlichen in einer SharePoint-Bibliothek über ein Erstellungstool](#publishingToDocLib) in diesem Thema.  
  
### <a name="urls-for-external-images"></a>URLs für externe Bilder  
 Eine Berichtsdefinition kann eine Bilddatei enthalten, die als externe Datei gespeichert ist. Sie können in der Berichtsdefinition auf diese Datei verweisen, indem Sie eine vollqualifizierte URL für die Bilddatei festlegen. Er kann auf einer SharePoint-Website oder auf einem Remotecomputer gespeichert sein.  
  
> [!IMPORTANT]  
>  Falls die externe URL auf ein Bild auf einer SharePoint-Website verweist, wird das Symbol für beschädigte Bilder angezeigt, wenn Sie den Bericht im Berichts-Generator in der Vorschau anzeigen. Wenn Sie den Bericht auf die SharePoint-Website hochladen und im verbundenen Modus rendern, wird das Symbol für beschädigte Bilder eingeblendet, wenn Sie lediglich über die Berechtigung **View Items** verfügen.  
  
 Unabhängig vom Berichtsservermodus muss es sich in einem Bericht bei Verweisen auf eine externe Bilddatei um eine vollqualifizierte URL handeln. Zudem ist es für Verweise auf eine externe Bilddatei im Allgemeinen erforderlich, dass Sie das Konto für die unbeaufsichtigte Berichtsverarbeitung konfigurieren.  
  
### <a name="specifying-subreports-and-drillthrough-reports"></a>Angeben von Unterberichten und Drillthroughberichten  
 Unterberichte müssen sich im gleichen Ordner wie der Hauptbericht befinden. Sie können keinen relativen Ordner angeben.  
  
 Schließen Sie zum Angeben von Drillthroughberichten die URL in einem Ausdruck ein. Wenn Sie z. B. den Bericht SalesDetails als Drillthroughbericht angeben möchten, legen Sie in der Aktion für das Textfeld oder den Platzhaltertext ReportName auf den folgenden Wert fest:  
  
```  
="http://site/subsite/documentlibrary/SalesDetails.rdl"  
```  
  
### <a name="reserved-names-on-sharepoint-sites"></a>Reservierte Namen auf SharePoint-Websites  
 Wenn Sie eine URL für ein Element erstellen oder konstruieren, das sich auf einer SharePoint-Website befindet, ist zu beachten, dass die Wörter **Persönlich** und **Websites** unter der Standardwebsite reservierte Namen darstellen.  
  
## <a name="examples-of-urls"></a>Beispiele für URLs  
 Wenn Sie Elemente in einer SharePoint-Bibliothek veröffentlichen, müssen Sie vollqualifizierte URLs zur Zielbibliothek angeben. Eine vollqualifizierte SharePoint-URL enthält die SharePoint-Webanwendung, die Website, die Bibliothek, den Ordner (optional), die Datei sowie die Dateinamenerweiterung. In den folgenden Beispielen wird die zu verwendende Syntax veranschaulicht.  
  
|Ziel|Beispiel-URL|  
|------------|-----------------|  
|Ein SharePoint-Server.|`http://TestServer`|  
|Eine SharePoint-Serverwebsite oder -Unterwebsite.|`http://TestServer/toplevelsite/subsite`|  
|Der Beispielbericht **Company Sales** unter Shared Documents [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] in einer [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] - oder -Bereitstellung.|`http://TestServer/TestSite/Shared%20Documents/Company%20Sales.rdl`|  
|Der Beispielbericht „Company Sales“ im Ordner **Documents/Doc** einer [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] - oder [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] -Instanz.|`http://TestServer/TestSite/Documents/Doc/Company%20Sales.rdl`|  
|Der Beispielbericht "Company Sales" im Ordner **Report Center** einer [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] - oder [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] -Instanz.|`http://TestServer/TestSite/Reports/Doc/Company%20Sales.rdl`|  
  
##  <a name="publishingToDocLib"></a> Veröffentlichen in einer SharePoint-Bibliothek über ein Erstellungstool  
 Wenn Sie ein Berichterstellungstool zum Veröffentlichen von Berichten und zugehörigen Dateien in einer Bibliothek verwenden, werden die Dateien überprüft, bevor sie hinzugefügt werden. Wenn Sie Berichte und zugehörige Dateien mithilfe der **Upload** -Aktion in einer SharePoint-Bibliothek hochladen, erfolgt keine Überprüfung. Sie wissen erst, ob die Datei gültig ist, wenn Sie den Bericht verwalten, bearbeiten oder ausführen und somit auf ihn zugreifen.  
  
> [!NOTE]  
>  Damit Sie Berichte aus [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf einer SharePoint-Website veröffentlichen können, müssen Sie die SharePoint-Website möglicherweise der Liste der vertrauenswürdigen Speicherorte im Internet Explorer-Browser hinzufügen.  
  
### <a name="shared-data-sources"></a>Freigegebene Datenquellen  
 Wenn Sie eine freigegebene Datenquelle in einem Berichterstellungstool veröffentlichen, legen Sie die **TargetDataSourceFolder**-Projekteigenschaft fest. Der Ordner für die Zieldatenquelle muss eine URL zu einer SharePoint-Bibliothek darstellen. Anders als im einheitlichen Modus von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] können Sie keinen relativen Ordner angeben. Relative Pfade sind ungültig. Wenn unter dem Pfad der Dokumentbibliothek kein Ordner vorhanden ist, wird einer erstellt.  
  
 Wenn Sie eine freigegebene Datenquellendatei (RDS-Datei) auf einer SharePoint-Website veröffentlichen, wird der Datenquellendatei die Dateinamenerweiterung RSDS zugewiesen. Die RSDS-Datei kann nicht lokal auf einer SharePoint-Website gespeichert und in ein vorhandenes [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Projekt importiert werden. Freigegebene Datenquellen mit den Dateinamenerweiterungen RDS und RSDS können nicht ausgetauscht werden.  
  
#### <a name="shared-data-sources-from-report-designer"></a>Freigegebene Datenquellen im Berichts-Designer  
 Wenn Sie freigegebene Datenquellen in einem Berichts-Designer-Projekt veröffentlichen, können Sie eine URL verwenden, die die Zielbibliothek angibt, oder die Eigenschaft leer lassen. Anders als im einheitlichen Modus von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] können Sie keinen relativen Ordner angeben. Relative Pfade sind ungültig. Wenn unter dem Pfad der Dokumentbibliothek kein Ordner vorhanden ist, wird einer erstellt. Wenn Sie den Ordner für die Zieldatenquelle leer lassen, wird die Datenquelle im Zielberichtsordner veröffentlicht.  
  
### <a name="file-names"></a>Dateinamen  
 Dateinamen in einer URL für Berichtselemente müssen eine Dateinamenerweiterung aufweisen. Durch die Dateinamenerweiterung wird der Dateityp bestimmt. Wenn Sie Berichtselemente über ein Berichterstellungstool veröffentlichen, wird die Dateinamenerweiterung automatisch eingeschlossen. Wenn Sie ein Berichtselement in eine SharePoint-Bibliothek hochladen, müssen Sie eine Dateinamenerweiterung einschließen.  
  
 Wenn Sie für Elemente, die Sie auf eine SharePoint-Website hochladen, keine Dateinamenerweiterung angeben, tritt der **rsInvalidDataSourceReference** -Fehler auf. Dateinamen dürfen keine Zeichen enthalten, die von SharePoint-Anwendungen nicht als gültige Dateinamenzeichen erkannt werden. Verwenden Sie keines der folgenden Zeichen: # % & * : < > ? / { | }.  
  
## <a name="differences-between-uploading-and-publishing"></a>Unterschiede zwischen Hochladen und Veröffentlichen  
 Wenn Sie den Berichts-Designer oder den Berichts-Generator zum Veröffentlichen von Berichten und zugehörigen Dateien in einer Bibliothek verwenden, werden die Dateien überprüft, bevor sie hinzugefügt werden. Wenn Sie Berichte und zugehörige Dateien mithilfe der **Upload** -Aktion in einer SharePoint-Bibliothek hochladen, erfolgt keine Überprüfung. Sie wissen erst, ob die Datei gültig ist, wenn Sie den Bericht verwalten, bearbeiten oder ausführen und somit auf ihn zugreifen.  
  
## <a name="updating-a-published-item"></a>Aktualisieren eines veröffentlichten Elements  
 Nachdem Sie ein Element in einer SharePoint-Bibliothek veröffentlicht oder hochgeladen haben, müssen Sie das Element aus der Bibliothek auschecken, bevor Sie es aktualisieren. Wenn der Bericht für Sie ausgecheckt wird, sind Sie der einzige Benutzer, der berechtigt ist, Änderungen am Bericht vorzunehmen. Checken Sie den Bericht wieder ein, wenn Sie den Vorgang abgeschlossen haben.  
  
 Wenn Sie einen Bericht hochladen oder veröffentlichen, ohne das Dokument vorher auszuchecken (z. B. indem Sie ein Element hochladen, das den gleichen Namen wie ein vorhandenes Element aufweist), wird das Dokument vom Berichtsserver ausgecheckt, der aktualisierte Bericht als neue Version des vorhandenen Elements hinzugefügt, und anschließend wird das Dokument erneut eingecheckt.  
  
## <a name="external-images-as-resources"></a>Externe Bilder als Ressourcen  
 Ein Berichtsserver, der im einheitlichen Modus ausgeführt wird, unterstützt das Konzept einer Ressource, die als eine Datei definiert ist, die auf dem Berichtsserver gespeichert und gesichert wird, die jedoch nicht vom Berichtsserver verarbeitet wird. Im einheitlichen Modus kann es sich dabei um einen beliebigen Dateityp handeln.  
  
 Wenn ein Berichtsserver im integrierten SharePoint-Modus ausgeführt wird, gilt für das Konzept einer Ressource eine engere Definition. Für den Berichtsserver wird das Konzept einer Ressource zum Speichern von Berichten beibehalten, die auf ein externes Bild verweisen. Dies gilt, wenn der Bericht eine Momentaufnahme oder eine Kopie darstellt, der bzw. die für die interne Verwendung beibehalten wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Veröffentlichen eines Berichts in einer SharePoint-Bibliothek](../../reporting-services/reports/publish-a-report-to-a-sharepoint-library.md)   
 [Veröffentlichen Sie eine freigegebene Datenquelle in einer SharePoint-Bibliothek](../../reporting-services/reports/publish-a-shared-data-source-to-a-sharepoint-library.md)   
 [Dialogfeld Projekt-Eigenschaftenseiten](../../reporting-services/tools/project-property-pages-dialog-box.md)  
  
  

