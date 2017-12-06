---
title: Installieren von benutzerdefinierten Sicherheitserweiterungen | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/10/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: bfa0a35b-ccfb-4279-bae6-106c227c5f16
caps.latest.revision: "3"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ed1cc06bb87d4f506c0aa94270740399775081af
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="how-to-install-custom-security-extensions"></a>Installieren von benutzerdefinierten Sicherheitserweiterungen

[!INCLUDE[ssrs-appliesto](../../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../../includes/ssrs-appliesto-pbirs.md)]

Mit Reporting Services 2016 wurde ein neues Webportal zum Hosten neuer OData-APIs und neuer Berichtsworkloads wie mobile Berichte und KPIs eingeführt. Dieses neue Portal basiert auf den neusten Technologien und unterscheidet sich von dem bereits bekannten Reporting Services-Dienst, da es in einem separaten Prozess ausgeführt wird. Bei diesem Prozess handelt es sich nicht um eine von ASP.NET gehostete Anwendung. Er bricht Annahmen von bereits vorhandenen benutzerdefinierten Sicherheitserweiterungen auf. Außerdem lassen aktuelle Schnittstellen es nicht zu, dass benutzerdefinierte Erweiterungen an einen externen Kontext übergeben werden, wodurch bei der Implementierung nur die Möglichkeit bleibt, bekannte globale ASP.NET-Objekte zu überprüfen. Dafür mussten einige Änderungen an der Schnittstelle vorgenommen werden.

## <a name="what-changed"></a>Vorgenommene Änderungen

Es wurde eine neue Schnittstelle eingeführt, die implementiert werden kann. Dadurch wird ein IRSRequestContext bereitgestellt, durch den allgemeinere von Erweiterungen verwendete Eigenschaften Entscheidungen in Bezug auf die Authentifizierung treffen können.

In den Vorgängerversionen war der Berichts-Manager das Front-End und konnte mit seiner eigenen benutzerdefinierten Anmeldungsseite konfiguriert werden. In Reporting Services 2016 wird nur eine vom Berichtsserver gehostete Seite unterstützt, die bei beiden Anwendungen authentifiziert werden sollte.

## <a name="implementation"></a>Implementierung

In den Vorgängerversionen basierten Erweiterungen auf der allgemeinen Annahme, dass ASP.NET-Objekte unmittelbar verfügbar sind. Da das neue Portal nicht auf ASP.NET ausgeführt werden kann, treten mit der Erweiterung möglicherweise Probleme auf, wenn Objekte den Wert NULL haben.

Das wohl generischste Beispiel dafür ist der Zugriff auf „HttpContext.Current“ zum Lesen von Anforderungsinformationen wie Headern und Cookies. Damit Erweiterungen dieselben Entscheidungen treffen können, wurde eine neue Methode in der Erweiterung eingeführt, die die Anforderungsinformationen zur Verfügung stellt und bei der Authentifizierung vom Portal aufgerufen wird. 

Erweiterungen müssen die <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension2>-Schnittstelle implementierten, um diese Funktion nutzen zu können. Die Erweiterungen müssen beide Versionen der <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension.GetUserInfo%2A>-Methode implementieren, die im Berichtsserverkontext aufgerufen und in anderen Webhostprozessen verwendet werden. Im untenstehenden Beispiel wird eine der einfachen Implementierungen für das Portal dargestellt, bei der die vom Berichtsserver aufgelöste Identität auch verwendet wird.

``` 
public void GetUserInfo(IRSRequestContext requestContext, out IIdentity userIdentity, out IntPtr userId)
{
    userIdentity = null;
    if (requestContext.User != null)
    {
        userIdentity = requestContext.User;
    }

    // initialize a pointer to the current user id to zero
    userId = IntPtr.Zero;
}
```

## <a name="deployment-and-configuration"></a>Bereitstellung und Konfiguration

Es werden dieselben grundlegenden Konfigurationen für benutzerdefinierte Sicherheitserweiterungen benötigt wie für die Vorgängerreleases. Änderungen müssen hingegen an den Konfigurationsdateien „web.config“ und „rsreportserver.config“ vorgenommen werden: Weitere Informationen dazu finden Sie unter [Configure Custom or Forms Authentication on the Report Server (Konfigurieren der benutzerdefinierten Authentifizierung oder der Formularauthentifizierung auf dem Berichtsserver)](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md).

Es gibt keine separate web.config-Konfigurationsdatei für den Berichts-Manager mehr. Das Portal übernimmt dieselben Einstellungen wie der Berichtsserverendpunkt.

## <a name="machine-keys"></a>Computerschlüssel

Bei der Formularauthentifizierung, für die die Entschlüsselung des Authentifizierungscookies erforderlich ist, müssen beide Prozesse mit demselben Computerschlüssel und Entschlüsselungsalgorithmus konfiguriert sein. Dieser Schritt ist den Benutzern bereits bekannt, die Reporting Services zuvor für Umgebungen zur horizontalen Skalierung eingerichtet haben. Jetzt ist diese Vorgehensweise allerdings auch für Bereitstellungen auf einem einzelnen Computer erforderlich.

Sie sollten einen für Ihre Bereitstellung spezifischen Validierungsschlüssel verwenden. Es gibt einige Tools wie den IIS-Manger (Internet Information Services Manager, Internetinformationsdienste-Manager), mit denen Sie Schlüssel generieren können. Andere Tools finden Sie im Internet.

### <a name="sql-server-reporting-services-2017-and-later"></a>SQL Server Reporting Services 2017 und höher

**\ReportServer\rsReportServer.config**

Unter `<configuration>` hinzufügen.

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

### <a name="sql-server-reporting-services-2016"></a>SQL Server Reporting Services 2016

**\ReportServer\web.config**

Unter `<system.web>` hinzufügen.
    
```
    <machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

**\RSWebApp\Microsoft.ReportingServices.Portal.WebHost.exe.config**

Unter `<configuration>` hinzufügen.

```
    <system.web>
        <machineKey validationKey=="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
    </system.web>
```

### <a name="power-bi-report-server"></a>Power BI-Berichtsserver

Verfügbar ab dem Release vom Juni 2017 (Build 14.0.600.301).

**\ReportServer\rsReportServer.config**

Unter `<configuration>` hinzufügen.

```
<machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

## <a name="configure-passthrough-cookies"></a>Konfigurieren von Passthrough-Cookies

Das neue Portal und der Berichtsserver kommunizieren bei einigen Vorgängen über interne SOAP-APIs (ähnlich wie die Vorgängerversion des Berichts-Managers). Wenn zusätzliche Cookies von dem Portal an den Server übergeben werden müssen, ist das PassThroughCookies-Element weiterhin verfügbar. Weitere Informationen finden Sie unter [Konfigurieren des Webportals für die Übergabe von benutzerdefinierten Authentifizierungscookies](../../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md).

```
<UI>
   <CustomAuthenticationUI>
      <PassThroughCookies>
         <PassThroughCookie>sqlAuthCookie</PassThroughCookie>
      </PassThroughCookies>
   </CustomAuthenticationUI>
</UI>
```

## <a name="next-steps"></a>Nächste Schritte

[Configure Custom or Forms Authentication on the Report Server (Konfiguration der benutzerdefinierten oder Formularauthentifizierung auf dem Berichtsserver)](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)  
[Konfigurieren des Berichts-Managers für die Übergabe von benutzerdefinierten Authentifizierungscookies](https://msdn.microsoft.com/library/ms345241(v=sql.120).aspx)

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
