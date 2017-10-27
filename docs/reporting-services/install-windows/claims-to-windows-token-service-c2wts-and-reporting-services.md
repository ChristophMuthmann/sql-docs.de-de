---
title: Claims to Windows Token Service (c2WTS) und Reporting Services | Microsoft Docs
ms.custom: The Claims to Windows Token Service (C2WTS) is used by SharePoint and needs to be configured for Kerberos constrained delegation to work with SQL Server Reporting Services properly.
ms.date: 09/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: a9397f427cac18d0c8bfc663f6bd477b0440b8a3
ms.openlocfilehash: 8a478bba3cde66967594d5ef02f867de5b33edd7
ms.contentlocale: de-de
ms.lasthandoff: 09/15/2017

---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>Claims to Windows Token Service (C2WTS) und Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

Claims to Windows Token Service (C2WTS) von SharePoint ist erforderlich, wenn Sie, zum Anzeigen von Berichten im einheitlichen Modus, in möchten der [SQL Server Reporting Services Berichts-Viewer-Webpart](../report-server-sharepoint/deploy-report-viewer-web-part.md).

C2WTS ist auch mit SQL Server Reporting Services SharePoint-Modus erforderlich, wenn Sie Windows-Authentifizierung für Datenquellen, die außerhalb der SharePoint-Farm sind, verwenden möchten. C2WTS wird auch dann benötigt, auch sich die Datenquelle(n) auf demselben Computer wie der gemeinsame Dienst befinden. In diesem Szenario ist jedoch keine eingeschränkte Delegierung erforderlich.

> [!NOTE]
> Reporting Services-Integration in SharePoint ist nach SQL Server 2016 nicht mehr verfügbar.

## <a name="report-viewer-web-part-configuration"></a>Berichts-Viewer Teil Webkonfiguration

Der Berichts-Viewer-Webpart kann zum Einbetten von Berichten für SQL Server Reporting Services im einheitlichen Modus in der SharePoint-Website verwendet werden. Dieses Webpart ist für SharePoint 2013 und SharePoint 2016 verfügbar. Stellen Sie SharePoint 2013 und SharePoint 2016 von der anspruchsbasierten Authentifizierung verwenden. SQL Server Reporting Services (einheitlicher Modus) wird standardmäßig Windows-Authentifizierung verwendet. Daher muss C2WTS für Berichte, die für das einwandfreie Rendering ordnungsgemäß konfiguriert sein.

## <a name="sharepoint-mode-integaration"></a>SharePoint-Modus integaration

**Dieser Abschnitt gilt nur in SQL Server 2016 Reporting Services und früheren Versionen.**

Claims to Windows Token Service (C2WTS) von SharePoint ist mit SQL Server Reporting Services SharePoint-Modus erforderlich, wenn Sie Windows-Authentifizierung für Datenquellen, die außerhalb der SharePoint-Farm sind, verwenden möchten. Dies gilt auch, wenn der Benutzer die Datenquellen mit Windows-Authentifizierung zugreift, da die Kommunikation zwischen dem Web-Front-End (WFE) und freigegebene Reporting Services-Diensts immer Anspruchsauthentifizierung verwendet werden.

## <a name="steps-needed-to-configure-c2wts"></a>Schritte zum Konfigurieren von c2WTS

Die von C2WTS erstellten Token funktionieren nur bei der eingeschränkten Delegierung (Einschränkungen für bestimmte Dienste) und bei Verwendung der Konfigurationsoption Beliebiges Authentifizierungsprotokoll verwenden. Wenn sich die Datenquellen auf demselben Computer wie der gemeinsame Dienst befinden, ist wie oben bereits erwähnt keine eingeschränkte Delegierung erforderlich.

Wenn in der Umgebung die eingeschränkte Kerberos-Delegierung verwendet wird, dann müssen sich der SharePoint Server-Dienst und externe Datenquellen in derselben Windows-Domäne befinden. Jeder Dienst, der auf C2WTS (Claims to Windows Token Service) basiert, muss die **eingeschränkte** Kerberos-Delegierung verwenden, damit C2WTS den Kerberos-Protokollübergang verwenden kann, um Ansprüche (Claims) in Windows-Anmeldeinformationen zu übersetzen. Diese Anforderungen gelten für alle gemeinsamen SharePoint-Dienste. Weitere Informationen finden Sie unter [Planen der Kerberos-Authentifizierung in SharePoint 2013](http://technet.microsoft.com/library/ee806870.aspx).  

1. Konfigurieren Sie das C2WTS-Dienstkonto. Fügen Sie das Dienstkonto der lokalen Administratorengruppe auf jedem Server, dass C2WTS verwendet werden soll.

    Für die **Berichts-Viewer-Webpart**, diese Funktion wird die Web-Front-End (WFE)-Server sein. Für **integrierten SharePoint-Modus**, werden die Anwendungsserver, auf dem Reporting Services-Diensts ausgeführt wird.

2. Konfigurieren Sie die Delegierung für das C2WTS-Dienstkonto.

    Das Konto benötigt die eingeschränkte Delegierung mit Protokollübergang und Berechtigungen für die Delegierung an Dienste ist es erforderlich, für die Kommunikation mit (d. h. SQL Server-Datenbankmodul, SQL Server Analysis Services). Die Delegierung konfigurieren, können Sie das Snap-in Active Directory-Benutzer und Computer und ein Domänenadministrator sein müssen.

    > [!IMPORTANT]
    > Alle Einstellungen konfigurieren Sie für das C2WTS-Dienstkonto auf der Registerkarte "Delegierung" Anforderungen entsprechend der Haupt-Dienstkonto verwendet wird. Für die **Berichts-Viewer-Webpart**, dies ist das Dienstkonto für die SharePoint-Webanwendung wird. Für **integrierten SharePoint-Modus**, dies ist das Reporting Services-Dienstkonto wird.
    >
    > Wenn Sie das C2WTS-Dienstkonto für die Delegierung an einen SQL-Dienst zulassen, müssen Sie z. B. auf dem Reporting Services-Dienstkonto für den integrierten SharePoint-Modus verwenden müssen.

    * Klicken Sie mit der rechten Maustaste auf jedes Dienstkonto, und öffnen Sie das Eigenschaftendialogfeld. Klicken Sie im Dialogfeld auf die Registerkarte **Delegierung** .

        Die Registerkarte "Delegierung" ist nur sichtbar, wenn das Objekt einen Service Prinicpal Name (SPN) zugewiesen wurde. C2WTS erfordert keinen SPN für das C2WTS-Dienstkonto jedoch ohne einen SPN der **Delegierung** Registerkarte nicht sichtbar sein. Eine Alternative zur Konfiguration der eingeschränkten Delegierung ist die Verwendung des Hilfsprogramms **ADSIEdit**.

    * Wesentliche Konfigurationsoptionen auf der Registerkarte "Delegierung":

        * Wählen Sie **Benutzer bei Delegierungen angegebener Dienste vertrauen**
        * Wählen Sie **Beliebiges Authentifizierungsprotokoll verwenden**

    * Wählen Sie **Hinzufügen** zum Hinzufügen eines Dienstes, an den Sie delegieren können.

    * Wählen Sie **Benutzer oder Computer...** *, und geben Sie das Konto, das den Dienst hostet. Angenommen, ein SQL-Server ausgeführt wird, unter einem Konto mit dem Namen *Sqlservice*, geben Sie `sqlservice`. 

    * Wählen Sie die Darstellung des Diensts. Dadurch werden die SPNs angezeigt, die über dieses Konto verfügbar sind. Wenn der Dienst unter diesem Konto nicht angezeigt wird, fehlt er möglicherweise oder befindet auf einem anderen Konto. Sie können das SetSPN-Dienstprogramm verwenden, um die SPNs anzupassen.

    * Wählen Sie „OK“ aus, um die Dialogfelder zu verlassen.

3. Konfigurieren von C2WTS *AllowedCallers*.

    C2WTS erfordert explizit die Identitäten der 'Aufrufer' in der Konfigurationsdatei aufgelisteten **C2WTShost.exe.config**. C2WTS akzeptiert keine Anforderungen sämtlicher authentifizierter Benutzer im System, e sei denn, der Dienst wurde entsprechend konfiguriert. In diesem Fall wird der 'Aufrufer' der WSS_WPG-Windows-Gruppe. Die Datei c2wtshost.exe.config wird im folgenden Verzeichnis gespeichert:

    Durch die Änderung des Dienstkontos für den C2WTS-Dienst in der SharePoint-Zentraladministration wird das Konto der Gruppe „WSS_WPG“ hinzugefügt.

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

4. Starten Sie den Claims to Windows Token Service über die SharePoint-Zentraladministration auf die **Dienste auf dem Server verwalten** Seite. Der Dienst sollte auf dem Server gestartet werden, auf dem die Aktion ausgeführt wird. Z. B. Wenn Sie einen Server haben, d. h. ein WFE und einem anderen Server, der ein Anwendungsserver, den freigegebenen SQL Server Reporting Services-Dienst ausgeführt wird, verfügt, Sie nur C2WTS auf dem Anwendungsserver starten müssen. C2WTS wird nur auf einen WFE-Server erforderlich, wenn Sie den Berichts-Viewer-Webpart ausgeführt werden.

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)

