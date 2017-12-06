---
title: "PowerShell-Cmdlets für den SharePoint-Modus von Reporting Services | Microsoft-Dokumentation"
ms.custom: 
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server-sharepoint
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 96e9ea12df36219b11fe74e3328e6817b03471e9
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="powershell-cmdlets-for-reporting-services-sharepoint-mode"></a>PowerShell-Cmdlets für den SharePoint-Modus von Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Bei der Installation von SQL Server 2016 Reporting Services im SharePoint-Modus werden auch PowerShell-Cmdlets installiert, die Unterstützung für Berichtsserver im SharePoint-Modus bieten. Die Cmdlets decken drei Funktionalitätskategorien ab.  
  
-   Installation des gemeinsamen SharePoint-Diensts und -Proxys von Reporting Services.  
  
-   Bereitstellung und Verwaltung von Reporting Services-Dienstanwendungen und zugeordneten Proxys.  
  
-   Verwaltung von Reporting Services-Funktionen wie Erweiterungen und Verschlüsselungsschlüssel.  

> [!NOTE]
> Die Integration von Reporting Services in SharePoint ist nach SQL Server 2016 nicht mehr möglich.

## <a name="cmdlet-summary"></a>Cmdlet-Zusammenfassung

 Um die Cmdlets auszuführen, müssen Sie die SharePoint-Verwaltungsshell öffnen. Sie können auch den Editor für grafische Benutzeroberflächen **Windows PowerShell Integrated Scripting Environment (ISE)**verwenden, der in Microsoft Windows enthalten ist. Weitere Informationen finden Sie unter [Starting Windows PowerShell on Windows Server](http://technet.microsoft.com/library/hh847814.aspx)verwenden, der in Microsoft Windows enthalten ist. In den folgenden Zusammenfassungen von Cmdlets verweisen die Verweise auf die Dienstanwendung „Databases“ auf sämtliche mit einer Reporting Services-Dienstanwendung erstellten und von ihr verwendeten Datenbanken. Dies schließt die Konfigurations- und Warnungsdatenbanken sowie temporären Datenbanken ein.  
  
 Wenn Sie bei der Eingabe der PowerShell-Beispiele eine Fehlermeldung mit etwa folgendem Wortlaut sehen:  
  
-   Install-SPRSService: Die Benennung 'Install-SPRSService' wurde nicht als  
    Name eines Cmdlets, einer Funktion, einer Skriptdatei oder eines ausführbaren Programms erkannt. Überprüfen Sie die Schreibweise des Namens, oder ob der Pfad enthalten und korrekt ist, und wiederholen Sie den Vorgang.  
  
 Eines der folgenden Probleme tritt auf:  
  
-   Der SharePoint-Modus von Reporting Services ist nicht installiert, weshalb auch die Reporting Services-Cmdlets nicht installiert sind.  
  
-   Sie haben den PowerShell-Befehl in Windows PowerShell oder Windows PowerShell ISE statt in der SharePoint-Verwaltungsshell ausgeführt. Verwenden Sie die SharePoint-Verwaltungsshell, oder fügen Sie dem Windows PowerShell-Fenster mithilfe des folgenden Befehls das SharePoint-Snap-In hinzu:  
  
    ```  
    Add-PSSnapin Microsoft.SharePoint.PowerShell  
    ```  
  
 Weitere Informationen finden Sie unter [Verwenden von Windows PowerShell zur Verwaltung von SharePoint 2013](http://technet.microsoft.com/library/ee806878.aspx)verwenden, der in Microsoft Windows enthalten ist.  
  
### <a name="open-the-sharepoint-management-shell-and-run-cmdlets"></a>Öffnen der SharePoint-Verwaltungsshell und Ausführen von Cmdlets
  
1.  Klicken Sie auf die Schaltfläche **Start** .  
  
2.  Klicken Sie auf die Gruppe **Microsoft SharePoint-Produkte** .  
  
3.  Klicken Sie auf **SharePoint-Verwaltungsshell**.  
  
 Um die Befehlszeilenhilfe für ein Cmdlet anzuzeigen, verwenden Sie in der PowerShell-Eingabeaufforderung den PowerShell-Befehl "Get-Help". Beispiel:  
  
 `Get-Help Get-SPRSServiceApplicationServers`  
  
##  <a name="shared-service-and-proxy-cmdlets"></a>Cmdlets des gemeinsamen Diensts und Proxys

 Die folgende Tabelle enthält die PowerShell-Cmdlets für den freigegebenen SharePoint-Dienst für Reporting Services.  
  
|Cmdlet|Description|  
|------------|-----------------|  
|Install-SPRSService|Installiert und registriert bzw. deinstalliert den freigegebenen Reporting Services-Dienst. Dieser Schritt kann nur auf einem Computer erfolgen, auf dem eine SQL Server Reporting Services-Installation im SharePoint-Modus vorhanden ist. Für die Installation sind zwei Vorgänge möglich:<br /><br /> – Der Reporting Services-Dienst wird in der Farm installiert.<br /><br /> – Die Reporting Services-Dienstinstanz wird auf dem aktuellen Computer installiert.<br /><br /> Für die Deinstallation sind zwei Vorgänge möglich:<br /><br /> – Der Reporting Services-Dienst wird auf dem aktuellen Computer deinstalliert.<br /><br /> – Der Reporting Services-Dienst wird in der Farm deinstalliert.<br /><br /> <br /><br /> Wenn die Farm andere Computer umfasst, auf denen der Reporting Services-Dienst installiert ist, oder wenn immer noch Reporting Services-Dienstanwendungen in der Farm ausgeführt werden, wird eine Fehlermeldung angezeigt.|  
|Install-SPRSServiceProxy|Installiert und registriert bzw. deinstalliert den Reporting Services-Dienstproxy in der SharePoint-Farm.|  
|Get-SPRSProxyUrl|Ruft die URL(s) für den Zugriff auf den Reporting Services-Dienst ab.|  
|Get-SPRSServiceApplicationServers|Ruft alle Server in der lokalen SharePoint-Farm ab, in der eine Installation des freigegebenen Reporting Services-Diensts enthalten ist. Dieses Cmdlet ist hilfreich für Reporting Services-Upgrades, um die Server zu ermitteln, auf denen der freigegebene Dienst ausgeführt wird, und die folglich aktualisiert werden müssen.|  
  
## <a name="service-application-and-proxy-cmdlets"></a>Dienstanwendungs- und Proxy-Cmdlets

 Die folgende Tabelle enthält die PowerShell-Cmdlets für Reporting Services-Dienstanwendungen und ihre zugeordneten Proxys.  
  
|Cmdlet|Description|  
|------------|-----------------|  
|Get-SPRSServiceApplication|Ruft mindestens ein Objekt für eine Reporting Services-Anwendung ab.|  
|New-SPRSServiceApplication|Erstellen Sie eine neue Reporting Services-Dienstanwendung und zugeordnete Datenbanken.<br /><br /> LogonType-Parameter: Gibt an, ob der Berichtsserver das SSRS-Anwendungspoolkonto oder einen SQL Server-Anmeldenamen für den Zugriff auf die Berichtsserver-Datenbank verwendet. Gültige Werte sind:<br /><br /> 0 Windows-Authentifizierung<br /><br /> 1 SQL Server<br /><br /> 2 Anwendungspoolkonto (Standard)|  
|Remove-SPRSServiceApplication|Entfernt die angegebene Reporting Services-Dienstanwendung. Dadurch werden auch die zugeordneten Datenbanken entfernt.|  
|Set-SPRSServiceApplication|Bearbeitet die Eigenschaften einer vorhandenen Reporting Services-Dienstanwendung.|  
|New-SPRSServiceApplicationProxy|Erstellt einen neuen Proxy für die Reporting Services-Dienstanwendung.|  
|Get-SPRSServiceApplicationProxy|Ruft mindestens einen Proxy für eine Reporting Services-Anwendung ab.|  
|Dismount-SPRSDatabase|Hebt die Einbindung der Dienstanwendungs-Datenbanken für eine Reporting Services-Dienstanwendung auf.|  
|Remove-SPRSDatabase|Entfernt die Einbindung der Dienstanwendungs-Datenbanken für eine Reporting Services-Dienstanwendung.|  
|Set-SPRSDatabase|Legt die Eigenschaften der Datenbanken fest, die einer Reporting Services-Dienstanwendung zugeordnet sind.|  
|Mount-SPRSDatabase|Bindet Datenbanken in eine Reporting Services-Dienstanwendung ein.|  
|New-SPRSDatabase|Erstellt neue Dienstanwendungs-Datenbanken für die angegebene Reporting Services-Dienstanwendung.|  
|Get-SPRSDatabaseCreationScript|Gibt das Datenbankerstellungsskript an eine Reporting Services-Dienstanwendung auf dem Bildschirm aus. Sie können dann das Skript in SQL Server Management Studio ausführen.|  
|Get-SPRSDatabase|Ruft mindestens eine Datenbank einer Reporting Services-Dienstanwendung ab. Rufen Sie über den Befehl die ID der Dienstanwendungsdatenbank ab, damit Sie anhand des Set-SPRSDatabase-Cmdlets Eigenschaften ändern können, beispielsweise das `querytimeout`. Sehen Sie sich das Beispiel unter dem Thema [Abrufen und Festlegen von Eigenschaften für die Reporting Services-Anwendungsdatenbank](#bkmk_example_db_properties)an.|  
|Get-SPRSDatabaseRightsScript|Gibt das Datenbankrechte-Skript für die Datenbank einer Reporting Services-Dienstanwendung auf dem Bildschirm aus. Es fordert die Eingabe des gewünschten Benutzers und der Datenbank und gibt dann Transact-SQL zurück, das zum Ändern von Berechtigungen ausgeführt werden kann. Sie können dann dieses Skript in SQL Server Management Studio ausführen.|  
|Get-SPRSDatabaseUpgradeScript|Gibt ein Datenbankupgradeskript auf dem Bildschirm aus. Das Skript führt ein Upgrade der Reporting Services-Dienstanwendungsdatenbanken auf die Datenbankversion der aktuellen Reporting Services-Installation durch.|  
  
## <a name="reporting-services-custom-runctionality-cmdlets"></a>Benutzerdefinierte Reporting Services-Funktionalitäts-Cmdlets
  
|Cmdlet|Description|  
|------------|-----------------|  
|Update-SPRSEncryptionKey|Aktualisiert den Verschlüsselungsschlüssel für die angegebene Reporting Services-Dienstanwendung und verschlüsselt die Daten erneut.|  
|Restore-SPRSEncryptionKey|Stellt einen zuvor gesicherten Verschlüsselungsschlüssel für eine Reporting Services-Dienstanwendung wieder her.|  
|Remove-SPRSEncryptedData|Löscht die verschlüsselten Daten für die angegebene Reporting Services-Dienstanwendung.|  
|Backup-SPRSEncryptionKey|Sichert den Verschlüsselungsschlüssel für die angegebene Reporting Services-Dienstanwendung.|  
|New-SPRSExtension|Registriert eine neue Erweiterung bei einer Reporting Services-Dienstanwendung.|  
|Set-SPRSExtension|Legt die Eigenschaften einer vorhandenen Reporting Services-Erweiterung fest.|  
|Remove-SPRSExtension|Entfernt eine Erweiterung aus einer Reporting Services-Dienstanwendung.|  
|Get-SPRSExtension|Ruft mindestens eine Reporting Services-Erweiterung für eine Reporting Services-Dienstanwendung ab.<br /><br /> Gültige Werte sind:<br /><br /> <br /><br /> Delivery<br /><br /> DeliveryUI<br /><br /> Render<br /><br /> Daten<br /><br /> Security<br /><br /> Authentifizierung<br /><br /> EventProcessing<br /><br /> Berichtselemente<br /><br /> Designer<br /><br /> ReportItemDesigner<br /><br /> ReportItemConverter<br /><br /> ReportDefinitionCustomization|  
|Get-SPRSSite|Ruft die SharePoint-Websites abhängig davon ab, ob die Funktion "ReportingService" aktiviert ist. Standardmäßig werden Websites zurückgegeben, für die die Funktion "ReportingService" aktiviert ist.|  
  
## <a name="basic-samples"></a>Basisbeispiele

 Gibt eine Liste von Cmdlets zurück, die "SPRS" im Namen enthalten. Diese Liste enthält sämtliche Reporting Services-Cmdlets.  
  
```  
Get-command –noun *SPRS*  
```  
  
 Alternativ erfolgt die Weiterleitung an eine Textdatei namens "commandlist.txt" mit genaueren Details.  
  
```  
Get-command -noun *SPRS* | Select name, definition | Format-List | Out-File c:\commandlist.txt  
```  
  
 Installieren Sie den Reporting Services-SharePoint-Dienst und den -Dienstproxy.  
  
```  
Install-SPRSService  
```  
  
```  
Install-SPRSServiceProxy  
```  
  
 Starten Sie den Reporting Services-Dienst  
  
```  
get-spserviceinstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
```  
  
 Geben Sie den folgenden Befehl in der SharePoint-Verwaltungsshell ein, um eine gefilterte Zeilenliste aus der Protokolldatei abzurufen. Durch den Befehl werden Zeilen herausgefiltert, die "ssrscustomactionerror" enthalten. Dieses Beispiel bezieht sich auf die Protokolldatei, die bei der Installation von "rssharepoint.msi" erstellt wurde.  
  
```  
Get-content -path C:\Users\testuser\AppData\Local\Temp\rs_sp_0.log | select-string "ssrscustomactionerror"  
```  
  
## <a name="detailed-samples"></a>Ausführliche Beispiele

 Zusätzlich zu den folgenden Beispielen finden Sie weitere Beispiele im Abschnitt "Windows PowerShell-Skript" im Thema [Windows PowerShell script for Steps 1–4](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md#bkmk_full_script).  
  
### <a name="create-a-reporting-services-service-application-and-proxy"></a>Erstellen einer Reporting Services-Dienstanwendung und eines entsprechenden Proxys

 Dieses Beispielskript führt die folgenden Tasks aus:  
  
1.  Erstellt eine Reporting Services-Dienstanwendung und einen entsprechenden Proxy. Das Skript geht davon aus, dass der Anwendungspool "Mein Anwendungspool" bereits vorhanden ist.  
  
2.  Hinzufügen des Proxys zur Standardproxygruppe  
  
3.  Gewähren Sie der Dienstanwendung Zugriff auf die Inhaltsdatenbank der Webanwendung (Port 80). Das Skript geht davon aus, dass die Website `http://sitename` bereits vorhanden ist.  
  
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
  
### <a name="review-and-update-a-reporting-services-delivery-extension"></a>Überprüfen und Aktualisieren einer Reporting Services-Übermittlungserweiterung

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
  
### <a name="get-and-set-properties-of-the-reporting-service-application-database"></a>Abrufen und Festlegen von Eigenschaften der Reporting Services-Anwendungsdatenbank

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
  
### <a name="list-reporting-services-data-extensions"></a>Auflisten von Reporting Services-Datenerweiterungen

 Das folgende Beispiel durchläuft alle Reporting Services-Dienstanwendungen und listet aktuelle Datenerweiterungen für diese auf.  
  
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
  
### <a name="change-and-list-reporting-services-subscription-owners"></a>Ändern und Auflisten von Reporting Services-Abonnementbesitzern

 Weitere Informationen finden Sie unter [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription (Verwenden von PowerShell zum Ändern und Auflisten von Reporting Services-Abonnementbesitzern und zum Ausführen eines Abonnements)](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md).  
  
## <a name="next-steps"></a>Nächste Schritte

[Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription (Verwenden von PowerShell zum Ändern und Auflisten von Reporting Services-Abonnementbesitzern und zum Ausführen eines Abonnements)](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
[CheckList: Use PowerShell to verify Power Pivot for SharePoint (Prüfliste: Überprüfen von Power Pivot für SharePoint mithilfe von PowerShell)](../../analysis-services/instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint.md)   
[Get Help SQL Server PowerShell (Hilfe für SQL Server PowerShell)](../../relational-databases/scripting/get-help-sql-server-powershell.md)   

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
