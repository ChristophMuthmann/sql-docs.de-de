---
title: 'Gewusst wie: Installieren von benutzerdefinierten sicherheitserweiterungen | Microsoft Docs'
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: bfa0a35b-ccfb-4279-bae6-106c227c5f16
caps.latest.revision: 3
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: e7058e9c0edce2b457dc63bf9e2d5cf61b6ee64f
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="how-to-install-custom-security-extensions"></a>Gewusst wie: Installieren von benutzerdefinierten sicherheitserweiterungen
Reporting Services 2016 eingeführt, ein neue Web-Portal um neue Odata-APIs und auch gehostet neue Bericht arbeitsauslastungen wie z. B. mobilen Berichte und KPIS. Dieses neue Portal basiert auf neuere Technologien sowie von vertrauten ReportingServicesService isoliert ist, indem Sie in einem separaten Prozess ausführen. Dieser Prozess ist keiner ASP.NET-Anwendung gehostet und als solche unterbricht Annahmen aus vorhandenen benutzerdefinierten sicherheitserweiterungen. Darüber hinaus nicht die aktuellen Schnittstellen für benutzerdefinierte sicherheitserweiterungen zulassen für jeden externen Kontext übergebene sein, verlassen Implementierer mit die einzige Auswahlmöglichkeit bekannten globale ASP.NET-Objekte untersuchen dies einige Änderungen an der Schnittstelle erforderlich.

## <a name="what-changed"></a>Was geändert?

Eine neue Schnittstelle eingeführt wurde, kann implementiert werden, die eine IRSRequestContext bereitstellen die zunehmend üblich, Eigenschaften, die von Erweiterungen verwendet, um die Entscheidungen, die im Zusammenhang mit Authentifizierung bereitstellt.
    
In früheren Versionen Berichts-Manager wurde die Front-End- und mit eigenen benutzerdefinierten Anmeldeseite konfiguriert werden konnte. In Reporting Services 2016 wird nur eine Seite, die vom Berichtsserver gehostet wird unterstützt und sollte für beide Anwendungen zu authentifizieren.

## <a name="implementation"></a>Implementierung
In früheren Versionen konnten Erweiterungen auf eine häufige Annahme verlassen, dass ASP.NET-Objekte sofort verfügbar ist. Da das neue Portal nicht in ASP.NET ausgeführt wird, kann die Erweiterung Probleme mit Objekten, die Null erreicht.
    
Die meisten generische Beispiel greift auf HttpContext.Current um Anforderungsinformationen wie Header und Cookies zu lesen. Damit können Erweiterungen für die gleichen Entscheidungen vorgestellt eine neue Methode in der Erweiterung, die Informationen für die Anforderung und wird aufgerufen, wenn über das Portal zu authentifizieren. 
    
Erweiterungen implementieren müssen die <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension2> Schnittstelle, um dies nutzen zu können. Die Erweiterungen müssen beide Versionen des implementieren <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension.GetUserInfo%2A> -Methode, wie von den Reportserver-Kontext und anderen bei Webhost verwendet aufgerufen wird. Das folgende Beispiel zeigt eine einfache Implementierung für das Portal, in dem die Identität aufgelöst, indem der Berichtsserver verwendet wird.

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
Die grundlegenden erforderlichen Konfigurationen für benutzerdefinierte sicherheitserweiterung sind identisch mit früheren Versionen. Änderungen für Datei "Web.config" und "rsreportserver.config" erforderlich sind: Weitere Informationen finden Sie unter [Konfigurieren von benutzerdefinierten oder Formularauthentifizierung auf dem Berichtsserver](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md).
    
Es ist nicht mehr eine separate Datei "Web.config" für den Berichts-Manager, das Portal übernimmt die gleichen Einstellungen wie den Reportserver-Endpunkt.

## <a name="machine-keys"></a>Computerschlüssel

Für die Groß-/Kleinschreibung Formularauthentifizierung verwenden, die die Entschlüsselung des Authentifizierungscookies erforderlich ist, müssen beide Prozesse mit dem gleichen Computer Schlüssel und Entschlüsselung der Algorithmus konfiguriert werden. Dies war ein Schritt vertraut, die zuvor hatte Setup Reporting Services in Umgebungen mit horizontaler Skalierung zu arbeiten, aber ist jetzt auch für Bereitstellungen auf einem einzelnen Computer erforderlich.

Beispiel:
    
**\ReportServer\web.config**

Fügen Sie unter `<system.web>`.
    
```
    <machineKey validationKey="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
```

**\RSWebApp\Microsoft.ReportingServices.Portal.Webhost.exe.config**

Fügen Sie unter `<configuration>`.

```
    <system.web>
        <machineKey validationKey=="[YOUR KEY]" decryptionKey=="[YOUR KEY]" validation="AES" decryption="AES" />
    </system.web>
```

Sie sollten eine Überprüfung Key spezifisch für die Bereitstellung verwenden, stehen mehrere Tools, die die Schlüssel wie IIS Manager (Internetinformationsdienste) zu generieren. Andere Tools können im Internet befinden.

## <a name="configure-passthrough-cookies"></a>Konfigurieren von Pass-Through-cookies

Das neue Portal und der Berichtsserver kommunizieren mithilfe von internen Soap-APIs für einige der Vorgänge (ähnlich wie die vorherige Version des Berichts-Managers). Zusätzliche Cookies erforderlich sind, aus dem Portal übergeben werden, mit dem Server ist die "passthroughcookies" Eigenschaften weiterhin verfügbar. Weitere Informationen finden Sie unter [konfigurieren Sie das Web-Portal zum Übergeben von benutzerdefinierten Authentifizierungscookies](../../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md).

```
<UI>
   <CustomAuthenticationUI>
      <PassThroughCookies>
         <PassThroughCookie>sqlAuthCookie</PassThroughCookie>
      </PassThroughCookies>
   </CustomAuthenticationUI>
</UI>
```

## <a name="see-also"></a>Siehe auch

[Konfigurieren von benutzerdefinierten oder Formularauthentifizierung auf dem Berichtsserver](../../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)  
[Konfigurieren Sie Berichts-Manager, um die Übergabe von benutzerdefinierten Authentifizierungscookies](https://msdn.microsoft.com/library/ms345241(v=sql.120).aspx)
