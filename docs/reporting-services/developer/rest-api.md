---
title: "Entwickeln Sie mit der REST-APIs für Reporting Services | Microsoft Docs"
ms.description: The REST API provides programmatic access to the objects in a SQL Server 2017 Reporting Services report server catalog.
ms.date: 10/19/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 7c2c34047ac316045387b036cf10ee149175580a
ms.contentlocale: de-de
ms.lasthandoff: 10/20/2017

---
# <a name="develop-with-the-rest-apis-for-reporting-services"></a>Entwickeln Sie mit der REST-APIs für Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

Microsoft SQL Server 2017 Reporting Services unterstützt Representational State Transfer (REST)-APIs. Die REST-APIs sind Dienstendpunkte, Unterstützung, die einen Satz von HTTP-Vorgänge (Methoden), geben Sie zu erstellen, abrufen, aktualisieren oder Löschzugriff für Ressourcen in einem Berichtsserver.

Die REST-API bietet programmgesteuerten Zugriff auf die Objekte in einer SQL Server 2017 Reporting Services-Berichtsserver-Katalog. Beispiele für Objekte sind Ordner, Berichte, KPIs, Datenquellen, Datasets, Aktualisierungspläne, Abonnements und vieles mehr. Verwenden die REST-API, können Sie, z. B. der Ordnerhierarchie navigieren, ermitteln den Inhalt eines Ordners oder Herunterladen eine Berichtsdefinition. Sie können auch erstellen, aktualisieren und Löschen von Objekten. Beispiele für das Arbeiten mit Objekten sind Hochladen eines Berichts, führen Sie einen Aktualisierungsplan Löschen eines Ordners und so weiter.

## <a name="components-of-a-rest-api-requestresponse"></a>Komponenten des eine REST-API-Anforderung/Antwort

Ein REST-API-Anforderung/Antwort-Paar kann in fünf Komponenten unterteilt werden:

* Die **Anforderungs-URI**, bestehend: `{URI-scheme} :// {URI-host} / {resource-path} ? {query-string}`. Obwohl die Anforderungs-URI im Anforderungsheader Nachricht enthalten ist, vergeben wir den Namen hier gesondert, da die meisten Sprachen oder Frameworks Sie diese getrennt aus der Anforderungsnachricht übergeben müssen.

    * URI-Schema: das übertragen die Anforderung verwendete Protokoll angibt. Beispielsweise `http` oder `https`.
    * URI-Host: Gibt den Domänennamen oder die IP-Adresse des Servers, auf dem REST-Endpunkt der Dienst, z. B. gehostet wird `myserver.contoso.com`.
    * Ressourcenpfad: Gibt an, die Ressource oder eine Ressourcensammlung, u. u. mehrere Segmente, die vom Dienst bei der Bestimmung der Auswahl dieser Ressourcen verwendet. Zum Beispiel: `CatalogItems(01234567-89ab-cdef-0123-456789abcdef)/Properties` können verwendet werden, um die angegebenen Eigenschaften für die CatalogItem abzurufen.
    * Abfragezeichenfolge (optional): zusätzliche einfache Parametern, wie die Auswahlkriterien für die API-Version oder eine Ressource enthält.

* Headerfelder für HTTP-Anforderung Nachricht:

    * Ein erforderliches [HTTP-Methode](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) (auch bekannt als ein Vorgang oder ein Verb) der weist den Dienst auf welche Art von Vorgang, die Sie anfordern. Reporting Services-REST-APIs unterstützen eine DELETE, GET, HEAD, PUT, POST, und PATCHEN Sie Methoden.
    * Optionale zusätzliche Headerfelder, gemäß der angegebenen URI- und HTTP-Methode.

* Optionale HTTP **Nachricht Anforderungstext** Felder zur Unterstützung des URI- und HTTP-Vorgangs. POST-Operationen enthalten z. B. MIME-codierten Objekte, die als komplexe Parameter übergeben werden. Für Post- oder PUT-Vorgänge, der Typ MIME-Codierung für den Text angegeben werden sollte, der `Content-type` sowie die Anforderungsheader. Einige Dienste benötigen Sie einen bestimmten MIME-Typ verwenden, z. B. `application/json`.

* HTTP **antwortnachrichtenheader** Felder:

    * Ein [HTTP-Statuscode:](http://www.w3.org/Protocols/HTTP/HTRESP.html), aus 2xx Erfolgscodes bis hin zu 4xx "oder" 5xx-Fehlercodes. Alternativ kann ein Dienstdefinition Statuscode zurückgegeben werden wie in der API-Dokumentation angegeben.
    * Optionale zusätzliche Headerfelder, wie erforderlich, um die Anforderung-Antwort, z. B. unterstützen eine `Content-type` Antwortheader.

* Optionale HTTP **antwortnachrichtentext** Felder:

    * MIME-codierten Antwortobjekte werden in den HTTP-Antworttext, z. B. eine Antwort von einer GET-Methode zurückgegeben, die Daten zurückgibt. In der Regel werden diese Objekte in einem strukturierten Format wie JSON oder XML-Code zurückgegeben, durch die `Content-type` -Antwortheader.

## <a name="api-documentation"></a>API-Dokumentation

Eine moderne REST-API-Aufrufe für moderne API-Dokumentation. Die REST-API wird auf der OpenAPI-Spezifikation (auch als) erstellt. die Swagger-Spezifikation) und Dokumentation steht in [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0). Hinter Dokumentierung der API, hilft SwaggerHub bei der Erstellung einer Clientbibliothek in der Sprache Ihrer Wahl – JavaScript TypeScript, c#, Java, Python, Ruby und vieles mehr.

## <a name="testing-api-calls"></a>Testen von API-Aufrufe

Ist ein Tool zum Testen von HTTP-Anforderung/Antwort-Nachrichten [Fiddler](http://www.telerik.com/fiddler). Fiddler ist ein kostenloses Web debugging-Proxy, die die REST-Anforderungen abfangen kann, die Dies erleichtert die Diagnose von der HTTP-Anforderung / Antwortnachrichten.

## <a name="next-steps"></a>Nächste Schritte

Überprüfen Sie die verfügbaren APIs über auf [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0).

Beispiele stehen auf [GitHub](https://github.com/Microsoft/Reporting-Services). Das Beispiel enthält eine HTML5-app für TypeScript reagieren und Webpaketdatei zusammen mit einer PowerShell-Beispiel erstellt.

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
