---
title: ADO-Entwurf Sicherheitsprobleme | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: "“drivers”"
ms.topic: article
helpviewer_keywords:
- ADO, security
ms.assetid: 86b83a38-efdf-4831-a6d5-7e470d517d1c
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 51c7e3cf9c99bdd76ce1b84a7c387b1e6e4d2f58
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="ado-security-design-features"></a>ADO-Sicherheitsfunktionen Entwurf
In den folgenden Abschnitten wird beschrieben, Entwurf Sicherheitsfunktionen in ActiveX Data Objects (ADO) 2.8 und höher. Diese Änderungen wurden in ADO 2.8 vorgenommen, um die Sicherheit zu verbessern. ADO 6.0, das in Windows DAC 6.0 in Windows Vista enthalten ist, ist funktionell gleichwertig mit ADO 2.8, die in MDAC 2.8 in Windows XP und Windows Server 2003 enthalten war. Dieses Thema enthält Informationen zum am besten Sichern Ihrer Anwendungen in ADO 2.8 oder höher.

> [!IMPORTANT]
>  Wenn Sie Ihre Anwendung von einer früheren Version von ADO aktualisieren, wird empfohlen, dass Sie die aktualisierte Anwendung auf einem Produktionscomputer testen, bevor Sie die Bereitstellung beim Kunden bereit. Auf diese Weise können Sie sicherstellen, dass Sie wissen Kompatibilitätsprobleme, bevor Sie die aktualisierte Anwendung bereitstellen.

## <a name="internet-explorer-file-access-scenarios"></a>Internet Explorer-Dateizugriffsszenarien
 Die folgenden Funktionen Auswirkungen, die Funktionsweise von ADO mit 2,8 und höher wird bei der Verwendung in Skripts verwendet, Webseiten in Internet Explorer.

### <a name="revised-and-improved-security-warning-message-box-now-used-to-alert-users"></a>Überarbeitete und verbesserte Sicherheit Warnhinweisfeld jetzt verwendet, um Benutzer darauf aufmerksam
 Für ADO 2.7 und früher wird die folgende Warnmeldung angezeigt, wenn es sich bei eine skriptgesteuerte Webseite versucht ADO-Code von einem nicht vertrauenswürdigen Anbieter ausgeführt wird:

```
This page accesses data on another domain. Do you want to allow this? To
avoid this message in Internet Explorer, you can add a secure Web site to
your Trusted Sites zone on the Security tab of the Internet Options dialog
box.
```

 Für ADO 2,8 und höher wird die oben genannte Meldung nicht mehr angezeigt. Stattdessen wird die folgende Meldung angezeigt, in diesem Kontext:

```
This Website uses a data provider that may be unsafe. If you trust the
Website, click OK, otherwise click Cancel.
```

 Die vorausgehende Nachricht ermöglicht dem Benutzer, während Sie die Folgen für jede der beiden Optionen wissen, fundierte Entscheidung treffen:

-   Wenn Benutzer die Website als vertrauenswürdig einstuft, klicken Sie auf OK lässt alle Datenträger Safe-Code (alle ADO-Methoden und Eigenschaften mit Ausnahme der Datenträger zugegriffen werden weiter unten in diesem Thema beschriebenen APIs) ausführen, und führen Sie im Browserfenster.

-   Wenn Benutzer nicht die Website vertraut wird, blockiert, klicken auf "Abbrechen" den ADO-Code für den Datenzugriff ausgeführt und in seiner Gesamtheit ausführen.

### <a name="disk-accessible-code-limited-now-to-trusted-sites"></a>Datenträger zugegriffen werden kann Code beschränkt sich jetzt auf vertrauenswürdige sites
 Zusätzliche Designänderungen wurden in ADO 2.8 vorgenommen, die die Fähigkeit eines einen eingeschränkten Satz von APIs, insbesondere zu begrenzen, die sodass das Potenzial zu lesen oder Schreiben von Dateien auf dem lokalen Computer verfügbar machen kann. Hier werden die API-Methoden, die weitere wurden aus Sicherheitsgründen eingeschränkt werden, wenn Internet Explorer ausgeführt:

-   Für das ADO **Stream** Objekt, wenn die [LoadFromFile](../../ado/reference/ado-api/loadfromfile-method-ado.md) oder [SaveToFile](../../ado/reference/ado-api/savetofile-method.md) Methoden verwendet werden.

-   Für das ADO **Recordset** Objekt, wenn entweder die [speichern](../../ado/reference/ado-api/save-method.md) Methode oder die [öffnen](../../ado/reference/ado-api/open-method-ado-recordset.md) Methode, z. B., wenn entweder die **AdCmdFile** Option wird festgelegt, oder die [Microsoft OLE DB-Anbieter für Persistenz (MSPersist)](../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) verwendet wird.

 Für diese eingeschränkter Sätze Funktionsreihe potenziell Datenträger zugegriffen werden kann tritt ein, das folgende Verhalten für ADO 2,8 und höher, wenn jeglicher Code, der diese Methoden verwendet, die in Internet Explorer ausgeführt wird:

-   Wenn die Website, die den Code bereitgestellt, die Liste der vertrauenswürdigen Sites Zone zuvor hinzugefügt wurde, der Code im Browser ausgeführt wird, und Zugriff auf lokale Dateien.

-   Wenn der Standort in der Liste der vertrauenswürdigen Sites Zone nicht angezeigt wird, der Code blockiert, und Zugriff auf lokale Dateien wurde verweigert.

    > [!NOTE]
    >  In ADO 2,8 und höher wird der Benutzer nicht benachrichtigt oder es wird empfohlen, die Liste der vertrauenswürdigen Sites Zone Websites hinzufügen. Aus diesem Grund ist die Verwaltung der Liste der vertrauenswürdigen Sites die Zuständigkeit für Personen sind bereitstellen oder die Unterstützung von Website-basierten Anwendungen, die auf dem lokalen Dateisystem zugreifen.

### <a name="access-blocked-to-the-activecommand-property-on-recordset-objects"></a>Zugriff auf die Eigenschaft ActiveCommand Recordset-Objekte blockiert
 Beim Ausführen in Internet Explorer blockiert ADO 2.8 jetzt den Zugriff auf die [ActiveCommand](../../ado/reference/ado-api/activecommand-property-ado.md) Eigenschaft für ein aktives **Recordset** -Objekt und gibt einen Fehler zurück. Der Fehler tritt auf, unabhängig davon, ob die Seite von einer Website, die in der Liste der vertrauenswürdigen Sites registriert stammt.

### <a name="changes-in-handling-for-ole-db-providers-and-integrated-security"></a>Änderungen bei der Verarbeitung für den OLE DB-Anbieter und der integrierten Sicherheit
 Beim Überprüfen der ADO 2.7 und früheren Versionen für potenzielle Sicherheitsprobleme und bedenken, ermittelt wurde. das folgende Szenario:

 In einigen Fällen, OLE DB-Anbieter, die die integrierte Sicherheit unterstützt [DBPROP_AUTH_INTEGRATED](https://msdn.microsoft.com/library/windows/desktop/ms712973.aspx) Eigenschaft zulässt potenziell skriptgesteuerten Webseiten Wiederverwenden der ADO-Verbindungsobjekt unbeabsichtigt mit anderen Servern herstellen verwenden die Anmeldeinformationen des aktuellen Benutzer. Um dies zu verhindern, ADO 2,8 und höher, behandeln OLE DB-Anbieter abhängig davon, wie sie ausgewählt haben, oder nicht bereitgestellt werden, für die integrierte Sicherheit.

 Für Webseiten, die von Standorten in der Liste der Zone vertrauenswürdiger Sites aufgeführten geladen werden, bietet die folgende Tabelle eine Aufschlüsselung der wie ADO mit 2,8 und höher ADO-Verbindungen in jedem Fall verwaltet.

|Internet Explorer-Einstellungen für die Benutzerauthentifizierung, anmelden|Anbieter unterstützt, die "Integrierte Sicherheit" und UID und PWD angegeben (SQLOLEDB)|Anbieter unterstützt "Integrated Security" (JOLT MSDASQL, MSPersist) nicht.|Anbieter "Integrierte Sicherheit" unterstützt und SSPI (es werden keine UID/PWD angegeben) festgelegt ist|
|------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
|Automatisches Anmelden mit aktuellen Benutzernamen und Kennwort|Verbindung zulassen|Verbindung zulassen|Verbindung zulassen|
|Benutzername und Kennwort auffordern|Verbindung zulassen|Verbindung fehlschlagen|Verbindung fehlschlagen|
|Automatisches Anmelden nur in der Intranetzone|Verbindung zulassen|Benutzer auffordern, mit der sicherheitswarnung|Benutzer auffordern, mit der sicherheitswarnung|
|Anonymous-Anmeldung|Verbindung zulassen|Verbindung fehlschlagen|Verbindung fehlschlagen|

 Im Fall, in dem jetzt eine Warnung mit Sicherheit angezeigt wird, informiert das Meldungsfeld Benutzer:

```
This Website is using your identity to access a data source. If you trust this Website, click OK, otherwise click Cancel.
```

 Die vorausgehende Nachricht ermöglicht den Benutzer eine fundierte Entscheidung treffen und entsprechend zu fortfahren.

> [!NOTE]
>  Für nicht vertrauenswürdige Websites (d. h. Websites nicht in der Liste der Zone vertrauenswürdiger Sites aufgeführt) Wenn der Anbieter auch (wie weiter oben in diesem Abschnitt erläutert) nicht vertrauenswürdig ist, möglicherweise der Benutzer zwei Sicherheitswarnungen in einer Zeile, eine Warnung zum unsafe-Anbieter und eine zweite Warnung zu den Versuchen Sie, ihre Identität zu verwenden. Wenn der Benutzer auf die erste Warnung OK klickt, werden die Internet Explorer-Einstellungen und in der vorherigen Tabelle beschriebenen Verhalten-Antwortcode ausgeführt.

## <a name="controlling-whether-password-text-is-returned-in-ado-connection-strings"></a>Steuert, ob Kennworttext in ADO-Verbindungszeichenfolgen zurückgegeben wird
 Wenn Sie versuchen, Abrufen des Werts der ["ConnectionString"](../../ado/reference/ado-api/connectionstring-property-ado.md) -Eigenschaft für ein ADO **Verbindung** Objekt die folgenden Ereignisse auftreten:

1.  Wenn die Verbindung geöffnet ist, wird eine Initialisierung dann an den zugrunde liegenden OLE DB-Anbieter Aufruf zum Abrufen der Verbindungszeichenfolge.

2.  Abhängig von der Einstellung in der OLE DB-Anbieter die [DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO](https://msdn.microsoft.com/library/windows/desktop/ms714905.aspx) -Eigenschaft, die Kennwörter sind enthalten, zusammen mit anderen Verbindungszeichenfolgen-Informationen, die zurückgegeben wird.

 Z. B. wenn die dynamische Eigenschaft des ADO-Verbindung **Persist Security Info** festgelegt ist, um **"true"**, Kennwortinformationen ist enthalten, in der Verbindungszeichenfolge zurückgegeben. Wenn der zugrunde liegende Anbieter die Eigenschaft auf festgelegt ist, andernfalls **"false"** Kennwortinformationen wird (z. B. mit dem SQLOLEDB-Anbieter) in der zurückgegebenen Verbindungszeichenfolge weggelassen.

 Bei Verwendung von Drittanbietern (d. h. nicht von Microsoft) OLE DB-Anbieter mit der ADO-Anwendungscode, überprüfen Sie wie die **DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO** Eigenschaft wird implementiert, um zu bestimmen, ob Einschluss von Kennwortinformationen mit ADO-Verbindungszeichenfolgen ist zulässig.

## <a name="checking-for-non-file-devices-when-loading-and-saving-recordsets-or-streams"></a>Überprüfung auf nicht-Datei Geräte beim Laden und Speichern von Recordsets oder streams
 Für ADO 2.7 und früher, Dateieingabe/-Ausgabe Vorgänge wie z. B. [öffnen](../../ado/reference/ado-api/open-method-ado-recordset.md) und [speichern](../../ado/reference/ado-api/save-method.md) , der zum Lesen und Schreiben von dateibasierte Daten können in einigen Fällen ermöglichen eine URL oder Dateiname verwendet werden, die einen nicht-Datenträger angegeben verwendet wurden Basis Dateityp an. Angenommen, LPT1, COM2, PRN. TXT "," AUX konnte als Alias für die Eingabe/Ausgabe zwischen Drucker und Geräte auf dem System mit bestimmten verwendet werden

 Diese Funktion wurde für ADO 2,8 und höher aktualisiert. Zum Öffnen und Speichern von **Recordset** und **Stream** Objekte aufweist, ADO jetzt führt eine typüberprüfung Datei, um sicherzustellen, dass in einer URL oder Dateinamen an das angegebene Gerät Eingabe- oder Ausgabespalte einer tatsächlichen Datei ist.

> [!NOTE]
>  Datei typüberprüfung gilt in diesem Abschnitt beschriebenen nur für Windows 2000 und höher. Es gilt nicht für Situationen, in denen ADO 2.8 oder höher unter früheren Versionen von Windows, z. B. Windows 98 ausgeführt wird.

