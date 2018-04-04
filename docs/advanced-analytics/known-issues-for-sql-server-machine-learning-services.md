---
title: Bekannte Probleme in Machine Learning Services | Microsoft Docs
ms.date: 02/05/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 65294b0b630b662e68d252312a865dc8e898dec5
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="known-issues-in-machine-learning-services"></a>Bekannte Probleme in Machine Learning-Diensten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel beschreibt bekannte Probleme oder Einschränkungen mit den Machine learning-Komponenten, die als Option in SQL Server 2016 und SQL Server-2017 bereitgestellt werden.

Die Informationen hier gilt für alle der folgenden, sofern nicht anders angegeben:

SQL Server 2016

- R Services (In-Database)
- Microsoft R Server (eigenständig)

SQL Server 2017

- Machine Learning-Dienste für R (In-Database)
- Machine Learning-Dienste für Python (In-Database)
- Machine Learning-Server (eigenständig)

## <a name="setup-and-configuration-issues"></a>Setup- und Konfigurationsprobleme

Eine Beschreibung der Prozesse und häufig gestellte Fragen, die auf der ersten Installation und Konfiguration beziehen, finden Sie unter [häufig gestellte Fragen zu Upgrade und Installation](r/upgrade-and-installation-faq-sql-server-r-services.md). Es enthält Informationen zu Upgrades, parallele Installation und Installation des neuen R oder Python-Komponenten.

### <a name="unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>So installieren Sie SQL Server-Machine Learning-Funktionen auf einem Domänencontroller

Wenn Sie versuchen, SQL Server 2016 R Services oder SQL Server 2017 Machine Learning Services auf einem Domänencontroller installieren, schlägt die Installation fehl, diese Fehler:

> *Während des Setups der Funktion ist ein Fehler aufgetreten.*
> 
> *Gruppe mit der Identität wurde nicht gefunden.*
> 
> *Komponente-Fehlercode: 0 x 80131509*

Der Fehler tritt auf, da auf einem Domänencontroller installiert, die 20 lokalen Konten zur Ausführung von Machine Learning erforderlich der Dienst erstellt werden kann. Im Allgemeinen empfohlen nicht installieren von SQL Server auf einem Domänencontroller installiert. Weitere Informationen finden Sie unter [Unterstützung Bulletin 2032911](https://support.microsoft.com/en-us/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont).

### <a name="install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>Installieren Sie das neueste Service Release, um die Kompatibilität mit Microsoft R Client sicherzustellen

Wenn Sie die neueste Version von Microsoft R-Client installieren und sie zum Ausführen von R auf SQL Server in einem remote-computekontext verwenden, erhalten Sie möglicherweise einen Fehler wie folgt:

> *Auf dem Computer, die mit Microsoft R Server Version 8.x.x nicht kompatibel ist, werden Sie 9.x.x der Version des Microsoft-R-Client ausgeführt. Laden Sie eine kompatible Version herunter und installieren Sie sie.*

SQL Server 2016 erfordert, dass die R-Bibliotheken auf dem Client die R-Bibliotheken auf dem Server genau übereinstimmen. Die Einschränkung wurde für Versionen höher als R-Server 9.0.1 entfernt. Dieser Fehler auftritt, überprüfen Sie die Version der R-Bibliotheken, die von Ihrem Client und Server verwendet wird, und aktualisieren Sie bei Bedarf den Client entsprechend die Serverversion Sie.

Die Version von R, die mit SQL Server R Services installierte wird aktualisiert, sobald eine SQL Server-Service-Version installiert ist. Um sicherzustellen, dass Sie immer die neuesten Versionen der R-Komponenten haben, werden Sie alle Servicepacks zu installieren.

Um die Kompatibilität mit Microsoft R Client 9.0.0 sichergestellt ist, installieren Sie die Updates, die beschrieben werden in diesem [Support-Artikel](https://support.microsoft.com/kb/3210262).

Zur Vermeidung von Problemen mit R-Pakete können Sie auch die Version der R-Bibliotheken, die auf dem Server installiert sind, durch die Wartung Vereinbarung mithilfe die modernen Lifecycle Support-Richtlinie ändern, wie in beschrieben aktualisieren [im nächsten Abschnitt](#bkmk_sqlbindr). Wenn Sie dies tun, wird die Version von R, die mit SQL Server installiert wird nach demselben Zeitplan zum Aktualisieren des Machine Learning-Servers (früher Microsoft R Server) aktualisiert.

**Gilt für:** SQL Server 2016 R Services mit R-Server Version 9.0.0 oder früher

### <a name="r-components-missing-from-cu3-setup"></a>R-Komponenten fehlt in der CU3-setup

Eine begrenzte Anzahl von Azure-virtuelle Computer wurden ohne die R-Installationsdateien bereitgestellt, die mit SQL Server eingeschlossen werden soll. Das Problem gilt für virtuelle Maschinen bereitgestellt werden, in dem Zeitraum zwischen 2018-01-05 und 2018-01-23. Dieses Problem beeinträchtigt auch für lokale Installationen, wenn Sie das CU3-Update für SQL Server-2017 während des Zeitraums von 2018-01-05 auf 2018-01-23 angewendet.

Es wurde eine Dienstversion bereitgestellt, die richtige Version der R-Installationsdateien enthält.

+ [Kumulatives Updatepaket 3 für SQL Server 2017 KB4052987](https://www.microsoft.com/en-us/download/details.aspx?id=56128).

Um die Komponenten zu installieren, und SQL Server 2017 CU3 reparieren, müssen Sie CU3 deinstallieren und installieren die aktualisierte Version:

1. Herunterladen der aktualisierten CU3-Installationsdatei, inklusive der R-Pakete.
2. Deinstallieren Sie CU3. Suchen Sie in der Systemsteuerung für **Deinstallieren eines Updates**, und wählen Sie dann auf "Hotfix 3015 für SQLServer 2017 (KB4052987) (64-Bit)". Fahren Sie mit der Schritte zur Deinstallation.
3. Installieren Sie das Update CU3 durch Doppelklicken auf das Update für KB4052987, die Sie gerade heruntergeladen haben: `SQLServer2017-KB4052987-x64.exe`. Befolgen Sie die Installationsanweisungen.

### <a name="unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>Es können Python-Komponenten in offline-Installationen von SQL Server 2017 CTP 2.0 oder höher installiert

Wenn Sie eine Vorabversion von SQL Server-2017 auf einem Computer ohne Internetzugang installieren, kann das Installationsprogramm auf der Seite angezeigt, die für den Speicherort der heruntergeladenen Python Komponenten fordert fehl. In solch einem Fall können Sie die Machine Learning-Datenbankdienste-Funktion, aber nicht die Python-Komponenten installieren.

Dieses Problem wird in der endgültigen Produktversion behoben. Darüber hinaus gilt diese Einschränkung nicht für R-Komponenten.

**Gilt für:** 2017 von SQLServer mit Python

### <a name="bkmk_sqlbindr"></a> Inkompatible Version Warnung, wenn Sie mit einer älteren Version von SQL Server R Services von einem Client mit verbinden [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

Beim Ausführen von R-Code in eine SQL Server 2016-computekontext, möglicherweise die folgende Fehlermeldung angezeigt:

> *Sie führen Version 9.0.0 von Microsoft R Client auf Ihrem Computer aus. Diese ist nicht mit der Microsoft R Server-Version 8.0.3 kompatibel. Laden Sie eine kompatible Version herunter und installieren Sie sie.*

Diese Meldung wird angezeigt, wenn eine der beiden folgenden Anweisungen ist "true",

+ R Server (eigenständig) wird auf einem Clientcomputer installiert, mithilfe des Setup-Assistenten für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].
+ Sie installiert Microsoft R Server mithilfe der [separate Windows Installer](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

Um sicherzustellen, dass der Server und der Client die gleiche Version verwenden, Sie möglicherweise verwenden müssen _Bindung_, unterstützte für Microsoft R Server 9.0 und späteren Versionen die R-Komponenten in SQL Server 2016-Instanzen zu aktualisieren. Zum bestimmen, ob die Unterstützung für Upgrades steht für Ihre Version von R-Services finden Sie unter [Aktualisieren einer Instanz von R-Dienste, die mithilfe von SqlBindR.exe](/r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

**Gilt für:** SQL Server 2016 R Services mit R-Server Version 9.0.0 oder früher

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>Setup für SQL Server 2016 Service Releases kann unter Umständen keine neueren R-Komponenten installieren

Wenn Sie ein kumulatives Update installieren oder ein Servicepack für SQL Server 2016 auf einem Computer, der nicht mit dem Internet verbunden ist, möglicherweise nicht der Setup-Assistenten die Aufforderung angezeigt, in dem Sie die R-Komponenten zu aktualisieren, indem Sie die heruntergeladenen CAB-Dateien können. Dieser Fehler tritt normalerweise auf, wenn mehrere Komponenten zusammen mit dem Datenbankmodul installiert wurden.

Dieses Problem zu umgehen, können Sie mithilfe der Befehlszeile und angeben die Dienstversion installieren die `MRCACHEDIRECTORY` Argument wie in diesem Beispiel gezeigt die CU1-Updates installiert wird:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

Um die neuesten Installationsprogramme zu erhalten, finden Sie unter [Machine Learning-Komponenten ohne Internetzugang installieren](install/sql-ml-component-install-without-internet-access.md).

**Gilt für:** SQL Server 2016 R Services mit R-Server Version 9.0.0 oder früher

### <a name="launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>Launchpad-Dienste nicht gestartet werden, wenn die Version der R-Version unterscheidet

Wenn Sie SQL Server R Services separat vom Datenbankmodul installieren, und die Buildversionen unterschiedlich sind, wird möglicherweise den folgenden Fehler im Systemereignisprotokoll angezeigt:

> *Der SQL Server Launchpad-Dienst konnte wegen des folgenden Fehlers nicht gestartet: der Dienst hat nicht auf die Start- oder Anforderung rechtzeitig reagiert.*

Beispielsweise kann dieser Fehler auftreten, wenn Sie das Datenbankmodul installiert, mit der endgültigen Produktversion Anwenden eines Patches, um das Datenbankmodul zu aktualisieren und dann die R-Services-Funktion hinzufügen, indem Sie mit der endgültigen Produktversion.

Um dieses Problem zu vermeiden, verwenden Sie ein Hilfsprogramm z. B. Datei-Manager, um die Versionen der Launchpad.exe mit Version der SQL-Binärdateien, z. B. sqldk.dll zu vergleichen. Alle Komponenten müssen die gleiche Versionsnummer. Wenn Sie eine Komponente aktualisieren, müssen Sie dasselbe Upgrade auf alle anderen installierten Komponenten anwenden.

Suchen Sie nach Launchpad in die `Binn` Ordner für die Instanz. Z. B. in einer Standardinstallation von SQL Server 2016, der Pfad möglicherweise `C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn`. 

### <a name="remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>Remote rechenkontexte werden durch eine Firewall in SQL Server-Instanzen blockiert, die auf virtuellen Azure-Computern ausgeführt werden

Wenn Sie installiert haben [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] auf einem Windows Azure-virtuellen Computer nicht können Sie möglicherweise rechenkontexte verwenden, die die Verwendung des Arbeitsbereichs des virtuellen Computers erfordern. Der Grund ist, dass standardmäßig die Firewall auf virtuellen Azure-Computern eine Regel enthält, dass der Netzwerkzugriff für lokale Benutzerkonten für R blockiert.

Öffnen Sie dieses Problem zu umgehen, auf der Azure-VM **Windows-Firewall mit erweiterter Sicherheit**Option **ausgehende Regeln**, und deaktivieren Sie die folgende Regel: **Netzwerkzugriff für lokale R-Benutzerkonten in blockieren SQL Server-Instanz MSSQLSERVER**. Sie können auch die Regel aktiviert lassen jedoch ändern Sie die Eigenschaft für die Sicherheit auf **zulassen bei sicheren Verbindungen**.

### <a name="implied-authentication-in-sqlexpress"></a>Implizite Authentifizierung in SQLEXPRESS

Wenn Sie R-Aufträge mithilfe der integrierten Windows-Authentifizierung über eine remote Data Science-Arbeitsstation ausführen, verwendet SQL Server *implizite Authentifizierung* alle lokalen ODBC-Aufrufe zu generieren, die unter Verwendung des Skripts erforderlich sein könnten. Im RTM-Build der SQL Server Express Edition funktionierte diese Funktion jedoch nicht.

Um das Problem zu beheben, empfehlen wir die Aktualisierung auf ein neueres Service Release.

Wenn das Upgrade nicht möglich ist, dieses Problem zu umgehen, verwenden Sie eine SQL-Anmeldung remote R-Aufträge ausgeführt werden, die eingebettete ODBC-Aufrufe möglicherweise fest.

**Gilt für:** SQL Server 2016-R Services Express Edition

### <a name="performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>Leistung beschränkt, wenn von SQL Server verwendeten Bibliotheken mithilfe anderer Tools aufgerufen werden

Es ist möglich, rufen Sie die Machine learning-Bibliotheken, die von einer externen Anwendung, z. B. "rgui.exe" für SQL Server installiert sind. Auf diese Weise ist möglicherweise die zweckmäßigste Art, wie neue Pakete installieren und Ausführen von ad-hoc-Tests auf sehr kurze Codebeispiele bestimmte Aufgaben ausgeführt werden können. Allerdings möglicherweise außerhalb von SQL Server, Leistung beschränkt sein. 

Beispielsweise, selbst wenn Sie die Enterprise Edition von SQL Server verwenden, führt R im Singlethread-Modus beim Ausführen des R-Code mithilfe von externen Tools. Rufen Sie die Vorteile der Leistung in SQL Server eine SQL Server-Verbindung initiieren, und verwenden Sie [Sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) der externen Skriptlaufzeit aufrufen.

Vermeiden Sie generell das Aufrufen von Machine learning-Bibliotheken, die von externen Tools von SQL Server verwendet werden. Wenn Sie zum Debuggen R "oder" Python-Code müssen, ist es in der Regel einfacher dazu außerhalb von SQL Server. Um die gleichen Bibliotheken zu erhalten, die in SQL Server sind, können Sie Microsoft R-Client installieren [SQL Server 2017 Machine Learning-Server (eigenständig)](install/sql-machine-learning-standalone-windows-install.md), oder [SQL Server 2016 R Server (eigenständig)](install/sql-r-standalone-windows-install.md).

### <a name="sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>Externer Skripts, die erforderlichen Berechtigungen für unterstützt SQL Server Data Tools nicht.

Wenn Sie Visual Studio oder SQL Server Data Tools verwenden, veröffentlichen ein Datenbankprojekt Prinzipal Berechtigungen, die speziell für externen skriptausführung verfügt, erhalten Sie möglicherweise einen Fehler wie diese:

> *TSQL-Modell: Fehler beim reverse engineering der Datenbank. Die Berechtigung wurde nicht erkannt und wurde nicht importiert.*

Das DACPAC-Modell unterstützt derzeit nicht die Berechtigungen, die von R Services "oder" Machine Learning-Dienste, z. B. GRANT ANY EXTERNAL SCRIPT oder EXECUTE ANY EXTERNAL SCRIPT verwendet. Dieses Problem wird in einer künftigen Version behoben werden.

Dieses Problem zu umgehen führen Sie die Gewährung für die zusätzliche Anweisungen in einem Skript nach der Bereitstellung.

### <a name="external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>Ausführen des externen Skripts wird aufgrund der Ressource Governance-Standardwerte eingeschränkt.

In Enterprise Edition können Sie Ressourcenpools verwenden, um externe Skriptprozesse zu verwalten. In einigen frühen Releasebuilds wurde der maximale Arbeitsspeicher, der an die R-Prozesse zugeordnet werden kann 20 Prozent. Daher wäre der Server über 32 GB RAM, konnte die ausführbaren Dateien R ("RTerm.exe" und "BxlServer.exe") maximal 6,4 GB in einer einzelnen Anforderung verwenden.

Wenn überprüfen Sie ressourceneinschränkungen auftreten, die aktuelle Standardeinstellung. Wenn 20 Prozent nicht ausreichend ist, finden Sie in der Dokumentation für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] zum Ändern dieses Werts.

**Gilt für:** SQL Server 2016-R-Services, Enterprise Edition

## <a name="r-issues"></a>R-Probleme

Dieser Abschnitt enthält bekannte Probleme, die zum Ausführen von R bei SQL Server beziehen, sowie einige Probleme mit der R-Bibliotheken und Tools, die von Microsoft, einschließlich "revoscaler" veröffentlicht werden.

Weitere bekannte Probleme, die R-Lösungen beeinträchtigen können, finden Sie unter der [Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues) Standort.

### <a name="access-denied-warning-when-executing-r-scripts-on-sql-server-in-a-non-default-location"></a>"Zugriff verweigert" Warnung bei der Ausführung von R-Skripts an SQL Server auf einem Nichtstandard-Speicherort

Wenn z. B. SQL Server-Instanz an einen nicht standardmäßigen Speicherort installiert wurde außerhalb der `Program Files` Ordner, der die Warnung ACCESS_DENIED ausgelöst wird, wenn Sie versuchen, Skripts auszuführen, die ein Paket zu installieren. Beispiel:

> *In `normalizePath(path.expand(path), winslash, mustWork)` : Pfad [2] = "~ExternalLibraries/R/8/1": Zugriff wurde verweigert.*

Der Grund hierfür ist, dass eine R-Funktion versucht, den Pfad zu lesen, und schlägt fehl, wenn die integrierte Benutzergruppe **SQLRUserGroup**, hat keinen Lesezugriff. Die Warnung, die ausgelöst wird, blockiert die Ausführung des aktuellen R-Skripts nicht, aber die Warnung möglicherweise mehrmals wiederholt werden, wenn der Benutzer alle R-Skript ausführt.

Wenn Sie SQL Server am Standardspeicherort installiert haben, dieser Fehler tritt nicht auf, da alle Windows-Benutzer auf über Leseberechtigungen verfügen die `Program Files` Ordner.

Dieses Problem behandelt ia in einer bevorstehenden Dienstversion. Dieses Problem zu umgehen, geben Sie der Gruppe "" **SQLRUserGroup**, mit Lesezugriff für alle übergeordneten Ordner der `ExternalLibraries`.

### <a name="serialization-error-between-old-and-new-versions-of-revoscaler"></a>Serialisierungsfehler zwischen den alten und neuen Versionen von "revoscaler"

Wenn Sie ein Modell mit einem serialisierten Format mit einer Remoteinstanz von SQL Server übergeben, wird möglicherweise die Fehlermeldung angezeigt: 

> *Error in memDecompress(data, type = decompress) internal error -3 in memDecompress(2).*

Dieser Fehler wird ausgelöst, wenn Sie das Modell über eine aktuelle Version von die Serialisierungsfunktion gespeichert [RxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel), aber SQL Server-Instanz, in dem Sie das Modell deserialisieren, hat eine ältere Version der APIs "revoscaler" von SQL Server 2017 CU2 oder früher.

Dieses Problem zu umgehen können Sie die 2017 von SQL Server-Instanz auf CU3 oder höher aktualisieren.

Der Fehler wird nicht angezeigt, wenn die API-Version identisch ist oder wenn Sie ein Modell mit einer älteren Serialisierungsfunktion auf einem Server, der eine neuere Version der Serialisierung API verwendet gespeicherte verschieben.

Verwenden Sie die gleiche Version von "revoscaler" heißt, für Serialisierungs-und Deserialisierungsvorgängen.

### <a name="real-time-scoring-does-not-correctly-handle-the-learningrate-parameter-in-tree-and-forest-models"></a>Echtzeit-Bewertung ist nicht ordnungsgemäß behandelt die _LearningRate_ Parameter in der Struktur und Gesamtstruktur-Modelle

Wenn Sie ein Modell mit einer Entscheidungsstruktur oder die Entscheidung Gesamtstruktur Methode erstellen, und gibt die lerngeschwindigkeit an, möglicherweise zu inkonsistente Ergebnissen mit `sp_rxpredict` oder der SQL- `PREDICT` -Funktion im Vergleich mit `rxPredict`.

Die Ursache ist ein Fehler in der API, Prozesse, die serialisiert modelliert und ist auf die `learningRate` Parameter: beispielsweise im [RxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees), oder

Dieses Problem wird in einer bevorstehenden Dienstversion behandelt.

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>Einschränkungen der Prozessoraffinität für R-Aufträge

In der ersten Version Build von SQL Server 2016 konnte die Prozessoraffinität nur für CPUs in der ersten k-Gruppe festgelegt werden. Wenn der Server einen 2-Socket-Computer mit zwei k-Gruppen ist, werden z. B. nur Prozessoren aus der ersten k-Gruppe für die R-Prozesse verwendet. Die gleiche Einschränkung gilt beim Konfigurieren der Ressourcenkontrolle für R-Skript-Aufträge.

Dieses Problem wurde in SQL Server 2016 Service Pack 1 behoben. Es wird empfohlen, ein upgrade auf die neueste Dienstversion.

**Gilt für:** SQL Server 2016 R Services-RTM-Version

### <a name="changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>Änderungen an Spaltentypen nicht möglich, wenn Daten in SQL Server-Rechenkontext gelesen werden

Wenn der Rechenkontext auf die SQL Server-Instanz festgelegt ist, können Sie das Argument _ColClasses_ (oder andere ähnliche Argumente) nicht verwenden, um den Datentyp von Spalten in Ihrem R-Code zu ändern.

Die folgende Anweisung würde beispielsweise zu einem Fehler würden, wenn die Spalte CRSDepTimeStr keine Ganzzahl ist:

```R
data <- RxSqlServerData(
  sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall", 
  connectionString = connectionString, 
  colClasses = c(CRSDepTimeStr = "integer"))
```

Dieses Problem zu umgehen, können Sie die SQL-Abfrage zum Verwenden von CAST umschreiben oder konvertieren, und präsentieren der Daten an R mit den richtigen Datentyp. Leistung ist im Allgemeinen besser, wenn Sie mit Daten mithilfe von SQL anstatt durch das Ändern von Daten in der R-Code arbeiten.

**Gilt für:** SQL Server 2016 R Services

### <a name="limits-on-size-of-serialized-models"></a>Beschränkungen der Größe der serialisierten Modelle

Wenn Sie ein Modell in einer SQL Server-Tabelle speichern, müssen Sie Serialisieren des Modells und in einem binären Format zu speichern. Theoretisch ist die maximale Größe eines Modells, die mit dieser Methode gespeichert werden können, 2 GB sind, die die maximale Größe eines Varbinary-Spalten in SQL Server ist.

Wenn Sie größere Modelle verwenden müssen, sind die folgenden problemumgehungen verfügbar:

+ Schritte zum Verringern der Größe des Modells. Einige open Source-R-Pakete enthalten einen Großteil der Informationen in der Model-Objekts, und ein Großteil dieser Informationen kann für die Bereitstellung entfernt werden. 
+ Verwenden Sie Funktionsauswahl, um nicht benötigte Spalten entfernen.
+ Wenn Sie einen open-Source-Algorithmus verwenden, sollten Sie eine ähnliche Implementierung, die mit dem entsprechenden Algorithmus in MicrosoftML oder "revoscaler". Diese Pakete sind für Bereitstellungsszenarien optimiert wurde.
+ Nachdem das Modell rationalisierte Infrastruktur wurde hat und die Größe verringert den vorangegangenen Schritten, festzustellen, ob die [MemCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress) -Funktion in R Basis kann zum Verringern der Größe des Modells, vor der Übergabe an SQL Server verwendet werden. Diese Option wird empfohlen, wenn das Modell in der Nähe der 2 GB beschränkt ist.
+ Für größere Modelle können Sie die SQL Server [FileTable](..\relational-databases\blob\filetables-sql-server.md) Funktion, um die Modelle zu speichern, anstatt eine Varbinary-Spalte.

    Um FileTables verwenden zu können, müssen Sie eine Firewallausnahme hinzufügen, da in FileTables gespeicherte Daten von den Filestream-Dateisystem-Treiber in SQL Server verwaltet werden und die Standardregeln für die Firewall blockiert werden Netzwerkzugriff für die Datei. Weitere Informationen finden Sie unter [aktivieren erforderlichen Komponenten für FileTable](../relational-databases/blob/enable-the-prerequisites-for-filetable.md). 

    Nachdem Sie FileTable, um dem Modell, Schreiben Sie einen Pfad von SQL erhalten mithilfe der FileTable-API aktiviert haben, und klicken Sie dann das Modell für diesen Speicherort aus dem Code schreiben. Wenn Sie das Modell lesen müssen, Sie den Pfad von SQL und rufen Sie dann das Modell mit dem Pfad in Ihrem Skript. Weitere Informationen finden Sie unter [zugreifen auf FileTables mit Datei-e / a-APIs](../relational-databases/blob/access-filetables-with-file-input-output-apis.md).

### <a name="avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>Zu vermeiden, deaktivieren Arbeitsbereiche, beim Ausführen von R-Code in einem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] computekontext

Wenn Sie einen R-Befehl verwenden, um den Arbeitsbereich von Objekten zu deaktivieren, während der Ausführung von R-Code in eine [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] computekontext, oder wenn Sie den Arbeitsbereich als Teil eines R-Skripts deaktivieren aufgerufen werden, mithilfe von [Sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), erhalten Sie möglicherweise diesen Fehler : *Arbeitsbereich Objekt RevoScriptConnection wurde nicht gefunden.*

`revoScriptConnection` ist ein Objekt im R-Arbeitsbereich, das Informationen über eine R-Sitzung enthält, die aus [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]aufgerufen wird. Wenn Ihr R-Code jedoch einen Befehl zum Löschen des Arbeitsbereichs enthält (wie z.B. `rm(list=ls()))`), werden alle Informationen über die Sitzung und andere Objekte im R-Arbeitsbereich ebenfalls gelöscht.

Vermeiden Sie dieses Problem zu umgehen, willkürliche Löschen von Variablen und andere Objekte während der Ausführung von R sind [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Obwohl das Löschen des Arbeitsbereichs üblich ist, bei der Arbeit in der R-Konsole, haben sie unerwartete Ergebnisse liefern.

* Um bestimmte Variablen zu löschen, verwenden Sie das R `remove` Funktion: z. B. `remove('name1', 'name2', ...)`
* Wenn mehrere zu löschende Variablen vorhanden sind, speichern Sie die Namen temporärer Variablen in einer Liste und führen eine regelmäßige automatische Speicherbereinigung durch.

### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>Einschränkungen von Daten, die als Eingabe für ein R-Skript bereitgestellt werden können

Sie können die folgenden Typen von Abfrageergebnissen nicht in einem R-Skript verwenden:

- Daten aus einer [!INCLUDE[tsql](../includes/tsql-md.md)] -Abfrage, die auf „AlwaysEncrypted“-Spalten verweist.
  
- Daten aus einer [!INCLUDE[tsql](../includes/tsql-md.md)] -Abfrage, die auf maskierte Spalten verweist.
  
     Wenn Sie maskierte Daten in einem R-Skript verwenden müssen, ist eine mögliche Problemumgehung das Erstellen einer Kopie der Daten in einer temporären Tabelle und anschließende Verwenden dieser Daten.

### <a name="use-of-strings-as-factors-can-lead-to-performance-degradation"></a>Verwenden von Zeichenfolgen als Faktoren zu Leistungseinbußen führen kann

Verwenden von Zeichenfolgenvariablen für Typ Faktoren die Speichermenge, die für R-Vorgänge verwendet, deutlich erhöhen können. Dies ist ein bekanntes Problem mit R in der Regel, und viele Artikel auf das Subjekt vorhanden sind. Deutet, finden Sie unter [Faktoren sind nicht in R von John einlegen, in R-Blogger hohem Maße für Webdaten)](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/) oder [StringsAsFactors: eine nicht autorisierte Informationen, indem Roger Peng](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/). 

Obwohl das Problem nicht spezifisch für SQL Server ist, kann es die Leistung von R-Code in SQl Server ausführen, erheblich beeinträchtigen. Zeichenfolgen werden in der Regel als Varchar oder nvarchar-Datentyp gespeichert, und wenn eine Spalte von Zeichenfolgendaten viele eindeutige Werte enthält, kann der Vorgang des Konvertierens intern in ganze Zahlen und Zeichenfolgen von R an selbst zu aufgrund von Zuordnungsfehlern der Arbeitsspeicher führen.

Wenn Sie nicht unbedingt einen Zeichenfolgen-Datentyp für andere Vorgänge benötigen die Zeichenfolgenwerte in einen numerischen Wert (Integer) zuordnen geben Daten als Teil der Vorbereitung der Daten im Hinblick auf Leistung und Skalierung Vorteil wäre.

Eine Erörterung von diesem Problem sowie weitere Tipps finden Sie [Leistung für R Services – datenoptimierung](r/r-and-data-optimization-r-services.md).

### <a name="arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>Argumente *VarsToKeep* und *VarsToDrop* werden für SQL Server-Datenquellen nicht unterstützt

Wenn Sie die RxDataStep-Funktion verwenden, um die Ergebnisse in eine Tabelle zu schreiben, verwenden die *VarsToKeep* und *VarsToDrop* ist eine praktische Möglichkeit der Angabe der Spalten ein-oder Ausschluss im Rahmen des Vorgangs. Diese Argumente werden jedoch für SQL Server-Datenquellen nicht unterstützt.

### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>Eingeschränkte Unterstützung für SQL-Datentypen in sp\_ausführen\_externen\_Skript

Nicht alle Datentypen, die in SQL unterstützt werden, können in r verwendet werden Dieses Problem zu umgehen, sollten Sie den nicht unterstützten Datentyp in einen unterstützten Datentyp umwandeln, vor der Übergabe an sp\_ausführen\_externen\_Skript.

Weitere Informationen finden Sie unter [R-Bibliotheken und Datentypen](r/r-libraries-and-data-types.md).

### <a name="possible-string-corruption"></a>Mögliche Zeichenfolgenbeschädigung

Alle Roundtrips von Zeichenfolgen von [!INCLUDE[tsql](../includes/tsql-md.md)] in R und anschließend [!INCLUDE[tsql](../includes/tsql-md.md)] erneut können zu Beschädigungen führen. Dies liegt daran, verwendeten in R und in unterschiedliche Codierungen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], sowie die verschiedenen Sortierungen und Sprachen, die in R unterstützt werden und [!INCLUDE[tsql](../includes/tsql-md.md)]. Zeichenfolgen mit einer Nicht-ASCII-Codierung werden möglicherweise nicht ordnungsgemäß verarbeitet.

Beim Senden von Zeichenfolgendaten an R konvertieren sie nach Möglichkeit in eine ASCII-Darstellung.

Diese Einschränkung gilt für Daten, die auch zwischen SQL Server und Python übergeben. Mehrbytezeichen sollte als UTF-8 übergeben und als Unicode gespeichert werden.

### <a name="only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>Nur ein Wert vom Typ `raw` zurückgegeben werden `sp_execute_external_script`

Bei einem binären Datentyp (der R **unformatierten** -Datentyp) von R zurückgegeben wird, muss der Wert im ausgabedatenrahmen entsprechen gesendet werden.

Mit Daten anderen Datentypen als **unformatierten**, Sie können Parameterwerte zusammen mit den Ergebnissen der gespeicherten Prozedur zurückgeben, indem Sie das OUTPUT-Schlüsselwort hinzufügen. Weitere Informationen finden Sie unter [Parameter](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters).

Wenn Sie mehrere ausgaberesultsets verwenden, die Werte des Typs einschließen möchten **unformatierten**, eine mögliche problemumgehung besteht, mehrere Aufrufe der gespeicherten Prozedur zu erledigen, oder senden Sie das Ergebnis wird wieder auf [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] unter Verwendung von ODBC.

### <a name="loss-of-precision"></a>Genauigkeitsverlust

Da [!INCLUDE[tsql](../includes/tsql-md.md)] und R unterstützen verschiedene Datentypen, numerische Datentypen Genauigkeitsverlust können beeinträchtigt werden, während der Konvertierung.

Weitere Informationen zu impliziten Datentyp konvertieren, finden Sie unter [R-Bibliotheken und Datentypen](r/r-libraries-and-data-types.md).

### <a name="variable-scoping-error-when-you-use-the-transformfunc-parameter"></a>Bereichsdefinition Fehler, wenn Sie den Parameter "transformfunc" Verwenden von Variablen

Zum Transformieren von Daten beim Erstellen von Modellen, übergeben Sie eine *"transformfunc"* Argument in einer Funktion wie z. B. `rxLinmod` oder `rxLogit`. Allerdings können Aufrufe geschachtelter Funktionen zu Bereichsdefinition von Fehlern in der SQL Server-computekontext führen, selbst wenn die Aufrufe im lokalen rechenkontext ordnungsgemäß.

> *Das Stichprobendataset für die Analyse wurde keine Variablen*

Nehmen wir beispielsweise an, dass Sie zwei Funktionen definiert haben `f` und `g`, in Ihrer lokalen globalen Umgebung und `g` Aufrufe `f`. Bei verteilten oder Remoteaufrufen unter Verwendung `g`, den Aufruf von `g` zu diesem Fehler fehlschlagen, da `f` kann nicht gefunden werden, auch wenn Sie beide erfolgreich abgeschlossen wurden `f` und `g` an den Remoteaufruf.

Wenn dieses Problem auftritt, können Sie es umgehen, indem Sie die Definition von `f` innerhalb der Definition von `g`an einer Stelle einbetten, vor der `g` normalerweise `f`aufrufen würde.

Beispiel:

```r
f <- function(x) { 2*x * 3 }
g <- function(y) {
              a <- 10 * y
               f(a)
}
```

Um den Fehler zu vermeiden, Schreiben Sie die Definition wie folgt:

```r
g <- function(y){
              f <- function(x) { 2*x +3}
              a <- 10 * y
              f(a)
}
```

### <a name="data-import-and-manipulation-using-revoscaler"></a>Importieren und Bearbeiten von Daten mithilfe von RevoScaleR

Wenn **Varchar** Spalten aus einer Datenbank gelesen werden Leerzeichen werden entfernt. Um dies zu verhindern, schließen Sie Zeichenfolgen in Zeichen ein, die keine Leerzeichen sind.

Wenn Funktionen wie `rxDataStep` werden verwendet, um Tabellen zu erstellen, die über **Varchar** Spalten, die Spaltenbreite wird basierend auf einer Stichprobe der Daten geschätzt. Wenn die Breite variieren kann, können alle Zeichenfolgen in einer gemeinsamen Länge aufgefüllt werden.

Das Verwenden einer Transformation zum Ändern des Datentyps einer Variablen wird nicht unterstützt, wenn wiederholte Aufrufe von `rxImport` oder `rxTextToXdf` zum Importieren und Anfügen von Zeilen verwendet werden, wobei mehrere Eingabedateien zu einer einzelnen XDF-Datei kombiniert werden.

### <a name="limited-support-for-rxexec"></a>Eingeschränkte Unterstützung für rxExec

In SQL Server 2016 wird die `rxExec` Funktion, sofern von der "revoscaler" Paket verwendet werden kann nur im Singlethread-Modus ist.

Parallelität für `rxExec` für mehrere Prozesse für eine zukünftige Version geplant ist.

### <a name="increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>Erhöhen Sie die maximale Parametergröße zur Unterstützung von rxGetVarInfo

Wenn Sie Datensätze mit extrem großen Anzahl von Variablen (z. B. über 40.000) verwenden, legen Sie die `max-ppsize` flag beim Starten von R mit Funktionen wie z. B. `rxGetVarInfo`. Das `max-ppsize` -Flag gibt die maximale Pointer Protection Stack-Größe an.

Wenn Sie die R-Konsole (z. B., "RGui.exe" oder "RTerm.exe") verwenden, legen Sie den Wert der _Max-Ppsize_ auf 500000, indem Sie Folgendes eingeben:

```R
R --max-ppsize=500000
```

### <a name="issues-with-the-rxdtree-function"></a>Probleme mit der RxDTree-Funktion

Die `rxDTree` -Funktion unterstützt derzeit keine formelinternen Transformationen. Insbesondere das Verwenden der `F()` -Syntax zum Erstellen von Faktoren bei laufendem Betrieb wird nicht unterstützt. Numerische Daten werden jedoch automatisch klassifiziert.

Geordnete Faktoren werden in allen RevoScaleR-Analysefunktionen außer `rxDTree`genauso wie Faktoren behandelt.

## <a name="python-code-execution-or-python-package-issues"></a>Python-code die Ausführung oder Python-Paket Probleme

Dieser Abschnitt enthält bekannte Probleme, die zum Ausführen von Python bei SQL Server als auch Probleme mit der Python-Pakete, die von Microsoft veröffentlichten sind spezifisch sind einschließlich [Revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) und [Microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

### <a name="call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>Vortrainierte Modell Aufruf fehlschlägt, wenn der Pfad zum Modell zu lang ist

Wenn Sie die vortrainierte Modelle in einer frühen Version von SQL Server-2017 installiert, möglicherweise der vollständige Pfad zur Modelldatei trainierten zu lang für Python zu lesen. Diese Einschränkung ist in einer späteren Dienstversion fest.

Es gibt mehrere mögliche problemumgehungen: 

+ Wählen Sie einen benutzerdefinierten Speicherort, bei der Installation die vortrainierte Modelle.
+ Wenn möglich, installieren Sie SQL Server-Instanz ein benutzerdefinierter Installationspfad mit einem kürzeren Pfad, z. B. C:\SQL\MSSQL14. MSSQLSERVER.
+ Verwenden Sie das Windows-Dienstprogramm [Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx) um einen festen Link zu erstellen, die Modelldatei zu einem kürzeren Pfad entspricht.
+ Aktualisieren Sie auf die neueste Dienstversion.

### <a name="error-when-saving-serialized-model-to-sql-server"></a>Fehler beim Speichern der serialisierten Modell mit SQL Server

Wenn Sie ein Modell mit einer Remoteinstanz von SQL Server übergeben, und versuchen, die binäres Modell mit Lesen der `rx_unserialize` -Funktion in [Revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), erhalten Sie möglicherweise die Fehlermeldung: 

> *NameError: Name 'Rx_unserialize_model' ist nicht definiert.*

Dieser Fehler wird ausgelöst, wenn Sie das Modell über eine aktuelle Version von die Serialisierungsfunktion gespeichert, aber SQL Server-Instanz, in dem Sie das Modell deserialisieren, die Serialisierung API nicht erkennt.

Um das Problem zu beheben, aktualisieren Sie die 2017 von SQL Server-Instanz, auf CU3 oder höher.

### <a name="failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>Fehler beim Initialisieren einer Variablen Varbinary verursacht einen Fehler in BxlServer

Wenn das Ausführen von Python-Code in SQL Server mit `sp_execute_external_script`, und der Code hat Variablen vom Typ varbinary(max), varchar(max) oder ähnliche Typen ausgegeben, die Variable initialisiert oder als Teil Ihres Skripts festgelegt werden muss. Andernfalls löst die Exchange-Komponente, BxlServer, Fehler und angehalten.

Diese Einschränkung wird in einer bevorstehenden Dienstversion behoben werden. Dieses Problem zu umgehen sicher, dass die Variable in der Python-Skript initialisiert wird. Jeder gültiger Wert kann verwendet werden, wie in den folgenden Beispielen:

```sql
declare @b varbinary(max);
exec sp_execute_external_script
  @language = N'Python'
  , @script = N'b = 0x0'
  , @params = N'@b varbinary(max) OUTPUT'
  , @b = @b OUTPUT;
go
```

```sql
declare @b varchar(30);
exec sp_execute_external_script
  @language = N'Python'
  , @script = N' b = ""  '
  , @params = N'@b varchar(30) OUTPUT'
  , @b = @b OUTPUT;
go
```

### <a name="telemetry-warning-on-successful-execution-of-python-code"></a>Telemetrie-Warnung bei erfolgreicher Ausführung des Python-code

Ab SQL Server 2017 CU2, möglicherweise die folgende Meldung angezeigt, selbst wenn andernfalls Python-Code erfolgreich ausgeführt wird:

> *Stderr-Meldung(en) aus dem externen Skript:*
> **~PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger*
> *SyntaxWarning: Telemetry_state ist vor der globale Deklaration verwendet*


Dieses Problem wurde in SQL Server 2017 kumulative Update 3 (CU3) behoben. 

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise und Microsoft R Open

Dieser Abschnitt enthält Probleme, die spezifisch für R-Konnektivität, Entwicklungs- und Leistungstools, die von Revolution Analytics bereitgestellt werden. Diese Tools wurden in früheren Versionen von Vorabversionen von bereitgestellten [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].

Im Allgemeinen wird empfohlen, dass Sie diese frühere Versionen deinstallieren und installieren die neueste Version von SQL Server oder Microsoft R Server.

### <a name="revolution-r-enterprise-is-not-supported"></a>Revolution R Enterprise wird nicht unterstützt.

Installieren von Revolution R Enterprise parallel mit einer Version von [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] wird nicht unterstützt.

Wenn Sie eine vorhandene Lizenzgruppe for Revolution R Enterprise haben, müssen Sie es ablegen, auf einem separaten Computer sowohl die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Instanz auch allen Arbeitsstationen, die Sie für die Verbindung verwenden möchten die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Instanz.

Einige Vorabversionen von [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] enthalten eine R-Entwicklungsumgebung für Windows, die von Revolution Analytics erstellt wurde. Dieses Tool wird nicht mehr bereitgestellt und wird nicht unterstützt.

Um die Kompatibilität mit [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)], es wird empfohlen, stattdessen Microsoft R-Client zu installieren. [R-Tools für Visual Studio](https://www.visualstudio.com/vs/rtvs/) und [Visual Studio Code](https://code.visualstudio.com/) unterstützt auch Microsoft R-Lösungen.

### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>Kompatibilitätsprobleme mit SQLite-ODBC-Treiber und RevoScaleR

Version 0.92 des SQLite-ODBC-Treiber ist nicht kompatibel mit RevoScaleR. Revisionen 0.88 0.91 und 0.93 und später sind bekanntermaßen kompatibel sein.

## <a name="see-also"></a>Siehe auch

[Neuerungen in SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)

[Problembehandlung bei Machine Learning in der SQL Server](machine-learning-troubleshooting-faq.md)
