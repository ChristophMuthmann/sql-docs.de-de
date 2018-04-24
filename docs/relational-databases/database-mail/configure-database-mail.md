---
title: Konfigurieren des Datenbank-E-Mail-Features | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: database-mail
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.sqlimail.profileandaccountmanagement.f1
- sql13.swb.sqlimail.newaccount.f1
- sql13.swb.dbmail. manageprofilesecurity.profileview.f1
- sql13.swb.sqlimail.manageexistingprofile.f1
- sql13.swb.sqlimail.addaccounttoprofile.f1
- sql13.swb.dbmail.manageexistingaccount.f1
- sql13.swb.sqlimail.manageprofilesecurity.profileview.f1
- sql13.swb.sqlimail.welcome.f1
- sql13.swb.sqlimail.manageprofilesecurity.principalview.f1
- sql13.swb.sqlimail.newsqlimailaccount.f1
- sql13.swb.sqlimail.selectconfiguration.f1
- sql13.swb.dbmail.completewizard.f1
- sql13.swb.dbmail.sendtestemail.test.f1
- sql13.swb.sqlimail.newprofile.f1
- sql13.swb.dbmail.addaccounttoprofile.f1
- sql13.swb.dbmail.newprofile.f1
- sql13.swb.sqlimail.manageexistingaccount.f1
- sql13.swb.dbmail.welcome.f1
- sql13.swb.dbmail.newaccount.f1
- sql13.swb.dbmail.profileandaccountmanagement.f1
- sql13.swb.dbmail.selectconfiguration.f1
- sql13.swb.dbmail.sendtestemail.f1
- sql13.swb.sqlimail.completewizard.f1
- sql13.swb.dbmail.configuresystem.f1
- sql13.swb.sqlimail.configuresystem.f1
- sql13.swb.dbmail.newsqlimailaccount.f1
- sql13.swb.dbmail.manageexistingprofile.f1
- sql13.swb.dbmail.manageprofilesecurity.principalview.f1
ms.assetid: 7edc21d4-ccf3-42a9-84c0-3f70333efce6
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 258e534b2291712f322cfb1dd611c3fb7a0c876c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="configure-database-mail"></a>Konfigurieren des Datenbank-E-Mail-Features
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Dieses Thema beschreibt die Aktivierung und Konfiguration von Datenbank-E-Mails mithilfe des Assistenten zum Konfigurieren von Datenbank-E-Mails sowie die Erstellung eines Datenbank-E-Mail-Konfigurationsskripts anhand von Vorlagen.  
  
-   **Vorbereitungen:**  [Einschränkungen](#Restrictions), [Sicherheit](#Security)  
  
-   **So konfigurieren Sie Datenbank-E-Mails mit folgenden Komponenten:**  [Assistent zum Konfigurieren von Datenbank-E-Mail](#DBWizard), [Vorlagen](#Template)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
 Verwenden Sie die Option **DatabaseMail XPs** , um Datenbank-E-Mail auf diesem Server zu aktivieren. Weitere Informationen finden Sie im Referenzthema [Database Mail XPs (Serverkonfigurationsoption)](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) .  
  
###  <a name="Restrictions"></a> Einschränkungen  
 Zum Aktivieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Broker in einer Datenbank ist eine Datenbanksperrung erforderlich. Wurde Service Broker in **msdb**deaktiviert, müssen Sie zum Aktivieren von Datenbank-E-Mails zuerst den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent beenden, damit Service Broker die erforderliche Sperre abrufen kann.  
  
###  <a name="Security"></a> Sicherheit  
 Sie müssen zum Konfigurieren von Datenbank-E-Mails ein Mitglied der festen Serverrolle **sysadmin** sein. Zum Senden von Datenbank-E-Mail muss der Benutzer ein Mitglied der **DatabaseMailUserRole** -Datenbankrolle in der **msdb** -Datenbank sein.  
  
##  <a name="DBWizard"></a> Verwenden des Assistenten zum Konfigurieren von Datenbank-E-Mail  
 **So konfigurieren Sie Datenbank-E-Mails mit einem Assistenten**  
  
1.  Erweitern Sie im Objekt-Explorer den Knoten für die Instanz, für die Sie Datenbank-E-Mails konfigurieren möchten.  
  
2.  Erweitern Sie den Knoten **Verwaltung** .  
  
3.  Klicken Sie mit der rechten Maustaste auf **Datenbank-E-Mail**, und klicken Sie dann auf **Datenbank-E-Mail konfigurieren**.  
  
4.  Abschließen der Dialogfelder des Assistenten  
  
    -   [Willkommensseite](#Welcome)  
  
    -   [Seite "Konfigurationsaufgabe auswählen"](#ConfigTask)  
  
    -   [Seite "Neues Konto"](#NewAccount)  
  
    -   [Seite "Vorhandenes Konto verwalten"](#ExistingAccount)  
  
    -   [Seite "Neues Profil"](#NewProfile)  
  
    -   [Seite "Vorhandenes Profil verwalten"](#ExistingProfile)  
  
    -   [Seite "Konto zum Profil hinzufügen"](#AddAccount)  
  
    -   [Seite zum Verwalten von Konten und Profilen](#AccountsProfiles)  
  
    -   [Option "Profilsicherheit verwalten", Registerkarte "Öffentlich"](#ProfileSecurityPublic)  
  
    -   [Option "Profilsicherheit verwalten", Registerkarte "Privat"](#ProfileSecurityPrivate)  
  
    -   [Seite "Systemparameter konfigurieren"](#SystemParameters)  
  
    -   [Seite "Assistenten abschließen"](#CompleteWizard)  
  
    -   [Seite "Test-E-Mail senden"](#TestEmail)  
  
###  <a name="Welcome"></a> Willkommensseite  
 Diese Seite beschreibt die Schritte zum Konfigurieren von Datenbank-E-Mails.  
  
 **Diese Seite nicht mehr anzeigen** – Aktivieren Sie diese Option, um die Willkommensseite künftig nicht mehr anzuzeigen.  
  
 **Weiter** – Wechselt zur Seite **Konfigurationsaufgabe auswählen** .  
  
 **Abbrechen** – Beendet den Assistenten ohne Konfiguration der Datenbank-E-Mails.  
  
 [Assistent zum Konfigurieren von Datenbank-E-Mail](#DBWizard)  
  
###  <a name="ConfigTask"></a> Konfigurationsaufgabe auswählen  
 Geben Sie auf der Seite **Konfigurationsaufgabe auswählen** die Aufgabe an, die Sie bei jeder Verwendung des Assistenten ausführen. Wenn Sie Ihre Entscheidung vor dem Beenden des Assistenten ändern, können Sie mithilfe der Schaltfläche **Zurück** zu dieser Seite zurückkehren und eine andere Aufgabe auswählen.  
  
> [!NOTE]  
>  Wenn die Datenbank-E-Mail nicht aktiviert wurde, wird folgende Meldung angezeigt: **Die Datenbank-E-Mail-Funktion ist nicht verfügbar.  Möchten Sie dieses Feature aktivieren?** Die Auswahl von **Ja**entspricht der Aktivierung von Datenbank-E-Mails mit der [Database Mail XPs](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) -Option der gespeicherten Systemprozedur **sp_configure** .  
  
 **Datenbank-E-Mail durch Ausführen der folgenden Aufgaben einrichten**  
 Führt alle Aufgaben durch, die zum ersten Einrichten der Datenbank-E-Mails erforderlich sind. Diese Option umfasst alle anderen drei Optionen.  
  
 **Konten und Profile für Datenbank-E-Mail verwalten**  
 Erstellt neue Datenbank-E-Mail-Konten und -Profile oder ändert oder löscht vorhandene Datenbank-E-Mail-Konten und -Profile oder zeigt diese an.  
  
 **Profilsicherheit verwalten**  
 Konfiguriert, welche Benutzer Zugriff auf Datenbank-E-Mail-Profile haben.  
  
 **Systemparameter anzeigen oder ändern**  
 Konfiguriert Datenbank-E-Mail-Systemparameter wie die maximale Dateigröße für Anlagen.  
  
 [Assistent zum Konfigurieren von Datenbank-E-Mail](#DBWizard)  
  
###  <a name="NewAccount"></a> Seite "Neues Konto"  
 Auf dieser Seite können Sie ein neues Konto für Datenbank-E-Mails erstellen. Ein Konto für Datenbank-E-Mails enthält Informationen für das Senden von E-Mails an einen SMTP-Server.  
  
 Ein Konto für Datenbank-E-Mails enthält Informationen, mit deren Hilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] E-Mail-Nachrichten an einen SMTP-Server gesendet werden. Jedes Konto enthält Informationen für einen E-Mail-Server.  
  
 Ein Konto für Datenbank-E-Mail wird nur für Datenbank-E-Mail verwendet. Ein Konto für Datenbank-E-Mail entspricht nicht einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konto oder einem Microsoft Windows-Konto. Datenbank-E-Mail kann mit den Anmeldeinformationen von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], mit von Ihnen angegebenen Anmeldeinformationen oder anonym gesendet werden. Bei Verwendung der Standardauthentifizierung werden der Benutzername und das Kennwort in einem Konto für Datenbank-E-Mail nur für die Authentifizierung beim E-Mail-Server verwendet. Ein Konto muss keinem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Benutzer oder einem Benutzer auf dem Computer entsprechen, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgeführt wird.  
  
 **Kontoname**  
 Geben Sie den Namen des neuen Kontos ein.  
  
 **Beschreibung**  
 Geben Sie eine Beschreibung des Kontos ein. Die Beschreibung ist optional.  
  
 **E-Mail-Adresse**  
 Geben Sie den Namen der E-Mail-Adresse für das Konto ein. Dies ist die E-Mail-Adresse, von der aus E-Mails versendet werden. Ein Konto für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent könnte E-Mails beispielsweise von der Adresse SqlAgent@Adventure-Works.com aus versenden.  
  
 **Anzeigename**  
 Geben Sie den Namen ein, der in den von diesem Konto aus versendeten E-Mail-Nachrichten angezeigt wird. Der angezeigte Name ist optional. Es handelt sich dabei um den Namen, der in den von diesem Konto versendeten Nachrichten angezeigt wird. Ein Konto für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] könnte beispielsweise den Namen "SQL Server Agent Automated Mailer" in den E-Mail-Nachrichten anzeigen.  
  
 **Antwort-E-Mail**  
 Geben Sie die E-Mail-Adresse ein, die für Antworten auf E-Mail-Nachrichten aus diesem Konto verwendet wird. Der Eintrag für die Antwort-E-Mail ist optional. Antworten auf ein Konto von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent könnten beispielsweise an den Datenbankadministrator gehen, danw@Adventure-Works.com.  
  
 **Servername**  
 Geben Sie den Namen oder die IP-Adresse des SMTP-Servers ein, der von diesem Konto zum Senden von E-Mails verwendet wird. Normalerweise hat der Eintrag ein ähnliches Format wie **smtp.***<Ihr_Unternehmen>***.com**. Informationen hierzu erhalten Sie von Ihrem E-Mail-Administrator.  
  
 **Portnummer**  
 Geben Sie die Portnummer des SMTP-Servers für dieses Konto ein. Die meisten SMTP-Server verwenden Port 25.  
  
 **Für diesen Server ist eine sichere Verbindung (SSL) erforderlich**  
 Verschlüsselt die Kommunikation mit SSL (Secure Sockets Layer).  
  
 **Windows-Authentifizierung mithilfe der Anmeldeinformationen des Datenbankmoduldiensts**  
 Die Verbindung mit dem SMTP-Server wird mithilfe der für den Dienst [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] konfigurierten Anmeldeinformationen hergestellt.  
  
 **Standardauthentifizierung**  
 Geben Sie den für den SMTP-Server erforderlichen Benutzernamen und das Kennwort ein.  
  
 **Benutzername**  
 Geben Sie den Benutzernamen ein, mit dem Datenbank-E-Mail sich beim SMTP-Server anmeldet. Der Benutzername ist erforderlich, wenn der SMTP-Server die Standardauthentifizierung erfordert.  
  
 **Kennwort**  
 Geben Sie das Kennwort ein, mit dem Datenbank-E-Mail sich beim SMTP-Server anmeldet. Das Kennwort ist erforderlich, wenn der SMTP-Server die Standardauthentifizierung erfordert.  
  
 **Kennwort bestätigen**  
 Geben Sie das Kennwort zur Bestätigung erneut ein. Das Kennwort ist erforderlich, wenn der SMTP-Server die Standardauthentifizierung erfordert.  
  
 **Anonyme Authentifizierung**  
 E-Mail wird ohne Anmeldeinformationen an den SMTP-Server gesendet. Verwenden Sie diese Option, wenn für den SMTP-Server keine Authentifizierung erforderlich ist.  
  
 [Assistent zum Konfigurieren von Datenbank-E-Mail](#DBWizard)  
  
###  <a name="ExistingAccount"></a> Seite "Vorhandenes Konto verwalten"  
 Mithilfe dieser Seite können Sie ein vorhandenes Datenbank-E-Mail-Konto verwalten.  
  
 **Kontoname**  
 Wählen Sie hier den Kontonamen aus, der angezeigt, aktualisiert oder gelöscht werden soll.  
  
 **Delete**  
 Löscht das ausgewählte Konto. Sie müssen dieses Konto aus zugeordneten Profilen entfernen oder diese Profile löschen, bevor Sie das ausgewählte Konto löschen.  
  
 **Beschreibung**  
 In diesem Bereich können Sie die Beschreibung des Kontos anzeigen oder bearbeiten. Die Beschreibung ist optional.  
  
 **E-Mail-Adresse**  
 Hier können Sie den Namen der E-Mail-Adresse für das Konto anzeigen oder aktualisieren. Dies ist die E-Mail-Adresse, von der aus E-Mails versendet werden. Ein Konto für Microsoft SQL Server Agent könnte E-Mails beispielsweise von der Adresse **SqlAgent@Adventure-Works.com**.  
  
 **Anzeigename**  
 Hier können Sie den Namen anzeigen oder bearbeiten, der in den von diesem Konto aus versendeten E-Mail-Nachrichten angezeigt wird. Der angezeigte Name ist optional. Es handelt sich dabei um den Namen, der in den von diesem Konto versendeten Nachrichten angezeigt wird. Ein Konto für SQL Server Agent könnte beispielsweise den Namen **SQL Server Agent Automated Mailer** in den E-Mails anzeigen.  
  
 **Antwort-E-Mail**  
 Hier können Sie die E-Mail-Adresse anzeigen und bearbeiten, die für Antworten auf E-Mail-Nachrichten für dieses Konto verwendet wird. Der Eintrag für die Antwort-E-Mail ist optional. Antworten auf ein Konto von SQL Server Agent könnten beispielsweise an den Datenbankadministrator gehen, **danw@Adventure-Works.com**.  
  
 **Servername**  
 Hier können Sie den Namen des SMTP-Servernamens anzeigen und bearbeiten, der zum Senden von E-Mail von diesem Konto verwendet wird. Normalerweise hat der Eintrag ein ähnliches Format wie **smtp.<Ihr_Unternehmen>.com**. Informationen hierzu erhalten Sie von Ihrem E-Mail-Administrator.  
  
 **Portnummer**  
 Hier können Sie die Portnummer des SMTP-Servers für dieses Konto anzeigen und bearbeiten. Die meisten SMTP-Server verwenden Port 25.  
  
 **Für diesen Server ist eine sichere Verbindung (SSL) erforderlich**  
 Verschlüsselt die Kommunikation mit SSL (Secure Sockets Layer).  
  
 **Windows-Authentifizierung mithilfe der Anmeldeinformationen des Datenbankmoduldiensts**  
 Die Verbindung mit dem SMTP-Server wird mithilfe der für den Dienst [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] konfigurierten Anmeldeinformationen hergestellt.  
  
 **Standardauthentifizierung**  
 Geben Sie den für den SMTP-Server erforderlichen Benutzernamen und das Kennwort ein.  
  
 **User name**  
 Hier können Sie den Benutzernamen anzeigen und bearbeiten, mit dem die Datenbank-E-Mail sich beim SMTP-Server anmeldet. Der Benutzername ist erforderlich, wenn der SMTP-Server die Standardauthentifizierung erfordert.  
  
 **Kennwort**  
 Ändert das Kennwort, mit dem die Datenbank-E-Mail sich beim SMTP-Server anmeldet. Das Kennwort ist erforderlich, wenn der SMTP-Server die Standardauthentifizierung erfordert.  
  
 **Kennwort bestätigen**  
 Geben Sie das Kennwort zur Bestätigung erneut ein. Das Kennwort ist erforderlich, wenn der SMTP-Server die Standardauthentifizierung erfordert.  
  
 **Anonyme Authentifizierung**  
 E-Mail wird ohne Anmeldeinformationen an den SMTP-Server gesendet. Verwenden Sie diese Option, wenn für den SMTP-Server keine Authentifizierung erforderlich ist.  
  
 [Assistent zum Konfigurieren von Datenbank-E-Mail](#DBWizard)  
  
###  <a name="NewProfile"></a> Seite "Neues Profil"  
 Auf dieser Seite können Sie ein Profil für Datenbank-E-Mails erstellen. Ein Datenbank-E-Mail-Profil ist eine Auflistung von Datenbank-E-Mail-Konten. In Fällen, wo ein E-Mail-Server nicht erreichbar ist, sorgen Profile für mehr Zuverlässigkeit, indem sie alternative Datenbank-E-Mail-Konten bereitstellen. Es ist mindestens ein Datenbank-E-Mail-Konto erforderlich. Weitere Informationen zum Festlegen der Prioritäten von Datenbank-E-Mail-Konten im Profil finden Sie unter [Create a Database Mail Profile](../../relational-databases/database-mail/create-a-database-mail-profile.md).  
  
 Mithilfe der Schaltflächen **Nach oben** und **Nach unten** ändern Sie die Reihenfolge, in der die Datenbank-E-Mail-Konten verwendet werden. Diese Reihenfolge wird durch einen Wert namens Sequenznummer festgelegt. **Nach oben** verringert die Sequenznummer und **Nach unten** erhöht die Sequenznummer. Über die Sequenznummer wird die Reihenfolge festgelegt, in der Konten im Profil von Datenbank-E-Mail verwendet werden. Für eine neue E-Mail-Nachricht beginnt Datenbank-E-Mail mit dem Konto mit der niedrigsten Sequenznummer. Wenn dieses Konto fehlschlägt, verwendet Datenbank-E-Mail das Konto mit der nächsthöheren Sequenznummer usw., bis entweder Datenbank-E-Mail die Nachricht erfolgreich versendet oder das Konto mit der höchsten Sequenznummer fehlschlägt. Wenn das Konto mit der höchsten Sequenznummer fehlschlägt, unterbricht Datenbank-E-Mail den Versuch, die E-Mail zu versenden, für den Zeitraum, der im Datenbank-E-Mail-Parameter **AccountRetryDelay** festgelegt ist. Verwenden Sie den **AccountRetryAttempts** -Parameter, um zu konfigurieren, wie oft der externe Mailprozess versuchen soll, die E-Mail mithilfe der einzelnen Konten des angegebenen Profils zu versenden. Sie können die Parameter **AccountRetryDelay** und **AccountRetryAttempts** auf der Seite **Systemparameter konfigurieren** des Assistenten zum Konfigurieren von Datenbank-E-Mail konfigurieren.  
  
 **Profilname**  
 Geben Sie einen Namen für das neue Profil ein. Das Profil wird mit diesem Namen erstellt. Verwenden Sie nicht den Namen eines bereits vorhandenen Profils.  
  
 **Beschreibung**  
 Geben Sie eine Beschreibung für das Profil ein. Die Beschreibung ist optional.  
  
 **SMTP-Konten**  
 Wählen Sie für das Profil eines oder mehrere Konten aus. Die Priorität legt die Reihenfolge fest, in der Konten von Datenbank-E-Mail verwendet werden. Wenn keine Konten aufgelistet werden, müssen Sie zum Fortfahren auf **Hinzufügen** klicken und dann ein neues SMTP-Konto hinzufügen.  
  
 **Hinzufügen**  
 Hinzufügen eines Kontos zum Profil.  
  
 **Entfernen**  
 Entfernen des ausgewählten Kontos aus dem Profil.  
  
 **Nach oben**  
 Erhöhen Sie die Priorität des ausgewählten Kontos.  
  
 **Nach unten**  
 Verringern Sie die Priorität des ausgewählten Kontos.  
  
 [Assistent zum Konfigurieren von Datenbank-E-Mail](#DBWizard)  
  
###  <a name="ExistingProfile"></a> Seite "Vorhandenes Profil verwalten"  
 Mit dieser Seite können Sie ein vorhandenes Datenbank-E-Mail-Profil verwalten. Ein Datenbank-E-Mail-Profil ist eine Auflistung von Datenbank-E-Mail-Konten. In Fällen, wo ein E-Mail-Server nicht erreichbar ist, sorgen Profile für mehr Zuverlässigkeit, indem sie alternative Datenbank-E-Mail-Konten bereitstellen. Es ist mindestens ein Datenbank-E-Mail-Konto erforderlich. Weitere Informationen zum Festlegen der Prioritäten von Datenbank-E-Mail-Konten im Profil finden Sie unter [Create a Database Mail Profile](../../relational-databases/database-mail/create-a-database-mail-profile.md).  
  
 Mithilfe der Schaltflächen **Nach oben** und **Nach unten** ändern Sie die Reihenfolge, in der die Datenbank-E-Mail-Konten verwendet werden. Diese Reihenfolge wird durch einen Wert namens Sequenznummer festgelegt. **Nach oben** verringert die Sequenznummer und **Nach unten** erhöht die Sequenznummer. Über die Sequenznummer wird die Reihenfolge festgelegt, in der Konten im Profil von Datenbank-E-Mail verwendet werden. Für eine neue E-Mail-Nachricht beginnt Datenbank-E-Mail mit dem Konto mit der niedrigsten Sequenznummer. Wenn dieses Konto fehlschlägt, verwendet Datenbank-E-Mail das Konto mit der nächsthöheren Sequenznummer usw., bis entweder Datenbank-E-Mail die Nachricht erfolgreich versendet oder das Konto mit der höchsten Sequenznummer fehlschlägt. Wenn das Konto mit der höchsten Sequenznummer fehlschlägt, unterbricht Datenbank-E-Mail den Versuch, die E-Mail zu versenden, für den Zeitraum, der im Datenbank-E-Mail-Parameter **AccountRetryDelay** festgelegt ist. Verwenden Sie den **AccountRetryAttempts** -Parameter, um zu konfigurieren, wie oft der externe Mailprozess versuchen soll, die E-Mail mithilfe der einzelnen Konten des angegebenen Profils zu versenden. Sie können die Parameter **AccountRetryDelay** und **AccountRetryAttempts** auf der Seite **Systemparameter konfigurieren** des Assistenten zum Konfigurieren von Datenbank-E-Mail konfigurieren.  
  
 **Profilname**  
 Wählen Sie den Namen des zu verwaltenden Profils aus.  
  
 **Delete**  
 Löscht das ausgewählte Profil. Sie werden aufgefordert, **Ja** auszuwählen, um das ausgewählte Profil zu löschen und nicht gesendete Nachrichten abzubrechen, oder **Nein** auszuwählen, um das ausgewählte Profil nur zu löschen, wenn keine ungesendeten Nachrichten vorhanden sind.  
  
 **Beschreibung**  
 Zeigen Sie die Beschreibung des ausgewählten Profils an oder ändern Sie diese. Die Beschreibung ist optional.  
  
 **SMTP-Konten**  
 Wählen Sie für das Profil eines oder mehrere Konten aus. Die Failoverpriorität legt die Reihenfolge fest, in der Datenbank-E-Mail die Konten bei einem Failover verwendet.  
  
 **Hinzufügen**  
 Hinzufügen eines Kontos zum Profil.  
  
 **Entfernen**  
 Entfernen des ausgewählten Kontos aus dem Profil.  
  
 **Nach oben**  
 Erhöht die Failoverpriorität des ausgewählten Kontos.  
  
 **Nach unten**  
 Verringert die Failoverpriorität des ausgewählten Kontos.  
  
 **Priority**  
 Anzeigen der aktuellen Failoverpriorität des Kontos.  
  
 **Kontoname**  
 Anzeigen des Namens des Kontos.  
  
 **E-mail Address**  
 Anzeigen der E-Mail-Adresse des Kontos.  
  
 [Assistent zum Konfigurieren von Datenbank-E-Mail](#DBWizard)  
  
###  <a name="AddAccount"></a> Add Account to Profile Page  
 Verwenden Sie diese Seite, um das dem Profil hinzuzufügende Konto auszuwählen. Wählen Sie ein vorhandenes Konto aus dem Feld **Kontoname** , oder klicken Sie auf **Neues Konto**.  
  
 **Kontoname**  
 Wählen Sie den Namen des Kontos aus, das Sie dem Profil hinzufügen möchten.  
  
 **E-Mail-Adresse**  
 Zeigt die E-Mail-Adresse des ausgewählten Kontos an. Sie können die E-Mail-Adresse auf dieser Seite nicht ändern. Gehen Sie zum Ändern der E-Mail-Adresse zurück zur Hauptseite des Assistenten, und wählen Sie die Option **Konten und Profile für Datenbank-E-Mail verwalten** aus.  
  
 **Servername**  
 Zeigt den Namen des Mailservers des ausgewählten Kontos an. Sie können den Servernamen auf dieser Seite nicht ändern. Gehen Sie zum Ändern des Servernamens für das Konto zurück zur Hauptseite des Assistenten, und wählen Sie die Option **Konten und Profile für Datenbank-E-Mail verwalten** aus.  
  
 **Neues Konto**  
 Erstellt ein neues Konto.  
  
 [Assistent zum Konfigurieren von Datenbank-E-Mail](#DBWizard)  
  
###  <a name="AccountsProfiles"></a> Seite zum Verwalten von Konten und Profilen  
 Verwenden Sie diese Seite, um eine Aufgabe zum Verwalten eines Profils oder Kontos auszuwählen.  
  
 **Neues Konto erstellen**  
 Erstellt ein neues Konto.  
  
 **Vorhandenes Konto anzeigen, ändern oder löschen**  
 Verwaltet oder löscht ein vorhandenes Konto.  
  
 **Neues Profil erstellen**  
 Erstellt ein neues Profil.  
  
 **Vorhandenes Konto anzeigen, ändern oder löschen. Sie können außerdem Konten für das Profil verwalten.**  
 Aktualisiert oder löscht ein vorhandenes Profil. Mit dieser Option können Sie außerdem Konten verwalten, die dem Profil zugeordnet sind.  
  
 [Assistent zum Konfigurieren von Datenbank-E-Mail](#DBWizard)  
  
###  <a name="ProfileSecurityPublic"></a> Option "Profilsicherheit verwalten", Registerkarte "Öffentlich"  
 Verwenden Sie diese Seite zum Konfigurieren eines öffentlichen Profils.  
  
 Profile sind entweder öffentlich oder privat. Auf ein privates Profil können nur bestimmte Benutzer oder Rollen zugreifen. Mit einem öffentlichen Profil kann jeder Benutzer oder jede Rolle mit Zugriff auf die Mailhostdatenbank (**msdb**) E-Mails mithilfe dieses Profils senden.  
  
 Ein Profil kann ein Standardprofil sein. In diesem Fall können Benutzer oder Rollen E-Mails mithilfe des Profils senden, ohne das Profil explizit anzugeben. Falls der Benutzer oder die Rolle, die/der die E-Mail-Nachricht sendet, über ein privates Standardprofil verfügt, verwendet Datenbank-E-Mail dieses Profil. Verfügt der Benutzer oder die Rolle nicht über ein privates Standardprofil, verwendet **sp_send_dbmail** das öffentliche Standardprofil für die **msdb** -Datenbank. Falls weder ein privates Standardprofil für den Benutzer oder die Rolle noch ein öffentliches Standardprofil für die Datenbank vorhanden ist, gibt **sp_send_dbmail** einen Fehler zurück. Nur ein Profil kann als Standardprofil gekennzeichnet werden.  
  
 **Öffentlich**  
 Wählen Sie diese Option aus, um das angegebene Profil als öffentliches Profil festzulegen.  
  
 **Profile Name**  
 Zeigt den Namen des Profils an.  
  
 **Standardprofil**  
 Wählen Sie diese Option aus, um das angegebene Profil als Standardprofil festzulegen.  
  
 **Nur vorhandene öffentliche Profile anzeigen**  
 Wählen Sie diese Option aus, um nur öffentliche Profile in der angegebenen Datenbank anzuzeigen.  
  
 [Assistent zum Konfigurieren von Datenbank-E-Mail](#DBWizard)  
  
###  <a name="ProfileSecurityPrivate"></a> Option "Profilsicherheit verwalten", Registerkarte "Privat"  
 Verwenden Sie diese Seite zum Konfigurieren eines privaten Profils.  
  
 Profile sind entweder öffentlich oder privat. Auf ein privates Profil können nur bestimmte Benutzer oder Rollen zugreifen. Mit einem öffentlichen Profil kann jeder Benutzer oder jede Rolle mit Zugriff auf die Mailhostdatenbank (**msdb**) E-Mails mithilfe dieses Profils senden.  
  
 Ein Profil kann ein Standardprofil sein. In diesem Fall können Benutzer oder Rollen E-Mails mithilfe des Profils senden, ohne das Profil explizit anzugeben. Falls der Benutzer oder die Rolle, die/der die E-Mail-Nachricht sendet, über ein privates Standardprofil verfügt, verwendet Datenbank-E-Mail dieses Profil. Verfügt der Benutzer oder die Rolle nicht über ein privates Standardprofil, verwendet **sp_send_dbmail** das öffentliche Standardprofil für die **msdb** -Datenbank. Falls weder ein privates Standardprofil für den Benutzer oder die Rolle noch ein öffentliches Standardprofil für die Datenbank vorhanden ist, gibt **sp_send_dbmail** einen Fehler zurück.  
  
 **User name**  
 Wählen Sie in der **msdb** -Datenbank einen Benutzer oder eine Rolle aus.  
  
 **Zugriff**  
 Wählen Sie aus, ob der Benutzer oder die Rolle Zugriff auf das angegebene Profil hat.  
  
 **Profilname**  
 Zeigen Sie den Namen des Profils an.  
  
 **Ist Standardprofil**  
 Wählen Sie aus, ob das Profil das Standardprofil für den Benutzer oder die Rolle ist. Jeder Benutzer oder jede Rolle kann nur über ein Standardprofil verfügen.  
  
 **Nur vorhandene private Profile für diesen Benutzer anzeigen**  
 Wählen Sie diese Option aus, um nur Profile anzuzeigen, auf die der angegebene Benutzer oder die angegebene Rolle bereits Zugriff hat.  
  
 [Assistent zum Konfigurieren von Datenbank-E-Mail](#DBWizard)  
  
###  <a name="SystemParameters"></a> Systemparameter konfigurieren  
 Verwenden Sie diese Seite, um Systemparameter für die Datenbank-E-Mail festzulegen. Zeigen Sie die Systemparameter und den aktuellen Wert der einzelnen Parameter an. Wählen Sie einen Parameter aus, um eine kurze Beschreibung im Informationsbereich anzuzeigen.  
  
 **Wiederholungsversuche für das Konto**  
 Gibt an, wie oft der externe E-Mail-Prozess versucht, die E-Mail-Nachricht zu senden, wobei jedes Konto im angegebenen Profil verwendet wird.  
  
 **Wiederholungsverzögerung für das Konto (Sekunden)**  
 Gibt die Zeitdauer in Sekunden an, die der externe E-Mail-Prozess nach dem Versuch, eine Nachricht mithilfe aller Konten im Profil zu übermitteln, warten soll, bevor er alle Konten erneut ausprobiert.  
  
 **Maximale Dateigröße (Bytes)**  
 Die maximale Größe einer Anlage in Bytes.  
  
 **Unzulässige Erweiterungen für Anlagendateien**  
 Eine durch Trennzeichen getrennte Liste mit Erweiterungen, die nicht als Anlagen einer E-Mail-Nachricht gesendet werden können. Klicken Sie auf die Schaltfläche zum Durchsuchen (**...**), um zusätzliche Erweiterungen hinzuzufügen.  
  
 **Minimale Lebensdauer der ausführbaren Datei von der Datenbank-E-Mail (Sekunden)**  
 Gibt an, wie lange (in Sekunden) der externe E-Mail-Prozess mindestens aktiv bleibt. Der Prozess bleibt aktiv, solange sich E-Mails in der Datenbank-E-Mail-Warteschlange befinden. Dieser Parameter gibt die Zeitdauer an, für die der Prozess aktiv bleibt, wenn keine Nachrichten zum Verarbeiten vorhanden sind.  
  
 **Protokolliergrad**  
 Gibt an, welche Nachrichten im Datenbank-E-Mail-Protokoll aufgezeichnet werden. Folgende Werte sind möglich:  
  
-   Normal - Nur Fehler werden protokolliert.  
  
-   Erweitert - Fehler, Warnungen und Informationsmeldungen werden protokolliert.  
  
-   Ausführlich - Fehler, Warnungen, Informationsmeldungen, Erfolgsmeldungen und zusätzliche interne Meldungen werden protokolliert. Verwenden Sie die ausführliche Protokollierung für die Problembehandlung.  
  
 Standardwert: Erweitert.  
  
 **Alles zurücksetzen**  
 Aktivieren Sie diese Option, um die Werte auf der Seite auf die Standardwerte zurückzusetzen.  
  
 [Assistent zum Konfigurieren von Datenbank-E-Mail](#DBWizard)  
  
###  <a name="CompleteWizard"></a> Seite "Assistenten abschließen"  
 Mithilfe dieser Seite können Sie die Aktionen überprüfen, die der **Assistent zum Konfigurieren von Datenbank-E-Mail** ausführt. Bis zum Abschließen des Assistenten werden keine Änderungen angewendet.  
  
 [Assistent zum Konfigurieren von Datenbank-E-Mail](#DBWizard)  
  
###  <a name="TestEmail"></a> Send Test E-Mail Page  
 Verwenden Sie die Seite **Test-E-Mail senden von***<Instanzname>*, um eine E-Mail mithilfe des angegebenen Datenbank-E-Mail-Profils zu senden. Nur Mitglieder der festen Serverrolle **sysadmin** können Test-E-Mails über diese Seite senden.  
  
 **Datenbank-E-Mail-Profil**  
 Wählen Sie aus der Liste ein Datenbank-E-Mail-Profil aus. Dies ist ein Pflichtfeld. Wenn keine Profile angezeigt werden, gibt es keine Profile, oder Sie haben für ein Profil keine Berechtigung. Verwenden Sie den **Assistent zum Konfigurieren von Datenbank-E-Mail** zum Erstellen und Konfigurieren von Profilen. Wenn keine Profile angezeigt werden, erstellen Sie mithilfe des Assistenten zum Konfigurieren von Datenbank-E-Mail ein Profil für die eigene Verwendung.  
  
 **Aktion**  
 Die E-Mail-Adresse der Nachrichtenempfänger. Mindestens ein Empfänger muss angegeben werden.  
  
 **Betreff**  
 Die Betreffzeile für die Test-E-Mail. Ändern Sie den Standardbetreff, damit Sie Ihre E-Mail bei der Problembehandlung besser identifizieren können.  
  
 **Textkörper**  
 Der Text der Test-E-Mail. Ändern Sie den Standardbetreff, damit Sie Ihre E-Mail bei der Problembehandlung besser identifizieren können.  
  
 Das Dialogfeld **Test-E-Mail von Datenbank-E-Mail** bestätigt, dass die Datenbank-E-Mail versuchte, die Testnachricht zu senden, und stellt die **mailitem_id** für die Test-E-Mail bereit. Fragen Sie beim Empfänger nach, ob die E-Mail angekommen ist. E-Mails werden normalerweise in wenigen Minuten empfangen. Aufgrund einer geringen Netzwerkleistung, eines Rückstands an Nachrichten beim Mailserver oder wenn der Server vorübergehend nicht erreichbar ist, kann es jedoch zu Verzögerungen beim E-Mail-Empfang kommen. Verwenden Sie die **mailitem_id** zur Problembehandlung.  
  
 **Gesendete E-Mail**  
 Die **mailitem_id** der Test-E-Mail.  
  
 **Problembehandlung**  
 Klicken Sie, um die Onlinedokumentation für das Thema [Problembehandlung bei Datenbank-E-Mail](http://msdn.microsoft.com/library/ms188663.aspx)zu öffnen.  
  
 [Assistent zum Konfigurieren von Datenbank-E-Mail](#DBWizard)  
  
##  <a name="Template"></a> Vorlagen  
 **So erstellen Sie ein Datenbank-E-Mail-Konfigurationsskript**  
  
1.  Wählen Sie im Menü **Ansicht** den **Vorlagen-Explorer**aus.  
  
2.  Erweitern Sie im Fenster **Vorlagen-Explorer** den Ordner **Database Mail** .  
  
3.  Doppelklicken Sie auf **Simple Database Mail Configuration**. Die Vorlage wird in einem neuen Abfragefenster geöffnet.  
  
4.  Wählen Sie im Menü **Abfrage** die Option **Werte für Vorlagenparameter angeben**aus. Das Fenster **Vorlagenparameter ersetzen** wird geöffnet.  
  
5.  Geben Sie die Werte für **profile_name**, **account_name**, **SMTP_servername**, **email_address**und **display_name**ein. SQL Server Management Studio füllt die Vorlage mit den von Ihnen angegebenen Werten aus.  
  
6.  Führen Sie das Skript aus, damit die Konfiguration erstellt wird.  
  
7.  Das Skript gewährt keinem Datenbankbenutzer den Zugriff auf das Profil. Aus diesem Grund kann das Profil standardmäßig nur durch Mitglieder der festen Sicherheitsrolle **sysadmin** verwendet werden. Weitere Informationen zum Gewähren des Zugriffs auf Profile finden Sie unter [sysmail_add_principalprofile_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql.md).  
  
  
