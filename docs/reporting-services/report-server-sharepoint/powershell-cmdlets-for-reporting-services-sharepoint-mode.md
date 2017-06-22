---
title: "PowerShell-Cmdlets für Reporting Services-SharePoint-Modus | Microsoft Docs"
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
ms.assetid: 7835bc97-2827-4215-b0dd-52f692ce5e02
caps.latest.revision: 32
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d68de45f8514de03e9804996da00d5f63d211311
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="powershell-cmdlets-for-reporting-services-sharepoint-mode"></a>PowerShell-Cmdlets für SharePoint-Modus von Reporting Services

Bei der Installation von SQL Server 2016 Reporting Services SharePoint-Modus sind PowerShell-Cmdlets installiert, um den Report Server im SharePoint-Modus zu unterstützen. Die Cmdlets decken drei Funktionalitätskategorien ab.  
  
-   Installation des gemeinsamen SharePoint-Diensts und -Proxys von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Bereitstellung und Verwaltung von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendungen und zugeordneten Proxys.  
  
-   Verwaltung von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Funktionen, z. B. Erweiterungen und Verschlüsselungsschlüssel.  

##  <a name="bkmk_cmdlet_sum"></a> Cmdlet-Zusammenfassung  
 Um die Cmdlets auszuführen, müssen Sie die SharePoint-Verwaltungsshell öffnen. Sie können auch den Editor für grafische Benutzeroberflächen **Windows PowerShell Integrated Scripting Environment (ISE)**verwenden, der in Microsoft Windows enthalten ist. Weitere Informationen finden Sie unter [Starten von Windows PowerShell unter Windows Server](http://technet.microsoft.com/library/hh847814.aspx). In den folgenden Cmdlet-Zusammenfassungen verweisen die Verweise auf die Dienstanwendung "databases" auf sämtliche mit einer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung erstellten und von ihr verwendeten Datenbanken. Dies schließt die Konfigurations- und Warnungsdatenbanken sowie temporären Datenbanken ein.  
  
 Wenn Sie bei der Eingabe der PowerShell-Beispiele eine Fehlermeldung mit etwa folgendem Wortlaut sehen:  
  
-   Install-SPRSService: Die Benennung 'Install-SPRSService' wurde nicht als  
    Name eines Cmdlets, einer Funktion, einer Skriptdatei oder eines ausführbaren Programms erkannt. Überprüfen Sie die Schreibweise des Namens, oder ob der Pfad enthalten und korrekt ist, und wiederholen Sie den Vorgang.  
  
 Eines der folgenden Probleme tritt auf:  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im SharePoint-Modus ist nicht installiert, und folglich sind auch keine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Cmdlets installiert.  
  
-   Sie haben den PowerShell-Befehl in Windows PowerShell oder Windows PowerShell ISE statt in der SharePoint-Verwaltungsshell ausgeführt. Verwenden Sie die SharePoint-Verwaltungsshell, oder fügen Sie dem Windows PowerShell-Fenster mithilfe des folgenden Befehls das SharePoint-Snap-In hinzu:  
  
    ```  
    Add-PSSnapin Microsoft.SharePoint.PowerShell  
    ```  
  
 Weitere Informationen finden Sie unter [Verwenden von Windows PowerShell zur Verwaltung von SharePoint 2013](http://technet.microsoft.com/library/ee806878.aspx).  
  
#### <a name="to-open-the-sharepoint-management-shell-and-run-cmdlets"></a>So öffnen Sie die SharePoint-Verwaltungsshell und führen Cmdlets aus  
  
1.  Klicken Sie auf die Schaltfläche **Start** .  
  
2.  Klicken Sie auf die Gruppe **Microsoft SharePoint-Produkte** .  
  
3.  Klicken Sie auf **SharePoint-Verwaltungsshell**.  
  
 Um die Befehlszeilenhilfe für ein Cmdlet anzuzeigen, verwenden Sie in der PowerShell-Eingabeaufforderung den PowerShell-Befehl "Get-Help". Beispiel:  
  
 `Get-Help Get-SPRSServiceApplicationServers`  
  
###  <a name="bkmk_sharedservice_cmdlets"></a> Shared Service- und Proxy-Cmdlets  
 Die folgende Tabelle enthält die PowerShell-Cmdlets für den gemeinsamen SharePoint-Dienst für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
|Cmdlet|Description|  
|------------|-----------------|  
|Install-SPRSService|Installiert und registriert bzw. deinstalliert den gemeinsamen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst. Dies kann nur auf dem Computer erfolgen, auf dem SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im SharePoint-Modus installiert ist. Für die Installation sind zwei Vorgänge möglich:<br /><br /> - Der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst wird in der Farm installiert.<br /><br /> - Die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstinstanz wird auf dem aktuellen Computer installiert.<br /><br /> Für die Deinstallation sind zwei Vorgänge möglich:<br /><br /> - Der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst wird auf dem aktuellen Computer deinstalliert.<br /><br /> - Der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst wird in der Farm deinstalliert.<br /><br /> <br /><br /> HINWEIS: Sind weitere Computer in der Farm vorhanden, auf denen der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst installiert ist, oder werden nach wie vor [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendungen in der Farm ausgeführt, wird eine Warnmeldung angezeigt.|  
|Install-SPRSServiceProxy|Installiert und registriert bzw. deinstalliert den Reporting Services-Dienstproxy in der SharePoint-Farm.|  
|Get-SPRSProxyUrl|Ruft die URL(s) für den Zugriff auf den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst ab.|  
|Get-SPRSServiceApplicationServers|Ruft alle Server in der lokalen SharePoint-Farm ab, die eine Installation des gemeinsamen Diensts für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] enthalten. Dieses Cmdlet ist hilfreich für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Upgrades, um die Server zu ermitteln, auf denen der freigegebene Dienst ausgeführt wird und die folglich aktualisiert werden müssen.|  
  
###  <a name="bkmk_serviceapp_cmdlets"></a> Dienstanwendungs- und Proxy-Cmdlets  
 Die folgende Tabelle enthält die PowerShell-Cmdlets für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendungen und ihre zugeordneten Proxys.  
  
|Cmdlet|Description|  
|------------|-----------------|  
|Get-SPRSServiceApplication|Ruft mindestens ein [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendungsobjekt ab.|  
|New-SPRSServiceApplication|Erstellen Sie eine neue Reporting Services-Dienstanwendung und zugeordnete Datenbanken.<br /><br /> LogonType-Parameter: Gibt an, ob der Berichtsserver das SSRS-Anwendungspoolkonto oder einen SQL Server-Anmeldenamen für den Zugriff auf die Berichtsserver-Datenbank verwendet. Gültige Werte sind:<br /><br /> 0 Windows-Authentifizierung<br /><br /> 1 SQL Server<br /><br /> 2 Anwendungspoolkonto (Standard)|  
|Remove-SPRSServiceApplication|Entfernt die angegebene Reporting Services-Dienstanwendung. Dadurch werden auch die zugeordneten Datenbanken entfernt.|  
|Set-SPRSServiceApplication|Bearbeitet die Eigenschaften einer vorhandenen Reporting Services-Dienstanwendung.|  
|New-SPRSServiceApplicationProxy|Erstellt einen neuen Proxy für die Reporting Services-Dienstanwendung.|  
|Get-SPRSServiceApplicationProxy|Ruft mindestens einen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendungsproxy ab.|  
|Dismount-SPRSDatabase|Hebt die Einbindung der Dienstanwendungsdatenbank für eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung auf.|  
|Remove-SPRSDatabase|Entfernen Sie die Dienstanwendungsdatenbanken für eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung.|  
|Set-SPRSDatabase|Legt die Eigenschaften der einer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung zugeordneten Datenbanken fest.|  
|Mount-SPRSDatabase|Bindet Datenbanken für eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung ein.|  
|New-SPRSDatabase|Erstellen Sie neue Dienstanwendungsdatenbanken für die angegebene [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung.|  
|Get-SPRSDatabaseCreationScript|Gibt für eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung das Datenbankerstellungsskript auf dem Bildschirm aus. Sie können dann das Skript in SQL Server Management Studio ausführen.|  
|Get-SPRSDatabase|Ruft mindestens eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendungsdatenbank ab. Rufen Sie über den Befehl die ID der Dienstanwendungsdatenbank ab, damit Sie anhand des Set-SPRSDatabase-Cmdlets Eigenschaften ändern können, beispielsweise das `querytimeout`. Sehen Sie sich das Beispiel unter dem Thema [Abrufen und Festlegen von Eigenschaften für die Reporting Services-Anwendungsdatenbank](#bkmk_example_db_properties)an.|  
|Get-SPRSDatabaseRightsScript|Gibt für eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung das Skript für Datenbankrechte auf dem Bildschirm aus. Es fordert die Eingabe des gewünschten Benutzers und der Datenbank und gibt dann Transact-SQL zurück, das zum Ändern von Berechtigungen ausgeführt werden kann. Sie können dann dieses Skript in SQL Server Management Studio ausführen.|  
|Get-SPRSDatabaseUpgradeScript|Gibt ein Datenbankupgradeskript auf dem Bildschirm aus. Das Skript führt ein Upgrade der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendungsdatenbanken auf die Datenbankversion der aktuellen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Installation durch.|  
  
###  <a name="bkmk_ssrsfeatures_cmdlets"></a> Benutzerdefinierte Reporting Services-Funktionalitäts-Cmdlets  
  
|Cmdlet|Description|  
|------------|-----------------|  
|Update-SPRSEncryptionKey|Aktualisiert den Verschlüsselungsschlüssel für die angegebene Reporting Services-Dienstanwendung und verschlüsselt die Daten erneut.|  
|Restore-SPRSEncryptionKey|Stellt einen zuvor gesicherten Verschlüsselungsschlüssel für eine Reporting Services-Dienstanwendung wieder her.|  
|Remove-SPRSEncryptedData|Löscht die verschlüsselten Daten für die angegebene Reporting Services-Dienstanwendung.|  
|Backup-SPRSEncryptionKey|Sichert den Verschlüsselungsschlüssel für die angegebene Reporting Services-Dienstanwendung.|  
|New-SPRSExtension|Registriert eine neue Erweiterung bei einer Reporting Services-Dienstanwendung.|  
|Set-SPRSExtension|Legt die Eigenschaften einer vorhandenen Reporting Services-Erweiterung fest.|  
|Remove-SPRSExtension|Entfernt eine Erweiterung aus einer Reporting Services-Dienstanwendung.|  
|Get-SPRSExtension|Ruft mindestens eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Erweiterung für eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung ab.<br /><br /> Gültige Werte sind:<br /><br /> <br /><br /> Delivery<br /><br /> DeliveryUI<br /><br /> Render<br /><br /> Daten<br /><br /> Security<br /><br /> Authentifizierung<br /><br /> EventProcessing<br /><br /> Berichtselemente<br /><br /> Designer<br /><br /> ReportItemDesigner<br /><br /> ReportItemConverter<br /><br /> ReportDefinitionCustomization|  
|Get-SPRSSite|Ruft die SharePoint-Websites abhängig davon ab, ob die Funktion "ReportingService" aktiviert ist. Standardmäßig werden Websites zurückgegeben, für die die Funktion "ReportingService" aktiviert ist.|  
  
##  <a name="bkmk_basic_samples"></a> PowerShell-Basisbeispiele für Reporting Services  
 Gibt eine Liste von Cmdlets zurück, die "SPRS" im Namen enthalten. Dies entspricht der vollständigen Liste mit [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Cmdlets.  
  
```  
Get-command –noun *SPRS*  
```  
  
 Alternativ erfolgt die Weiterleitung an eine Textdatei namens "commandlist.txt" mit genaueren Details.  
  
```  
Get-command -noun *SPRS* | Select name, definition | Format-List | Out-File c:\commandlist.txt  
```  
  
 Installieren Sie den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint-Dienst und -Dienstproxy.  
  
```  
Install-SPRSService  
```  
  
```  
Install-SPRSServiceProxy  
```  
  
 Starten Sie den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst.  
  
```  
get-spserviceinstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
```  
  
 Geben Sie den folgenden Befehl in der SharePoint-Verwaltungsshell ein, um eine gefilterte Zeilenliste aus der Protokolldatei abzurufen. Durch den Befehl werden Zeilen herausgefiltert, die "ssrscustomactionerror" enthalten. Dieses Beispiel bezieht sich auf die Protokolldatei, die bei der Installation von "rssharepoint.msi" erstellt wurde.  
  
```  
Get-content -path C:\Users\testuser\AppData\Local\Temp\rs_sp_0.log | select-string "ssrscustomactionerror"  
```  
  
##  <a name="bkmk_detailedsamples"></a> Detaillierte PowerShell-Beispiele für Reporting Services  
 Zusätzlich zu den folgenden Beispielen finden Sie weitere Beispiele im Abschnitt "Windows PowerShell-Skript" im Thema [Windows PowerShell script for Steps 1–4](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md#bkmk_full_script).  
  
###  <a name="bkmk_example_create_service_application"></a> Erstellen einer Reporting Services-Dienstanwendung und eines entsprechenden Proxys  
 Dieses Beispielskript führt die folgenden Tasks aus:  
  
1.  Erstellt eine Reporting Services-Dienstanwendung und einen entsprechenden Proxy. Das Skript geht davon aus, dass der Anwendungspool "Mein Anwendungspool" bereits vorhanden ist.  
  
2.  Hinzufügen des Proxys zur Standardproxygruppe  
  
3.  Gewähren Sie der Dienstanwendung Zugriff auf die Inhaltsdatenbank der Webanwendung (Port 80). Das Skript geht davon aus Standort `http://sitename` ist bereits vorhanden.  
  
```  
# Create service application and service application proxy  
$appPool = Get-SPServiceApplicationPool “My App Pool”  
$serviceApp = New-SPRSServiceApplication “My RS Service App” –ApplicationPool $appPool  
$serviceAppProxy = New-SPRSServiceApplicationProxy –Name “My RS Service App Proxy” –ServiceApplication $serviceApp  
  
# Add service application proxy to default proxy group.  Any web application that uses the default proxy group will now be able to use this service application.  
Get-SPServiceApplicationProxyGroup –default | Add-SPServiceApplicationProxyGroupMember –Member $serviceAppProxy  
  
# Grant application pool account access to the port 80 web application’s content database.  
$webApp = Get-SPWebApplication “http://sitename”  
$appPoolAccountName = $appPool.ProcessAccount.LookupName()  
$webApp.GrantAccessToProcessIdentity($appPoolAccountName)  
  
```  
  
###  <a name="bkmk_example_delivery_extension"></a> Überprüfen und Aktualisieren einer Reporting Services-Übermittlungserweiterung  
 Das folgende PowerShell-Skript-Beispiel aktualisiert die Konfiguration der Berichtsserver-E-Mail-Übermittlungserweiterung für die Dienstanwendung mit dem Namen `My RS Service App`. Aktualisieren Sie die Werte für den SMTP-Server (`<email server name>`) und für den E-Mail-Absenderalias „FROM“ (`<your FROM email address>`).  
  
```  
$app=get-sprsserviceapplication -Name "My RS Service App"  
$emailCfg = Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml   
$emailXml = [xml]$emailCfg   
$emailXml.SelectSingleNode("//SMTPServer").InnerText = “<email server name>”  
$emailXml.SelectSingleNode("//SendUsing").InnerText = "2"  
$emailXml.SelectSingleNode("//SMTPAuthenticate").InnerText = "2"  
$emailXml.SelectSingleNode("//From").InnerText = '<your FROM email address>'  
Set-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" -ExtensionConfiguration $emailXml.OuterXml  
```  
  
 Wenn Sie im oben genannten Beispiel den genauen Namen der Dienstanwendung nicht kennen, besteht die Möglichkeit, die erste Anweisung umzuschreiben, um die Dienstanwendung auf Grundlage einer Suche nach dem Teilnamen abzurufen. Beispiel:  
  
```  
$app=get-sprsserviceapplication | where {$_.name -like " ssrs_testapp *"}  
```  
  
 Das folgende Skript gibt die aktuellen Konfigurationswerte für die Berichtsserver-E-Mail-Übermittlungserweiterung der Dienstanwendung namens "Reporting Services-Anwendung" zurück. Im ersten Schritt wird der Wert der Variablen $app auf das Objekt der Dienstanwendung mit dem Namen "Meine RS-Dienstanwendung" festgelegt.  
  
 Die zweite Anweisung ruft die Übermittlungserweiterung "Berichtsserver-E-Mail" für das Dienstanwendungsobjekt in der Variablen $app ab und wählt configurationXML aus.  
  
```  
$app=get-sprsserviceapplication –Name "Reporting Services Application"  
Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
```  
  
 Sie können die beiden oben stehenden Anweisungen auch in einer Anweisung zusammenfassen:  
  
```  
get-sprsserviceapplication –Name "Reporting Services Application" | Get-SPRSExtension -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
```  
  
###  <a name="bkmk_example_db_properties"></a> Abrufen und Festlegen von Eigenschaften für die Reporting Services-Anwendungsdatenbank  
 Mit dem folgenden Beispiel wird eine Liste von Datenbanken und Eigenschaften zurückgegeben, sodass Sie die Datenbank-GUID (ID) bestimmen können, die Sie anschließend zum Festlegen des Befehls angeben. Eine vollständige Liste der Eigenschaften erhalten Sie anhand von `Get-SPRSDatabase | format-list`.  
  
```  
get-SPRSDatabase | select id, querytimeout,connectiontimeout, status, server, ServiceInstance   
```  
  
 Unten ist ein Beispiel für die Ausgabe angegeben. Bestimmen Sie die ID für die zu ändernde Datenbank und verwenden Sie die ID im SET-Cmdlet.  
  
-   `Id                : 56f8d1bc-cb04-44cf-bd41-a873643c5a14`  
  
     `QueryTimeout      : 120`  
  
     `ConnectionTimeout : 15`  
  
     `Status            : Online`  
  
     `Server            : SPServer Name=uetestb01`  
  
     `ServiceInstance   : SPDatabaseServiceInstance`  
  
```  
Set-SPRSDatabase –identity 56f8d1bc-cb04-44cf-bd41-a873643c5a14 -QueryTimeout 300  
```  
  
 Um zu überprüfen, ob der Wert festgelegt ist, führen Sie das GET-Cmdlet erneut aus.  
  
```  
Get-SPRSDatabase –identity 56f8d1bc-cb04-44cf-bd41-a873643c5a14 | select id, querytimeout,connectiontimeout, status, server, ServiceInstance  
```  
  
###  <a name="bkmk_example_list_data_extensions"></a> Auflisten von Reporting Services-Datenerweiterungen  
 Das folgende Beispiel durchläuft alle [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendungen und listet aktuelle Datenerweiterungen für diese auf.  
  
```  
$apps = Get-SPRSServiceApplication  
foreach ($app in $apps)   
{  
Write-host -ForegroundColor "yellow" Service App Name $app.Name  
Get-SPRSExtension -identity $app -ExtensionType “Data” | select name,extensiontype | Format-Table -AutoSize  
}  
```  
  
 **Beispielausgabe:**  
  
-   `Name           ExtensionType`  
  
     `----           -------------`  
  
     `SQL                     Data`  
  
     `SQLAZURE                Data`  
  
     `SQLPDW                  Data`  
  
     `OLEDB                   Data`  
  
     `OLEDB-MD                Data`  
  
     `ORACLE                  Data`  
  
     `ODBC                    Data`  
  
     `XML                     Data`  
  
     `SHAREPOINTLIST          Data`  
  
###  <a name="bkmk_change_subscription_owner"></a> Ändern und Auflisten von Reporting Services-Abonnementbesitzern  
 Siehe [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md).  
  
## <a name="next-steps"></a>Nächste Schritte

[Verwenden von PowerShell, um Reporting Services-Abonnenten zu ändern und aufzulisten sowie ein Abonnement auszuführen](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
[Prüfliste: Verwenden von PowerShell zum Überprüfen von PowerPivot für SharePoint](../../analysis-services/instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint.md)   
[Abrufen von SQL Server PowerShell-Hilfe](../../relational-databases/scripting/get-help-sql-server-powershell.md)   
[CodePlex-SharePoint-Verwaltungs-PowerShell-Skripts](http://sharepointpsscripts.codeplex.com/)   

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
