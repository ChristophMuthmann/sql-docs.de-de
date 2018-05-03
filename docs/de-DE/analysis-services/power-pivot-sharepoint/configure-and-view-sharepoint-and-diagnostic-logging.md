---
title: Konfigurieren und Anzeigen von SharePoint und Diagnoseprotokollierung | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b4e2842e06d26d1e9df60fac01b44f850aa758e7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="configure-and-view-sharepoint-and-diagnostic-logging"></a>Konfigurieren und Anzeigen von SharePoint und Diagnoseprotokollierung
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Server-Vorgänge, Ereignisse und Meldungen werden in SharePoint-Protokolldateien aufgezeichnet. Verwenden Sie die Informationen in diesem Thema, um Protokolliergrade zu konfigurieren und Protokolldatei-Informationen anzuzeigen. Sie können steuern, welche [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] Serverereignisse in einer Datei protokolliert werden. Sie können auch den Schweregrad von Meldungen steuern, die protokolliert werden. Weitere Informationen finden Sie unter [Konfigurieren der Sammlung von Verwendungsdaten für &#40;PowerPivot für SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md).  
  
 In diesem Thema:  
  
-   [Protokolldatei-Speicherort](#bkmk_filelocation)  
  
-   [Ändern diagnostischer Protokolliergrade für einzelne Ereigniskategorien](#bkmk_modifyloglevels)  
  
-   [So zeigen Sie die SharePoint-Protokolldateien an](#bkmk_how2viewlogfiles)  
  
##  <a name="bkmk_filelocation"></a> Protokolldatei-Speicherort  
 Standardmäßig werden SharePoint-Protokolldateien am folgenden Speicherort gespeichert:  
  
 `C:\Program files\Common Files\Microsoft Shared\Web Server Extensions\14\LOGS`  
  
 Der Ordner LOGS enthält Protokolldateien (`.log`), Datendateien (`.txt`) und Verwendungsdateien (`.usage`). Die Dateinamenskonvention für ein SharePoint-Ablaufverfolgungsprotokoll ist der von einem Datum und einem Zeitstempel gefolgte Servername. SharePoint-Ablaufverfolgungsprotokolle werden in regelmäßigen Abständen erstellt, sowie immer dann, wenn ein IISRESET erfolgt. Im Allgemeinen gibt es viele Ablaufverfolgungsprotokolle innerhalb eines 24 Stundenzeitraums.  
  
##  <a name="bkmk_modifyloglevels"></a> Ändern diagnostischer Protokolliergrade für einzelne Ereigniskategorien  
 Standardmäßig wird die ULS-Protokollierung von [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Ereignissen auf *Medium*festgelegt. Diese Einstellung ist für SQL Server 2012 neu. Wenn Sie einen Server von der vorherigen Version aktualisieren, könnte der Protokolliergrad immer noch auf *Ausführlich*festgelegt sein, der Standardebene in SQL Server 2008 R2. Wenn Sie daran gewöhnt sind, die ULS-Protokolle für die [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Serverauslastung anzuzeigen, werden Sie feststellen, dass aufgrund der Änderung weniger Informationen über die [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Servervorgänge zur Verfügung stehen.  
  
 Abgesehen von Ausnahmen vom Typ *Hoch*sind alle [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Meldungen der Kategorie „Ausführlich“ zuzuordnen. Wenn Sie Einträge für routinemäßige Servervorgänge, beispielsweise Verbindungen, Anforderungen oder Abfrageerstellung, protokollieren möchten, müssen Sie den Protokolliergrad auf Ausführlich festlegen.  
  
 So ändern Sie diagnostische Protokolliergrade für einzelne Ereigniskategorien:  
  
1.  Klicken Sie in der SharePoint-Zentraladministration auf **Überwachung**.  
  
2.  Klicken Sie auf **Diagnoseprotokollierung konfigurieren**.  
  
3.  Scrollen Sie zum **[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienst**.  
  
4.  Erweitern Sie die Kategorie, und wählen Sie einzelne Kategorien aus:  
  
     Unter**Anwendungsseitenanforderung** werden Ereignisse angegeben, die beim Suchen einer [!INCLUDE[ssGeminiSrv_md](../../includes/ssgeminisrv-md.md)] -Instanz zum Laden einer [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Datenquelle und zum Kommunizieren mit anderen Servern in der Farm von der Dienstanwendung ausgelöst werden.  
  
     Unter**Anforderungsverarbeitung** werden Ereignisse angegeben, die durch Abfrageanforderungen für eine auf einem Server in der Farm geladene [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Datenbank ausgelöst wurden.  
  
     **Verwendung** gibt ein auf die Sammlung von [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Verwendungsdaten bezogenes Ereignis an.  
  
5.  Wählen Sie unter Unwichtigstes, im Ereignisprotokoll aufzuzeichnendes Ereignis die Option **Keine** aus, um die Ereignisprotokollierung für die Kategorie zu deaktivieren, oder **Fehler** , um die Protokollierung auf Fehler zu beschränken.  
  
6.  Wählen Sie **Ausführlich** aus, um alle Ereignisse zum Ereignisprotokoll zu protokollieren.  
  
7.  Wählen Sie unter Unwichtigstes, im Ablaufverfolgungsprotokoll aufzuzeichnendes Ereignis die Option **Keine** aus, um die Ablaufverfolgung für die Kategorie zu deaktivieren, oder **Fehler** , um die Ablaufverfolgung auf Fehler zu beschränken.  
  
8.  Wählen Sie **Ausführlich** aus, um alle Ereignisse zum Ablaufverfolgungsprotokoll zu protokollieren.  
  
9. Klicken Sie auf **OK**.  
  
##  <a name="bkmk_how2viewlogfiles"></a> So zeigen Sie die SharePoint-Protokolldateien an  
 Protokolldateien sind Textdateien. Sie können sie in jedem Text-Editor öffnen. Sie können auch Protokoll-Viewer-Anwendungen von Drittanbietern verwenden.  
  
#### <a name="use-a-text-editor"></a>Verwenden eines Text-Editors  
 Wenn Sie einen [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Serverfehler mit einem Text-Editor beheben, können Ihnen die folgenden Tipps dabei helfen, relevante Informationen in der Datei zu suchen:  
  
-   Für Fehler im Zusammenhang mit dem Veröffentlichen, Anzeigen oder Aktualisieren einer [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Arbeitsmappe, durchsuchen Sie die Protokolldatei nach dem Namen der Arbeitsmappe.  
  
-   Für Fehler, die eine Korrelations-ID ausgeben, kopieren Sie diese und verwenden Sie sie als Suchbegriff in der Protokolldatei.  
  
-   Suchen Sie nach dem Fehlerstatus "Hoch" oder "Ausnahme". Suchen Sie nach „[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienst“.  
  
-   Wenn Sie wissen, wann der Fehler aufgetreten ist, verwenden Sie die Datums- und Uhrzeitinformationen, um den Bereich von Einträgen, den Sie durchsuchen müssen, einzugrenzen.  
  
#### <a name="use-a-log-viewer-application"></a>Verwenden einer Protokoll-Viewer-Anwendung  
 Obwohl Sie die Ablaufverfolgungsprotokolle mithilfe eines Text-Editors einzeln anzeigen können, kann eine Protokoll-Viewer-Anwendung, die Ihnen ermöglicht, mehrere Protokolldateien anzuzeigen, viel nützlicher sein. Glücklicherweise gibt es mehrere Protokoll-Viewer-Anwendungen von Drittanbietern auf der CodePlex-Website zum Download, die Ihnen helfen können, mehrere Ablaufverfolgungsprotokolle in einem einzelnen Arbeitsbereich anzuzeigen.  
  
 Die folgenden Anweisungen enthalten Links zu gängigen SharePoint ULS Protokoll-Viewern, die Sie aus CodePlex herunterladen können.  
  
1.  Gehen Sie zu [SharePoint LogViewer](http://sharepointlogviewer.codeplex.com) oder [SharePoint ULS Log Viewer](http://go.microsoft.com/fwlink/?LinkId=150052) auf der Codeplex-Website.  
  
2.  Klicken Sie auf die Registerkarte **Downloads** .  
  
3.  Klicken Sie auf die ausführbare Datei. Es handelt sich entweder um **SharePointLogViewer.exe** oder um **ULS Viewer 2.0 Binary**.  
  
4.  Lesen Sie die Lizenzbedingungen und stimmen Sie ihnen zu.  
  
5.  Klicken Sie auf **Speichern** , um die Software auf Ihr lokales System herunterzuladen.  
  
     Wenn Sie SharePoint ULS Log Viewer herunterladen, speichern Sie ULSViewer.zip im Ordner "Downloads".  
  
6.  Klicken Sie im Ordner Downloads mit der rechten Maustaste auf „ULSViewer.zip“, und wählen Sie **Alle extrahieren**aus.  
  
7.  Geben Sie einen Zielordner an, und klicken Sie dann auf **Extrahieren**.  
  
8.  Doppelklicken Sie im Ordner, der die extrahierten Programmdateien enthält, auf **ULSViewer** , und führen Sie die Anwendung aus.  
  
9. Klicken Sie auf das Ordnersymbol oben links in der Ecke des Anwendungsfensters.  
  
10. Navigieren Sie zu \Programme\Gemeinsame Dateien\Microsoft Shared\Web Server Extensions\14\Logs.  
  
11. Wählen Sie ein oder mehrere Ablaufverfolgungsprotokolle aus. Standardmäßig bestehen Ablaufverfolgungsprotokolldateinamen aus dem Computernamen plus Datums- und Uhrzeitinformationen. Der Dateityp ist Textdokument.  
  
12. Klicken Sie auf **Öffnen** , und warten Sie, bis die Dateien geladen sind.  
  
13. Wählen Sie die Daten mithilfe der integrierten Filter nach Schweregrad, Prozess, Kategorie oder nach einer benutzerdefinierten Textdatei aus. Sie können auch auf Spaltenüberschriften klicken, um die Sortierreihenfolge zu ändern.  
  
#### <a name="entries-for-power-pivot-services"></a>Einträge für PowerPivot-Dienste  
 Die folgende Tabelle beschreibt die Einträge für [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] Servervorgänge, die am häufigsten in einer SharePoint-Protokolldatei gefunden werden.  
  
|Verarbeiten|Bereich|Kategorie|Ebene|MessageBox|Details|  
|-------------|----------|--------------|-----------|-------------|-------------|  
|w3wp.exe|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] Dienst|Verwendung|Ausführlich|Es gibt keine aktuellen Anforderungsstatistiken, nichts ist zu protokollieren.|Die Serviceberichte fragen in vordefinierten Intervallen Reaktionsstatistiken als Verwendungsereignis für das Verwendungsdatensammlungssystem ab. Diese Meldung gibt an, dass es keine Abfragestatistiken für einen Bericht gibt.|  
|w3wp.exe|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienst|Web-Front-End|Ausführlich|Beginnt mit der Suche nach einem Anwendungsserver für Datenquelle =\<*Pfad*>|Wenn das Programm eine Verbindungsanforderung empfängt, identifiziert der [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienst einen verfügbaren [!INCLUDE[ssGeminiSrv_md](../../includes/ssgeminisrv-md.md)] , um die Anforderung zu behandeln. Wenn es nur einen Server in der Farm gibt, akzeptiert der lokale Server die Anforderung in allen Fällen.|  
|w3wp.exe|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienst|Web-Front-End|Ausführlich|Die Suche nach dem Anwendungsserver war erfolgreich.|Die Anfrage wurde einer [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] Dienstanwendung zugeordnet.|  
|w3wp.exe|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienst|Web-Front-End|Ausführlich|Umleiten der Anforderung für die \< *PowerPivotdata-Quelle*> auf die [!INCLUDE[ssGeminiSrv_md](../../includes/ssgeminisrv-md.md)].|Die Anforderung wurde an den [!INCLUDE[ssGeminiSrv_md](../../includes/ssgeminisrv-md.md)]weitergeleitet.|  
|w3wp.exe|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] Dienst|Anforderungsverarbeitung|Ausführlich|Umleiten der Anforderung für username-\<*SharePoint-Benutzer*> in der Datenbank|Eine personifizierte Verbindung zur [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Datenquelle wurde für den SharePoint-Benutzer erstellt.|  
  
## <a name="see-also"></a>Siehe auch  
 [Sammlung von Power Pivot-Verwendungsdaten](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md)   
 [Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [Konfigurieren der Sammlung von Verwendungsdaten für Power Pivot für SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  
