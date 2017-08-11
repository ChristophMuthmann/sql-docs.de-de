---
title: "Skript für Bereitstellungs- und Verwaltungsaufgaben | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripts [Reporting Services]
- moving reports
- report servers [Reporting Services], duplicating settings
- deploying [Reporting Services], scripts
- copying report server settings
- administrative tasks [Reporting Services]
- duplicating report server environment
- migrating reports [Reporting Services]
- scripts [Reporting Services], deployments
- transferrng reports
- reports [Reporting Services], migrating
ms.assetid: d0416c9e-e3f9-456d-9870-2cfd2c49039b
caps.latest.revision: 62
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 707cf39041be5c96ac4898e462580b3630feaaaf
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---

# <a name="script-deployment-and-administrative-tasks"></a>Skripts für Bereitstellungs- und Verwaltungsaufgaben

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] unterstützt die Verwendung von Skripts, um routinemäßige Installations-, Bereitstellungs- und Verwaltungsaufgaben zu automatisieren. Die Bereitstellung eines Berichtsservers stellt einen aus mehreren Schritten bestehenden Vorgang dar. Sie müssen mehrere Tools und Prozesse verwenden, um eine Bereitstellung zu konfigurieren. Es gibt kein einzelnes Programm oder Verfahren, das zum Automatisieren aller zugehörigen Aufgaben verwendet werden kann.  
  
 Es sollte nicht jeder Schritt automatisiert werden. In einigen Fällen stellt die Ausführung eines Schritts auf manuelle Weise oder in einem Grafiktool die einfachste und effektivste Vorgehensweise dar. Wenn Sie z. B. eine große Anzahl von Berichten und Modellen bereitstellen möchten, empfiehlt es sich, die Berichtsserver-Datenbanken zu kopieren statt Code zu schreiben, der die Berichtsserverumgebung neu erstellt.  
  
 Einige Schritte erfordern benutzerdefinierten Code. Zum Beispiel kann die Konfiguration der URLs für den Webdienst und den Berichts-Manager automatisiert werden, jedoch nur, wenn Sie benutzerdefinierten Code schreiben, der den Berichtsserver-WMI-Anbieter aufruft (Windows Management Instrumentation). Wenn Sie keinen Code schreiben möchten, müssen Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool verwenden, um diesen Schritt auszuführen.  
  
 Zum Ausführen eines Skripts, das einen Berichtsserver konfiguriert, müssen Sie auf dem von Ihnen konfigurierten Computer als lokaler Administrator angemeldet sein. Weitere Informationen finden Sie unter [Konfigurieren eines Berichtsservers für die Remoteverwaltung](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md).  
  
 In diesem Thema werden die empfohlenen Vorgehensweisen für die Automatisierung bestimmter Schritte beschrieben. Einige Programme und Programmierschnittstellen werden erwähnt; die jeweils dazugehörigen Beschreibungen finden Sie weiter unten in diesem Thema.  
  
## <a name="deployment-tasks-and-how-to-automate-them"></a>Bereitstellungsaufgaben und deren Automatisierung  
 In der folgenden Tabelle sind die Installations- und Konfigurationsaufgaben zusammengefasst, die zum Bereitstellen eines Berichtsservers erforderlich sind. Sie können die Tabelle verwenden, um eine bestimmte Aufgabe an eine Vorgehensweise anzupassen, die die Automatisierung und unbeaufsichtigte Ausführung der Aufgabe ermöglicht.  
  
|Task|Vorgehensweise|  
|----------|--------------|  
|Installieren von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|Sie können an der Befehlszeile das Setupprogramm ausführen, um eine unbeaufsichtigte Installation auszuführen.<br /><br /> Mit dem Setupprogramm können Sie einen Berichtsserver installieren und konfigurieren, jedoch nur, wenn Sie die Standardkonfigurationsoption angeben und Ihr System sämtliche Anforderungen für diesen Installationstyp erfüllt. Wenn Sie die Installation nicht mit der Standardkonfiguration vornehmen können, können Sie nur die Dateien installieren.|  
|Konfigurieren des Dienstkontos.|Das Dienstkonto wird anfänglich im Rahmen des Setups konfiguriert. Wenn Sie Änderungen am Dienstkonto als nach dem Setup durchzuführende Aufgabe automatisieren möchten, müssen Sie benutzerdefinierten Code schreiben, der den Berichtsserver-WMI-Anbieter aufruft (Windows Management Instrumentation). Es gibt keine Eingabeaufforderungs-Hilfsprogramme oder Skriptvorlagen für die programmgesteuerte Konfiguration des Dienstkontos.<br /><br /> Wenn die Codierungsanforderungen Sie von der Automatisierung dieses Schritts abhalten, können Sie das Konto auf einfache Weise manuell konfigurieren, indem Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool ausführen. Weitere Informationen finden Sie unter [Konfigurieren des Berichtsserver-Dienstkontos &#40;SSRS-Konfigurations-Manager&#41;](http://msdn.microsoft.com/library/25000ad5-3f80-4210-8331-d4754dc217e0).|  
|Konfigurieren von URLs für den Report Server-Webdienst und den Berichts-Manager.|Sie müssen benutzerdefinierten Code schreiben, der den Berichtsserver-WMI-Anbieter aufruft. Es gibt keine Befehlszeilenprogramme oder Skriptvorlagen für die Konfiguration der URLs.<br /><br /> Wenn Sie keinen Code schreiben möchten, können Sie die URLs manuell konfigurieren, indem Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool ausführen. Weitere Informationen finden Sie unter [Konfigurieren einer URL &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md).|  
|Erstellen der Berichtsserver-Datenbank.|Sie müssen benutzerdefinierten Code schreiben, der den Berichtsserver-WMI-Anbieter aufruft. Es gibt keine Eingabeaufforderungs-Hilfsprogramme oder Skriptvorlagen zum Erstellen der Berichtsserver-Datenbanken und von RSExecRole.<br /><br /> Wenn Sie keinen Code schreiben möchten, können Sie die Datenbank manuell erstellen, indem Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool ausführen. Weitere Informationen finden Sie unter [erstellen einen einheitlichen Modus Berichtsserver-Datenbank &#40; SSRS-Konfigurations-Manager &#41; ](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).|  
|Konfigurieren der Verbindung mit der Berichtsserver-Datenbank.|Wenn Sie die Verbindungszeichenfolge, das Konto oder Kennwort oder den Authentifizierungstyp ändern möchten, führen Sie das Hilfsprogramm **rsconfig** zum Konfigurieren der Verbindung aus. Weitere Informationen finden Sie unter [konfigurieren Sie eine Verbindung mit der Berichtsserver-Datenbank &#40; SSRS-Konfigurations-Manager &#41; ](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md) und [Rsconfig-Hilfsprogramm &#40; SSRS &#41; ](../../reporting-services/tools/rsconfig-utility-ssrs.md).<br /><br /> Mit rsconfig.exe können Sie die Datenbank nicht erstellen oder aktualisieren. Die Datenbank und RSExecRole müssen bereits vorhanden sein.|  
|Konfigurieren Sie eine Bereitstellung für horizontales Skalieren.|Wählen Sie eine der folgenden Vorgehensweisen zum Automatisieren der Bereitstellung für horizontales Skalieren aus:<br /><br /> -   Führen Sie das Hilfsprogramm rskeymgmt.exe aus, um die Berichtsserverinstanzen in einer vorhandenen Installation zusammenzuführen. Weitere Informationen finden Sie unter [hinzufügen und Entfernen von Verschlüsselungsschlüsseln für die Bereitstellung für horizontales Skalieren &#40; SSRS-Konfigurations-Manager &#41; ](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md).<br />-   Schreiben Sie benutzerdefinierten Code, der für den Berichtsserver-WMI-Anbieter ausgeführt wird.|  
|Sichern Sie Verschlüsselungsschlüssel.|Wählen Sie eine der folgenden Vorgehensweisen zum Automatisieren der Sicherung der Verschlüsselungsschlüssel aus:<br /><br /> -   Führen Sie das Hilfsprogramm rskeymgmt.exe aus, um die Schlüssel zu sichern. Weitere Informationen finden Sie unter [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).<br />-   Schreiben Sie benutzerdefinierten Code, der für den Berichtsserver-WMI-Anbieter ausgeführt wird.|  
|Konfigurieren Sie Berichtsserver-E-Mail-Optionen.|Schreiben Sie benutzerdefinierten Code, der für den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -WMI-Anbieter ausgeführt wird. Der Anbieter unterstützt eine Teilmenge der E-Mail-Konfigurationseinstellungen.<br /><br /> Obwohl die Datei RSReportServer.config alle Einstellungen enthält, verwenden Sie die Datei nicht in automatisierter Art und Weise. Verwenden Sie insbesondere keine Batchdatei, um die Datei auf einen anderen Berichtsserver zu kopieren. Jede Konfigurationsdatei enthält für die aktuelle Instanz spezifische Werte. Diese Werte sind in anderen Berichtsserverinstanzen ungültig.<br /><br /> Weitere Informationen zu den Einstellungen finden Sie unter [Konfigurieren eines Berichtsservers für die E-Mail-Übermittlung (SSRS-Konfigurations-Manager)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83).|  
|Konfigurieren Sie das Konto für die unbeaufsichtigte Ausführung.|Wählen Sie eine der folgenden Vorgehensweisen zum Automatisieren der Konfiguration des Kontos für die unbeaufsichtigte Ausführung aus:<br /><br /> -   Führen Sie das Hilfsprogramm rsconfig.exe aus, um das Konto zu konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren des unbeaufsichtigten Ausführungskontos &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).<br />-   Schreiben Sie benutzerdefinierten Code, der den Berichtsserver-WMI-Anbieter aufruft.|  
|Stellen Sie vorhandenen Inhalt auf einem anderen Berichtsserver bereit, einschließlich der Ordnerhierarchie, Rollenzuweisungen, Berichte, Abonnements, Zeitpläne, Datenquellen und Ressourcen.|Die beste Möglichkeit, eine vorhandene Berichtsserverumgebung neu zu erstellen, besteht im Kopieren der Berichtsserver-Datenbank in eine neue Berichtsserverinstanz.<br /><br /> Eine alternative Vorgehensweise besteht im Schreiben von benutzerdefiniertem Code, der vorhandenen Berichtsserverinhalt programmgesteuert neu erstellt. Beachten Sie jedoch, dass Abonnements, Berichtsmomentaufnahmen und der Berichtsverlauf nicht programmgesteuert neu erstellt werden können.<br /><br /> Für manche Bereitstellungen empfiehlt es sich, beide Verfahren zusammen zu verwenden (d. h., Wiederherstellen einer Berichtsserver-Datenbank und anschließendes Ausführen von benutzerdefiniertem Code, der die Berichtsserver-Datenbank für eine bestimmte Installation ändert).<br /><br /> Ein ausführliches Beispiel finden Sie unter [Reporting Services-Beispielskript „rs.exe“ zum Migrieren von Inhalten zwischen Berichtsservern](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).<br /><br /> Weitere Informationen zum Verschieben einer Berichtsserver-Datenbank finden Sie unter [Verschieben der Berichtsserver-Datenbanken auf einem anderen Computer &#40; SSRS im einheitlichen Modus &#41; ](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md). Weitere Informationen zum programmgesteuerten Erstellen einer Berichtsserverumgebung finden Sie in diesem Thema im Abschnitt "Migrieren von Berichtsserverinhalt und -ordnern mithilfe von Skripts".|  
  
## <a name="tools-and-technologies-for-automating-server-deployment"></a>Tools und Verfahren zum Automatisieren der Serverbereitstellung  
 In der folgenden Liste sind die Programme und Schnittstellen zusammengefasst, mit denen Bereitstellungs- und Verwaltungsaufgaben automatisiert werden können:  
  
-   Das Setupprogramm kann im unbeaufsichtigten Modus ausgeführt werden, um Berichtsserverkomponenten zu installieren und in einigen Fällen zu konfigurieren. Sie müssen die Option zum ausschließlichen Installieren von Dateien verwenden, damit vom Setupprogramm eine Berichtsserverinstanz konfiguriert wird.  
  
-   Für die Serverkonfiguration im lokalen und Remotemodus können der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -WMI-Anbieter und die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Befehlszeilenprogramme verwendet werden.  
  
     Der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -WMI-Anbieter macht Klassen, Eigenschaften und Methoden verfügbar, mit denen Sie alle Aspekte einer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Installation konfigurieren können. Dazu zählen u.a. das Angeben des Dienstkontos, das Konfigurieren von URLs, das Erstellen und Konfigurieren der Berichtsserver-Datenbank und das Konfigurieren eines Berichtsservers für die E-Mail-Übermittlung. Sie können den WMI-Anbieter nur verwenden, wenn Sie benutzerdefinierten Code oder ein benutzerdefiniertes Skript schreiben. Weitere Informationen finden Sie unter [Zugreifen auf den Reporting Services-WMI-Anbieter](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md).  
  
     Eine Alternative zum Schreiben von Code besteht in der Verwendung der Befehlszeilen-Hilfsprogramme (rsconfig.exe und rskeymgmt.exe). Zum Ausführen der Hilfsprogramme können Sie Batchdateien schreiben. Mit den Hilfsprogrammen können Sie einige, aber nicht alle Konfigurationsaufgaben automatisieren.  
  
-   Mit dem Berichtsserver-Skript-Hosttool (rs.exe) kann benutzerdefinierter [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] -Code ausgeführt werden, den Sie schreiben, um vorhandenen Inhalt neu zu erstellen oder von einem Berichtsserver auf einen anderen zu verschieben. Mit dieser Vorgehensweise schreiben Sie ein Skript in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], speichern es als RSS-Datei und verwenden rs.exe zum Ausführen des Skripts auf dem Zielberichtsserver. Das von Ihnen verfasste Skript kann die SOAP-Schnittstelle zum Report Server-Webdienst aufrufen. Bereitstellungsskripts werden mithilfe dieser Methode geschrieben, da Sie auf diese Weise den Ordnernamespace und -inhalt eines Berichtsservers sowie die rollenbasierte Sicherheit neu erstellen können.  
  
-   Die SQL Server 2012-Version, PowerShell-Cmdlets für den integrierten SharePoint-Modus eingeführt. Sie können PowerShell zur Konfiguration und Verwaltung der SharePoint-Integration verwenden.  Weitere Informationen finden Sie unter [PowerShell-Cmdlets für SharePoint-Modus von Reporting Services](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
## <a name="use-scripts-to-migrate-report-server-content-and-folders"></a>Migrieren von Berichtsserverinhalten und -ordnern mithilfe von Skripts  
 Sie können Skripts schreiben, mit denen eine Berichtsserverumgebung in einer anderen Berichtsserverinstanz dupliziert werden. Bereitstellungsskripts werden in der Regel in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] geschrieben und dann mithilfe des Skripthost-Hilfsprogramms des Berichtsservers verarbeitet.  
  
 Ein ausführliches Beispiel finden Sie unter [Reporting Services-Beispielskript „rs.exe“ zum Migrieren von Inhalten zwischen Berichtsservern](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
 Verwenden Sie Skripts, um Ordner, freigegebene Datenquellen, Ressourcen, Berichte, Rollenzuweisungen und Einstellungen von einem Server auf einen anderen zu kopieren. Schreiben Sie ein Skript für eine Berichtsserverinstanz, und führen Sie es dann auf einem anderen Server aus, um den Berichtsserver-Namespace erneut zu erstellen. Wenn in Ihrer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bereitstellung mehrere Berichtsserver vorhanden sind, können Sie das Skript auf jedem Server einzeln ausführen, um alle Server identisch zu konfigurieren.  
  
 In der folgenden Liste sind die erforderlichen Schritte zum Migrieren von Berichten von einem Server auf einen anderen beschrieben.  
  
1.  Legen Sie die Skriptvariable auf die URL des Quellberichtsservers fest.  
  
2.  Verwenden Sie die Methoden <xref:ReportService2010.ReportingService2010.GetItemDefinition%2A> und <xref:ReportService2010.ReportingService2010.GetProperties%2A> , um die Berichtsdefinition und die Eigenschaften des Berichts abzurufen.  
  
3.  Legen Sie die URL so fest, dass sie auf den Zielserver verweist.  
  
4.  Verwenden Sie die <xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A> -Methode, um die von <xref:ReportService2010.ReportingService2010.GetProperties%2A> zurückgegebenen Eigenschaften und die von <xref:ReportService2010.ReportingService2010.GetItemDefinition%2A>.  
  
 Mit einer Kombination von get- und create-Methoden können Sie ähnliche Schritte zum Migrieren von Einstellungen, Ordnern, freigegebenen Datenquellen und Ressourcen ausführen. Weitere Informationen zu den verfügbaren Methoden finden Sie unter [technische Referenz &#40; SSRS &#41; ](../../reporting-services/technical-reference-ssrs.md).  
  
> [!NOTE]  
>  Sofern nicht explizit Anmeldeinformationen festgelegt wurden, werden Skripts mit den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anmeldeinformationen des Benutzers ausgeführt, der das Skript ausführt.  
  
 Weitere Informationen zum Formatieren und Ausführen einer Skriptdatei finden Sie unter [Skripterstellung mit dem Hilfsprogramm rs.exe und dem Webdienst](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md).  
  
## <a name="using-scripts-to-set-server-properties"></a>Festlegen von Servereigenschaften mithilfe von Skripts  
 Sie können Skripts schreiben, um Systemeigenschaften auf dem Berichtsserver festzulegen. Das folgende [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET-Skript zeigt eine Möglichkeit, Eigenschaften festzulegen. In diesem Beispiel wird das RSClientPrint-ActiveX-Steuerelement deaktiviert. Sie können jedoch **EnableClientPrinting** und **False** durch einen beliebigen gültigen Eigenschaftennamen und -wert ersetzen. Eine vollständige Liste der Servereigenschaften finden Sie unter [Report Server System Properties](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md).  
  
 Um dieses Skript zu verwenden, speichern Sie es in einer Datei mit der Erweiterung RSS und verwenden anschließend das Eingabeaufforderungs-Hilfsprogramm rs.exe, um die Datei auf dem Berichtsserver auszuführen. Das Skript wird nicht kompiliert, daher wird keine Installation von [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]benötigt. In diesem Beispiel wird davon ausgegangen, dass Sie über die entsprechenden Berechtigungen für den lokalen Computer verfügen, der den Berichtsserver hostet. Wenn Sie mit einem Konto angemeldet sind, das nicht über die erforderlichen Berechtigungen verfügt, müssen Sie Kontoinformationen über zusätzliche Befehlzeilenargumente angeben. Weitere Informationen finden Sie unter [RS.exe-Hilfsprogramm &#40; SSRS &#41; ](../../reporting-services/tools/rs-exe-utility-ssrs.md).  
  
> [!TIP]  
>  Ein ausführliches Beispiel finden Sie unter [Reporting Services-Beispielskript „rs.exe“ zum Migrieren von Inhalten zwischen Berichtsservern](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
```  
Public Sub Main()  
        Dim props(0) As [Property]  
        Dim setProp As New [Property]  
        setProp.Name = "EnableClientPrinting"  
        setProp.Value = “False”   
        props(0) = setProp  
        Try  
            rs.SetSystemProperties(props)  
        Catch ex As System.Web.Services.Protocols.SoapException  
            Console.Write(ex.Detail.InnerXml)  
        Catch e as Exception  
            Console.Write(e.Message)  
        End Try  
End Sub  
```

## <a name="next-steps"></a>Nächste Schritte

[GenerateDatabaseCreationScript-Methode &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabasecreationscript.md)   
[GenerateDatabaseRightsScript-Methode &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaserightsscript.md)   
[GenerateDatabaseUpgradeScript-Methode &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaseupgradescript.md)   
[Installieren von SQL Server 2016 von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
[Installieren des Reporting Services-Berichtsservers im einheitlichen Modus](~/reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)   
[Reporting Services-Berichtsserver &#40;einheitlicher Modus&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
[Eingabeaufforderungs-Hilfsprogramme für Berichtsserver &#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md)   
[Browserunterstützung für Reporting Services und Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)   
[Reporting Services-Tools](../../reporting-services/tools/reporting-services-tools.md)  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
