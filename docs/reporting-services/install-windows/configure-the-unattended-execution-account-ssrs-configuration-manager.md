---
title: "Konfigurieren des unbeaufsichtigten Ausführungskontos (SSRS-Konfigurations-Manager) | Microsoft Docs"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- no credentials option [Reporting Services]
- security [Reporting Services], unattended report processing
- unattended report processing [Reporting Services]
- credentials [Reporting Services]
- external data sources [Reporting Services]
- accounts [Reporting Services]
- reports [Reporting Services], processing
ms.assetid: 4e50733e-bd8c-4bf6-8379-98b1531bb9ca
caps.latest.revision: 10
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4c18054b5c11569239af51e7c3808bdb9ce05109
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="configure-the-unattended-execution-account-ssrs-configuration-manager"></a>Konfigurieren des unbeaufsichtigten Ausführungskontos (SSRS-Konfigurations-Manager)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] stellt ein besonderes Konto bereit, das für die unbeaufsichtigte Berichtsverarbeitung und zum Senden von Verbindungsanforderungen über das Netzwerk verwendet wird. Das Konto wird bei folgenden Vorgängen verwendet:  
  
-   Senden Sie Verbindungsanforderungen über das Netzwerk für Berichte, die Datenbankauthentifizierung verwenden, oder stellen Sie die Verbindung mit externen Berichtsdatenquellen her, für die keine Authentifizierung erforderlich ist oder verwendet wird. Weitere Informationen finden Sie unter [Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md) in der SQL Server-Onlinedokumentation.  
  
-   Abrufen externer Imagedateien, die im Bericht verwendet werden. Wenn Sie eine Bilddatei verwenden möchten, auf die kein anonymer Zugriff möglich ist, können Sie das Konto für die unbeaufsichtigte Berichtsverarbeitung konfigurieren und dem Konto die Zugriffsberechtigung für die Datei erteilen.  
  
 Mit unbeaufsichtigter Berichtsverarbeitung wird jede Berichtsausführung bezeichnet, die durch ein Ereignis (entweder ein geplantes Ereignis oder ein Datenaktualisierungsereignis) und nicht durch eine Benutzeranforderung ausgelöst wird. Der Berichtsserver verwendet das Konto für die unbeaufsichtigte Berichtsverarbeitung, um sich am Computer anzumelden, der die externe Datenquelle hostet. Dieses Konto ist erforderlich, da die Anmeldeinformationen des für den Berichtsserver verwendeten Dienstkontos nie für Verbindungen mit anderen Computern verwendet werden.  
  
> [!IMPORTANT]  
>  Das Konfigurieren des Kontos ist optional. Wenn Sie es jedoch nicht konfigurieren, beschränken Sie die Möglichkeiten zur Verbindung mit einigen Datenquellen und können möglicherweise keine Imagedateien von Remotecomputern abrufen. Wenn Sie das Konto konfigurieren, müssen Sie es auf dem neuesten Stand halten. Besonders, wenn Sie das Ablaufen eines Kennworts zulassen oder wenn die Kontoinformationen in Active Directory geändert werden, tritt bei der nächsten Verarbeitung eines Berichts der folgende Fehler auf: "Fehler bei der Anmeldung (rsLogonFailed) Anmeldefehler: unbekannter Name oder falsches Kennwort." Die ordnungsgemäße Verwaltung des Kontos für die unbeaufsichtigte Berichtsverarbeitung ist wesentlich, auch wenn Sie nie externe Images abrufen oder Verbindungsanforderungen an externe Computer senden. Wenn Sie das Konto konfigurieren und dann doch nicht verwenden, können Sie es löschen und so routinemäßige Kontoverwaltungsaufgaben vermeiden.  
  
## <a name="how-to-configure-the-account"></a>Konfigurieren des Kontos  
 Sie müssen ein Domänenbenutzerkonto verwenden. Damit das Konto seinen Zweck erfüllt, sollte es nicht mit dem Konto identisch sein, unter dem Report Server-Webdienst ausgeführt wird. Verwenden Sie unbedingt ein Konto mit minimalen Berechtigungen (Nur-Lese-Zugriff mit Berechtigungen für Netzwerkverbindungen ist ausreichend) und eingeschränktem Zugriff auf die Computer, die Datenquellen und Ressourcen für den Berichtsserver bereitstellen.  
  
 Verwenden Sie zum Angeben des Kontos das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool oder das Hilfsprogramm **rsconfig** . Das einfachste Verfahren zum Konfigurieren des Kontos für die unbeaufsichtigte Ausführung besteht darin, das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool auszuführen und die Anmeldeinformationen auf der Seite Ausführungskonto anzugeben.  
  
1.  Starten Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Konfigurationstool, und stellen Sie eine Verbindung zu der zu konfigurierenden Berichtsserverinstanz her. Weitere Informationen finden Sie unter [Reporting Services-Konfigurations-Manager &#40;einheitlicher Modus&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).  
  
2.  Wählen Sie auf der Seite „Ausführungskonto“ die Option **Ausführungskonto angeben** aus.  
  
3.  Geben Sie das Konto und das Kennwort ein, geben Sie das Kennwort erneut ein, und klicken Sie anschließend auf **Anwenden**.  
  
### <a name="using-rsconfig-utility"></a>Verwendung des RSCONFIG-Hilfsprogramms  
 Eine andere Möglichkeit, das Konto festzulegen, bietet das **rsconfig** -Hilfsprogramm. Verwenden Sie zum Angeben des Kontos das **-e** -Argument von **rsconfig**. Die Angabe des **-e** -Arguments für **rsconfig** bewirkt, dass das Hilfsprogramm die Kontoinformationen in die Konfigurationsdatei schreibt. Sie müssen keinen Pfad zu RSReportServer.Config angeben. Führen Sie folgende Schritte aus, um das Konto zu konfigurieren.  
  
1.  Erstellen Sie ein Domänenkonto, oder wählen Sie ein Domänenkonto aus, das auf Computer und Server zugreifen kann, die Daten oder Dienste für einen Berichtsserver bereitstellen. Sie sollten ein Konto verwenden, das über beschränkte Berechtigungen verfügt (z. B. Nur-Lese-Zugriff).  
  
2.  Öffnen Sie eine Eingabeaufforderung: Klicken Sie im **Startmenü** auf **Ausführen**, geben Sie **cmd**ein, und klicken Sie anschließend auf **OK**.  
  
3.  Geben Sie den folgenden Befehl ein, um das Konto in einer lokalen Berichtsserverinstanz zu konfigurieren:  
  
     **RSConfig -e -u\<Domäne/Benutzername > – p\<Kennwort >**  
  
 **rsconfig -e** unterstützt weitere Argumente. Weitere Informationen zur Syntax und zum Anzeigen von Beispielbefehlen finden Sie in der SQL Server-Onlinedokumentation unter [rsconfig-Hilfsprogramm &#40;SSRS&#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md).  
  
### <a name="how-account-information-is-stored"></a>Speichern von Kontoinformationen  
 Wenn Sie das Konto festlegen, werden die folgenden Einstellungen als verschlüsselte Werte in der Datei RSreportserver.config in einer lokalen oder einer Remote-Berichtsserverinstanz angegeben:  
  
```  
<UnattendedExecutionAccount>  
     <UserName></UserName>  
     <Password></Password>  
     <Domain></Domain>  
</UnattendedExecutionAccount>  
```  
  
 Nachdem Sie die Werte festgelegt haben, können Sie sie nicht mehr entschlüsseln, um sie als Nur-Text anzuzeigen. Wenn Sie die Werte falsch eingeben oder die angegebenen Werte vergessen, müssen Sie das Reporting Services-Konfigurationstool verwenden oder **rsconfig -e** ausführen, um von vorn zu beginnen.  
  
## <a name="how-to-use-the-unattended-report-processing-account"></a>Verwenden des Kontos für die unbeaufsichtigte Berichtsverarbeitung  
 Zum Abrufen von Imagedateien verwendet der Berichtsserver das Konto automatisch, ohne dass Sie aktiv werden müssen. Sie müssen auf der Seite „Datenquelleneigenschaften“ der Berichtsdatenquelle oder der freigegebenen Datenquelle eine Option für den **Anmeldeinformationstyp** festlegen, um über das Konto eine Verbindung mit externen Datenquellen von Berichtsdaten herzustellen:  
  
-   Aktivieren Sie im [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] oder auf einer SharePoint-Website die Option **Anmeldeinformationen sind nicht erforderlich** .  
  
 Das Konto für die unbeaufsichtigte Berichtsverarbeitung wird hauptsächlich dazu verwendet, die Verbindung mit externen Servern herzustellen, und nicht für die Anmeldung bei Datenbankservern. Möchten Sie die Kontoanmeldeinformationen zur Anmeldung an einer Datenbank verwenden, müssen Sie die Anmeldeinformationen in der Verbindungszeichenfolge angeben. Sie können **Integrated Security=SSPI** angeben, wenn der Datenbankserver die integrierte Sicherheit von Windows unterstützt und das für die unbeaufsichtigte Berichtsverarbeitung verwendete Konto über die Berechtigung zum Lesen der Datenbank verfügt. Andernfalls müssen Sie den Benutzernamen und das Kennwort in die Verbindungszeichenfolge eingeben. Dort wird es als Klartext jedem Benutzer angezeigt, der zur Bearbeitung von Datenquellen-Verbindungseigenschaften berechtigt ist.  
  
 Obwohl dies möglich ist, sollten Sie das unbeaufsichtigte Berichtsverarbeitungskonto nicht zum Abrufen von Daten nach dem Herstellen der Verbindung verwenden. Das Konto ist für ganz spezielle Funktionen gedacht. Wenn Sie es zum Abrufen von Daten verwenden, untergraben Sie seinen eigentlichen Zweck.  
  
## <a name="how-to-maintain-the-unattended-report-processing-account"></a>Warten des Kontos für die unbeaufsichtigte Berichtsverarbeitung  
 Wenn Sie das Konto definiert haben, müssen Sie sicherstellen, dass das Konto und das Kennwort immer aktuell sind. Sie können das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool verwenden, um die Konfigurationseinstellungen zu aktualisieren, in denen Informationen zu diesem Konto gespeichert sind.  
  
1.  Starten Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool, und stellen Sie eine Verbindung zu der zu konfigurierenden Berichtsserverinstanz her.  
  
2.  Überprüfen Sie, ob auf der Seite „Ausführungskonto“ die Option **Ausführungskonto angeben** ausgewählt ist.  
  
3.  Geben Sie das neue Konto oder Kennwort ein, geben Sie das Kennwort erneut ein, und klicken Sie anschließend auf **Anwenden**.  
  
## <a name="how-to-delete-the-unattended-report-processing-account"></a>Löschen des Kontos für die unbeaufsichtigte Berichtsverarbeitung  
 Wenn Sie das Konto nicht verwenden, können Sie es löschen, um routinemäßige Kontoverwaltungsaufgaben zu vermeiden.  
  
1.  Starten Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool, und stellen Sie eine Verbindung zu der zu konfigurierenden Berichtsserverinstanz her.  
  
2.  Deaktivieren Sie auf der Seite „Ausführungskonto“ die Option **Ausführungskonto angeben**.  
  
3.  Klicken Sie auf **Anwenden**.  
  
 Die Kontoinformationen werden aus der Datei RSReportServer.config entfernt.  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Konfigurations-Manager (einheitlicher SSRS-Modus)](http://msdn.microsoft.com/en-us/379eab68-7f13-4997-8d64-38810240756e)  
  
  

