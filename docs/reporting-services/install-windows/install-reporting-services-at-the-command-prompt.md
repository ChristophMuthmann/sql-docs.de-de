---
title: "Installieren von Reporting Services über die Eingabeaufforderung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: command line
ms.assetid: 048169b3-512c-41e4-895a-0416eff41268
caps.latest.revision: "11"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 20a34323b2803bf9d68dd94eb058d5ac158961a4
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="install-reporting-services-at-the-command-prompt"></a>Installieren von Reporting Services über die Eingabeaufforderung

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] unterstützt eine Befehlszeileninstallation vom SQL Server-Setupprogramm aus. Dieses Thema enthält mehrere Beispiele für die Installation über die Befehlszeile, die speziell für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]gelten. Eine vollständige Beschreibung der für alle SQL Server-Komponenten verfügbaren Befehlszeilenoptionen finden Sie unter [Installieren von SQL Server von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Die Befehlszeilenoptionen für das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In für SharePoint-Produkte werden in diesem Thema nicht behandelt. Informationen zur Befehlszeileninstallation des Add-Ins finden Sie unter [Installieren des Add-Ins mithilfe der Installationsdatei "rsSharePoint.msi"](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md#bkmk_install_rssharepoint).

##  <a name="bkmk_native_mode"></a> Einheitlicher Modus – Reporting Services

### <a name="rsinstallmode-native-mode"></a>RSINSTALLMODE (einheitlicher Modus)
 Die primäre Eingabeeinstellung zum Installieren von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ist die **/RSINSTALLMODE** -Eingabeeinstellung. Die Einstellung verfügt über zwei Optionen: **DefaultNativeMode** und **FilesOnlyMode**.  
  
 Wenn das SQL Server-Datenbankmodul in die Installation eingeschlossen wird, lautet der standardmäßige RSINSTALLMODE "DefaultNativeMode". Wird das SQL Server-Datenbankmodul nicht in die Installation einbezogen, lautet der standardmäßige RSINSTALLMODE "FilesOnlyMode". Wenn Sie "DefaultNativeMode" auswählen, ohne dass das SQL Server-Datenbankmodul in die Installation einbezogen wird, wird der RSINSTALLMODE bei der Installation automatisch in "FilesOnlyMode" geändert. Weitere Informationen zu den Eingabeeinstellungen finden Sie unter [Installieren von SQL Server 2016 von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).

### <a name="examples-of-native-mode-installation"></a>Beispiele für die Installation des einheitlichen Modus

 Im folgenden Beispiel wird Folgendes installiert und folgende Konten werden konfiguriert:  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im einheitlichen Modus.  
  
-   Die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
-   Der SQL Server-Agent für die Abonnementfunktionen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]gelten.  
  
```  
Setup.exe /q /IACCEPTSQLSERVERLICENSETERMS /ACTION="install" /ERRORREPORTING=1 /UPDATEENABLED="False" /INSTANCENAME="MSSQLSERVER" /FEATURES="SQLEngine,Adv_SSMS,RS" /RSINSTALLMODE="DefaultNativeMode" /SQLSVCACCOUNT="[DOMAIN\ACCOUNT]" /SQLSVCPASSWORD="[PASSWORD]" /AGTSVCACCOUNT="[DOMAIN\ACCOUNT]" /AGTSVCPASSWORD="[PASSWORD]" /SQLSYSADMINACCOUNTS="[DOMAIN\ACCOUNT]"  
```  
  
##  <a name="bkmk_sharepoint_mode"></a> SharePoint-Modus – Reporting Services  
  
### <a name="rsshpinstallmode-sharepoint-mode"></a>RSSHPINSTALLMODE (SharePoint-Modus)  
 Die Eingabeeinstellung zum Installieren von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im SharePoint-Modus ist **/RSSHPINSTALLMODE**. Die Eingabeeinstellung hat eine Option: SharePointFilesOnlyMode. Mit der Option werden alle für den SharePoint-Modus benötigten Dateien installiert, nach der Installation sind jedoch Konfigurationsschritte erforderlich. Die zusätzlichen Konfigurationsschritte werden mithilfe der SharePoint-Zentraladministration ausgeführt. Weitere Informationen finden Sie unter [Installieren des ersten Berichtsservers im SharePoint-Modus](http://msdn.microsoft.com/en-us/b29d0f45-0068-4c84-bd7e-5b8a9cd1b538).  
  
### <a name="examples-of-sharepoint-mode-installation"></a>Beispiele für die Installation des SharePoint-Modus  
 Im folgenden Beispiel werden SQL Server, der Datenbankmoduldienst und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im SharePoint-Modus sowie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In für SharePoint (RS_SHPWFE) installiert.  
  
```  
setup /q /ACTION=install /FEATURES=SQL, RS_SHP, RS_SHPWFE,TOOLS /INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /SQLSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /AGTSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE"  
```  
  
 Im folgenden Beispiel wird nur der SharePoint-Modus von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installiert.  
  
```  
Setup.exe /q /ACTION="Install" /IACCEPTSQLSERVERLICENSETERMS /FEATURES="RS_SHP" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SECURITYMODE="SQL" /SAPWD="[PASSWORD]" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Name]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="[Account Name]" /UPDATEENABLED="False"  
  
```  
  
### <a name="examples-of-sharepoint-mode-upgrade"></a>Beispiele für ein Upgrade des SharePoint-Modus  
 Im folgenden Beispiel wird der SharePoint-Modus von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aktualisiert. Das Kennwort des vorhandenen Berichtsserver-Dienstkontos lautet**RSUPGRADEPASSWORD** . RSUPGRADEPASSWORD ist ein Pflichtfeld in einem Upgradeszenario, sofern das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstkonto kein integriertes Konto ist.  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[PID value]" /FTSVCACCOUNT="[DOMAIN\ACCOUNT]" /FTSVCPASSWORD="[PASSWORD]" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSUPGRADEPASSWORD="[PASSWORD]"  
```  
  
 Das folgende Beispiel kann verwendet werden, um eine Installation des SharePoint-Modus zu aktualisieren, die auf der Architektur für den gemeinsamen SharePoint-Dienst basiert. Im Beispiel wird der ALLOWUPGRADEFORSSRSSHAREPOINTMODE-Schalter verwendet. Der Schalter wird nicht zum Upgrade älterer Versionen benötigt, die nicht auf der Architektur für den gemeinsamen Dienst basieren:  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[Your PID Value]" /FTSVCACCOUNT="[ACCOUNT Name]" /FTSVCPASSWORD="[PASSWORD]" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /ALLOWUPGRADEFORSSRSSHAREPOINTMODE="True"  
```

## <a name="next-steps"></a>Nächste Schritte

[Installieren von SQL Server von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
[SysPrep-Parameter](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#SysPrep)   
[Installieren von PowerPivot über die Eingabeaufforderung](http://msdn.microsoft.com/en-us/7f1f2b28-c9f5-49ad-934b-02f2fa6b9328)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
