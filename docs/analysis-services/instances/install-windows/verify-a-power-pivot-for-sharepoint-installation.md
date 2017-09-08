---
title: "Überprüfen einer PowerPivot für SharePoint-Installation | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 855bd055-5ad3-493f-9c5b-1f5297b2e6e2
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: abc618942a95b28fd2b93f72e4b511e519c58191
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="verify-a-power-pivot-for-sharepoint-installation"></a>Überprüfen einer Power Pivot für SharePoint-Installation
  Eine Instanz von [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint, die Sie in einer SharePoint-Farm installieren, wird über die SharePoint-Zentraladministration verwaltet. Sie können zumindest die Seiten in der Zentraladministration und auf SharePoint-Websites durchsuchen, um zu überprüfen, ob [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Serverkomponenten und -funktionen verfügbar sind. Um jedoch eine Installation vollständig zu überprüfen, müssen Sie eine [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Arbeitsmappe haben, die Sie in SharePoint veröffentlichen und auf die Sie über eine Bibliothek zugreifen können. Zu Testzwecken können Sie eine Beispielarbeitsmappe veröffentlichen, die bereits [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]-Daten enthält, und damit überprüfen, ob die SharePoint-Integration ordnungsgemäß konfiguriert wurde.  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]** SharePoint 2016 &#124; SharePoint 2013|  
  
##  <a name="verifyinstall"></a> Überprüfen der Integration der Zentraladministration  
 Um die [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Integration über die Zentraladministration zu überprüfen, gehen Sie wie folgt vor:  
  
1.  Klicken Sie im Startmenü auf **Alle Programme**, öffnen Sie Microsoft SharePoint 2016-Produkte oder Microsoft SharePoint 2013-Produkte, und klicken Sie auf **SharePoint 2016-Zentraladministration oder SharePoint 2013-Zentraladministration**.  
  
2.  Geben Sie Ihren Benutzernamen und Ihr Kennwort ein, und klicken Sie dann auf **OK**.  
  
     Optional können Sie Browsereinstellungen ändern, damit Sie den Benutzernamen und das Kennwort nicht bei jedem Öffnen der Zentraladministration eingeben müssen. Gehen Sie wie folgt vor, um die Zentraladministration als vertrauenswürdige Website hinzuzufügen:  
  
    1.  Klicken Sie in Internet Explorer im Menü „Extras“ auf **Internetoptionen**.  
  
    2.  Klicken Sie auf der Registerkarte „Sicherheit“ im Abschnitt **Zone auswählen, um Einstellungen anzuzeigen oder zu ändern** auf „Vertrauenswürdige Sites“ und dann auf „Sites“.  
  
    3.  Deaktivieren Sie das Kontrollkästchen **Für Sites dieser Zone ist eine Serverüberprüfung (https:) erforderlich** .  
  
    4.  Geben Sie in **Diese Website zur Zone hinzufügen**die URL zu Ihrer Website ein, und klicken Sie dann auf **Hinzufügen**.  
  
    5.  Klicken Sie auf **Schließen**und dann auf **OK**.  
  
        > [!NOTE]  
        >  Die Dokumentation zur SharePoint-Installation enthält weitere Anweisungen zum Umgehen von Proxyserverfehlern und Deaktivieren der verstärkten Sicherheitskonfiguration für Internet Explorer, damit Updates heruntergeladen und installiert werden können. Weitere Informationen finden Sie im Abschnitt **Ausführen zusätzlicher Aufgaben** unter [Bereitstellen eines einzelnen Servers mit SQL Server](http://go.microsoft.com/fwlink/?LinkId=177754) auf der Microsoft-Website.  
  
3.  Klicken Sie in der Zentraladministration unter Systemeinstellungen auf **Farmfunktionen verwalten**.  
  
4.  Überprüfen Sie, ob die Funktion zur **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Integration** auf **Aktiv**festgelegt ist.  
  
5.  Klicken Sie in der Zentraladministration unter Systemeinstellungen auf **Dienste auf dem Server verwalten**.  
  
6.  Vergewissern Sie sich, dass der **SQL Server [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]-Systemdienst** gestartet ist.  
  
     In einer SharePoint-Farm mit mehreren Servern müssen Sie möglicherweise den angezeigten Server ändern, um sich zu vergewissern, dass alle Server, auf denen Sie [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] bereitgestellt haben, ausgeführt werden.  
  
7.  Klicken Sie in der Zentraladministration unter Anwendungsverwaltung auf **Dienstanwendungen verwalten**.  
  
8.  Klicken Sie auf **Standard-[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]-Dienstanwendung**, um das [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]-Management-Dashboard für diese Anwendung zu öffnen. Bei seiner ersten Verwendung dauert das Laden des Dashboards einige Minuten.  
  
     Klicken Sie alternativ auf den leeren Bereich neben **Standard-[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]-Dienstanwendung**, um die Zeile auszuwählen, und klicken Sie auf **Eigenschaften**, um die Konfigurationseinstellungen für diese Dienstanwendung anzuzeigen. Sie können sowohl die Konfigurationseinstellungen als auch die Anwendungseigenschaften ändern, um Ihre Serverkonfiguration zu ändern. Weitere Informationen finden Sie unter [Erstellen und Konfigurieren einer Power Pivot-Dienstanwendung in der Zentraladministration](../../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md).  
  
## <a name="verify-integration-at-the-site-level"></a>Überprüfen der Integration auf Websiteebene  
 Um die [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Integration in eine SharePoint-Website zu überprüfen, gehen Sie wie folgt vor:  
  
1.  Öffnen Sie in einem Browser die Webanwendung, die Sie erstellt haben. Wenn Sie Standardwerte verwendet haben, können Sie angeben, dass http://\<Ihr Computername > in der URL-Adresse.  
  
2.  Überprüfen Sie, ob die [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Funktionen für Datenzugriff und -verarbeitung in der Anwendung verfügbar sind. Überprüfen Sie hierzu, ob durch [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]bereitgestellte Bibliotheksvorlagen vorhanden sind:  
  
    1.  Wählen Sie **Websiteinhalt**aus.  
  
    2.  In der App-Liste sollten **Datenfeedbibliothek** und **[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Katalog**angezeigt werden. Diese Bibliotheksvorlagen werden von der [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Funktion bereitgestellt und sind in der Bibliothekenliste sichtbar, sofern die Funktion ordnungsgemäß integriert wurde.  
  
## <a name="verify-data-access-on-the-server"></a>Überprüfen des Datenzugriffs auf dem Server  
 Um den [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Datenzugriff auf dem Server zu überprüfen, gehen Sie wie folgt vor:  
  
1.  [Laden Sie das Datenbeispiel „Picnic“ herunter](http://go.microsoft.com/fwlink/?LinkID=219108) , das zu einem Reporting Services-Tutorial gehört. Sie verwenden die Beispielarbeitsmappe in diesem Download, um den [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Datenzugriff zu überprüfen. Extrahieren Sie die Dateien.  
  
2.  Laden Sie die Excel-Arbeitsmappe (.xlsx) in die freigegebenen Dokumente hoch. Die Arbeitsmappe enthält eingebettete [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Daten.  
  
3.  Klicken Sie auf das Dokument, um es von der Bibliothek aus zu öffnen.  
  
4.  Klicken Sie oben in der Arbeitsmappe auf einen Slicer oder einen Filter. Slicer in dieser Arbeitsmappe sind Month, Color und Type. Durch das Klicken auf einen Slicer wird eine [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Abfrage gestartet und die Betriebsbereitschaft des Servers nachgewiesen. Der Server lädt [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Daten im Hintergrund und gibt die Ergebnisse zurück.  
  
5.  Wechseln Sie erneut zur Bibliothek. Klicken Sie auf den Abwärtspfeil rechts neben der Arbeitsmappe und dann auf **Power View starten**. Durch diesen Schritt wird bestätigt, dass die [!INCLUDE[ssCrescent](../../../includes/sscrescent-md.md)] -Funktion in Reporting Services betriebsbereit ist. Überspringen Sie diesen Schritt, wenn Sie Reporting Services nicht installiert haben.  
  
     Im nächsten Schritt stellen Sie eine Verbindung mit dem Server in Management Studio her, um zu überprüfen, ob die Daten geladen und zwischengespeichert wurden.  
  
6.  Starten Sie SQL Server Management Studio im Startmenü in der Programmgruppe [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)] . Wenn dieses Tool nicht auf dem Server installiert ist, können Sie mit dem letzten Schritt fortfahren, um das Vorhandensein zwischengespeicherter Dateien zu bestätigen.  
  
7.  Wählen Sie unter Servertyp die Option **Analysis Services**aus.  
  
8.  Geben Sie im Server  **\<Servername > \powerpivot**, wobei  **\<Servername >** der Namen des Computers ist, wird die [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint die Installation.  
  
9. Klicken Sie auf **Verbinden**. Dies überprüft, ob der Analysis Services-Server verfügbar ist.  
  
10. Im Objekt-Explorer können Sie auf **Datenbanken** klicken, um die Liste der [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Datendateien anzuzeigen, die geladen wurden.  
  
11. Überprüfen Sie im Computerdateisystem den folgenden Ordner, um zu bestimmen, ob Dateien auf dem Datenträger zwischengespeichert wurden. Das Vorhandensein zwischengespeicherter Dateien ist eine weitere Bestätigung, dass die Bereitstellung betriebsbereit ist. Um den Dateicache anzuzeigen, wechseln Sie in den [!INCLUDE[ssInstallPathVar](../../../includes/ssinstallpathvar-md.md)]-Dienstanwendungsordner [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] MSAS13.POWERPIVOT\OLAP\Backup\Sandboxes\Default. Jede zwischengespeicherte Datenbank wird in einem eigenen Ordner gespeichert. Dabei wird eine GUID-basierte Namenskonvention verwendet, um einen eindeutigen Namen sicherzustellen.  
  
  
