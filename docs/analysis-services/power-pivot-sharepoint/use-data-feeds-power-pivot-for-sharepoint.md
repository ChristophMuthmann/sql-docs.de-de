---
title: "Verwenden von Datenfeeds (Power Pivot f&#252;r SharePoint) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 50140fdf-6fd1-41a1-9c14-8ecfb97ba2e1
caps.latest.revision: 13
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 13
---
# Verwenden von Datenfeeds (Power Pivot f&#252;r SharePoint)
  Datenfeeds sind einzelne oder mehrere Datenströme, die von einer Onlinedatenquelle generiert und in ein Zieldokument oder eine Zielanwendung gestreamt werden. Wenn Sie [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für Excel verwenden, können Datenfeeds Ihnen helfen, vorhandene Unternehmens- oder Geschäftsdaten von beliebigen Datenquellen in das [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Fenster in der Excel 2010-Arbeitsmappe abzurufen. Nachdem Sie einen Datenfeed in eine Arbeitsmappe importiert haben, können Sie später in allen Datenaktualisierungsvorgängen, die Sie auf einem SharePoint Server planen, darauf verweisen.  
  
 Wie Sie einen Datenfeed verwenden, hängt davon ab, ob Sie integrierte Exportfunktionen in Anwendungen verwenden, die Atom-Datenfeeds unterstützen, oder ob Sie benutzerdefinierte Datendienste erstellen und verwenden. Anwendungen, die in der Lage sind, Atom-XML-Daten zu veröffentlichen und zu lesen, unterstützen eine nahtlose Datenübertragung, die die Datenfeed- und Datendienstmechanismen für den Benutzer nicht erkennen lässt. Für den Benutzer werden einfach nur Daten von einer Anwendung in eine andere verschoben.  
  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] und Microsoft SharePoint 2010 bieten Datenfeeds, die in [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Arbeitsmappen verwendet werden können. Mithilfe der in diesem Thema enthaltenen Informationen erfahren Sie, wie auf Datenfeeds aus Berichten und Listen zugegriffen wird, über die Sie bereits verfügen.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [Erforderliche Komponenten](#prereq)  
  
 [Erstellen eines Datenfeeds aus einer SharePoint-Liste](#sharepointlist)  
  
 [Erstellen eines Datenfeeds aus einem Reporting Services-Bericht](#rsreport)  
  
 [Erstellen eines Datenfeeds aus einem Datendienstdokument](#dsdoc)  
  
##  <a name="prereq"></a> Erforderliche Komponenten  
 Sie benötigen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für Excel, um ein Datenfeed nach Excel 2010 zu importieren.  
  
 Sie müssen über einen Webdienst oder Datendienst verfügen, der Daten im Atom 1.0-Format bereitstellt. Sowohl [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] als auch SharePoint 2010 können Daten in diesem Format bereitstellen.  
  
 Bevor Sie eine SharePoint-Liste als Datenfeed exportieren können, müssen Sie ADO.NET Data Services auf dem SharePoint-Server installieren. Weitere Informationen finden Sie unter [Installieren von ADO.NET Data Services, um Datenfeedexporte von SharePoint-Listen zu unterstützen](http://msdn.microsoft.com/de-de/f32527ae-f623-4e08-adfb-6d3262f5c2ac).  
  
##  <a name="sharepointlist"></a> Erstellen eines Datenfeeds aus einer SharePoint-Liste  
 In einer SharePoint 2010-Farm verfügt eine SharePoint-Liste über eine Schaltfläche Als Datenfeed exportieren auf dem Listenmenüband. Sie können auf diese Schaltfläche klicken, um die Liste als Feed zu exportieren. Excel 2010 sollte mit der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Clientanwendung auf der Arbeitsstation ausgeführt werden, um optimale Ergebnisse zu erzielen. Die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Clientanwendung wird als Reaktion auf den Datenfeedexport gestartet und erstellt eine neue [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Tabelle, die die Liste enthält.  
  
1.  Öffnen Sie die Liste auf Ihrer SharePoint-Website.  
  
2.  Klicken Sie unter Listentools auf **Liste**.  
  
3.  Klicken Sie unter Verbinden und Exportieren auf **Als Datenfeed exportieren**.  
  
    > [!NOTE]  
    >  Die Schaltfläche **Als Datenfeed exportieren** wird über [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] zu SharePoint hinzugefügt. Wenn [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint nicht installiert ist oder Sie die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Funktion nicht aktiviert haben, ist diese Schaltfläche nicht verfügbar.  
  
4.  Klicken Sie auf **Öffnen**, wenn [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für Excel lokal installiert ist, oder klicken Sie auf **Speichern**, um das ATOMSVC-Dokument für Importvorgänge zu einem späteren Zeitpunkt auf der Festplatte zu speichern.  
  
5.  Wenn Sie **Öffnen** auswählen, verwenden Sie den Tabellenimport-Assistenten, um ein Datenfeed in ein Arbeitsblatt zu importieren. Der Datenfeed wird als neue Tabelle im [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Fenster hinzugefügt.  
  
 Wenn ADO.NET Data Services 3.5.1 nicht auf dem SharePoint-Server installiert ist, tritt ein Fehler auf. Weitere Informationen über den Fehler und seine Behebung finden Sie unter [Installieren von ADO.NET Data Services, um Datenfeedexporte von SharePoint-Listen zu unterstützen](http://msdn.microsoft.com/de-de/f32527ae-f623-4e08-adfb-6d3262f5c2ac).  
  
##  <a name="rsreport"></a> Erstellen eines Datenfeeds aus einem Reporting Services-Bericht  
 Wenn Sie über eine SQL Server 2008 R2 Reporting Services-Bereitstellung verfügen, können Sie einen Datenfeed mithilfe der neuen Atom-Renderingerweiterung aus einem vorhandenen Bericht generieren. Excel 2010 sollte mit dem [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für Excel-Add-In auf der Arbeitsstation ausgeführt werden, um optimale Ergebnisse zu erzielen. Die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Clientanwendung wird als Reaktion auf den Datenfeedexport gestartet, fügt automatisch die gestreamten Tabellen und Spalten hinzu und verknüpft diese.  
  
 Anweisungen zum Exportieren eines Datenfeeds aus einem Bericht finden Sie unter [Generieren von Datenfeeds aus einem Bericht &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/generate-data-feeds-from-a-report-report-builder-and-ssrs.md) in der [Hilfedatei zum Berichts-Generator](http://go.microsoft.com/fwlink/?LinkId=154494).  
  
> [!NOTE]  
>  Zum Einrichten eines Zeitplans mit wiederholter Datenaktualisierung, durch den Berichtsdaten in eine in einer SharePoint-Bibliothek veröffentlichte [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Arbeitsmappe erneut importiert werden, muss der Berichtsserver für die SharePoint-Integration konfiguriert sein. Weitere Informationen zur gemeinsamen Verwendung von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint und Reporting Services finden Sie unter [Konfiguration und Verwaltung eines Berichtsservers &#40;Reporting Services im SharePoint-Modus&#41;](../../reporting-services/report-server-sharepoint/configuration and administration of a report server.md).  
  
##  <a name="dsdoc"></a> Erstellen eines Datenfeeds aus einem Datendienstdokument  
 Wenn Sie über einen benutzerdefinierten Datendienst verfügen, der Atom-Feeds generiert, haben Sie die Möglichkeit, die Daten für Benutzer und Anwendungen verfügbar zu machen. In einem *Datendienstdokument* (ATOMSVC-Datei) ist mindestens eine Verbindung mit Onlinequellen angegeben, die Daten im Atom-Übertragungsformat veröffentlichen. Datendienstdokumente können in einer *Datenfeedbibliothek* erstellt werden. Dabei handelt es sich um eine zweckgebundene Bibliothek, die einen allgemeinen Zugriffspunkt für die Durchsuchung von Datendienstdokumenten ermöglicht, die zu einem SharePoint Server veröffentlicht wurden. IT-Arbeiter, die die Berechtigung haben, in der Datenfeedbibliothek auf Datendienstdokumente zuzugreifen, können auf die SharePoint-URL des Dokuments verweisen, um die Datenfeeds in ihre Arbeitsmappen und Anwendungen zu importieren.  
  
1.  Öffnen Sie eine Datenfeedbibliothek, die vom Websiteadministrator erstellt wurde. Weitere Informationen finden Sie unter [Erstellen oder Anpassen einer Datenfeedbibliothek &#40;Power Pivot für SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/create-or-customize-a-data-feed-library-power-pivot-for-sharepoint.md).  
  
2.  Klicken Sie unter Bibliothekstools auf **Dokumente**.  
  
3.  Klicken Sie auf **Neues Dokument**.  
  
4.  Geben Sie einen Dateinamen und eine Beschreibung an.  
  
5.  Geben Sie eine oder mehrere URLs an, die den Feed bereitstellen:  
  
    1.  **Basis-URL** ist optional. Sie sollten dies angeben, wenn ein Datendienstdokument mehrere Feeds bereitstellt. Basis-URL sollte den Teil der URL angeben, der allen Feeds (z. B. der Servername und die Website) gemeinsam ist. Wenn Sie zu einem Reporting Services-Bericht ein Datendienstdokument erstellen, wäre die Basis-URL die Berichtsserver-URL und der Bericht.  
  
    2.  **Webdienst-URL** ist erforderlich. Ohne die Basis-URL muss dieser Wert http :// oder https:// in der Adresse enthalten. Wenn Sie eine Basis-URL angegeben haben, ist die Webdienst-URL der Teil, der der Basis-URL folgt. Zum Beispiel: Wenn die vollständige URL http://adventure-works/inventory/today.aspx ist, wäre die Basis-URL http://adventure-works/inventory, und die Webdienst-URL wäre /today.aspx.  
  
         Die Webdienst-URL kann Parameter enthalten, die eine Teilmenge der Daten filtern oder auswählen. Die Anwendung oder der Dienst, die/der den Feed bereitstellt, muss die Parameter unterstützen, die Sie in der URL angeben.  
  
6.  Geben Sie einen **Tabellennamen** ein, eine Tabelle für jeden Feed. Dieser Wert ist erforderlich. Der Tabellenname wird von einer Clientanwendung verwendet, die den Datenfeed nutzt. In [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für Excel wird der Tabellenname verwendet, um Tabellen im [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Fenster zu benennen, die die importierten Daten enthalten.  
  
## Siehe auch  
 [Aktivieren der PowerPivot-Funktionsintegration für Websitesammlungen in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/activate power pivot integration for site collections in ca.md)   
 [Freigeben von Datenfeeds mithilfe einer Datenfeedbibliothek &#40;PowerPivot für SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/share-data-feeds-using-a-data-feed-library-power-pivot-for-sharepoint.md)  
  
  