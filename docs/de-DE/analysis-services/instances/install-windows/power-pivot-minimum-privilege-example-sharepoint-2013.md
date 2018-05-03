---
title: Power Pivot Mindestberechtigungen Beispiel – SharePoint 2013 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9f30e9b8b997a4fefd39acd9797de5d19d2a7d29
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="power-pivot-minimum-privilege-example---sharepoint-2013"></a>Power Pivot Mindestberechtigungen Beispiel – SharePoint 2013
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Dieses Thema veranschaulicht eine Beispielkonfiguration für [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint 2013 mit Mindestberechtigungen. Bei der Konfiguration wird für jede der drei Komponenten ein anderes Konto verwendet, von denen jedes über Mindestberechtigungen verfügt.  
  
## <a name="summary-of-accounts"></a>Übersicht der Konten  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint 2013 unterstützt die Verwendung des Netzwerkdienstkontos für das Analysis Services-Dienstkonto. Das Netzwerkdienstkonto ist kein unterstütztes Szenario unter SharePoint 2010. Weitere Informationen zu Dienstkonten finden Sie unter [Konfigurieren von Windows-Dienstkonten und-Berechtigungen](http://msdn.microsoft.com/library/ms143504.aspx) (http://msdn.microsoft.com/library/ms143504.aspx).  
  
 In der folgenden Tabelle werden die Eigenschaften der drei Konten zusammengefasst, die in diesem Beispiel für eine Konfiguration mit Mindestberechtigungen verwendet werden.  
  
|Scope|Name|  
|-----------|----------|  
|SharePoint-Administratorkonto|**SPAdmin**|  
|SharePoint-Farmkonto|**SPFarm**|  
|Analysis Services-Dienstkonto|**SPsvc**|  
  
### <a name="the-sharepoint-administrator-account-spadmin"></a>Das SharePoint-Administratorkonto (SpAdmin)  
 **SPAdmin** ist ein Domänenkonto, das Sie zum Installieren und Konfigurieren der Farm verwenden. Unter diesem Konto werden der SharePoint-Konfigurations-Assistent und das [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Konfigurationstool für SharePoint 2013 ausgeführt. Das **SPAdmin** -Konto ist das einzige Konto, für das lokale Administratorrechte erforderlich sind. Vor dem Ausführen des [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Konfigurationstools gewähren Sie dem **SPAdmin** -Konto Berechtigungen für die SQL Server-Datenbankinstanz, auf der SharePoint Inhalts- und Konfigurationsdatenbanken einrichtet. Damit Sie das SPAdmin-Konto in einem Szenario mit Mindestberechtigungen konfigurieren können, muss es Mitglied in den Rollen **securityadmin** und **dbcreator**sein.  
  
### <a name="the-farm-account-spfarm"></a>Das Farmkonto (SPFarm)  
 **SPFarm** ist ein Domänenkonto, das der SharePoint-Timerdienst und die Webanwendung der Zentraladministration für den Zugriff auf die SharePoint-Inhaltsdatenbank verwenden. Dieses Konto muss nicht als lokaler Administrator eingerichtet sein. Der SharePoint-Konfigurations-Assistent gewährt die entsprechenden Mindestberechtigungen in der SQL Server-Back-End-Datenbank. Die Mindestberechtigung für die SQL Server-Konfiguration ist die Mitgliedschaft in den Rollen **securityadmin** und **dbcreator**.  
  
### <a name="the-service-account-for-power-pivot-service-spsvc"></a>Das Dienstkonto für den PowerPivot-Dienst (SPsvc)  
 Wenn eine neue SharePoint-Farm vor dem Ausführen des [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Konfigurationstools noch nicht konfiguriert wurde, werden standardmäßig folgende Anwendungen vom [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Konfigurationstool erstellt:  
  
-   [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Dienstanwendung.  
  
-   Excel Services-Anwendung  
  
-   Secure Storage-Anwendung  
  
 Das [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Konfigurationstool konfiguriert alle drei Dienstanwendungen im Standardanwendungspool. Dieser Anwendungspool ist normalerweise für die Ausführung als SPFarm-Konto konfiguriert, das Zugriff auf viele Ressourcen hat, die von einem Dienstkonto jedoch nicht benötigt werden. Um eine Umgebung mit Mindestberechtigungen zu erhalten, konfigurieren Sie ein neues Domänenkonto, das vom betreffenden Anwendungspool und der betreffenden Webanwendung verwendet wird.  
  
 **So erstellen Sie ein neues SPsvc-Domänenkonto, das als SharePoint-Dienstkonto verwendet werden soll**  
  
1.  Wählen Sie in der SharePoint-Zentraladministration **Sicherheit**aus.  
  
2.  Wählen Sie **Dienstkonten konfigurieren**aus.  
  
3.  Wählen Sie **Neues verwaltetes Konto registrieren**aus.  
  
 Das **SPSvc** -Konto verfügt über keine lokalen Administratorberechtigungen, und SPsvc verfügt über keine Berechtigungen in der SharePoint-Datenbank. Die einzigen Berechtigungen, die SPsvc erfordert, sind Administratorrechte für die [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Instanz von Analysis Services.  
  
 **So konfigurieren Sie den entsprechenden Anwendungspool für die Verwendung des SPsvc-Kontos**  
  
1.  Wählen Sie in der SharePoint-Zentraladministration **Sicherheit**aus.  
  
2.  Wählen Sie **Dienstkonten konfigurieren**aus.  
  
3.  Wählen Sie den von der [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Dienstanwendung verwendeten Dienstanwendungspool aus. Wählen Sie dann das SPSvc-Konto aus.  
  
 **So gewähren Sie Zugriff auf die Webanwendung mit PowerShell**  
  
1.  Führen Sie die SharePoint 2013-Verwaltungsshell mit Administratorberechtigungen aus.  
  
2.  Führen Sie den folgenden PowerShell-Code aus:  
  
    ```  
    $webApp = Get-SPWebApplication "http://<servername>"  
    $webApp.GrantAccessToProcessIdentity("DOMAIN\<ServiceAccountName>")  
  
    ```  
  
  
