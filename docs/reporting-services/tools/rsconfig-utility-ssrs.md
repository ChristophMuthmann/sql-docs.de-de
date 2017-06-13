---
title: RSConfig-Hilfsprogramm (SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [Reporting Services], configuring
- rsconfig utility
- report servers [Reporting Services], connections
- command prompt utilities [Reporting Services]
- command prompt utilities [SQL Server], rsconfig
ms.assetid: 84e45a2f-3ca6-4c16-8259-c15ff49d72ad
caps.latest.revision: 47
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 68b5e38f2b4e71298fbf7b6ec6970fc7824c3cde
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="rsconfig-utility-ssrs"></a>rsconfig-Hilfsprogramm (SSRS)
  Mit dem Hilfsprogramm **rsconfig.exe** werden Verbindungs- und Kontowerte in der Datei „RSReportServer.config“ verschlüsselt und gespeichert. Die verschlüsselten Werte umfassen Verbindungsinformationen für Berichtsserver-Datenbanken und Kontowerte, die für die unbeaufsichtigte Berichtsverarbeitung verwendet werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
rsconfig {-?}  
{–cconnection}  
{–eunattendedaccount}  
{–mcomputername}  
{–iinstancename}  
{–sservername}  
{–ddatabasename}  
{–aauthmethod}  
{-uusername}  
{-ppassword}  
{-ttrace}  
```  
  
## <a name="arguments"></a>Argumente  
  
|Begriff|Optional/erforderlich|Definition|  
|----------|------------------------|----------------|  
|**-?**|Optional.|Zeigt die Syntax der Argumente von Rsconfig.exe an.|  
|**-c**|Erforderlich, wenn das **-e** -Argument nicht verwendet wird.|Gibt die Verbindungszeichenfolge, die Anmeldeinformationen und die Datenquellenwerte an, die verwendet werden, um die Verbindung zwischen einem Berichtsserver und der Berichtsserver-Datenbank herzustellen.<br /><br /> Dieses Argument enthält keinen Wert. Es müssen jedoch weitere Argumente angegeben werden, um alle erforderlichen Verbindungswerte für dieses Argument bereitzustellen.<br /><br /> Zu den Argumenten, die Sie mit **-c** angeben können, gehören **-m**, **-s**, **-i**,**-d**,**-a**,**-u**,**-p**und**-t**.|  
|**-e**|Erforderlich, wenn das **-c** -Argument nicht verwendet wird.|Gibt das Konto für die unbeaufsichtigte Berichtsausführung an.<br /><br /> Dieses Argument enthält keinen Wert. Sie müssen jedoch zusätzliche Argumente in der Befehlszeile einschließen, um die in der Konfigurationsdatei verschlüsselten Werte anzugeben.<br /><br /> Zu den Argumenten, die Sie mit **-e** angeben können, gehören **-u** und **-p**. Darüber hinaus können Sie auch **-t**festlegen.|  
|**-m**  *computername*|Erforderlich, wenn Sie eine Remote-Berichtsserverinstanz konfigurieren.|Gibt den Namen des Computers an, der den Berichtsserver hostet. Wird dieses Argument nicht angegeben, wird der Standardwert **localhost**verwendet.|  
|**-s**  *servername*|Erforderlich.|Gibt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz an, die die Berichtsserver-Datenbank hostet.|  
|**-i**  *instancename*|Erforderlich, wenn Sie benannte Instanzen verwenden.|Wenn Sie eine benannte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz zum Hosten der Berichtsserver-Datenbank verwenden, gibt dieser Wert die benannte Instanz an.|  
|**-d**  *databasename*|Erforderlich.|Gibt den Namen der Berichtsserver-Datenbank an.|  
|**-a**  *authmethod*|Erforderlich.|Gibt die Authentifizierungsmethode an, die vom Berichtsserver zum Herstellen der Verbindung mit der Berichtsserver-Datenbank verwendet wird. Gültige Werte sind **Windows** oder **SQL** (die Groß- und Kleinschreibung wird bei diesem Argument nicht berücksichtigt).<br /><br /> **Windows** gibt an, dass der Berichtsserver die Windows-Authentifizierung verwendet.<br /><br /> **SQL** gibt an, dass der Berichtsserver die SQL Server-Authentifizierung verwendet.|  
|**-u** *[Domäne\\]Benutzername*|Erforderlich, wenn **-e** verwendet wird; optional, wenn **-c** angegeben wird.|Gibt ein Benutzerkonto für die Verbindung mit der Berichtsserver-Datenbank oder für ein Konto für unbeaufsichtigte Vorgänge an.<br /><br /> Bei Angabe von **rsconfig -e**ist dieses Argument erforderlich. Bei dem Konto muss es sich um ein Domänenbenutzerkonto handeln.<br /><br /> Bei Angabe von **rsconfig -c** und **-a SQL**muss mit diesem Argument ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldename angegeben werden.<br /><br /> Bei Angabe von **rsconfig -c** und **-a Windows**können mit diesem Argument Anmeldeinformationen für ein Domänenbenutzerkonto, ein integriertes Konto oder ein Dienstkonto angegeben werden. Wenn Sie ein Domänenkonto angeben, geben Sie *Domäne* und *Benutzername* im Format *Domäne\Benutzername*an. Wenn Sie ein integriertes Konto verwenden, ist dieses Argument optional. Wenn Sie die Anmeldeinformationen für ein Dienstkonto verwenden möchten, geben Sie dieses Argument nicht an.|  
|**-p**  *password*|Erforderlich, wenn **-u** angegeben wird.|Gibt das Kennwort an, das mit dem *Benutzername* -Argument verwendet wird. Sie können für dieses Argument einen leeren Wert festlegen, falls für das Konto kein Kennwort erforderlich ist. Bei Domänenkonten wird bei diesem Wert die Groß- und Kleinschreibung beachtet.|  
|**-t**|Optional.|Schreibt Fehlermeldungen in das Ablaufverfolgungsprotokoll. Dieses Argument enthält keinen Wert. Weitere Informationen finden Sie unter [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md).|  
  
## <a name="permissions"></a>Berechtigungen  
 Auf dem Computer, der den von Ihnen konfigurierten Berichtsserver hostet, müssen Sie als lokaler Administrator angemeldet sein.  
  
## <a name="file-location"></a>Dateispeicherort  
 „Rsconfig.exe“ befindet sich unter **\Programme\Microsoft SQL Server\110\Tools\Binn**. Sie können das Hilfsprogramm von einem beliebigen Ordner im Dateisystem ausführen.  
  
## <a name="remarks"></a>Hinweise  
 Es gibt zwei Gründe für die Verwendung von Rsconfig.exe:  
  
-   Ändern der Verbindungsinformationen, die ein Berichtsserver für die Verbindung mit einer Berichtsserver-Datenbank verwendet.  
  
-   Konfiguration eines besonderen Kontos, das der Berichtsserver für die Anmeldung an einem Remote-Datenbankserver verwendet, wenn keine anderen Anmeldeinformationen verfügbar sind.  
  
 Sie können das Hilfsprogramm**rsconfig** auf einer lokalen Instanz oder auf einer Remoteinstanz von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]ausführen. Sie können das Hilfsprogramm **rsconfig** nicht verwenden, um bereits festgelegte Werte zu entschlüsseln oder anzuzeigen.  
  
 Bevor Sie dieses Hilfsprogramm ausführen, müssen Sie die Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) auf dem Computer installieren, den Sie konfigurieren.  
  
## <a name="examples"></a>Beispiele  
 Die folgenden Beispiele veranschaulichen mögliche Verwendungsweisen von **rsconfig**.  
  
#### <a name="specifying-a-domain-user-account"></a>Angeben eines Domänenbenutzerkontos  
 In diesem Beispiel wird gezeigt, wie ein Berichtsserver so konfiguriert wird, dass er ein Domänenbenutzerkonto für die Verbindung mit einer lokalen Berichtsserver-Datenbank verwendet.  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows -u <MYDOMAIN\MYACCOUNT> -p <PASSWORD>  
```  
  
#### <a name="specifying-a-sql-server-database-user-account"></a>Angeben eines Benutzerkontos für eine SQL Server-Datenbank  
 In diesem Beispiel wird gezeigt, wie ein Berichtsserver so konfiguriert wird, dass er einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldenamen für die Verbindung mit einer Datenbank auf einem Remoteberichtsserver verwendet.  
  
```  
rsconfig -c -m <REMOTECOMPUTERNAME> -s <SQLSERVERNAME> -d reportserver -a SQL -u SA -p <SAPASSWORD>  
```  
  
#### <a name="specifying-a-built-in-account"></a>Angeben eines integrierten Kontos  
 In diesem Beispiel wird gezeigt, wie ein Berichtsserver so konfiguriert wird, dass er ein integriertes Konto für die Verbindung mit einer lokalen Berichtsserver-Datenbank verwendet. Beachten Sie, dass **-u** nicht verwendet wird. Beispielwerte für unterstützte integrierte Konten umfassen NT AUTHORITY\SYSTEM für das Konto „Lokales System“ und NT AUTHORITY\NETWORKSERVICE für das Konto „Netzwerkdienst“ (nur[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] ).  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows "NT AUTHORITY\SYSTEM"  
```  
  
#### <a name="specifying-a-service-account"></a>Angeben eines Dienstkontos  
 In diesem Beispiel wird gezeigt, wie ein Berichtsserver so konfiguriert wird, dass er das Windows-Dienstkonto und das Webdienstkonto für den Berichtsserver verwendet, um eine Verbindung mit einer lokalen Berichtsserver-Datenbank herzustellen. Beachten Sie, dass **-u** nicht verwendet wird und dass keine Kontoinformationen angegeben werden. Wenn Sie Kontowerte aus dem Befehl ausschließen, verwendet das Hilfsprogramm **rsconfig** die integrierte Sicherheit und das Dienstkonto, unter dem der jeweilige Dienst ausgeführt wird.  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows  
```  
  
#### <a name="specifying-the-unattended-account-on-a-local-server"></a>Angeben des Kontos für unbeaufsichtigte Vorgänge auf einem lokalen Server  
 In diesem Beispiel wird gezeigt, wie das Konto, das für die unbeaufsichtigte Berichtsausführung verwendet wird, für Berichte konfiguriert wird, die keine Anmeldeinformationen für die externe Datenquelle übergeben. Bei dem Konto muss es sich um ein Windows-Domänenkonto handeln. Es ist nicht möglich, einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldenamen für den Benutzernamen und das Kennwort anzugeben. Das Konto wird auf einer lokalen Berichtsserverinstanz konfiguriert. Fehlermeldungen werden in den Ablaufverfolgungsprotokollen im Ordner ReportingServices\LogFiles erfasst.  
  
```  
rsconfig -e -u <DOMAIN\ACCOUNT> -p <PASSWORD> -t  
```  
  
#### <a name="specifying-the-unattended-account-on-a-remote-server"></a>Angeben des Kontos für unbeaufsichtigte Vorgänge auf einem Remoteserver  
 In diesem Beispiel wird veranschaulicht, wie das Konto auf einer Remote-Berichtsserverinstanz konfiguriert wird, die dieselbe Version wie Rsconfig.exe aufweist (z. B. wenn sowohl Berichtsserver als auch Rsconfig.exe aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 R2 stammen). Fehlermeldungen werden in den Ablaufverfolgungsprotokollen auf dem Remoteserver erfasst.  
  
```  
rsconfig -e -m <REMOTECOMPUTERNAME> -s <SQLSERVERNAME> -u <DOMAIN\ACCOUNT> -p <PASSWORD> -t  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren einer Verbindung mit der Berichtsserver-Datenbank &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Konfigurieren des unbeaufsichtigten Ausführungskontos &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)   
 [Reporting Services-Berichtsserver &#40;einheitlicher Modus&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Speichern verschlüsselter Berichtsserverdaten &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Reporting Services-Konfigurationsdateien](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Eingabeaufforderungs-Hilfsprogramme für Berichtsserver &#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md)   
 [RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  
