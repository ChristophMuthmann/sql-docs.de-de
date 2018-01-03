---
title: "Häufige Probleme mit der externen skriptausführung in SQL Server | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 10/11/2017
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4f515ba26c4eeae70eaf9244c0eaedaa954954b4
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="common-issues-with-external-script-execution-in-sql-server"></a>Häufige Probleme mit der externen skriptausführung in SQL Server

Dieser Artikel enthält eine Liste der bekannten Probleme und allgemeine Probleme im Zusammenhang mit R oder Python-Code in SQL Server.

Bevor Sie beginnen, empfehlen wir, dass Sie einige Informationen über Ihr System sammeln. Um zu erfahren, wie, finden Sie unter [Datensammlung für die Problembehandlung](data-collection-ml-troubleshooting-process.md).

Überprüfen Sie außerdem eine Liste der Probleme, die anfängliche Einrichtung oder Konfiguration spezifisch sind: [Setup und Upgrade – häufig gestellte Fragen](r/upgrade-and-installation-faq-sql-server-r-services.md).

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Dienste

## <a name="launchpad-issues"></a>Launchpad-Probleme

Der SQL Server vertrauenswürdige Launchpad-Dienst verwaltet die Ausführung externer Skripts und die Kommunikation mit R, Python oder anderen externen Laufzeiten. Mehrere Probleme können Launchpad aus starten, einschließlich von Konfigurationsproblemen oder Änderungen oder fehlende Netzwerkprotokolle verhindert werden.

Beginnen Sie im Rahmen der Problembehandlung beginnen indem Sie die folgenden Fragen beantworten:

- Nicht Launchpad immer ausgeführt werden oder reagiert nicht mehr?
- Welche Dienstkonto wird unter Launchpad ausgeführt?
- Welche Benutzerrechte verfügt das Konto des Launchpad-Dienst?

### <a name="determine-whether-launchpad-is-running"></a>Bestimmen Sie, ob Launchpad ausgeführt wird

1. Öffnen der **Services** Bereich ("Services.msc"). Oder geben Sie an der Befehlszeile **"sqlservermanager13.msc"** oder **SQLServerManager14.msc** öffnen [SQL Server-Konfigurations-Manager](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager).

2. Notieren Sie das Dienstkonto, unter dem Launchpad ausgeführt wird. Jede Instanz, wobei R oder Python aktiviert ist, sollte eine eigene Instanz des Launchpad-Dienst haben. Beispielsweise der Dienst für eine benannte Instanz möglicherweise etwas _MSSQLLaunchpad$ InstanceName_.

3. Wenn der Dienst beendet wird, starten Sie ihn aus. Auf Neustart, wenn Probleme bei der Konfiguration vorhanden sind, eine Meldung in das Systemereignisprotokoll veröffentlicht wird und erneut wird der Dienst beendet. Überprüfen Sie das Systemereignisprotokoll für Details, warum der Dienst beendet wurde.

4. Überprüfen Sie den Inhalt der RSetup.log, und stellen Sie sicher, dass keine Fehler, im Setup vorliegen. Angenommen, die Nachricht *mit Code 0 beendet* weisen auf Fehler hin des Diensts zu starten.

5. Überprüfen Sie den Inhalt von "rlauncher.log", um nach anderen Fehlern suchen.

### <a name="check-the-launchpad-service-account"></a>Überprüfen Sie das Launchpad-Dienstkonto

Ist möglicherweise das Standarddienstkonto das Konto "NT-Dienst\$SQL2016" oder "NT-Dienst\$SQL2017". Das letzte Teil variieren abhängig von der SQL-Instanzname.

Der Launchpad-Dienst (Launchpad.exe) wird mithilfe eines Dienstkontos mit geringen Rechten-ausgeführt. Allerdings erfordert das Launchpad-Dienstkonto zum Starten von R und Python und kommunizieren mit der Datenbankinstanz, die folgenden Berechtigungen:

- Anmelden als Dienst (SeServiceLogonRight)
- Ersetzen von Token auf Prozessebene (SeAssignPrimaryTokenPrivilege)
- Umgehen von durchsuchenden Prüfungen (SeChangeNotifyPrivilege)
- Anpassen von Speicherkontingenten für einen Prozess (SeIncreaseQuotaSizePrivilege)

Informationen über diese Benutzerrechte, finden Sie im Abschnitt "Windows-Berechtigungen und Rechte" in [service Konfigurieren von Windows-Dienstkonten und-Berechtigungen](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

> [!TIP]
> Wenn Sie mit der Verwendung des Tools Unterstützung Diagnose Plattform (SDP) für SQL Server-Diagnose vertraut sind, können Sie SDP verwenden, um die Ausgabedatei mit dem Namen MachineName_UserRights.txt zu überprüfen.

### <a name="review-launchpad-requirements"></a>Überprüfen Sie die Launchpad-Anforderungen

Einige Probleme können Launchpad verhindert. Der Launchpad-Dienst starten und beenden dann möglicherweise oder Absturz oder der Dienst möglicherweise nicht mehr mit einem Verbindungstimeout. In diesen Fällen ist wurde das System in der Regel geändert oder so konfiguriert, dass Launchpad nicht ausgeführt werden kann.

#### <a name="determine-whether-8dot3-notation-is-enabled"></a>Bestimmt, ob 8.3-Notation aktiviert ist

Aus Kompatibilitätsgründen mit R SQL Server 2016 R Services (Datenbankintern) erforderlich, das Laufwerk, in dem das Feature installiert wird, um die Erstellung von kurzen Dateinamen mithilfe von *8.3-Notation*. Ein 8.3-Dateiname wird auch bezeichnet eine *kurzer Dateiname*, und es wird verwendet, um die Kompatibilität mit früheren Versionen von Microsoft Windows oder alternativ langen Dateinamen.

Wenn das Volume, in dem Sie R installieren, keine kurze Dateinamen unterstützt, die Prozesse, die R aus SQL Server zu starten möglicherweise nicht die richtige ausführbare Datei zu suchen und Launchpad wird nicht gestartet.

Dieses Problem zu umgehen können Sie die 8.3-Notation auf dem Volume, auf dem SQL Server installiert ist und am Installationsort von R Services. Sie müssen dann den kurzen Namen für das Arbeitsverzeichnis in der R Services-Konfigurationsdatei angeben.

1. Um 8.3-Notation zu aktivieren, führen Sie das Dienstprogramm Fsutil mit der *8dot3name* Argument wie hier beschrieben: [Fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx).

2. Nachdem die 8.3-Notation aktiviert ist, öffnen Sie die Datei RLauncher.config, und beachten Sie die Eigenschaft des `WORKING_DIRECTORY`. Weitere Informationen dazu, wie sich diese Datei befindet, finden Sie unter [Datensammlung für die Problembehandlung von Machine Learning](data-collection-ml-troubleshooting-process.md).

3. Verwenden Sie das Dienstprogramm Fsutil mit der *Datei* Argument, um einen kurzen Pfad für den Ordner anzugeben, die in WORKING_DIRECTORY angegeben ist.

4. Bearbeiten Sie die Konfigurationsdatei, um die gleichen Arbeitsverzeichnis angeben, das Sie in der Eigenschaft WORKING_DIRECTORY eingegeben haben. Sie können alternativ Geben Sie einen anderen Arbeitsverzeichnis und wählen Sie einen vorhandenen Pfad, der bereits mit dem 8.3-Notation kompatibel ist.

> [!NOTE] 
> Diese Einschränkung wurde in späteren Versionen behoben. Wenn Sie dieses Problem auftritt, installieren Sie eine der folgenden:
> * SQL Server 2016 SP1 und CU1: [kumulativen Update 1 für SQLServer](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1).
> * SQL Server 2016 RTM, das kumulative Update 3 und dies [Hotfix](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3), die bei Bedarf verfügbar ist.

#### <a name="the-user-group-for-launchpad-cannot-log-on-locally"></a>Die Benutzergruppe für Launchpad kann nicht lokal anmelden

Während des Setups von Machine Learning-Services, SQL Server erstellt die Windows-Benutzergruppe **SQLRUserGroup** , und klicken Sie dann mit allen Regeln für Launchpad, um eine Verbindung mit SQL Server, und führen die externe Skripts für Aufträge erforderlichen bereitgestellt. Wenn der Benutzer der Gruppe aktiviert ist, wird er auch zum Ausführen von Python-Skripts verwendet.

Allerdings in Organisationen, die denen restriktivere Sicherheitsrichtlinien durchgesetzt werden, die Rechte, die von dieser Gruppe erforderlich sind möglicherweise manuell entfernt, oder sie können automatisch von der Richtlinie aufgehoben werden. Wenn die Rechte entfernt wurden, Launchpad kann nicht mehr Verbinden mit SQL Server und SQL Server kann nicht die externen Laufzeit aufgerufen.

Stellen Sie sicher, dass die Gruppe **SQLRUserGroup** über die Systemberechtigung **Allow Log in locally**  (Lokale Anmeldung erlauben) verfügt, um dieses Problem zu beheben.

Weitere Informationen finden Sie unter [service Konfigurieren von Windows-Dienstkonten und-Berechtigungen](https://msdn.microsoft.com/library/ms143504.aspx#Windows).

#### <a name="improper-setup-leading-to-mismatched-dlls"></a>Falsche Setup führt zu nicht übereinstimmenden DLLs

Wenn Sie das Datenbankmodul mit anderen Funktionen, Patch für die Server installieren, und klicken Sie dann später die Machine Learning-Funktion mit den Originalmedien hinzufügen, kann die falsche Version der Machine Learning-Komponenten installiert werden. Wenn Launchpad einen Versionskonflikt erkennt, heruntergefahren und erstellt eine Dumpdatei.

Um dieses Problem zu vermeiden, werden Sie sicher, dass keine neuen Features auf dem gleichen Patchebene als die Server-Instanz zu installieren.

**Die falsche Möglichkeit, zu aktualisieren:**

1. Installieren von SQLServer 2016 ohne R-Services.
2. SQL Server 2016 Kumulatives Update 2 zu aktualisieren.
3. Installieren von R Services (Datenbankintern) unter Verwendung der RTM-Medien.

**Die richtige Vorgehensweise zum upgrade:**

1. Installieren von SQLServer 2016 ohne R-Services.
2. Aktualisieren Sie SQL Server 2016 auf die gewünschte Patchebene an. Installieren Sie z. B. Service Pack 1, und klicken Sie dann kumulativen Update 2.
3. Um die Funktion auf die richtige Patchebene hinzuzufügen, führen Sie SP1 und CU2-Setup erneut aus, und drücken Sie R Services (Datenbankintern). 

#### <a name="check-whether-a-user-has-rights-to-run-external-scripts"></a>Überprüfen Sie, ob ein Benutzer Berechtigungen zum Ausführen externer Skripts verfügt.

Auch wenn Launchpad ordnungsgemäß konfiguriert ist, wird ein Fehler zurückgegeben, wenn der Benutzer keine Berechtigung zum Ausführen von R oder Python-Skripts.

Wenn Sie SQL Server als ein Datenbankadministrator installiert, oder Sie ein Datenbankbesitzer sind, werden Sie automatisch durch diese Berechtigung gewährt. Allerdings haben andere Benutzer in der Regel mehr Berechtigungen beschränkt. Wenn sie versuchen, ein R-Skript auszuführen, erhalten sie einen Launchpad-Fehler.

Zum Beheben des Problems, in SQL Server Management Studio kann ein Administrator für die Sicherheit der SQL-Anmeldung oder die Windows-Benutzerkonto ändern, indem das folgende Skript ausführen:

```SQL
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

Weitere Informationen finden Sie unter [GRANT (Transact-SQL](../t-sql/statements/grant-transact-sql.md).

### <a name="common-launchpad-errors"></a>Häufige Launchpad-Fehler

Dieser Abschnitt enthält die häufigsten Fehlermeldungen, die Launchpad zurückgibt.

#### <a name="error-unable-to-launch-runtime-for-r-script"></a>Fehler: *kann nicht zum Starten der Common Language Runtime für R-Skript*

Wenn die Windows-Gruppe für Benutzer von R (auch für Python verwendet) auf die Instanz nicht anmelden, die R-Services ausgeführt wird, können Sie die folgenden Fehler angezeigt:

- Der Fehler generiert, wenn Sie versuchen, R-Skripts auszuführen:

    * *Laufzeit für 'R'-Skript kann nicht gestartet werden. Überprüfen Sie die Konfiguration der 'R'-Laufzeit.*

    * *Ein externer Skriptfehler ist aufgetreten. Laufzeit kann nicht gestartet werden.*

- Fehler, die durch die [!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)] Dienst:

    * *Fehler beim Initialisieren des Startprogramms RLauncher.dll*

    * *Keine Startprogramm-DLLs registriert!*

    * *Sicherheitsprotokolle darauf hinweisen, dass das Konto NT-Dienst konnte sich nicht anmelden*

Weitere Informationen zu dieser Benutzergruppe die erforderlichen Berechtigungen erteilen, finden Sie unter [Einrichten von SQL Server R Services](r/set-up-sql-server-r-services-in-database.md).

> [!NOTE]
> Diese Einschränkung gilt nicht, wenn Sie SQL-Benutzernamen verwenden, um von einer Remotearbeitsstation R-Skripts auszuführen.

#### <a name="error-logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>Fehler: *Anmeldung fehlgeschlagen: der Benutzer nicht gewährt wurde die angeforderte Anmeldetyp*

Standardmäßig [!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)] verwendet das folgende Konto beim Start: `NT Service\MSSQLLaunchpad`. Das Konto wird konfiguriert, indem [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] Setup alle erforderliche Berechtigungen verfügen.

Wenn Sie ein anderes Konto zum Launchpad zuweisen, oder nach rechts durch eine Richtlinie auf dem SQL Server-Computer entfernt wird, das Konto möglicherweise nicht die erforderlichen Berechtigungen, und möglicherweise diese Fehlermeldung angezeigt:

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) 	Anmeldung fehlgeschlagen: Der Benutzer besitzt nicht den benötigten Anmeldetyp auf diesem Computer.*

Um die erforderlichen Berechtigungen für das neue Dienstkonto zu gewähren, verwenden Sie die lokale Sicherheitsrichtlinie-Anwendung, und Aktualisieren der Berechtigungen für das Konto für die folgenden Berechtigungen:

+ Anpassen des Arbeitsspeicherkontingents für einen Prozess (SeIncreaseQuotaPrivilege)
+ Umgehen von durchsuchenden Prüfungen (SeChangeNotifyPrivilege)
+ Anmelden als Dienst (SeServiceLogonRight)
+ Ersetzen von Token auf Prozessebene (SeAssignPrimaryTokenPrivilege)

#### <a name="error-unable-to-communicate-with-the-launchpad-service"></a>Fehler: *für die Kommunikation mit dem Launchpad-Dienst nicht möglich*

Wenn Sie installiert und aktiviert dann Machine Learning, aber Sie diesen Fehler, erhalten Wenn Sie versuchen, ein R oder Python-Skript auszuführen, das Launchpad-Dienst für die Instanz möglicherweise beendet wurden.

1. Öffnen Sie SQL Server Configuration Manager von Eingabeaufforderung aus. Weitere Informationen finden Sie unter [SQL Server Configuration Manager](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager).

2. Maustaste auf SQL Server Launchpad für die Instanz, und wählen Sie dann **Eigenschaften**.

3. Wählen Sie die **Service** Registerkarte, und überprüfen Sie, dass der Dienst ausgeführt wird. Wenn er nicht ausgeführt wird, ändern Sie die **Startmodus** auf **automatische**, und wählen Sie dann **übernehmen**.

4. Neustarten des Diensts in der Regel wird das Problem behebt, sodass Machine Learning-Skripts ausgeführt werden können. Wenn der Neustart nicht das Problem behoben wird, beachten Sie den Pfad und den Argumenten in der **Binärpfad** -Eigenschaft, und führen Sie folgende Schritte:

    A. Überprüfen Sie das Startprogramm config-Datei, und stellen Sie sicher, dass das Arbeitsverzeichnis gültig ist.

    B. Stellen Sie sicher, dass die Windows-Gruppe, die vom Launchpad verwendet SQL Server-Instanz herstellen kann wie in beschrieben die [vorherigen Abschnitt](#bkmk_LaunchpadTS).

    c. Wenn Sie die Diensteigenschaften nicht ändern, starten Sie den Launchpad-Dienst neu.

#### <a name="error-fatal-error-creation-of-tmpfile-failed"></a>Fehler: *beim Schwerwiegender Fehler beim Erstellen eines TmpFile*

In diesem Szenario Machine Learning-Funktionen wurden erfolgreich installiert und Launchpad ausgeführt wird. Sie versuchen, einige einfache R oder Python-Code auszuführen, aber Launchpad tritt ein Fehler wie folgt: 

>*Kann nicht für die Kommunikation mit der Common Language Runtime für R-Skript. Überprüfen Sie die Anforderungen des R-Laufzeit.*

Gleichzeitig schreibt die Laufzeit des externen Skripts die folgende Meldung als Teil der Nachricht "stderr": 

>*Schwerwiegender Fehler: Erstellung von Tmpfile ist fehlgeschlagen.*

Dieser Fehler zeigt an, dass das Konto, das Launchpad versucht, verwenden Sie keine Berechtigung zum Anmelden bei der Datenbank. Diese Situation kann auftreten, wenn strengen Sicherheitsrichtlinien implementiert werden. Um zu bestimmen, ob dies der Fall ist, überprüfen Sie die SQL Server-Protokolle, und überprüfen um festzustellen, ob bei der Anmeldung für das Konto MSSQLSERVER01 verweigert wurde. Die gleiche Informationen werden bereitgestellt, in den Protokollen, die für R spezifisch sind\_Dienste oder PYTHON\_Dienste. Suchen Sie nach ExtLaunchError.log.

Standardmäßig werden 20 Konten einrichten und dem Launchpad.exe-Prozess, mit dem Namen MSSQLSERVER01 über MSSQLSERVER20 zugeordnet. Wenn Sie starke Nutzung von R oder Python vornehmen, können Sie die Anzahl der Konten erhöhen.

Um das Problem zu beheben, stellen Sie sicher, dass die Gruppe hat *lokal anmelden zulassen* Berechtigungen mit der lokalen Instanz, in dem Machine Learning-Funktionen installiert und aktiviert wurde. In einigen Umgebungen kann dieser Berechtigungsstufe eine Gruppenrichtlinienobjekt-Ausnahme aus der Netzwerkadministrator erfordern.

## <a name="r-script-issues"></a>R-Skript-Probleme

Dieser Abschnitt enthält einige häufig auftretende Probleme, die für die Ausführung von R-Skripts und Skriptfehler R spezifisch sind. Die Liste ist nicht vollständig, da es viele R-Pakete gibt und Fehlern sich zwischen verschiedenen Versionen der gleichen R-Paket unterscheiden. Es wird empfohlen, dass Sie R-Skript-Fehler bereitstellen, auf die [Microsoft R Server-Forum](https://social.msdn.microsoft.com/Forums/home?category=MicrosoftR), das Machine learning in R-Services (Datenbankintern) Machine Learning Services mit Microsoft R, Python und Microsoft R-Client verwendete Komponenten unterstützt Server.

### <a name="multiple-r-instances-on-the-same-computer"></a>Mehrere R-Instanzen auf demselben computer

Leicht selbst in verschiedenen Versionen durch mehrere Verteilungen des R auf demselben Computer wie auch mehrere Kopien der gleichen R-Paket gefunden können werden. Bei der Installation von Machine Learning-Server (eigenständig) und Machine Learning-Services (Datenbankintern) erstellen Sie die Installationsprogramme z. B. separate Versionen der R-Bibliotheken. 

Solche Duplizierung wird ein Problem auf, wenn Sie versuchen, ein Skript über die Befehlszeile auszuführen, und Sie sind nicht sicher sind, welche Bibliotheken, die Sie verwenden. Alternativ können Sie möglicherweise installiert ein Paket auf der falschen Bibliothek und klicken Sie dann später Fragen, warum Sie das Paket von SQL Server nicht finden kann.

+ Vermeiden Sie die direkte Verwendung von R-Bibliotheken und Tools, die in selteneren Fällen, beispielsweise für die Problembehandlung für die Verwendung von SQL Server-Instanz, mit Ausnahme von installiert sind oder die Installation von neuen Paketen. 
+ Wenn Sie ein R-Befehlszeilentool verwenden müssen, können Sie installieren [Microsoft R Client](https://docs.microsoft.com/r-server/r-client/what-is-microsoft-r-client). 
+ SQL Server bietet in der Datenbank die Verwaltung von R-Paketen. Dies ist die einfachste Möglichkeit zum Erstellen von R-Paket-Bibliotheken, die von Benutzern gemeinsam genutzt werden können. Weitere Informationen finden Sie unter [paketverwaltung für SQL Server R](r/r-package-management-for-sql-server-r-services.md).

### <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>Vermeiden Sie den Arbeitsbereich löschen, während Sie R in einer SQL-computekontext ausführen

Obwohl das Löschen des Arbeitsbereichs üblich ist, bei der Arbeit in der R-Konsole, haben sie unbeabsichtigte Folgen in einer SQL-computekontext.

`revoScriptConnection`ist ein Objekt in den R-Arbeitsbereich, der Informationen über eine R-Sitzung enthält, die von SQL Server aufgerufen wird. Jedoch Wenn R-Code einen Befehl zum Deaktivieren des Arbeitsbereichs enthält (z. B. `rm(list=ls())`), alle Informationen über die Sitzung und anderen Objekten im Arbeitsbereich "R" ist ebenfalls deaktiviert.

Vermeiden Sie dieses Problem zu umgehen die willkürliche Löschen von Variablen und andere Objekte während Sie R in SQL Server ausführen. Sie können bestimmte Variablen löschen, indem Sie mit der **entfernen** Funktion:

```R
remove('name1', 'name2', ...)
```

Wenn es mehrere Variablen sind löschen, wird empfohlen, dass Sie eine Liste der Namen von temporären Variablen speichern, und führen Sie regelmäßige Ausführung von Garbage Collections auf der Liste.

### <a name="implied-authentication-for-remote-execution-via-odbc"></a>Implizite Authentifizierung für die Remoteausführung über ODBC

Wenn Sie zum Verbinden der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Computer für die Ausführung von R-Befehle mithilfe der **"revoscaler"** Funktionen die, Sie erhalten möglicherweise eine Fehlermeldung bei Verwendung von ODBC-Aufrufe, die Daten an den Server zu schreiben. Dieser Fehler tritt nur auf, wenn Sie Windows-Authentifizierung verwenden.

Der Grund ist, dass die Konten, die für R Services erstellt werden nicht für die Verbindung mit dem Server berechtigt sind. Aus diesem Grund können die ODBC-Aufrufe in Ihrem Auftrag ausgeführt werden. Das Problem tritt nicht mit SQL-Anmeldungen, da mit SQL-Anmeldungen, die Anmeldeinformationen explizit von der R-Client in SQL Server-Instanz und dann in ODBC übergeben werden. Es ist jedoch auch weniger sicher als die Windows-Authentifizierung, SQL-Anmeldungen verwenden.

Ihre Anmeldeinformationen muss emulieren, zum Aktivieren der Windows-Anmeldeinformationen, die sicher aus einem Skript übergeben werden, die Remote SQL Server initiiert hat. Dieser Prozess wird als bezeichnet _implizite Authentifizierung_. Damit dies funktioniert, benötigen die Worker-Konten, die R oder Python-Skripts auf dem SQL Server-Computer ausgeführt, die richtigen Berechtigungen.

1. Open [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] als Administrator für die Instanz, auf dem R-Code ausgeführt werden soll.

2. Führen Sie das folgende Skript aus: Achten Sie darauf, um Benutzergruppennamen, wenn Sie die Standardeinstellung geändert haben und die Namen von Computern und die Instanz zu bearbeiten.

    ```SQL
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

### <a name="the-r-script-works-outside-of-t-sql-but-not-in-a-stored-procedure"></a>R-Skript funktioniert außerhalb von T-SQL, aber nicht in einer gespeicherten Prozedur

Vor dem umschließen Ihrer R-Codes in einer gespeicherten Prozedur, ist es ratsam, Ihre R-Code in einer externen IDE oder in einem R-Tools, z. B. RTerm oder "rgui.exe" ausgeführt. Mithilfe dieser Methoden können können Sie testen und Debuggen von Code mithilfe der detaillierte Fehlermeldungen, die von r zurückgegeben werden

Allerdings manchmal Code, der in einem externen IDE oder Hilfsprogramm perfekt funktioniert möglicherweise nicht in einer gespeicherten Prozedur ausführen oder in einer SQL Server-computekontext. In diesem Fall stehen eine Reihe von Problemen, der gesucht werden soll, bevor Sie davon ausgehen können, dass das Paket in SQL Server funktionieren nicht.

1. Überprüfen, ob Sie Launchpad ausgeführt wird.

2. Überprüfen Sie die Nachrichten, um festzustellen, ob die Eingabedaten oder die Ausgabedaten Spalten mit Datentypen nicht kompatibel oder nicht unterstützt enthält. Beispielsweise zurückgeben Abfragen für eine SQL­Datenbank häufig GUIDs oder aktualisieren, die nicht unterstützt werden. Weitere Informationen finden Sie unter [R-Bibliotheken und Datentypen](r/r-libraries-and-data-types.md).

3. Überprüfen Sie die Hilfeseiten für einzelne R-Funktionen, um zu bestimmen, ob alle Parameter für die SQL Server-computekontext unterstützt werden. Für ScaleR Hilfe zu erhalten, verwenden Sie die Befehle der Inline-R-Hilfe oder finden Sie unter [Paket Verweis](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler).

### <a name="you-get-different-results-from-the-same-script-when-running-in-sql-compared-to-other-environments"></a>Erhalten Sie unterschiedliche Ergebnisse aus dem gleichen Skript bei der Ausführung in SQL im Vergleich zu anderen Umgebungen

R-Skripts können unterschiedliche Werte in einem SQL Server-Kontext, verschiedene Ursachen zurückgeben:

- Implizite Typumwandlung ist für einige Datentypen automatisch ausgeführt, wenn die Daten zwischen SQL Server und r übergeben wird Weitere Informationen finden Sie unter [R-Bibliotheken und Datentypen](r/r-libraries-and-data-types.md).

- Bestimmen Sie, ob Bitanzahl ein Faktor ist. Es gibt z. B. häufig Unterschiede in den Ergebnissen aus mathematischen Vorgängen für 32-Bit und 64-Bit-floating Point-Bibliotheken.

- Bestimmen Sie, ob bei jedem Vorgang NaNs erzeugt wurden. Dadurch kann die Ergebnisse ungültig.

- Geringfügige Unterschiede können verstärkt werden, wenn Sie einen Kehrwert einer Zahl in der Nähe von 0 (null) erstellen.

- Akkumulierte Rundungsfehler kann u. a. die Werte, die sind kleiner als null statt 0 (null).

### <a name="error-not-enough-quota-to-process-this-command"></a>Fehler: *nicht genügend Kontingent für diesen Befehl*

Dieser Fehler kann eine von mehreren Aktionen bedeuten:

- Launchpad möglicherweise nicht genügend externe Benutzer auf die externe Abfrage auszuführen. Wenn Sie mehr als 20 externe Abfragen gleichzeitig ausgeführt werden, und es nur 20 Standardbenutzern sind, könnte z. B. eine oder mehrere Abfragen fehl.

- Nicht genügend Arbeitsspeicher ist verfügbar, um den R-Task zu verarbeiten. Dieser Fehler tritt am häufigsten in einer standardumgebung, in dem SQL Server bis zu 70 Prozent der Ressourcen des Computers verwendet werden kann. Informationen zum Ändern der Serverkonfiguration zur Unterstützung größer Verwendung von Ressourcen, die von R finden Sie unter [Operationalisieren Ihres R-Codes](r/operationalizing-your-r-code.md).

### <a name="error-cant-find-package"></a>Fehler: *Paket wurde nicht gefunden*

Wenn Sie R-Code in SQL Server ausführen und diese Nachricht erhalten, aber die Nachricht nicht abgerufen werden, wenn Sie den gleichen Code außerhalb von SQL Server ausgeführt haben, bedeutet dies, dass das Paket nicht am Standardspeicherort-Bibliothek verwendet, die von SQL Server installiert wurde.

Dieser Fehler kann in vielerlei Hinsicht auftreten:

- Sie haben ein neues Paket auf dem Server installiert, aber der Zugriff wurde verweigert, damit R in einer Benutzerbibliothek das Paket installiert.

- Sie R Services installiert haben und dann ein anderes R-Tool installiert oder Satz von Bibliotheken, einschließlich Microsoft R Server (eigenständig), Microsoft R-Client RStudio, usw.

Um den Speicherort der R-Paket-Bibliothek zu bestimmen, die von der Instanz verwendet wird, öffnen Sie SQL Server Management Studio (oder einem anderen Datenbank-Abfrage-Tool), eine Verbindung mit der Instanz, und führen Sie die folgende gespeicherte Prozedur:

```SQL
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>Bespielergebnisse

*STDOUT message(s) from external script:*

*[1] "" c: "\\Programmdateien\\Microsoft SQL Server\\MSSQL13. SQL2016\\R_SERVICES "*

*[1] "c: / Program Programme/Microsoft SQL Server/MSSQL13. SQL2016/R_SERVICES/Library"*

Um das Problem zu beheben, müssen Sie das Paket in der Bibliothek der SQL Server-Instanz neu installieren.

>[!NOTE]
>Wenn Sie eine Instanz von SQL Server 2016, verwenden Sie die neueste Version von Microsoft R aktualisiert haben, unterscheidet sich der Standardspeicherort für die Bibliothek. Weitere Informationen finden Sie unter [verwenden SqlBindR zum Aktualisieren einer Instanz des R Services](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="next-steps"></a>Nächste Schritte

[Machine Learning Services Problembehandlung und bekannte Probleme](machine-learning-troubleshooting-faq.md)

[Die Datensammlung für die Problembehandlung von Machine learning](data-collection-ml-troubleshooting-process.md)

[Häufig gestellte Fragen zu Upgrade und Installation](r/upgrade-and-installation-faq-sql-server-r-services.md)

[Problembehandlung bei Datenbank-Engine-Verbindungen](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
