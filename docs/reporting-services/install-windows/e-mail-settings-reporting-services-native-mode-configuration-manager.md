---
title: "E-Mail-Einstellungen – Reporting Services im einheitlichen Modus (Konfigurations-Manager) | Microsoft Docs"
ms.custom: 
ms.date: 06/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.rsconfigtool.emailsettings.F1
helpviewer_keywords:
- SQL11.rsconfigtool.emailsettings.F1
ms.assetid: cdad1529-bfa6-41fb-9863-d9ff1b802577
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 45aad2cc5dbdbc23fa28f1f70b138da4ec05f281
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="e-mail-settings---reporting-services-native-mode-configuration-manager"></a>E-Mail-Einstellungen – Einheitlicher Modus von Reporting Services (Konfigurations-Manager)
Reporting Services enthält eine Erweiterung zur E-Mail-Übermittlung, damit Sie Berichte per E-Mail verteilen können. Je nachdem, wie Sie das Abonnieren von E-Mails definieren, kann eine E-Mail-Übermittlung aus einer Nachricht, einem Link, einem Anhang oder einem eingebetteten Bericht bestehen. Die Erweiterung der E-Mail-Übermittlung arbeitet mit Ihrer vorhandenen E-Mail-Server-Technologie. Der E-Mail-Server muss ein SMTP-Server oder eine Weiterleitung sein. Der Berichtsserver stellt über CDO-Bibliotheken (Collaboration Data Objects, cdosys.dll), die das Betriebssystem stellt, eine Verbindung zu einem SMTP-Server her.

Die E-Mail-Übermittlungserweiterung des Berichtsservers ist standardmäßig nicht konfiguriert. Sie müssen den Reporting Services-Konfigurations-Manager verwenden, um die Erweiterung minimal zu konfigurieren. Sie müssen die Datei RSReportServer.config bearbeiten, um die erweiterten Eigenschaften festzulegen. Wenn Sie den Berichtsserver für die Verwendung dieser Erweiterung nicht konfigurieren können, können Sie stattdessen Berichte an einen freigegebenen Ordner übermitteln. Weitere Informationen finden Sie unter „Dateifreigabeübermittlung in Reporting Services“.

## <a name="configuration-requirements"></a>Konfigurationsanforderungen

- Die E-Mail-Übermittlung des Berichtsservers wird über Collaboration Data Objects (CDO) implementiert und erfordert einen SMTP-Remoteserver oder einen lokalen SMTP-Server (Simple Mail Transfer Protocol) bzw. eine SMTP-Weiterleitung. SMTP wird nicht von allen Windows-Betriebssystemen unterstützt. Wenn Sie die Itanium-basierte Edition von Windows Server 2008 verwenden, wird SMTP nicht unterstützt. Weitere Informationen zu den Konfigurationsoptionen von CDO finden Sie unter [Configuration CoClass](http://go.microsoft.com/fwlink/?LinkId=98237) auf MSDN.

Das konfigurierte Authentifizierungskonto muss auf dem SMTP-Server berechtigt sein, E-Mails zu senden.

- Für die Erweiterung der E-Mail-Übermittlung wird in E-Mail-Anlagen die UTF-8-Codierung verwendet. Die Codierung kann nicht geändert werden. Die HTML-Renderingerweiterung unterstützt ausschließlich UTF-8.

> [!NOTE] 
> Die standardmäßige E-Mail-Übermittlungserweiterung bietet keine Unterstützung für digitale Signaturen oder für die Verschlüsselung ausgehender E-Mail-Nachrichten.

## <a name="setting-configuration-options-for-e-mail-delivery"></a>Festlegen von Konfigurationsoptionen für die E-Mail-Übermittlung
Bevor Sie die E-Mail-Übermittlung des Berichtsservers verwenden können, müssen Sie Konfigurationswerte festlegen, die angeben, welcher SMTP-Server verwendet werden soll.

Gehen Sie wie folgt vor, um einen Berichtsserver für die E-Mail-Übermittlung zu konfigurieren:

- Verwenden Sie den Reporting Services-Konfigurations-Manager, wenn Sie nur einen SMTP-Server und ein Benutzerkonto angeben, das über die Berechtigung zum Senden von E-Mail verfügt. Dies sind die zum Konfigurieren der E-Mail-Übermittlungserweiterung für einen Berichtsserver erforderlichen Mindesteinstellungen.

- (Optional) Verwenden Sie einen Text-Editor, um zusätzliche Einstellungen in der Datei RSreportserver.config anzugeben. Diese Datei enthält alle Konfigurationseinstellungen für die Berichtsserver-E-Mail-Übermittlung. Wenn Sie einen lokalen SMTP-Server verwenden oder die E-Mail-Übermittlung auf bestimmte Hosts beschränken, müssen Sie zusätzliche Einstellungen in diesen Dateien angeben. Weitere Informationen zum Suchen und Ändern von Konfigurationsdateien finden Sie unter [Ändern einer Reporting Services-Konfigurationsdatei (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) in der SQL Server-Onlinedokumentation.

> [!NOTE] 
> E-Mail-Einstellungen für den Berichtsserver basieren auf CDO (Collaboration Data Objects). Ausführlichere Informationen zu bestimmten Einstellungen finden Sie in der CDO-Produktdokumentation.

## <a name="a-namersconfigmanconfigure-report-server-e-mail-using-the-reporting-services-configuration-manager"></a><a name="rsconfigman"/>Konfigurieren der Berichtsserver-E-Mail mit dem Konfigurations-Manager für Reporting Services

1. Starten Sie den Reporting Services-Konfigurations-Manager, und stellen Sie eine Verbindung mit der Berichtsserverinstanz her.

2. Geben Sie in **Absenderadresse**die E-Mail-Adresse an, die im Feld **Von:** einer generierten E-Mail verwendet werden soll. 

     Sie müssen ein Benutzerkonto angeben, das über die Berechtigung zum Senden von E-Mails vom SMTP-Server verfügt. Der Wert, den Sie für **Absenderadresse** eingeben, wird im `<From>` -Feld in der Datei „rsreportserver.config“ gespeichert.  

3.  Geben Sie in **SMTP-Server**den zu verwendenden SMTP-Server oder das Gateway an. 

     Bei diesem Wert kann es sich um eine IP-Adresse, einen NetBIOS-Namen eines Computers im Firmenintranet oder um einen vollqualifizierten Domänennamen handeln. Der Wert, den Sie für **SMTP-Server** eingeben, wird im `<SMTPServer>` -Feld in der Datei „rsreportserver.config“ gespeichert.

4. Geben Sie in der Dropdownliste **Authentifizierung** an, wie die Authentifizierung beim SMTP-Server erfolgen soll. Diese 

     - **Keine Authentifizierung** bedeutet, dass die Verbindung mit dem angegebenen Mailserver anonym hergestellt wird.
     
          Wenn Sie diese Option auswählen, wird `<SendUsing>` in der Datei „rsreportserver.config“ auf den Wert **2** und `<SMTPAuthenticate>` auf den Wert **0** festgelegt.
     
     - **Benutzername und Kennwort (Standard)** ermöglicht Ihnen, einen Benutzernamen und ein Kennwort zum Herstellen der Verbindung mit dem Mailserver anzugeben. Sie können außerdem **Sichere Verbindung verwenden** auswählen, damit der Benutzername und das Kennwort über eine verschlüsselte Verbindung an den Mailserver übertragen werden.
     
          Wenn Sie diese Option auswählen, wird `<SendUsing>` in der Datei „rsreportserver.config“ auf den Wert **2** und `<SMTPAuthenticate>` auf den Wert **1** festgelegt. Wenn Sie **Sichere Verbindung verwenden** auswählen, wird `SMTPUseSSL` auf **True**festgelegt. **Username** wird in `<SendUserName>` als verschlüsselter Wert festgelegt. **Password** wird in `<SendPassword>` als verschlüsselter Wert festgelegt.
     
     - **Berichtsserver-Dienstkonto (NTLM)** verwendet das Dienstkonto, das Sie für den Berichtsserver angegeben haben. Wenn Sie das Berichtsserver-Dienstkonto für die Authentifizierung verwenden, müssen Sie sicherstellen, dass das Dienstkonto auf dem SMTP-Server über die Berechtigung **Senden als** verfügt.
     
          Wenn Sie diese Option auswählen, wird `<SendUsing>` in der Datei „rsreportserver.config“ auf den Wert **2** und `<SMTPAuthenticate>` auf den Wert **2** festgelegt.

5. Wählen Sie **Anwenden**aus.

6. Optional können Sie in der Datei „rsreportserver.config“ weitere Felder für die E-Mail-Konfiguration anpassen.

## <a name="example-report-server-e-mail-configuration"></a>Beispielkonfiguration für Berichtsserver-E-Mail
Das folgende Beispiel veranschaulicht die Einstellungen für einen SMTP-Remoteserver in der Datei RSreportserver.config. Weitere Beschreibungen zu Einstellungen und gültigen Werten finden Sie unter [Rsreportserver.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) in der SQL Server-Onlinedokumentation.

```
<RSEmailDPConfiguration>
     <SMTPServer>mySMTPServer.Adventure-Works.com</SMTPServer>
     <SMTPServerPort></SMTPServerPort>
     <SMTPAccountName></SMTPAccountName>
     <SMTPConnectionTimeout></SMTPConnectionTimeout>
     <SMTPServerPickupDirectory></SMTPServerPickupDirectory>
     <SMTPUseSSL>False</SMTPUseSSL>
     <SendUsing>2</SendUsing>
     <SMTPAuthenticate>2</SMTPAuthenticate>
     <From>my-rs-email-account@Adventure-Works.com</From>
     <EmbeddedRenderFormats>
          <RenderingExtension>MHTML</RenderingExtension>
     </EmbeddedRenderFormats>
     <PrivilegedUserRenderFormats></PrivilegedUserRenderFormats>
     <ExcludedRenderFormats>
          <RenderingExtension>HTMLOWC</RenderingExtension>
          <RenderingExtension>NULL</RenderingExtension>
          <RenderingExtension>RGDI</RenderingExtension>
     </ExcludedRenderFormats>
     <SendEmailToUserAlias>True</SendEmailToUserAlias>
     <DefaultHostName></DefaultHostName>
     <PermittedHosts>
          <HostName>Adventure-Works.com</HostName>
          <HostName>hotmail.com</HostName>
     </PermittedHosts>
     <SendUserName></SendUserName>
     <SendPassword></SendPassword>
</RSEmailDPConfiguration>
```
## <a name="configuration-options-for-setting-the-to-field-in-a-message"></a>Konfigurationsoptionen für die Einstellung des "An:"-Felds in einer Nachricht
Benutzerdefinierte Abonnements, die gemäß den durch den Task „Einzelne Abonnements verwalten“ erteilten Berechtigungen erstellt werden, enthalten einen vorher festgelegten Benutzernamen, der auf dem Domänenbenutzerkonto basiert. Wenn der Benutzer das Abonnement erstellt, wird der Empfängername im **An:** -Feld mit dem Domänenbenutzerkonto der Person ausgefüllt, die das Abonnement erstellt.

Bei Verwendung eines SMTP-Servers bzw. einer Weiterleitung, der bzw. die E-Mail-Konten verwendet, die mit dem Domänenbenutzerkonto nicht übereinstimmen, erzeugt die Berichtsübermittlung einen Fehler, wenn der SMTP-Server den Bericht an diesen Benutzer übermitteln will.

Sie können die Konfigurationseinstellungen ändern, die Benutzern das Eingeben eines Namens im Feld **An:** ermöglichen, um das Problem zu umgehen:

1. Öffnen Sie RSReportServer.config mit einem Text-Editor.

2. Legen Sie `<SendEmailToUserAlias>` auf **False**fest.

3. Legen Sie `<DefaultHostName>` auf den DNS-Namen (Domain Name System) oder die IP-Adresse des SMTP-Servers bzw. der Weiterleitung fest.

4. Speichern Sie die Datei.

## <a name="configuration-options-for-remote-smtp-service"></a>Konfigurationsoptionen für den SMTP-Remotedienst
Die Verbindung zwischen dem Berichtsserver und einem SMTP-Server oder einer SMTP-Weiterleitung wird durch die folgenden Konfigurationseinstellungen bestimmt:

- `<SendUsing>` gibt eine Methode für das Senden von Nachrichten an. Sie können zwischen einem SMTP-Netzwerkdienst und einem lokalen SMTP-Dienstabholverzeichnis wählen. Um einen SMTP-Remotedienst zu verwenden, muss dieser Wert in der Datei RSReportServer.config auf **2** eingestellt werden.
- `<SMTPServer>` gibt den SMTP-Remoteserver bzw. die SMTP-Weiterleitung an. Dieser Wert ist erforderlich, wenn Sie einen SMTP-Remoteserver oder eine SMTP-Weiterleitung verwenden.
- `<From>` legt den Wert fest, der in der **Von:** -Zeile einer E-Mail angezeigt wird. Dieser Wert ist erforderlich, wenn Sie einen SMTP-Remoteserver oder eine SMTP-Weiterleitung verwenden.

Andere Werte, die für den SMTP-Remotedienst verwendet werden, sind folgende (diese Werte müssen Sie nur angeben, wenn Sie die Standardwerte überschreiben möchten).

- `<SMTPServerPort>` wird standardmäßig für Port 25 konfiguriert.
- `<SMTPAuthenticate>` gibt an, wie der Berichtsserver eine Verbindung mit dem SMTP-Remoteserver herstellt. Der Standardwert ist **0** (d.h. keine Authentifizierung). In diesem Fall wird die Verbindung über den anonymen Zugriff hergestellt. Je nach Domänenkonfiguration müssen der Berichtsserver und der SMTP-Server unter Umständen zu derselben Domäne gehören.
- Um E-Mail an eingeschränkte Verteilerlisten zu senden (z.B. Verteilerlisten, die nur eingehende Nachrichten von authentifizierten Konten akzeptieren), legen Sie `<SMTPAuthenticate>` auf **1** oder **2**fest. Wenn Sie den Wert auf **1**festlegen, müssen Sie auch `<SendUserName>` und `<SendPassword>`festlegen. Es wird empfohlen, dazu den Konfigurations-Manager für Reporting Services zu verwenden, weil dieser die Werte für `<SendUserName>` und `<SendPassword>`verschlüsselt.

### <a name="to-configure-a-remote-smtp-service-for-the-report-server"></a>So konfigurieren Sie einen Remote-SMTP-Dienst für den Berichtsserver

> [!NOTE] 
> Es wird empfohlen, den Mailserver über den Konfigurations-Manager für Reporting Services zu konfigurieren.

1. Überprüfen Sie, ob der Report Server-Windows-Dienst über **Send As** -Berechtigungen auf dem SMTP-Server verfügt.

2. Öffnen Sie die Datei RSReportServer.config in einem Text-Editor.

3. Überprüfen Sie, ob `<UrlRoot>` auf die URL-Adresse des Berichtsservers festgelegt ist. Dieser Wert wird beim Konfigurieren des Berichtsservers festgelegt und sollte bereits ausgefüllt sein. Geben Sie andernfalls die URL-Adresse des Berichtsservers ein.

4. Suchen Sie im Abschnitt „Delivery“ nach `<RSEmailDPConfiguration>`.
     
5. Geben Sie in `<SMTPServer>`den Namen des SMTP-Servers ein. Bei diesem Wert kann es sich um eine IP-Adresse, den UNC-Namen eines Computers im Firmenintranet oder um einen vollqualifizierten Domänennamen handeln.

6. Legen Sie `<SendUsing>` auf den Wert **2** fest, um das Dienstkonto für den Berichtsserver zu verwenden. Legen Sie `<SendUsing>` auf den Wert **1** fest, um die Standardauthentifizierung zu verwenden. Wenn Sie den Wert **1**festlegen, müssen Sie außerdem einen Wert für `<SendUserName>` und `<SendPassword>`festlegen. Wenn diese Werte verschlüsselt werden sollen, müssen Sie die Authentifizierung mit dem Konfigurations-Manager für Reporting Services festlegen.

7. Legen Sie `<SMTPAuthenticate>` auf den Wert **1** fest, wenn Sie `<SendUsing>` auf 1 oder 2 festlegen.

7. Legen Sie `<From>`fest. Sie müssen ein Benutzerkonto angeben, das über die Berechtigung zum Senden von E-Mails vom SMTP-Server verfügt.

8. Speichern Sie die Datei.

     Die neuen Einstellungen werden automatisch vom Berichtsserver verwendet, Sie müssen den Dienst nicht neu starten. Sie können weitere SMTP-Einstellungen angeben, um die Verwendung des SMTP-Servers für die Berichtsserver-E-Mail-Übermittlung weiter zu konfigurieren.

## <a name="configuration-options-for-local-smtp-service"></a>Konfigurationsoptionen für den lokalen SMTP-Dienst
Das Konfigurieren eines lokalen SMTP-Dienstes ist sinnvoll, wenn Sie die E-Mail-Übermittlung des Berichtsservers testen oder entsprechende Probleme behandeln. Der lokale SMTP-Dienst ist standardmäßig nicht aktiviert.

Die Verbindung zwischen dem Berichtsserver und einem lokalen SMTP-Server oder einer SMTP-Weiterleitung wird durch die folgenden Konfigurationseinstellungen bestimmt:

- **SendUsing** ist auf **1**festgelegt.
- Für**SMTPServerPickupDirectory** ist ein Ordner auf dem lokalen Laufwerk festgelegt.

  > [!NOTE] 
  > Stellen Sie sicher, dass bei Verwendung eines lokalen SMTP-Servers nicht „SMTPServer“ festgelegt wurde.

- **From** legt den Wert fest, der in der **Von:** -Zeile einer E-Mail angezeigt wird. Dieser Wert ist erforderlich.

### <a name="to-configure-a-local-smtp-service-for-the-report-server"></a>So konfigurieren Sie einen lokalen SMTP-Dienst für den Berichtsserver

1. Wählen Sie in der Systemsteuerung **Windows-Features aktivieren oder deaktivieren** aus, um den **Assistenten zum Hinzufügen von Rollen und Features**zu starten.

2. Wählen Sie **Rollenbasierte oder featurebasierte Installation** aus, und klicken Sie auf **Weiter**.

3. Wählen Sie den Server aus, auf dem Internetinformationsdienste (IIS) installiert werden sollen, und klicken Sie auf **Weiter**.

4. Klicken Sie auf der Seite für **Serverrollen** * auf *Weiter*.
     
5. Wählen Sie auf der Seite *Features* die Option **SMTP-Server** aus, und klicken Sie auf **Weiter**.

     Wenn Sie zum Hinzufügen von Features aufgefordert werden, die für den SMTP-Server erforderlich sind, klicken Sie auf **Features hinzufügen**.

6. Klicken Sie auf der Seite **Rolle "Webserver" (IIS)** auf *Weiter* .

7. Klicken Sie auf der Seite **Rollendienste** auf *Weiter* .

8. Klicken Sie auf der Seite **Bestätigung** auf **Installieren** .

9. Vergewissern Sie sich in der Dienstekonsole, dass der Windows-Dienst **Simple Mail Transfer Protocol (SMTP)** ausgeführt wird.

     Zum Konfigurieren des lokalen SMTP-Servers müssen Sie in den Verwaltungstools den IIS 6.0-Manager verwenden.

10. Öffnen Sie die Datei RSReportServer.config in einem Text-Editor.

11. Überprüfen Sie, ob `<UrlRoot>` auf die URL-Adresse des Berichtsservers festgelegt ist. Dieser Wert wird beim Konfigurieren des Berichtsservers festgelegt und sollte bereits ausgefüllt sein. Wenn sie noch nicht festgelegt ist, geben Sie die Webdienst-URL-Adresse für Ihren Berichtsserver ein.

12. Suchen Sie im Abschnitt „Delivery“ nach `<RSEmailDPConfiguration>`.
     
13. Stellen Sie sicher, dass `<SMTPServer>` vorhanden, aber leer ist.
     
14. Legen Sie `<SendUsing>` auf 1 fest.
     
14. Legen Sie `<SMTPAuthenticate>` auf 0 fest.
     
15. Legen Sie `<SMTPServerPickupDirectory>` auf den Abholordner für den SMTP-Dienst fest.
     
     Standardmäßig ist dies *C:\inetpub\mailroot\Pickup*.
     
16. Legen Sie `<From>`fest. Dadurch wird der Wert festgelegt, der in der **Von:** -Zeile einer E-Mail angezeigt wird.
     
17. Speichern Sie die Datei.
  
## <a name="see-also"></a>Siehe auch  
[Reporting Services-Konfigurations-Manager (einheitlicher Modus)](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
[Ändern einer Reporting Services-Konfigurationsdatei (rsreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
[Rsreportserver.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)
  
  

