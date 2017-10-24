---
title: Bekannte Probleme in Machine Learning Services | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 10/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2b37a63a-5ff5-478e-bcc2-d13da3ac241c
caps.latest.revision: 53
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 63ad249e32f259eca850d5b872d940faa313750c
ms.contentlocale: de-de
ms.lasthandoff: 10/24/2017

---
# <a name="known-issues-in-machine-learning-services"></a>Bekannte Probleme in Machine Learning-Diensten

Dieser Artikel beschreibt bekannte Probleme oder Einschränkungen mit den Machine learning-Komponenten, die als Option in SQL Server 2016 und SQL Server-2017 bereitgestellt werden.

Die Informationen hier gilt für alle der folgenden, sofern nicht ausdrücklich angegeben:

* SQL Server 2016

  - R Services (In-Database)
  - Microsoft R Server (eigenständig)

* SQL Server 2017

  - Machine Learning-Dienste für R (In-Database)
  - Machine Learning-Dienste für Python (In-Database)
  - Machine Learning-Server (eigenständig)

## <a name="setup-and-configuration-issues"></a>Setup- und Konfigurationsprobleme

Eine Beschreibung der Prozesse und häufig gestellte Fragen, die auf der ersten Installation und Konfiguration beziehen, finden Sie unter [häufig gestellte Fragen zu Upgrade und Installation](r/upgrade-and-installation-faq-sql-server-r-services.md). Es enthält Informationen zu Upgrades, parallele Installation und Installation des neuen R oder Python-Komponenten.

### <a name="unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>Es können Python-Komponenten in offline-Installationen von SQL Server 2017 CTP 2.0 oder höher installiert

Wenn Sie eine Vorabversion von SQL Server-2017 auf einem Computer ohne Internetzugang installieren, kann das Installationsprogramm auf der Seite angezeigt, die für den Speicherort der heruntergeladenen Python Komponenten fordert fehl. In solch einem Fall können Sie die Machine Learning-Datenbankdienste-Funktion, aber nicht die Python-Komponenten installieren.

Dieses Problem wird in der endgültigen Produktversion behoben. Wenn dieses, dieses Problem zu umgehen Problem, können Sie Zugriff auf das Internet vorübergehend für die Dauer der Installation aktivieren. Diese Einschränkung gilt nicht, r

**Gilt für:** 2017 von SQLServer mit Python

### <a name="install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>Installieren Sie das neueste Service Release, um die Kompatibilität mit Microsoft R Client sicherzustellen

Wenn Sie die neueste Version von Microsoft R-Client installieren und sie zum Ausführen von R auf SQL Server in einem remote-computekontext verwenden, erhalten Sie möglicherweise einen Fehler wie folgt:

>*Auf dem Computer, die mit Microsoft R Server Version 8.x.x nicht kompatibel ist, werden Sie 9.x.x der Version des Microsoft-R-Client ausgeführt. Laden Sie eine kompatible Version herunter und installieren Sie sie.*

SQL Server 2016 erfordert, dass die R-Bibliotheken auf dem Client die R-Bibliotheken auf dem Server genau übereinstimmen. Die Einschränkung wurde für Versionen höher als R-Server 9.0.1 entfernt. Dieser Fehler auftritt, überprüfen Sie die Version der R-Bibliotheken, die von Ihrem Client und Server verwendet wird, und aktualisieren Sie bei Bedarf den Client entsprechend die Serverversion Sie.

Die Version von R, die mit SQL Server R Services installierte wird aktualisiert, sobald eine SQL Server-Service-Version installiert ist. Um sicherzustellen, dass Sie immer die neuesten Versionen der R-Komponenten haben, werden Sie alle Servicepacks zu installieren.

Um die Kompatibilität mit Microsoft R Client 9.0.0 sichergestellt ist, installieren Sie die Updates, die beschrieben werden in diesem [Support-Artikel](https://support.microsoft.com/kb/3210262).

Zur Vermeidung von Problemen mit R-Pakete können Sie auch die Version der R-Bibliotheken, die auf dem Server installiert sind, indem Sie in der modernen Lifecycle-Richtlinie, die in beschriebenen ändern aktualisieren [im nächsten Abschnitt](#bkmk_sqlbindr). Wenn Sie dies tun, wird die Version von R, die mit SQL Server installiert wird nach demselben Zeitplan aktualisiert, dass Updates für Microsoft R Server, der sicherstellt veröffentlicht werden, dass sowohl Client als auch Server immer die neuesten Versionen von Microsoft R. haben

**Gilt für:** SQL Server 2016 R Services mit R-Server Version 9.0.0 oder früher

### <a name="bkmk_sqlbindr"></a>Inkompatible Version Warnung, wenn Sie mit einer älteren Version von SQL Server R Services von einem Client mit verbinden[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

Wenn Sie R-Code in eine SQL Server 2016-computekontext ausführen und eine der beiden folgenden Anweisungen ist "true", Sie möglicherweise eine Fehlermeldung wie die folgende angezeigt:
* R Server (eigenständig) wird auf einem Clientcomputer installiert, mithilfe des Setup-Assistenten für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].
* Sie installiert Microsoft R Server mithilfe der [separate Windows Installer](https://docs.microsoft.com/r-server/install/r-server-install-windows).

>*Sie führen Version 9.0.0 von Microsoft R Client auf Ihrem Computer aus. Diese ist nicht mit der Microsoft R Server-Version 8.0.3 kompatibel. Laden Sie eine kompatible Version herunter und installieren Sie sie.*

Sie können _Bindung_ in Microsoft R Server 9.0 und späteren Versionen die R-Komponenten in SQL Server 2016-Instanzen zu aktualisieren. Zum bestimmen, ob die Unterstützung für Upgrades steht für Ihre Version von R-Services finden Sie unter [Aktualisieren einer Instanz von R-Dienste, die mithilfe von SqlBindR.exe](/r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

**Gilt für:** SQL Server 2016 R Services mit R-Server Version 9.0.0 oder früher

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>Setup für SQL Server 2016 Service Releases kann unter Umständen keine neueren R-Komponenten installieren

Wenn Sie ein kumulatives Update installieren oder ein Servicepack für SQL Server 2016 auf einem Computer, der nicht mit dem Internet verbunden ist, möglicherweise nicht der Setup-Assistenten die Aufforderung angezeigt, in dem Sie die R-Komponenten zu aktualisieren, indem Sie die heruntergeladenen CAB-Dateien können. Dieser Fehler tritt normalerweise auf, wenn mehrere Komponenten zusammen mit dem Datenbankmodul installiert wurden.

Dieses Problem zu umgehen, können Sie mithilfe der Befehlszeile und angeben die Dienstversion Installieren der */MRCACHEDIRECTORY* Argument wie in diesem Beispiel gezeigt die CU1-Updates installiert wird:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

Um die neuesten Installationsprogramme zu erhalten, finden Sie unter [Machine Learning-Komponenten ohne Internetzugang installieren](r/installing-ml-components-without-internet-access.md).

**Gilt für:** SQL Server 2016 R Services mit R-Server Version 9.0.0 oder früher

### <a name="launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>Launchpad-Dienste nicht gestartet werden, wenn die Version der R-Version unterscheidet

Wenn Sie SQL Server R Services separat vom Datenbankmodul installieren, und die Buildversionen unterschiedlich sind, wird möglicherweise den folgenden Fehler im Systemereignisprotokoll angezeigt:

>_Der SQL Server Launchpad-Dienst konnte wegen des folgenden Fehlers nicht gestartet: der Dienst hat nicht auf die Start- oder Anforderung rechtzeitig reagiert._

Beispielsweise kann dieser Fehler auftreten, wenn Sie das Datenbankmodul installiert, mit der endgültigen Produktversion Anwenden eines Patches, um das Datenbankmodul zu aktualisieren und dann die R-Services-Funktion hinzufügen, indem Sie mit der endgültigen Produktversion.

Um dieses Problem zu vermeiden, sollten Sie sicherstellen, dass alle Komponenten dieselbe Versionsnummer aufweisen. Wenn Sie eine Komponente aktualisieren, müssen Sie dasselbe Upgrade auf alle anderen installierten Komponenten anwenden.

Um eine Liste der R-Versionsnummern anzuzeigen, die für jede Version von SQL Server 2016 erforderlich sind, finden Sie unter [Installieren von R-Komponenten ohne Internetzugang](r/installing-ml-components-without-internet-access.md).

### <a name="remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>Remote rechenkontexte werden durch eine Firewall in SQL Server-Instanzen blockiert, die auf virtuellen Azure-Computern ausgeführt werden

Wenn Sie installiert haben [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] auf einem Windows Azure-virtuellen Computer nicht können Sie möglicherweise rechenkontexte verwenden, die die Verwendung des Arbeitsbereichs des virtuellen Computers erfordern. Der Grund ist, dass standardmäßig die Firewall auf virtuellen Azure-Computern eine Regel enthält, dass der Netzwerkzugriff für lokale Benutzerkonten für R blockiert.

Öffnen Sie dieses Problem zu umgehen, auf der Azure-VM **Windows-Firewall mit erweiterter Sicherheit**Option **ausgehende Regeln**, und deaktivieren Sie die folgende Regel: **Netzwerkzugriff für lokale R-Benutzerkonten in blockieren SQL Server-Instanz MSSQLSERVER**. Sie können auch die Regel aktiviert lassen jedoch ändern Sie die Eigenschaft für die Sicherheit auf **zulassen bei sicheren Verbindungen**.

### <a name="implied-authentication-in-sqlexpress"></a>Implizite Authentifizierung in SQLEXPRESS

Wenn Sie R-Aufträge mithilfe der integrierten Windows-Authentifizierung über eine remote Data Science-Arbeitsstation ausführen, verwendet SQL Server *implizite Authentifizierung* alle lokalen ODBC-Aufrufe zu generieren, die unter Verwendung des Skripts erforderlich sein könnten. Im RTM-Build der SQL Server Express Edition funktionierte diese Funktion jedoch nicht.

Um das Problem zu beheben, empfehlen wir die Aktualisierung auf ein neueres Service Release.

Wenn ein Upgrade nicht möglich ist, können Sie eine SQL-Anmeldung verwenden, um R-Remoteaufträge auszuführen, die unter Umständen eingebettete ODBC-Aufrufe benötigen.

**Gilt für:** SQL Server 2016-R Services Express Edition

### <a name="performance-limits-when-r-libraries-are-called-from-other-r-tools"></a>Die Leistungsgrenze bei der R-Bibliotheken von anderen R-Tools aufgerufen werden

Es ist möglich, rufen Sie die R-Tools und Bibliotheken, die von einer externen R-Anwendung, z. B. "rgui.exe" für SQL Server installiert sind. Dieser Aufruf kann nützlich sein, wenn Sie neue Pakete installieren, oder beim Ausführen von ad-hoc-Tests auf sehr kurze Codebeispiele.

Bedenken Sie jedoch, dass außerhalb von SQL Server, die Leistung beschränkt werden kann. Beispielsweise, selbst wenn Sie die Enterprise Edition von SQL Server erworben haben, führt R im Singlethread-Modus beim Ausführen des R-Code mithilfe von externen Tools. Leistung sollte besser, wenn Sie R-Code ausführen, indem ein SQL Server-Verbindung initiiert, und Verwenden von [Sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), R-Bibliotheken für Sie aufruft.

* Vermeiden Sie das Aufrufen von R-Bibliotheken, die aus externen R-Tools von SQL Server verwendet werden.
* Wenn Sie eine umfangreiche R-Code auf dem SQL Server-Computer ausführen, ohne Verwendung von SQL Server müssen, installieren Sie eine separate Instanz des R, z. B. Microsoft R-Client, und stellen Sie sicher, dass Ihre R-Entwicklungstools in der neuen Bibliothek verweisen.

Weitere Informationen finden Sie unter [Erstellen eines eigenständigen R-Servers](r/create-a-standalone-r-server.md).

### <a name="the-r-script-is-throttled-due-to-resource-governance-default-values"></a>R-Skript wird aufgrund der Ressource Governance-Standardwerte eingeschränkt.

In Enterprise Edition können Sie Ressourcenpools verwenden, um externe Skriptprozesse zu verwalten. In einigen frühen Releasebuilds wurde der maximale Arbeitsspeicher, der an die R-Prozesse zugeordnet werden kann 20 Prozent. Daher wäre der Server über 32 GB RAM, konnte die ausführbaren Dateien R ("RTerm.exe" und "BxlServer.exe") maximal 6,4 GB in einer einzelnen Anforderung verwenden.

Wenn überprüfen Sie ressourceneinschränkungen auftreten, die aktuelle Standardeinstellung. Wenn 20 Prozent nicht ausreichend ist, finden Sie in der Dokumentation für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] zum Ändern dieses Werts.

**Gilt für:** SQL Server 2016-R-Services, Enterprise Edition

## <a name="r-code-execution-and-package-or-function-issues"></a>Ausführung von R-Code und Probleme Paket oder -Funktion

Dieser Abschnitt enthält bekannte Probleme, die zum Ausführen von R bei SQL Server beziehen, sowie einige Probleme mit der R-Bibliotheken und Tools, die von Microsoft, einschließlich "revoscaler" veröffentlicht werden.

Weitere bekannte Probleme, die R-Lösungen beeinträchtigen können, finden Sie unter der [Microsoft R Server Site](https://msdn.microsoft.com/microsoft-r/rserver-known-issues).

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>Einschränkungen der Prozessoraffinität für R-Aufträge

In der ersten Version Build von SQL Server 2016 konnte die Prozessoraffinität nur für CPUs in der ersten k-Gruppe festgelegt werden. Wenn der Server einen 2-Socket-Computer mit zwei k-Gruppen ist, werden z. B. nur Prozessoren aus der ersten k-Gruppe für die R-Prozesse verwendet. Die gleiche Einschränkung gilt beim Konfigurieren der Ressourcenkontrolle für R-Skript-Aufträge.

Dieses Problem wurde in SQL Server 2016 Service Pack 1 behoben. Es wird empfohlen, ein upgrade auf die neueste Dienstversion.

**Gilt für:** SQL Server 2016 R Services-RTM-Version

### <a name="changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>Änderungen an Spaltentypen nicht möglich, wenn Daten in SQL Server-Rechenkontext gelesen werden

Wenn der Rechenkontext auf die SQL Server-Instanz festgelegt ist, können Sie das Argument _ColClasses_ (oder andere ähnliche Argumente) nicht verwenden, um den Datentyp von Spalten in Ihrem R-Code zu ändern.

Die folgende Anweisung würde beispielsweise zu einem Fehler würden, wenn die Spalte CRSDepTimeStr keine Ganzzahl ist:

```r
data <- RxSqlServerData(sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall",
                                connectionString = connectionString,
                                colClasses = c(CRSDepTimeStr = "integer"))
```

Dieses Problem zu umgehen, können Sie die SQL-Abfrage zum Verwenden von CAST umschreiben oder konvertieren, und präsentieren der Daten an R mit den richtigen Datentyp. Leistung ist im Allgemeinen besser, wenn Sie mit Daten mithilfe von SQL anstatt durch das Ändern von Daten in der R-Code arbeiten.

**Gilt für:** SQL Server 2016 R Services

### <a name="limits-on-size-of-serialized-models"></a>Beschränkungen der Größe der serialisierten Modelle

Wenn Sie ein Modell in einer SQL Server-Tabelle speichern, müssen Sie Serialisieren des Modells und in einem binären Format zu speichern. Theoretisch ist die maximale Größe eines Modells, die mit dieser Methode gespeichert werden können, 2 GB sind, die die maximale Größe eines Varbinary-Spalten in SQL Server ist.

Wenn Sie größere Modelle verwenden müssen, sind die folgenden problemumgehungen verfügbar:

+ Verwenden der [MemCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress) Funktion in Basis R, um die Größe des Modells, die vor der Übergabe an SQL Server zu reduzieren. Diese Option wird empfohlen, wenn das Modell in der Nähe der 2 GB beschränkt ist.
+ Für größere Modelle, statt eine Varbinary-Spalte zum Speichern der Modelle verwenden, können Sie die [FileTable](..\relational-databases\blob\filetables-sql-server.md) in SQL Server bereitgestellte Funktion.

    Um FileTables verwenden zu können, müssen Sie eine Firewallausnahme hinzufügen, da in FileTables gespeicherte Daten von den Filestream-Dateisystem-Treiber in SQL Server verwaltet werden und die Standardregeln für die Firewall blockiert werden Netzwerkzugriff für die Datei. Weitere Informationen finden Sie unter [aktivieren erforderlichen Komponenten für FileTable](../relational-databases/blob/enable-the-prerequisites-for-filetable.md). 

    Nachdem Sie FileTable, um dem Modell, Schreiben Sie einen Pfad von SQL erhalten mithilfe der FileTable-API aktiviert haben, und klicken Sie dann das Modell für diesen Speicherort aus dem R-Code schreiben. Wenn Sie das Modell lesen müssen, Sie den Pfad von SQL und rufen Sie dann das Modell mit dem Pfad in Ihrem R-Skript. Weitere Informationen finden Sie unter [zugreifen auf FileTables Angebote-Datei-e/a-APIs](../relational-databases/blob/access-filetables-with-file-input-output-apis.md).

### <a name="avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>Zu vermeiden, deaktivieren Arbeitsbereiche, beim Ausführen von R-Code in einem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] computekontext

Wenn Sie den R-Befehl verwenden, um Ihrem Arbeitsbereich von Objekten zu löschen, während der Ausführung von R-Code in eine [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] computekontext, oder wenn Sie den Arbeitsbereich als Teil eines R-Skripts deaktivieren aufgerufen werden, mithilfe von [Sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), erhalten Sie möglicherweise dadurch Fehler: 

>*Arbeitsbereich "Objekt"RevoScriptConnection"nicht gefunden*

`revoScriptConnection` ist ein Objekt im R-Arbeitsbereich, das Informationen über eine R-Sitzung enthält, die aus [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]aufgerufen wird. Wenn Ihr R-Code jedoch einen Befehl zum Löschen des Arbeitsbereichs enthält (wie z.B. `rm(list=ls()))`), werden alle Informationen über die Sitzung und andere Objekte im R-Arbeitsbereich ebenfalls gelöscht.

Vermeiden Sie dieses Problem zu umgehen, willkürliche Löschen von Variablen und andere Objekte während der Ausführung von R sind [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Obwohl das Löschen des Arbeitsbereichs üblich ist, bei der Arbeit in der R-Konsole, haben sie unerwartete Ergebnisse liefern.

* Um bestimmte Variablen zu löschen, verwenden Sie das R *entfernen* Funktion: `remove('name1', 'name2', ...)`.
* Wenn mehrere zu löschende Variablen vorhanden sind, speichern Sie die Namen temporärer Variablen in einer Liste und führen eine regelmäßige automatische Speicherbereinigung durch.

### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>Einschränkungen von Daten, die als Eingabe für ein R-Skript bereitgestellt werden können

Sie können die folgenden Typen von Abfrageergebnissen nicht in einem R-Skript verwenden:

- Daten aus einer [!INCLUDE[tsql](../includes/tsql-md.md)] -Abfrage, die auf „AlwaysEncrypted“-Spalten verweist.
  
- Daten aus einer [!INCLUDE[tsql](../includes/tsql-md.md)] -Abfrage, die auf maskierte Spalten verweist.
  
     Wenn Sie maskierte Daten in einem R-Skript verwenden müssen, ist eine mögliche Problemumgehung das Erstellen einer Kopie der Daten in einer temporären Tabelle und anschließende Verwenden dieser Daten.

### <a name="arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>Argumente *VarsToKeep* und *VarsToDrop* werden für SQL Server-Datenquellen nicht unterstützt

Wenn Sie die RxDataStep-Funktion verwenden, um die Ergebnisse in eine Tabelle zu schreiben, verwenden die *VarsToKeep* und *VarsToDrop* ist eine praktische Möglichkeit der Angabe der Spalten ein-oder Ausschluss im Rahmen des Vorgangs. Diese Argumente werden jedoch für SQL Server-Datenquellen nicht unterstützt.

### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>Eingeschränkte Unterstützung für SQL-Datentypen in`sp_execute_external_script`

Nicht alle Datentypen, die in SQL unterstützt werden, können in R verwendet werden. Um dieses Problem zu umgehen, sollten Sie es in Erwägung ziehen, den nicht unterstützten Datentyp in einen unterstützten Datentypen umzuwandeln, bevor die Daten an sp_execute_external_script übergeben werden.

Weitere Informationen finden Sie unter [R-Bibliotheken und Datentypen](r/r-libraries-and-data-types.md).

### <a name="possible-string-corruption"></a>Mögliche Zeichenfolgenbeschädigung

Alle Roundtrips von Zeichenfolgen von [!INCLUDE[tsql](../includes/tsql-md.md)] in R und anschließend [!INCLUDE[tsql](../includes/tsql-md.md)] erneut können zu Beschädigungen führen. Dies liegt daran, verwendeten in R und in unterschiedliche Codierungen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], sowie die verschiedenen Sortierungen und Sprachen, die in R unterstützt werden und [!INCLUDE[tsql](../includes/tsql-md.md)]. Zeichenfolgen mit einer Nicht-ASCII-Codierung werden möglicherweise nicht ordnungsgemäß verarbeitet.

Beim Senden von Zeichenfolgendaten an R konvertieren sie nach Möglichkeit in eine ASCII-Darstellung.

Diese Einschränkung gilt für Daten, die auch zwischen SQL Server und Python übergeben. Mehrbytezeichen sollte als UTF-8 übergeben und als Unicode gespeichert werden.

### <a name="only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>Nur ein Wert vom Typ `raw` zurückgegeben werden`sp_execute_external_script`

Bei einem binären Datentyp (der R **unformatierten** -Datentyp) von R zurückgegeben wird, muss der Wert im ausgabedatenrahmen entsprechen gesendet werden.

Mit Daten anderen Datentypen als **unformatierten**, Sie können Parameterwerte zusammen mit den Ergebnissen der gespeicherten Prozedur zurückgeben, indem Sie einfach das OUTPUT-Schlüsselwort hinzufügen. Weitere Informationen finden Sie unter [Zurückgeben von Daten mithilfe von OUTPUT-Parameter](https://technet.microsoft.com/library/ms187004.aspx).

Wenn Sie mehrere ausgaberesultsets verwenden, die Werte des Typs einschließen möchten **unformatierten**, eine mögliche problemumgehung besteht, mehrere Aufrufe der gespeicherten Prozedur zu erledigen, oder senden Sie das Ergebnis wird wieder auf [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] unter Verwendung von ODBC.

### <a name="loss-of-precision"></a>Genauigkeitsverlust

Da [!INCLUDE[tsql](../includes/tsql-md.md)] und R unterstützen verschiedene Datentypen, numerische Datentypen Genauigkeitsverlust können beeinträchtigt werden, während der Konvertierung.

Weitere Informationen zu impliziten Datentyp konvertieren, finden Sie unter [R-Bibliotheken und Datentypen](r/r-libraries-and-data-types.md).

### <a name="variable-scoping-error-when-you-use-the-transformfunc-parameter-the-sample-data-set-for-the-analysis-has-no-variables"></a>Bereichsauswahl Fehler bei der Verwendung des Parameters "transformfunc" Variable: *der Beispieldatensatz für die Analyse wurde keine Variablen*

Zum Transformieren von Daten beim Erstellen von Modellen, übergeben Sie eine *"transformfunc"* Argument in einer Funktion wie z. B. `rxLinmod` oder `rxLogit`. Allerdings können Aufrufe geschachtelter Funktionen zu Bereichsdefinition von Fehlern in der SQL Server-computekontext führen, selbst wenn die Aufrufe im lokalen rechenkontext ordnungsgemäß.

Nehmen wir beispielsweise an, dass Sie zwei Funktionen definiert haben `f` und `g`, in Ihrer lokalen globalen Umgebung und `g` Aufrufe `f`. Bei verteilten oder Remoteaufrufen unter Verwendung von `g`kann der Aufruf von `g` misslingen, da `f` nicht gefunden werden kann, selbst wenn Sie `f` und `g` an den Remoteaufruf übergeben haben.

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

Wenn Sie die R-Konsole verwenden (z. B. in „rgui.exe“ oder „rterm.exe“), können Sie den Wert von „max-ppsize“ auf 500.000 festlegen, indem Sie Folgendes eingeben:

```r
R --max-ppsize=500000
```

Bei Verwendung der [!INCLUDE[rsql_developr](../includes/rsql-developr-md.md)] -Umgebung, die Sie festlegen können die `max-ppsize` Flag durch den folgenden Aufruf an die ausführbare RevoIDE-Datei:

```
RevoIDE.exe /RCommandLine --max-ppsize=500000  
```

### <a name="issues-with-the-rxdtree-function"></a>Probleme mit der RxDTree-Funktion

Die `rxDTree` -Funktion unterstützt derzeit keine formelinternen Transformationen. Insbesondere das Verwenden der `F()` -Syntax zum Erstellen von Faktoren bei laufendem Betrieb wird nicht unterstützt. Numerische Daten werden jedoch automatisch klassifiziert.

Geordnete Faktoren werden in allen RevoScaleR-Analysefunktionen außer `rxDTree`genauso wie Faktoren behandelt.

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise und Microsoft R Open

Dieser Abschnitt enthält Probleme, die spezifisch für R-Konnektivität, Entwicklungs- und Leistungstools, die von Revolution Analytics bereitgestellt werden. Diese Tools wurden in früheren Versionen von Vorabversionen von bereitgestellten [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].

Im Allgemeinen wird empfohlen, dass Sie diese frühere Versionen deinstallieren und installieren die neueste Version von SQL Server oder Microsoft R Server.

### <a name="running-side-by-side-versions-of-revolution-r-enterprise"></a>Seite-an-Seite-Versionen von Revolution R Enterprise ausführen

Installieren von Revolution R Enterprise parallel mit einer Version von [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] wird nicht unterstützt.

Wenn Sie eine Lizenz für eine andere Version von Revolution R Enterprise haben, müssen Sie diese auf einem Computer verwenden, der sowohl von der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz als auch allen Arbeitsstationen getrennt ist, über die Sie eine Verbindung mit der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz herstellen möchten.

### <a name="the-use-of-an-r-productivity-environment-is-not-supported"></a>Die Verwendung von einem R-produktivitätsumgebung wird nicht unterstützt.

Einige Vorabversionen von [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] enthalten eine R-Entwicklungsumgebung für Windows, die von Revolution Analytics erstellt wurde. Dieses Tool wird nicht mehr bereitgestellt, und es wird nicht unterstützt.

Um die Kompatibilität mit [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)], es wird dringend empfohlen, Microsoft R-Client oder Microsoft R Server anstelle von Revolution Analytics-Tools zu installieren. [R-Tools für Visual Studio](https://www.visualstudio.com/vs/rtvs/) und [Visual Studio Code](https://code.visualstudio.com/) unterstützt auch Microsoft R-Lösungen.

### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>Kompatibilitätsprobleme mit SQLite-ODBC-Treiber und RevoScaleR

Version 0.92 des SQLite-ODBC-Treiber ist nicht kompatibel mit RevoScaleR. Revisionen 0.88 0.91 und 0.93 und später sind bekanntermaßen kompatibel sein.

## <a name="python-code-execution-or-python-package-issues"></a>Python-code die Ausführung oder Python-Paket Probleme

Dieser Abschnitt enthält bekannte Probleme, die zum Ausführen von Python bei SQL Server als auch Probleme mit der Python-Pakete, die von Microsoft veröffentlichten sind spezifisch sind einschließlich [Revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) und [Microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).


## <a name="see-also"></a>Siehe auch

[Neuerungen in SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)

[Problembehandlung bei Machine Learning in der SQL Server](machine-learning-troubleshooting-faq.md)

