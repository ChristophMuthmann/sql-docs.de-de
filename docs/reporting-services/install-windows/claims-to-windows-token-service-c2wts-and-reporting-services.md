---
title: Claims to Windows Token Service (c2WTS) und Reporting Services | Microsoft Docs
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- c2wts.exe.config
- SharePoint mode
- C2WTS
- WSS_WPG
ms.assetid: 4d380509-deed-4b4b-a9c1-a9134cc40641
caps.latest.revision: 17
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 2ab5f4b5d2774d9dc944ad17bb55063388b70a6d
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>Übersicht über Claims to Windows Token Service (c2WTS) und Reporting Services

[!INCLUDE[ssrs-appliesto-sql2016-xpreview](../../includes/ssrs-appliesto-sql2016-xpreview.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  Der SharePoint-Dienst „Claims to Windows Token Service“ (C2WTS) ist im SharePoint-Modus von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] erforderlich, wenn Sie die Windows-Authentifizierung für Datenquellen verwenden möchten, die außerhalb der SharePoint-Farm liegen. Dies gilt auch, wenn der Benutzer über die Windows-Authentifizierung auf die Datenquellen zugreift, weil die Kommunikation zwischen dem Web-Front-End (WFE) und dem gemeinsamen Dienst für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] immer der Forderungsauthentifizierung unterliegt.  
  
 c2WTS wird auch dann benötigt, auch sich die Datenquelle(n) auf demselben Computer wie der gemeinsame Dienst befinden. In diesem Szenario ist jedoch keine eingeschränkte Delegierung erforderlich.  
  
 Die von c2WTS erstellten Token funktionieren nur bei der eingeschränkten Delegierung (Einschränkungen für bestimmte Dienste) und bei Verwendung der Konfigurationsoption "Beliebiges Authentifizierungsprotokoll verwenden". Wenn sich die Datenquellen auf demselben Computer wie der gemeinsame Dienst befinden, ist wie oben bereits erwähnt keine eingeschränkte Delegierung erforderlich.  
  
 Wenn in der Umgebung die eingeschränkte Kerberos-Delegierung verwendet wird, dann müssen sich der SharePoint Server-Dienst und externe Datenquellen in derselben Windows-Domäne befinden. Jeder Dienst, der auf C2WTS (Claims to Windows Token Service) basiert, muss die **eingeschränkte** Kerberos-Delegierung verwenden, damit C2WTS den Kerberos-Protokollübergang verwenden kann, um Ansprüche (Claims) in Windows-Anmeldeinformationen zu übersetzen. Diese Anforderungen gelten für alle gemeinsamen SharePoint-Dienste. Weitere Informationen finden Sie unter [Planen der Kerberos-Authentifizierung in SharePoint 2013](http://technet.microsoft.com/library/ee806870.aspx).  
  
 Die Prozedur wird in diesem Thema zusammengefasst.

## <a name="prerequisites"></a>Voraussetzungen

> [!NOTE]
>  Hinweis: Einige der Konfigurationsschritte ändern sich möglicherweise oder funktionieren nicht in bestimmten Farmtopologien. Bei der Installation eines einzelnen Servers werden beispielsweise keine Windows Identity Foundations-c2WTS-Dienste unterstützt, sodass Claims to Windows Token-Delegierungsszenarien innerhalb dieser Farmkonfiguration nicht zulässig sind.

> [!IMPORTANT]
> Wenn Sie Power View für Power Pivot-Arbeitsmappen zu verwenden, müssen Sie zusätzliche Konfigurationsschritte für Office Online Server durchführen: [Office Online Server overview](https://technet.microsoft.com/library/jj219437\(v=office.16\).aspx)(Übersicht über Office Online Server). Weitere Informationen finden Sie in den folgenden Whitepapers: 
>
> - [Bereitstellen von SQL Server 2016 PowerPivot und Power View in SharePoint 2016](../../analysis-services/instances/install-windows/deploying-sql-server-2016-powerpivot-and-power-view-in-sharepoint-2016.md)
> 
> - [Bereitstellen von SQL Server 2016 PowerPivot und Power View in einer Multi-Tier SharePoint 2016-Farm](../../analysis-services/instances/install-windows/deploy-powerpivot-and-power-view-multi-tier-sharepoint-2016-farm.md)
  
### <a name="basic-steps-needed-to-configure-c2wts"></a>Grundlegende Schritte für die c2WTS-Konfiguration  
  
1.  Konfigurieren Sie das c2WTS-Dienstkonto. Fügen Sie das Dienstkonto der lokalen Administratorengruppe auf jedem Anwendungsserver, auf dem c2WTS ausgeführt wird, hinzu. Stellen Sie außerdem sicher, dass das Konto über die folgenden lokalen Sicherheitsrichtlinienrechte verfügt:  
  
    -   Einsetzen als Teil des Betriebssystems  
  
    -   Annehmen der Identität eines Clients nach der Authentifizierung  
  
    -   Anmelden als Dienst  
  
2.  Konfigurieren Sie die Delegierung für das c2WTS-Dienstkonto. Das Konto muss für die eingeschränkte Delegierung mit Protokollübergang konfiguriert werden. Außerdem benötigt es Berechtigungen für die Delegierung an Dienste, mit denen es kommunizieren muss (d.h. SQL Server Engine, SQL Server Analysis Services). Verwenden Sie das Snap-In "Active Directory-Benutzer und -Computer", um die Delegierung zu konfigurieren.  

    > [!IMPORTANT]
    > Alle Einstellungen, die Sie für das C2WTS-Dienstkonto auf der Registerkarte „Delegierung“ konfigurieren, müssen dem Reporting Services-Dienstkonto entsprechen. Wenn Sie C2WTS-Dienstkonto beispielsweise erlauben, an einen SQL-Dienst zu delegieren, müssen Sie auf dem Reporting Services-Dienstkonto dieselbe Konfiguration verwenden.
  
    1.  Klicken Sie mit der rechten Maustaste auf jedes Dienstkonto, und öffnen Sie das Eigenschaftendialogfeld. Klicken Sie im Dialogfeld auf die Registerkarte **Delegierung** .  
  
        > [!NOTE]  
        >  Hinweis: Die Registerkarte „Delegierung“ ist nur sichtbar, wenn dem Objekt ein Dienstprinzipalname (Service Prinicpal Name; SPN) zugewiesen wurde. C2WTS erfordert grundsätzlich keinen SPN für das C2WTS-Konto; ohne einen SPN ist die Registerkarte **Delegierung** jedoch nicht sichtbar. Eine Alternative zur Konfiguration der eingeschränkten Delegierung ist die Verwendung des Hilfsprogramms **ADSIEdit**.  
  
    2.  Wesentliche Konfigurationsoptionen auf der Registerkarte "Delegierung":  
  
        -   Option "Benutzer bei Delegierungen angegebener Dienste vertrauen"  
  
        -   Option "Beliebiges Authentifizierungsprotokoll verwenden"  

    3. Wählen Sie **Hinzufügen** zum Hinzufügen eines Dienstes, an den Sie delegieren können.
    
    4. Wählen Sie **Benutzer oder Computer...** *, und geben Sie das Konto, das den Dienst hostet. Angenommen, ein SQL-Server ausgeführt wird, unter einem Konto mit dem Namen *Sqlservice*, geben Sie `sqlservice`.
    
    5. Wählen Sie die Darstellung des Diensts. Dadurch werden die SPNs angezeigt, die über dieses Konto verfügbar sind. Wenn der Dienst unter diesem Konto nicht angezeigt wird, fehlt er möglicherweise oder befindet auf einem anderen Konto. Sie können das SetSPN-Dienstprogramm verwenden, um die SPNs anzupassen.
    
    6. Wählen Sie „OK“ aus, um die Dialogfelder zu verlassen.
  
3.  Konfigurieren von c2WTS 'AllowedCallers'  
  
     C2WTS erfordert, dass die Identitäten der „Aufrufer“ in der Konfigurationsdatei **c2WTShost.exe.config**explizit aufgeführt werden. c2WTS akzeptiert keine Anforderungen sämtlicher authentifizierter Benutzer im System, e sei denn, der Dienst wurde entsprechend konfiguriert. In diesem Fall entspricht der 'Aufrufer' der WSS_WPG-Windows-Gruppe. Die Datei c2WTShost.exe.config wird im folgenden Ordner gespeichert:  
     
     > [!NOTE]
     > Durch die Änderung des Dienstkontos für den C2WTS-Dienst in der SharePoint-Zentraladministration wird das Konto der Gruppe „WSS_WPG“ hinzugefügt.
  
     **\Programme\Windows Identity Foundation\v3.5 \c2WTShost.exe.config**  
  
     Im folgenden Beispiel wird die Konfigurationsdatei gezeigt:  
  
    ```  
    <configuration>  
      <windowsTokenService>  
        <!--  
            By default no callers are allowed to use the Windows Identity Foundation Claims To NT Token Service.  
            Add the identities you wish to allow below.  
          -->  
        <allowedCallers>  
          <clear/>  
          <add value="WSS_WPG" />  
        </allowedCallers>  
      </windowsTokenService>  
    </configuration>  
    ```    
4.  Starten Sie den Claims to Windows Token Service von SharePoint: Starten Sie den Claims to Windows Token Service über die SharePoint-Zentraladministration auf der Seite **Dienste auf dem Server verwalten** . Der Dienst sollte auf dem Server gestartet werden, auf dem die Aktion ausgeführt wird. Wenn Sie z.B. über einen WFE-Server und einen Anwendungsserver verfügen, auf dem der gemeinsame Dienst von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ausgeführt wird, müssen Sie C2WTS nur auf dem Anwendungsserver starten. c2WTS wird auf dem WFE-Server nicht benötigt.

## <a name="next-steps"></a>Nächste Schritte

[Übersicht über Claims to Windows Token Service (C2WTS)](http://msdn.microsoft.com/library/ee517278.aspx)   
[Planen der Kerberos-Authentifizierung in SharePoint 2013](http://technet.microsoft.com/library/ee806870.aspx)  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
