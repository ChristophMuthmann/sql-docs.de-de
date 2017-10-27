---
title: Konfigurieren der Berichtsserver-Dienstkontos (SSRS-Konfigurations-Manager) | Microsoft Docs
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f880c623-67c8-4167-b98b-ace17e800faa
caps.latest.revision: 14
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3e1fde5db0ebdf332d82cdb7269342aea036ec61
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="configure-the-report-server-service-account-ssrs-configuration-manager"></a>Konfigurieren des Berichtsserver-Dienstkontos (SSRS-Konfigurations-Manager)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] wird als Einzeldienst mit einem Report Server-Webdienst (Berichts-Manager), [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)], und einer Hintergrundverarbeitungsanwendung implementiert, die für die geplante Berichtsverarbeitung und die Abonnementübermittlung verwendet wird. In diesem Thema wird erläutert, wie das Dienstkonto zu Beginn konfiguriert wird. Außerdem wird beschrieben, wie das Konto oder das Kennwort mit dem Reporting Services-Konfigurationstool geändert wird.  
  
## <a name="initial-configuration"></a>Anfängliche Konfiguration  
 Das Berichtsserver-Dienstkonto wird während der Ausführung von Setup definiert. Sie können den Dienst unter einem Domänenbenutzerkonto oder unter einem integrierten Konto wie einem **virtuellen Dienstkonto**ausführen. Da es kein Standardkonto gibt, wird das Konto, das Sie auf der Seite **Dienstkonten** des Installations-Assistenten angeben, als Konto für den Berichtsserver-Dienst verwendet.  
  
> [!IMPORTANT]  
>  Obwohl der Berichtsserver-Webdienst und [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] separate [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] -Anwendungen sind, werden sie unter einer einzelnen Dienstarchitektur innerhalb der gleichen Berichtsserver-Prozessidentität ausgeführt.  
  
> [!NOTE]  
>  Integrierte Windows-Dienstkonten (Lokaler Dienst oder Netzwerkdienst) werden auf einem Domänencontrollercomputer nicht als Berichtsserver-Dienstkonten unterstützt.  
  
## <a name="changing-the-service-account"></a>Ändern des Dienstkontos  
 Verwenden Sie stets den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurations-Manager, um die Informationen für das Dienstkonto anzuzeigen und neu zu konfigurieren. Die Informationen zur Dienstidentität werden intern an mehreren Speicherorten gespeichert. Durch die Verwendung des Tools wird sichergestellt, dass alle Verweise entsprechend aktualisiert werden, wenn Sie das Konto oder das Kennwort ändern. Vom [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurations-Manager werden die folgenden zusätzlichen Schritte ausgeführt, um sicherzustellen, dass der Berichtsserver verfügbar bleibt:  
  
-   Das neue Konto wird automatisch der auf dem lokalen Computer erstellten Berichtsservergruppe hinzugefügt. Diese Gruppe wird in den Zugriffssteuerungslisten (Access Control Lists, ACLs) angegeben, die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dateien schützen.  
  
-   Die Anmeldeberechtigungen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz, die als Host für die Berichtsserver-Datenbank fungiert, werden automatisch aktualisiert. Das neue Konto wird der **RSExecRole**hinzugefügt.  
  
     Die Datenbankanmeldung für das alte Konto wird nicht automatisch entfernt. Stellen Sie sicher, dass nicht mehr benötigte Konten entfernt werden. Weitere Informationen finden Sie unter [Verwalten einer Berichtsserver-Datenbank &#40; SSRS im einheitlichen Modus &#41; ](../../reporting-services/report-server/administer-a-report-server-database-ssrs-native-mode.md) in SQL Server-Onlinedokumentation.  
  
     Um einem neuen Dienstkonto Datenbankberechtigungen gewähren zu können, muss die Berichtsserver-Datenbankverbindung zuvor für das Dienstkonto konfiguriert worden sein. Wenn Sie die Berichtsserver-Datenbankverbindung für ein Domänenbenutzerkonto oder eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankanmeldung konfiguriert haben, hat die Aktualisierung des Dienstkontos keine Auswirkungen auf die Verbindungsinformationen.  
  
-   Der Verschlüsselungsschlüssel wird automatisch aktualisiert, sodass er die Profilinformationen des neuen Kontos enthält.  
  
    > [!NOTE]  
    >  Wenn der Berichtsserver Teil einer Bereitstellung für horizontales Skalieren ist, ist nur der Berichtsserver betroffen, den Sie aktualisieren. Auf die Verschlüsselungsschlüssel für andere Berichtsserver in der Bereitstellung hat die Änderung des Dienstkontos keine Auswirkung.  
      
## <a name="to-configure-the-report-server-service-account"></a>So konfigurieren Sie das Berichtsserver-Dienstkonto  
  
1.  Starten Sie den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurations-Manager, und stellen Sie eine Verbindung mit dem Berichtsserver her.  
  
2.  Wählen Sie auf der Seite Dienstkontoseite die Option aus, die den gewünschten Kontotyp beschreibt.  
  
3.  Wenn Sie ein Windows-Benutzerkonto ausgewählt haben, geben Sie das neue Konto und das Kennwort an. Der Kontoname darf nicht länger als 20 Zeichen sein.  
  
     Wenn der Berichtsserver in einem Netzwerk bereitgestellt wird, der die Kerberos-Authentifizierung unterstützt, müssen Sie den Berichtsserver-Dienstprinzipalnamen (Service Principal Name, SPN) mit dem Domänenbenutzerkonto registrieren, das Sie soeben angegeben haben. Weitere Informationen finden Sie unter [Register a Service Principal Name &#40;SPN&#41; for a Report Server](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md) (Registrieren eines Dienstprinzipalnamens [SPN] für einen Berichtsserver).  
  
4.  Klicken Sie auf **Anwenden**.  
  
5.  Geben Sie bei der Aufforderung zum Sichern des symmetrischen Schlüssels einen Dateinamen und einen Speicherort für die Sicherung des symmetrischen Schlüssels ein, geben Sie ein Kennwert zum Sperren und Entsperren der Datei ein, und klicken Sie auf **OK**.  
  
6.  Wenn der Berichtsserver die Verbindung zur Berichtsserver-Datenbank mithilfe des Dienstkontos erstellt, werden die Verbindungsinformationen auf das neue Konto oder Kennwort aktualisiert. Zum Aktualisieren der Verbindungsinformationen ist eine Verbindung mit der Datenbank erforderlich. Wenn das Dialogfeld für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **-Datenbankverbindung** angezeigt wird, geben Sie die Anmeldeinformationen ein, die zur Verbindung mit der Datenbank berechtigen, und klicken Sie anschließend auf **OK**.  
  
7.  Geben Sie bei der Aufforderung zum Wiederherstellen des symmetrischen Schlüssels das in Schritt 5 angegebene Kennwort ein, und klicken Sie auf **OK**.  
  
8.  Überprüfen Sie die Statusmeldungen im Ergebnisbereich, um zu überprüfen, ob alle Tasks erfolgreich abgeschlossen wurden.  
  
## <a name="choosing-an-account"></a>Auswählen eines Kontos  
 Geben Sie am besten ein Konto an, das über Berechtigungen für Netzwerkverbindungen verfügt und auf die Netzwerkdomänencontroller und die SMTP-Server oder -Gateways des Unternehmens zugreifen kann. In der folgenden Tabelle werden die Konten zusammengefasst und Empfehlungen für ihre Verwendung gegeben.  
  
|Konto|Erklärung|  
|-------------|-----------------|  
|Domänenbenutzerkonten|Wenn Sie über ein Windows-Domänenbenutzerkonto verfügen, das mindestens die für Berichtsservervorgänge erforderlichen Berechtigungen aufweist, sollten Sie dieses verwenden.<br /><br /> Ein Domänenbenutzerkonto wird empfohlen, da es den Berichtsserverdienst von anderen Anwendungen trennt. Wenn Sie mehrere Anwendungen unter einem freigegebenen Konto wie Netzwerkdienst ausführen, steigt das Risiko, dass böswillige Benutzer die Kontrolle über den Berichtsserver erlangen, da sich eine Sicherheitsverletzung in einer Anwendung leicht auf alle anderen Anwendungen auswirken kann, die unter diesem Konto ausgeführt werden.<br /><br /> Wenn Sie ein Domänenbenutzerkonto verwenden, ist eine Änderung Ihres Kennworts in regelmäßigen Abständen erforderlich, sofern eine entsprechende Richtlinie von Ihrer Organisation angewendet wird. Möglicherweise müssen Sie auch den Dienst für das Benutzerkonto registrieren. Weitere Informationen finden Sie unter [Register a Service Principal Name &#40;SPN&#41; for a Report Server](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md) (Registrieren eines Dienstprinzipalnamens [SPN] für einen Berichtsserver).<br /><br /> Verwenden Sie kein lokales Windows-Benutzerkonto. Lokale Konten weisen in der Regel keine ausreichenden Berechtigungen für den Zugriff auf Ressourcen auf anderen Computern auf. Weitere Informationen über Einschränkungen der Berichtsserverfunktion bei Verwendung lokaler Konten finden Sie unter [Überlegungen zur Verwendung lokaler Konten](#localaccounts) in diesem Thema.|  
|**virtuellen Dienstkonto**|Das**virtuelle Dienstkonto** repräsentiert den Windows-Dienst. Es ist ein integriertes Konto mit Minimalprivilegien, das über Berechtigungen für die Netzwerkanmeldung verfügt. Dieses Konto wird empfohlen, wenn kein Domänenbenutzerkonto verfügbar ist oder wenn Sie mögliche Dienstausfälle aufgrund von Richtlinien zum Ablauf von Kennwörtern vermeiden möchten.|  
|**Netzwerkdienst**|**Netzwerkdienst** ist ein integriertes Konto mit Minimalprivilegien, das über Berechtigungen für die Netzwerkanmeldung verfügt. <br /><br /> Versuchen Sie, die Anzahl der Dienste, die unter einem Konto ausgeführt werden, so gering wie möglich zu halten, wenn Sie **Netzwerkdienst**auswählen. Eine Sicherheitsverletzung bei einer Anwendung gefährdet die Sicherheit aller anderen Anwendungen, die unter diesem Konto ausgeführt werden.|  
|**Lokaler Dienst**|**Lokaler Dienst** ist ein integriertes Konto, das einem authentifizierten lokalen Windows-Benutzerkonto entspricht. Bei Diensten, die unter dem Konto **Lokaler Dienst** ausgeführt werden, erfolgt der Zugriff auf Netzwerkressourcen als NULL-Sitzung ohne Anmeldeinformationen. Dieses Konto ist nicht für Bereitstellungsszenarien im Intranet geeignet, bei denen eine Verbindung zwischen dem Berichtsserver und einer Remoteberichtsserver-Datenbank oder einem Netzwerkdomänencontroller hergestellt werden muss, um einen Benutzer vor dem Öffnen eines Berichts oder vor dem Verarbeiten eines Abonnements zu authentifizieren.|  
|**Lokales System**|**Lokales System** ist ein Konto mit weit reichenden Berechtigungen, das für die Ausführung eines Berichtsservers nicht erforderlich ist. Verwenden Sie dieses Konto nicht für Berichtsserverinstallationen. Wählen Sie stattdessen ein Domänenkonto oder einen **Netzwerkdienst** aus.|  
  
##  <a name="localaccounts"></a> Überlegungen zur Verwendung lokaler Konten  
 Die vorrangige Überlegung im Hinblick auf die Verwendung lokaler Konten ist, ob der Berichtsserver auf Remotedatenbankserver, Mailserver und Domänencontroller zugreifen muss. Wenn Sie den Berichtsserver als lokales Windows-Benutzerkonto, lokalen Dienst oder lokales System konfigurieren, müssen bestimmte Überlegungen bei anderen Konfigurationseinstellungen sowie bei der Erstellung und Übermittlung von Abonnements berücksichtigt werden:  
  
-   Durch die Ausführung des Dienstes unter einem lokalen Konto werden die Optionen eingeschränkt, die später beim Konfigurieren einer Verbindung mit einer Remoteberichtsserver-Datenbank verfügbar sind. Genauer gesagt: Wenn Sie eine Remoteberichtsserver-Datenbank verwenden, müssen Sie die Verbindung so konfigurieren, dass ein Domänenbenutzerkonto oder ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankbenutzer verwendet wird, das bzw. der über die Berechtigung zur Anmeldung an der Remoteinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügt.  
  
-   Mit der Ausführung des Dienstes unter einem lokalen Konto sind neue Anforderungen im Hinblick auf die Erstellung von Abonnements verbunden. Der Berichtsserver speichert Informationen zum Benutzer, der das Abonnement erstellt. Wenn der Benutzer das Abonnement erstellt, während er mit einem Domänenkonto angemeldet ist, versucht der Berichtsserver-Dienst, eine Verbindung mit einem Domänencontroller herzustellen, um den Benutzer zu authentifizieren, wenn das Abonnement verarbeitet wird. Wenn der Dienst unter einem lokalen Konto ausgeführt wird, löst die Authentifizierungsanforderung einen Fehler aus, wenn der Berichtsserver versucht, die Anforderung an einen Remotedomänencontroller zu senden. Sie können diese Beschränkung umgehen, indem Sie eine formularbasierte Authentifizierungserweiterung verwenden oder alle Benutzer anweisen, die Verbindung mit einem Berichtsserver über ein lokales Benutzerkonto herzustellen.  
  
-   Mit der Ausführung des Dienstes unter einem lokalen Konto sind neue Anforderungen im Hinblick auf die Übermittlung von Abonnements verbunden. Die Abonnementdefinitionen einiger Übermittlungserweiterungen enthalten Benutzerkontoinformationen. Wenn Sie Berichte an E-Mail-Adressen senden, die auf Domänenbenutzerkonten basieren, und den Berichtsserver-Dienst unter einem lokalen Konto ausführen, kann dieser zum Auflösen der Ziel-E-Mail-Konten nicht auf einen Remotedomänencontroller zugreifen.  
  
-   Integrierte Windows-Dienstkonten (Lokaler Dienst oder Netzwerkdienst) werden auf einem Domänencontrollercomputer nicht als Berichtsserver-Dienstkonten unterstützt.  
  
Die folgenden Richtlinien und Links in diesem Abschnitt können Ihnen helfen, den für Ihre Bereitstellung am besten geeigneten Ansatz zu finden.  
  
-   [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) in SQL Server-Onlinedokumentation.  
  
-   [The Services and Service Accounts Security Planning Guide](http://go.microsoft.com/fwlink/?LinkId=69155) auf MSDN.  
  
## <a name="updating-an-expired-password"></a>Aktualisieren eines abgelaufenen Kennworts  
 Wenn der Berichtsserver-Dienst unter einem Domänenkonto ausgeführt wird und das Kennwort abläuft, bevor Sie es im Reporting Services-Konfigurations-Manager aktualisieren können, wird der Dienst erst wieder gestartet, wenn Sie ein neues Kennwort angeben.  
  
 Wenn das Kennwort des Dienstkontos für das [!INCLUDE[ssDE](../../includes/ssde-md.md)] abgelaufen ist, tritt beim Versuch, eine Verbindung mit dem Berichtsserver herzustellen, der Fehler **rsReportServerDatabaseUnavailable** auf. Durch Zurücksetzen des Kennworts wird der Fehler behoben.  
  
## <a name="troubleshooting-service-identity-update-errors"></a>Problembehandlung bei Fehlern beim Update der Dienstidentität  
 Durch Ändern der Dienstidentität wird eine Reihe von Ereignissen ausgelöst, einschließlich Neustart des Diensts, Aktualisieren des kennwortgeschützten Verschlüsselungsschlüssels, Aktualisieren von URL-Reservierungen und Aktualisieren der Verbindungsinformationen für die Berichtsserver-Datenbank, wenn Sie das Dienstkonto zum Herstellen der Verbindung zur Berichtsserver-Datenbank verwenden. Sie können den Status dieser Ereignisse überwachen, indem Sie die Benachrichtigungen im Ergebnisbereich unten auf der Seite anzeigen. Wenn während dieses Prozesses Fehler auftreten, können Sie versuchen, sie mit den folgenden Techniken zu beheben:  
  
-   Wenn der symmetrische Schlüssel nicht wiederhergestellt werden kann, können Sie versuchen, ihn manuell wiederherzustellen, indem Sie auf der Seite mit Verschlüsselungsschlüsseln auf **Wiederherstellen** klicken. Wenn das nicht funktioniert, erwägen Sie, den verschlüsselten Inhalt zu löschen. Sie müssen die Verbindungsinformationen und Abonnements für die Datenquelle neu erstellen, der übrige Inhalt ist jedoch weiterhin verfügbar. Weitere Informationen finden Sie unter [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
-   Wird der Dienst nicht gestartet, starten Sie ihn manuell über die Dienstkonsolenanwendung in der Verwaltung.  
  
-   URL-Reservierungsfehler können auftreten, wenn Sie das Dienstkonto aktualisieren. Jede URL-Reservierung umfasst eine Sicherheitsbeschreibung mit einer freigegebenen Zugriffssteuerungsliste (Discretionary Access Control List, DACL), die das Dienstkonto berechtigt, Anforderungen für die URL zu akzeptieren. Wenn Sie das Konto aktualisieren, muss die URL erneut erstellt werden, um die DACL mit den neuen Kontoinformationen zu aktualisieren. Wenn die URL-Reservierung nicht neu erstellt werden kann und das Konto mit Sicherheit gültig ist, versuchen Sie, den Computer neu zu starten. Wenn der Fehler weiterhin auftritt, versuchen Sie, ein anderes Konto zu verwenden.  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren von Berichtsserver-URLs &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Reporting Services-Konfigurations-Manager &#40; Im einheitlichen Modus &#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)

