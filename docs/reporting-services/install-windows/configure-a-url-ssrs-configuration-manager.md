---
title: Konfigurieren einer URL (SSRS-Konfigurations-Manager) | Microsoft Docs
ms.custom: 
ms.date: 05/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- URL access [Reporting Services], syntax
ms.assetid: 851e163a-ad2a-491e-bc1e-4df92327092f
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 99c21c41115748c82267ed72845607b044ee3a6a
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="configure-a-url--ssrs-configuration-manager"></a>Konfigurieren einer URL (SSRS-Konfigurations-Manager)
  Bevor Sie das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] oder den Berichtsserver-Webdienst verwenden können, müssen Sie mindestens eine URL für jede Anwendung konfigurieren. Die Konfiguration der URLs ist obligatorisch, wenn Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im Modus zur ausschließlichen Installation von Dateien installiert haben (also durch Auswahl der Option **Server installieren, jedoch nicht konfigurieren** auf der Seite mit den Berichtsserver-Installationsoptionen im Installations-Assistenten). Wenn Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in der Standardkonfiguration installiert haben, sind die URLs bereits für jede Anwendung konfiguriert.  
  
 Verwenden Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool zur Konfiguration der URLs: Alle Teile der URL werden in diesem Tool definiert. Im Gegensatz zu früheren Versionen bieten die Websites des Internetinformationsdienste-Managers (IIS) keinen Zugriff mehr auf [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Anwendungen in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höheren Versionen.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] bietet Standardwerte, die in den meisten Bereitstellungszenarien gut funktionieren, einschließlich parallelen Bereitstellungen mit anderen Webdiensten und -anwendungen. Standard-URLs beinhalten Instanznamen, wodurch das Risiko von URL-Konflikten bei Ausführung mehrerer Berichtsserverinstanzen auf demselben Computer minimiert wird.  
  
 Dieses Thema enthält Anweisungen für die folgenden Aufgaben:  
  
-   Erstellen Sie eine URL für den Report Server-Webdienst.  
  
-   Erstellen Sie eine URL für das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)].  
  
-   Legen Sie erweiterte URL-Eigenschaften fest, um zusätzliche URLs zu definieren.  
  
 Weitere Informationen zum Speichern und Verwalten von URLs sowie zu Interoperabilitätsproblemen finden Sie unter [Informationen zu URL-Reservierungen und Registrierungen &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md) und [Gleichzeitiges Installieren von Reporting Services und Internetinformationsdiensten &#40;einheitlicher SSRS-Modus&#41;](../../reporting-services/install-windows/install-reporting-and-internet-information-services-side-by-side.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation. Beispiele für URLs, die häufig in Reporting Services-Installationen verwendet werden, finden Sie unter [Beispiele für URLs](#URLExamples) in diesem Thema.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 Bevor Sie eine URL erstellen oder ändern, beachten Sie folgende Punkte:  
  
-   Sie müssen ein Mitglied der lokalen Administratorengruppe auf dem Berichtsservercomputer sein.  
  
-   Wenn die Internetinformationsdienste (IIS) auf demselben Computer installiert sind, müssen Sie die Namen der virtuellen Verzeichnisse auf jeder Website überprüfen, die Port 80 verwendet. Wenn virtuelle Verzeichnisse angezeigt werden, die die Reporting Service-Standardnamen für virtuelle Verzeichnisse verwenden (also Reports und ReportServer), wählen Sie andere Namen für virtuelle Verzeichnisse für die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -URLs aus, die Sie konfigurieren.  
  
-   Zum Konfigurieren der URL müssen Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool neu starten. Verwenden Sie kein Systemhilfsprogramm. Ändern Sie niemals die URL-Reservierungen im Abschnitt **URLReservations** der Datei RSReportServer.config direkt. Die Verwendung des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstools ist zur Aktualisierung der zugrunde liegenden URL-Reservierung, die intern gespeichert wird, sowie zur Synchronisation der URL-Einstellungen, die in der Datei RSReportServer.config gespeichert werden.  
  
-   Wählen Sie eine Zeit mit niedriger Berichtsaktivität aus. Bei jeder Änderung der URL-Reservierung können Sie davon ausgehen, dass die Anwendungsdomänen für den Report Server-Webdienst und das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] möglicherweise wiederverwendet werden.  
  
-   Eine Übersicht über die Erstellung und Verwendung von URLs in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]finden Sie unter [Konfigurieren von Berichtsserver-URLs &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md).  
  
### <a name="to-configure-a-url-for-the-report-server-web-service"></a>So konfigurieren Sie eine URL für den Report Server-Webdienst  
  
1.  Starten Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool, und stellen Sie eine Verbindung mit einer lokalen Berichtsserverinstanz her.  
  
2.  Klicken Sie auf **Webdienst-URL**.  
  
3.  Geben Sie das virtuelle Verzeichnis an. Der Name des virtuellen Verzeichnisses gibt an, welche Anwendung die Anforderung empfängt. Da eine IP-Adresse und ein Port von mehreren Anwendungen gemeinsam verwendet werden können, gibt der Name des virtuellen Verzeichnisses an, welche Anwendung die Anforderung erhält.  
  
     Dieser Wert muss eindeutig sein, um sicherzustellen, dass die Anforderung das beabsichtigte Ziel erreicht. Dieser Wert ist erforderlich. Dabei wird die Groß- und Kleinschreibung nicht berücksichtigt. Es gibt eine 1:1-Entsprechung zwischen dem Namen eines virtuellen Verzeichnisses und einer Instanz einer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Anwendung. Wenn Sie mehrere URLs zur selben Anwendungsinstanz erstellen, müssen Sie in allen URLs, die Sie für diese Anwendungsinstanz erstellen, denselben Namen für das virtuelle Verzeichnis verwenden.  
  
     Beim Report Server-Webdienst lautet der Standardname für das virtuelle Verzeichnis **reportserver**.  
  
4.  Geben Sie die IP-Adresse an, die den Berichtsservercomputer im Netzwerk eindeutig identifiziert. Wenn Sie einen Hostheader angeben oder weitere URLs für dieselbe Anwendungsinstanz definieren möchten, müssen Sie auf **Erweitert**klicken. Anweisungen zur Einrichtung erweiterter Eigenschaften für die URL finden Sie weiter unten in diesem Thema. Verwenden Sie andernfalls die Seite **Webdienst-URL** , um eine Auswahl aus folgenden Werten zu treffen:  
  
    -   Der Wert**Alle zugewiesenen** gibt an, dass alle IP-Adressen, die dem Computer zugewiesen sind, in einer URL verwendet werden können, die auf eine Berichtsserveranwendung verweist. Dieser Wert umfasst auch Host-Anzeigenamen (z. B. Computernamen), die durch einen Domänennamenserver in eine IP-Adresse aufgelöst werden können, die dem Computer zugewiesen ist. Dies ist der Standardwert für eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -URL.  
  
    -   Mit**Alle nicht zugewiesenen** wird angegeben, dass der Berichtsserver alle Anforderungen erhält, die nicht von einer anderen Anwendung bearbeitet werden. Sie sollten diese Option vermeiden. Wenn Sie diese Option auswählen, kann eine andere Anwendung, die eine stärkere URL-Reservierung aufweist, Anforderungen abfangen, die für den Berichtsserver gedacht waren.  
  
    -   **127.0.0.1** ist die für den Zugriff auf localhost verwendete IPv4-Adresse. Sie unterstützt die lokale Verwaltung auf dem Berichtsservercomputer. Wenn Sie nur diesen Wert auswählen, haben nur Benutzer, die lokal auf dem Berichtsservercomputer angemeldet sind, Zugriff auf die Anwendung.  
  
    -   **::1** ist die Loopback-Adresse im IPv6-Format.  
  
    -   Bestimmte IP-Adressen werden ebenfalls in dieser Liste angezeigt. IP-Adressen können in den Formaten IPv4 und IPv6 vorliegen *Nnn.nnn.nnn.nnn* ist die 32-Bit-IPv4-Adresse einer Netzwerkadapterkarte auf dem Computer. IPv6-Adressen sind 128-Bit, mit acht durch Doppelpunkte getrennten 4-Byte-Feldern: \<Präfix >:*Nnnn:nnnn:nnnn:nnnn:nnnn:nnnn*  
  
         Wenn Sie über mehrere Karten verfügen oder wenn Ihr Netzwerk sowohl IPv4- als auch IPv6-Adressen unterstützt, werden Ihnen mehrere IP-Adressen angezeigt. Wenn Sie nur eine einzige IP-Adresse auswählen, wird der Anwendungszugriff auf genau diese IP-Adresse (und jeden Hostnamen, den ein Domänennamenserver dieser Adresse zuordnet) beschränkt. Sie können localhost nicht für den Zugriff auf einen Berichtsserver verwenden, und Sie können nicht die IP-Adressen anderer Netzwerkadapterkarten verwenden, die auf den Berichtsservercomputer installiert sind. Normalerweise wählen Sie diesen Wert aus, weil Sie mehrere URL-Reservierungen konfigurieren, die auch explizite IP-Adressen oder Hostnamen angeben (z. B. einen für eine Netzwerkadapterkarte für Intranetverbindungen und einen zweiten für Extranetverbindungen).  
  
5.  Geben Sie den Port an. Port 80 ist der Standard, da er gemeinsam mit anderen Anwendungen genutzt werden kann. Wenn Sie eine benutzerdefinierte Portnummer verwenden möchten, müssen Sie sie immer in der URL angeben, die für den Zugriff auf den Berichtsserver verwendet wird. Mit folgenden Verfahren können Sie nach einem verfügbaren Port suchen:  
  
    -   Geben Sie an einer Eingabeaufforderung den folgenden Befehl ein, um eine Liste der verwendeten TCP-Anschlüsse auszugeben:  
  
         `netstat –anp tcp`  
  
    -   Im Microsoft-Support-Artikel [Informationen zur Zuweisung von TCP/IP-Ports](http://support.microsoft.com/kb/174904)finden Sie Informationen zur Zuweisung von TCP-Ports und zu den Unterschieden zwischen bekannten Ports (0 bis 1023), registrierten Ports (1024 bis 49151) und dynamischen bzw. privaten Ports (49152 bis 65535).  
  
    -   Bei Verwendung der Windows-Firewall müssen Sie den Port öffnen. Anweisungen finden Sie unter [Configure a Firewall for Report Server Access](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
6.  Wenn nicht bereits geschehen, überprüfen Sie, dass IIS (sofern installiert) kein virtuelles Verzeichnis besitzt, das den Namen trägt, den Sie verwenden möchten.  
  
7.  Wenn Sie ein SSL-Zertifikat installiert haben, können Sie es nun auswählen, um die URL an das SSL-Zertifikat zu binden, das auf Ihrem Computer installiert ist.  
  
8.  Optional können Sie bei Auswahl eines SSL-Zertifikats einen benutzerdefinierten Port angeben. Standardmäßig wird Port Nummer&nbsp;443 verwendet, aber Sie können jeden Port verwenden, der verfügbar ist.  
  
9. Klicken Sie auf **Anwenden** , um die URL zu erstellen.  
  
10. Testen Sie die URL, indem Sie auf den Link im Abschnitt **URLs** der Seite klicken. Beachten Sie, dass die Berichtsserver-Datenbank erstellt und konfiguriert werden muss, bevor Sie die URL testen können. Anweisungen finden Sie unter [Erstellen einer Berichtsserver-Datenbank im einheitlichen Modus &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  

> [!NOTE]  
>  Wenn Sie über vorhandene SSL-Bindungen und URL-Reservierungen verfügen und die SSL-Bindung ändern möchten, um z. B. ein anderes Zertifikat bzw. einen anderen Hostheader zu verwenden, wird empfohlen, die folgenden Schritte in der angegebenen Reihenfolge auszuführen:  
>   
>  1.  Entfernen Sie zuerst alle URL-Reservierungen.  
> 2.  Entfernen Sie anschließend alle SSL Bindungen.  
> 3.  Erstellen Sie die URLs und SSL-Bindungen anschließend neu.  
>   
>  Die vorangehenden Schritte können mit dem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurations-Manager ausgeführt werden.  
>   
>  Microsoft Windows unterstützt eine Bindung für jede Kombination aus IP-Adresse und Port. Wenn Sie einen Berichtsserver für die Verwendung eines bestimmten Hostheaderwerts konfigurieren und das Zertifikat für die Kombination aus Port und IP-Adresse ebenfalls in einen anderen Hostheaderwert ausgegeben wird, wird im Browser eine Warnung angezeigt, dass das Zertifikat nicht mit der verwendeten URL übereinstimmt.  
>   
>  Um den Fehler zu beheben, löschen Sie alle Bindungen und erstellen anschließend neue Bindungen mit eindeutigen Einstellungen oder konfigurieren die Registrierungen der Reporting Services-URLs mit Platzhaltern.
  
### <a name="to-create-a-url-reservation-for-the-includessrswebportalincludesssrswebportalmd"></a>So erstellen Sie eine URL-Reservierung für das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]  
  
1.  Starten Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool, und stellen Sie eine Verbindung mit der Berichtsserverinstanz her.  
  
2.  Klicken Sie auf **Webportal-URL**.  
  
3.  Geben Sie das virtuelle Verzeichnis an. Das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] lauscht auf derselben IP-Adresse und demselben Port wie der Berichtsserver-Webdienst. Wenn Sie das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] so konfiguriert haben, dass es auf einen anderen Berichtsserver-Webdienst verweist, müssen Sie die [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] -URL-Einstellungen in der Datei RSReportServer.config überprüfen.  
  
4.  Wenn Sie ein SSL-Zertifikat installiert haben, können Sie es auswählen, um festzulegen, dass alle Anforderungen an das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] über HTTPS geleitet werden.  
  
     Optional können Sie bei Auswahl eines SSL-Zertifikats einen benutzerdefinierten Port angeben. Standardmäßig wird Port Nummer&nbsp;443 verwendet, aber Sie können jeden Port verwenden, der verfügbar ist.  
  
5.  Klicken Sie auf **Anwenden** , um die URL zu erstellen.  
  
6.  Testen Sie die URL, indem Sie auf den Link im Abschnitt **URLs** der Seite klicken.  
  
## <a name="setting-advanced-properties-to-specify-additional-urls"></a>Festlegen der erweiterten Eigenschaften zur Angabe zusätzlicher URLs  
 Sie können mehrere URLs für den Berichtsserver-Webdienst oder das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] reservieren, indem Sie verschiedene Ports bzw. Hostnamen angeben (entweder eine IP-Adresse oder ein Hostheadernamen, den ein Domänennamenserver in eine IP-Adresse auflösen kann, die dem Computer zugewiesen ist). Indem Sie mehrere URLs erstellen, können Sie verschiedene Zugriffspfade zur gleichen Berichtsserverinstanz einrichten. Um beispielsweise Intranet- und Extranet-Zugriff auf einen Berichtsserver zu aktivieren, könnten Sie die Standard-URL für den Zugriff im gesamten Intranet und einen weiteren vollqualifizierten Hostnamen für Extranetzugriff verwenden:  
  
-   `http://myserver01/reportserver`  
  
-   `http://www.adventure-works.com/reportserver`  
  
 Sie können nicht mehrere Namen für virtuelle Verzeichnisse für dieselbe Anwendungsinstanz festlegen. Jede [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Anwendungsinstanz wird genau einem Namen für virtuelle Verzeichnisse zugeordnet. Wenn mehrere Instanzen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] auf demselben Computer vorliegen, sollte der Name für das virtuelle Verzeichnis für eine Anwendung den Instanznamen beinhalten, um sicherzustellen, dass jede Anforderung ihr vorgesehenes Ziel erreicht.  
 
  **Hostheader**  
 Wenn Sie bereits einen Hostheader in einem Domänennamenserver definiert haben, der auf Ihrem Computer aufgelöst wird, können Sie diesen Hostheader in einer URL angeben, die Sie für den Zugriff auf den Berichtsserver konfigurieren.  
  
 Ein Hostheader ist ein eindeutiger Name, der es mehreren Websites erlaubt, dieselbe IP-Adresse und denselben Port zu verwenden. Hostheadernamen sind leichter zu behalten und einzugeben als IP-Adressen und Portnummern. Ein Beispiel für einen Hostheadernamen könnte www.adventure-works.com sein.  
  
 **SSL-Port**  
 Gibt den Port für SSL-Verbindungen an. Der Standardport für SSL ist 443.  
  
 **SSL-Zertifikat**  
 Gibt den Zertifikatsnamen eines SSL-Zertifikats an, das Sie auf diesem Computer installiert haben. Wenn das Zertifikat einem Platzhalter zugeordnet wird, können Sie es für eine Berichtsserververbindung verwenden.  
  
 Gibt den vollqualifizierten Namen des Computers an, für den das Zertifikat registriert ist. Der von Ihnen angegebene Namen muss mit dem Namen identisch sein, für den das Zertifikat registriert ist.  
  
 Um diese Option verwenden zu können, müssen Sie ein Zertifikat installiert haben. Sie müssen auch die UrlRoot-Konfigurationseinstellung in der Datei RSReportServer.config so ändern, dass der vollqualifizierte Name des Computers angegeben wird, für den das Zertifikat registriert ist. Weitere Informationen finden Sie unter [Konfigurieren von SSL-Verbindungen auf einem Berichtsserver im einheitlichen Modus](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
### <a name="to-set-advanced-properties-on-a-url"></a>So legen Sie erweiterte Eigenschaften für eine URL fest  
  
1.  Klicken Sie auf der Seite **Webdienst-URL** oder **Webportal-URL** auf **Erweitert**.  
  
2.  Klicken Sie auf **Hinzufügen**.  
  
3.  Klicken Sie auf IP-Adresse oder Hostheadernamen. Achten Sie bei der Angabe eines Hostheaders darauf, einen Namen anzugeben, den der DNS-Service auflösen kann. Wenn Sie einen öffentlich verfügbaren Domänennamen angeben, schließen Sie die ganze URL ein, einschließlich `http://www`.  
  
4.  Geben Sie den Port an. Wenn Sie einen benutzerdefinierten Port angeben, muss die URL für die Anwendung immer die Portnummer einschließen.  
  
5.  Klicken Sie auf **OK**.  
  
6.  Testen Sie die URL durch das Öffnen eines Browserfensters und Eingeben der URL.  
  
## <a name="urls-for-multiple-report-server-instances-on-the-same-computer"></a>URLs für mehrere Berichtsserverinstanzen auf demselben Computer.  
 Wenn Sie URLs für mehrere Instanzen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] reservieren, sollten Sie Benennungskonventionen einhalten, um Namenskonflikte zu vermeiden. Weitere Informationen finden Sie unter [URL-Reservierungen für Berichtsserver-Bereitstellungen mit mehreren Instanzen &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/url-reservations-for-multi-instance-report-server-deployments.md).  
  
##  <a name="URLExamples"></a> Beispiele für URL-Konfigurationen  
 In der folgenden Liste sind einige Beispiele für Berichtsserver-URLs aufgeführt:  
  
-   `http://localhost/reportserver`  
  
-   `http://localhost/reportserver_SQLEXPRESS`  
  
-   `http://sales01/reportserver`  
  
-   `http://sales01:8080/reportserver`  
  
-   `https://sales.adventure-works.com/reportserver`  
  
-   `https://www.adventure-works.com:8080/reportserver01`  
  
 Für den Zugriff auf das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] verwendete URLs weisen ein ähnliches Format auf und werden üblicherweise in derselben Website erstellt, die den Berichtsserver hostet. Der einzige Unterschied ist der Name des virtuellen Verzeichnisses (in diesem Fall lautet er **reports** , Sie können jedoch einen beliebigen Namen konfigurieren):  
  
-   `http://localhost/reports`  
  
-   `http://localhost/reports_SQLEXPRESS`  
  
-   `http://sales01/reports`  
  
-   `http://sales01:8080/reports`  
  
-   `https://sales.adventure-works.com/reports`  
  
-   `https://www.adventure-works.com:8080/reports`  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Konfigurations-Manager &#40;einheitlicher Modus&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Konfigurieren von Berichtsserver-URLs &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)

