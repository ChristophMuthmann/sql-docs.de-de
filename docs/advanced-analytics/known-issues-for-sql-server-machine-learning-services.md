---
title: "Bekannte Probleme für Machine Learning-Dienste | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/16/2017
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
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b7b9d53a87490e83f888b47b1cff87191b9693a8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="known-issues-for-machine-learning-services"></a>Bekannte Probleme für Machine Learning-Dienste

Dieses Thema beschreibt bekannte Probleme oder Einschränkungen mit den Machine learning-Komponenten, die als Option in SQL Server 2016 und SQL Server-2017 bereitgestellt werden.

Gilt für alle der folgenden, sofern nicht ausdrücklich angegeben:

+ SQL Server 2016

  - R Services (In-Database)
  - Microsoft R Server (eigenständig)

+ SQL Server 2017

  - Machine Learning-Dienste für R (In-Database)
  - Machine Learning-Dienste für Python (In-Database)
  - Machine Learning-Server (eigenständig)

## <a name="setup-and-configuration-issues"></a>Setup- und Konfigurationsprobleme

Eine Beschreibung des verarbeitet und häufige Fragen im Zusammenhang mit der ersten Installation und Konfiguration sind hier aufgeführt: [Upgrade und Installation – häufig gestellte Fragen](r/upgrade-and-installation-faq-sql-server-r-services.md).

Außerdem finden Sie im Artikel Informationen zu Upgrades, parallele Installation und Installation des neuen R oder Python-Komponenten.

### <a name="unable-to-install-python-components-in-in-offline-installs-of-sql-server-2017"></a>Kann nicht in den offline-Installationen von SQL Server-2017 Python-Komponenten in installiert

Bei der Installation von SQL Server-2017 auf einem Computer ohne Internetzugriff möglicherweise nicht das Installationsprogramm die Seite anzuzeigen, die für den Speicherort der heruntergeladenen Python Komponenten angefordert; aus diesem Grund werden Sie damit die Machine Learning-Datenbankdienste-Funktion, aber nicht die Python-Komponenten zu installieren.

Dieses Problem wird in einer zukünftigen Version behoben werden. Dieses Problem zu umgehen können Sie vorübergehend den Zugriff auf das Internet für die Dauer der Installation aktivieren. Diese Einschränkung gilt nicht, r

**Gilt für:** 2017 von SQLServer mit Python

### <a name="install-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>Installieren des aktuellsten Service Release, um die Kompatibilität mit Microsoft R Client sicherzustellen

Wenn Sie die neueste Version von Microsoft R-Client installieren und verwenden, um R ausgeführt wird, auf SQL Server mit einem Remote-computekontext, Sie erhalten möglicherweise eine Fehlermeldung ähnlich der folgenden:

*Sie sind 9.x.x der Version des Microsoft-R-Clients auf Ihrem Computer ausführen, die nicht mit dem Microsoft R Server Version 8.x.x kompatibel ist. Laden Sie eine kompatible Version herunter und installieren Sie sie.*

SQL Server 2016 erforderlich, dass die R-Bibliotheken auf dem Client die R-Bibliotheken auf dem Server genau übereinstimmen. Dass die Einschränkung später als R-Server 9.0.1 für Versionen entfernt wurde. Wenn dieser Fehler auftritt, überprüfen Sie die Version der R-Bibliotheken verwendet werden, von Ihrem Client und der Server, nad bei Bedarf aktualisiert Serverversion den Client aus.

Die Version von R, die mit SQL Server R Services installierte wird aktualisiert, sobald eine SQL Server-Service-Version installiert ist. Um sicherzustellen, dass Sie immer die neuesten Versionen der R-Komponenten haben, sollten Sie daher alle Servicepacks installieren.

Für eine Kompatibilität mit Microsoft R Client 9.0.0 müssen Sie die Updates installieren, die in diesem [Support-Artikel](https://support.microsoft.com/kb/3210262)beschrieben werden.

Zur Vermeidung von Problemen mit R-Pakete können Sie auch die Version der R-Bibliotheken, die auf dem Server installiert sind, durch Ändern der moderne Lifecycle-Richtlinie, wie in beschrieben aktualisieren [in diesem Abschnitt](#bkmk_sqlbindr). Wenn Sie dies tun, wird die Version von R mit SQL Server installiert nach demselben Zeitplan aktualisiert, dass Updates für Microsoft R Server, um sicherzustellen, dass sowohl Client als auch Server immer die neuesten Versionen von Microsoft R. haben, können veröffentlicht werden

**Gilt für:** SQL Server 2016 R Services mit R-Server Version 9.0.0 oder früher

### <a name="bkmk_sqlbindr"></a>Inkompatible Version Warnung beim Herstellen einer älteren Version von SQL Server R Services von einem Client mit[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

Wenn Sie Microsoft R Server mithilfe des Setup-Assistenten für [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] oder mithilfe des neuen eigenständige Installationsprogramms für [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)auf einen Clientcomputer installiert haben und R-Code in einem Rechenkontext ausführen, der eine frühere Version von SQL Server R Services verwendet, wird möglicherweise eine Fehlermeldung wie die folgende ausgegeben:

*Sie führen Version 9.0.0 von Microsoft R Client auf Ihrem Computer aus. Diese ist nicht mit der Microsoft R Server-Version 8.0.3 kompatibel. Laden Sie eine kompatible Version herunter und installieren Sie sie.*

Das **SqlBindR.exe**-Tool wird in Microsoft R Server Version 9.0 bereitgestellt, um ein Upgrade von SQL Server-Instanzen auf die kompatible Version 9.0 zu unterstützen. Die Unterstützung für die Aktualisierung der R Services-Instanzen auf 9.0 wird in SQL Server als Teil eines bevorstehenden Service Release hinzugefügt werden. Versionen, die als für zukünftige Upgrades Kandidaten einschließen, SQL Server 2016 RTM CU3 + und + SP1 und SQL Server 2017 CTP-Version 1.1.

**Gilt für:** SQL Server 2016 R Services mit R-Server Version 9.0.0 oder früher

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>Setup für SQL Server 2016 Service Releases kann unter Umständen keine neueren R-Komponenten installieren

Wenn Sie ein kumulatives Update installieren oder ein Servicepack für SQL Server 2016 auf einem Computer installieren, der nicht mit dem Internet verbunden ist, zeigt der Setup-Assistent möglicherweise nicht die Aufforderung an, mit der Sie die R-Komponenten mithilfe heruntergeladener CAB-Dateien aktualisieren können. Dieses Problem tritt üblicherweise auf, wenn mehrere Komponenten zusammen mit dem Datenbankmodul installiert werden.

Dieses Problem zu umgehen, können Sie mithilfe der Befehlszeile und angeben die Dienstversion Installieren der */MRCACHEDIRECTORY* Argument wie in diesem Beispiel gezeigt die CU1-Updates installiert wird:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

Um die neuesten Installationsprogramme zu erhalten, finden Sie unter [Machine Learning-Komponenten ohne Internetzugang installieren](r/installing-ml-components-without-internet-access.md).

**Gilt für:** SQL Server 2016 R Services mit R-Server Version 9.0.0 oder früher

### <a name="launchpad-services-fails-to-start-if-version-is-different-than-r-version"></a>Launchpad-Dienste werden nicht gestartet, wenn die Version von der R-Version abweicht

Wenn Sie R Services separat vom Datenbankmodul installieren, und die Buildversionen unterschiedlich sind, sehen Sie möglicherweise dieser Fehler im Systemereignisprotokoll: _SQL Server Launchpad-Dienst konnte wegen des folgenden Fehlers nicht gestartet: der Dienst reagiert nicht Antworten Sie auf die Start- oder Anforderung rechtzeitig verarbeitet._

Dieser Fehler tritt möglicherweise auf, wenn Sie das Datenbankmodul mithilfe der endgültigen Produktversion installieren, einen Patch anwenden, um das Datenbankmodul zu aktualisieren, und anschließend R Services mithilfe der endgültigen Produktversion hinzufügen.

Um dieses Problem zu vermeiden, sollten Sie sicherstellen, dass alle Komponenten dieselbe Versionsnummer aufweisen. Wenn Sie eine Komponente aktualisieren, müssen Sie dasselbe Upgrade auf alle anderen installierten Komponenten anwenden.

Eine Liste der R-Versionsnummern, die für jede Version von SQL Server 2016 erforderlich sind, finden Sie unter [Installation von R-Komponenten ohne Internetzugang](r/installing-ml-components-without-internet-access.md).

### <a name="remote-compute-contexts-blocked-by-firewall-in-sql-server-instances-running-on-azure-virtual-machines"></a>Remoterechenkontexte werden in SQL Server-Instanzen, die auf virtuellen Computern in Azure ausgeführt werden, durch die Firewall blockiert

Falls Sie [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] auf einem virtuellen Computer in Azure installiert haben, können Sie Rechenkontexte, die die Verwendung des Arbeitsbereichs des virtuellen Computers erfordern, möglicherweise nicht verwenden. Der Grund ist, dass die Firewall auf Azure-VMs standardmäßig eine Regel enthält, die den Netzwerkzugriff für lokale Benutzerkonten für R blockiert.

Öffnen Sie zur Umgehung dieses Problems auf der Azure-VM **Windows-Firewall mit erweiterter Sicherheit**, wählen Sie **Ausgehende Regeln**aus, und deaktivieren Sie die folgende Regel: „Netzwerkzugriff für lokale R-Benutzerkonten in der SQL Server-Instanz MSSQLSERVER blockieren“.

### <a name="implied-authentication-in-sqlexpress"></a>Implizite Authentifizierung in SQLEXPRESS

Beim Ausführen von R-Aufträgen auf einer Data Science-Remotearbeitsstation mithilfe der integrierten Windows-Authentifizierung verwendet SQL Server die *implizite Authentifizierung* , um lokale ODBC-Aufrufe zu generieren, die das Skript möglicherweise benötigt. Im RTM-Build der SQL Server Express Edition funktionierte diese Funktion jedoch nicht.

Um das Problem zu beheben, empfehlen wir die Aktualisierung auf ein neueres Service Release.

Wenn ein Upgrade nicht möglich ist, können Sie eine SQL-Anmeldung verwenden, um R-Remoteaufträge auszuführen, die unter Umständen eingebettete ODBC-Aufrufe benötigen.

**Gilt für:** SQL Server 2016-R Services Express Edition

### <a name="performance-limits-when-r-libraries-are-called-from-standalone-r-tools"></a>Leistung beschränkt, wenn R-Bibliotheken von eigenständigen R-Tools aufgerufen werden

Es ist möglich, rufen Sie die R-Tools und Bibliotheken, die von einer externen R-Anwendung, z. B. "rgui.exe" für SQL Server R Services installiert sind. Dies kann hilfreich sein, wenn Sie neue Pakete installieren oder Ausführen von ad-hoc-Tests auf sehr kurze Codebeispiele.

Bedenken Sie jedoch, dass außerhalb von SQL Server, Leistung beschränkt sein. Z. B., auch wenn Sie die Enterprise Edition von SQL Server erworben haben, wird R im Singlethread-Modus ausgeführt, wenn Sie R-Code mit externen Tools ausführen. Leistung überlegen, wenn Sie R-Code ausführen, indem ein SQL Server-Verbindung initiiert, und Verwenden von werden [Sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), der R-Bibliotheken für Sie aufgerufen.

+ Vermeiden Sie es, die von SQL Server verwendeten R-Bibliotheken mit externen R-Tools aufzurufen.
+ Wenn Sie eine umfangreiche R-Code auf dem SQL Server-Computer ausgeführt werden, ohne die Verwendung von SQLServer müssen, installieren Sie eine separate Instanz des R, z. B. Microsoft R-Client, und stellen Sie sicher, dass Ihre R-Entwicklungstools in der neuen Bibliothek verweisen.

Weitere Informationen finden Sie unter [Erstellen eines eigenständigen R-Servers](r/create-a-standalone-r-server.md).

### <a name="r-script-throttled-due-to-resource-governance-default-values"></a>R-Skript aufgrund der Ressource Governance-Standardwerte gedrosselt

In Enterprise Edition können Sie Ressourcenpools verwenden, um externe Skriptprozesse zu verwalten. In einigen frühen Releasebuilds wurde der maximale Arbeitsspeicher, der an die R-Prozesse zugeordnet werden kann 20 %. Wenn der Server über 32 GB RAM-Speicher verfügte, konnten die ausführbaren R-Dateien (RTerm.exe und BxlServer.exe) in einer einzelnen Anforderung maximal 6,4 GB verwenden.

Wenn Sie Ressourceneinschränkungen feststellen, sollten Sie den aktuellen Standardwert überprüfen. Sollten 20 % nicht ausreichend sein, finden Sie in der Dokumentation für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Informationen, wie Sie diesen Wert ändern können.

**Gilt für:** SQL Server 2016-R-Services, Enterprise Edition

## <a name="r-code-execution-and-package-or-function-issues"></a>Ausführung von R-Code und -Paket oder Funktion Probleme

Dieser Abschnitt enthält bekannte Probleme, die zum Ausführen von R bei SQL Server beziehen, sowie einige Probleme im Zusammenhang mit der R-Bibliotheken und Tools von Microsoft, einschließlich "revoscaler" veröffentlicht.

Weitere bekannte Probleme, die R-Lösungen beeinträchtigen können, finden Sie unter der Website Microsoft R Server: [bekannte Probleme mit Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-known-issues)

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>Einschränkungen der Prozessoraffinität für R-Aufträge

In der ersten Version Build von SQL Server 2016 konnte die Prozessoraffinität nur für CPUs in der ersten k-Gruppe festgelegt werden. Wenn es sich bei dem Server um einen 2-Socket-Computer mit zwei k-Gruppen handelt, werden beispielsweise nur Prozessoren der ersten k-Gruppe für die R-Prozesse verwendet. Dieselbe Einschränkung gilt beim Konfigurieren der Ressourcenkontrolle für R-Skriptaufträge.

Dieses Problem wurde in SQL Server 2016 Service Pack 1 behoben.

**Gilt für:** SQL Server 2016 R Services-RTM-Version

### <a name="changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>Änderungen an Spaltentypen nicht möglich, wenn Daten in SQL Server-Rechenkontext gelesen werden

Wenn der Rechenkontext auf die SQL Server-Instanz festgelegt ist, können Sie das Argument _ColClasses_ (oder andere ähnliche Argumente) nicht verwenden, um den Datentyp von Spalten in Ihrem R-Code zu ändern.

Die folgende Anweisung würde beispielsweise zu einem Fehler würden, wenn die Spalte CRSDepTimeStr keine Ganzzahl ist:

~~~~
data <- RxSqlServerData(sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall",
                                connectionString = connectionString,
                                colClasses = c(CRSDepTimeStr = "integer"))
~~~~

Dieses Problem wird in einer künftigen Version behoben werden.

Um dieses Problem zu umgehen, können Sie die SQL-Abfrage so umschreiben, dass sie CAST oder CONVERT verwendet, um die Daten R mit dem richtigen Datentyp vorzulegen. Generell ist es hinsichtlich der Leistung besser, unter Verwendung von SQL mit Daten zu arbeiten, anstatt Daten im R-Code zu ändern.

**Gilt für:** SQL Server 2016 R Services

### <a name="avoid-clearing-workspaces-when-executing-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>Löschen von Arbeitsbereichen vermeiden, wenn R-Code in einem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Rechenkontext ausgeführt wird

Wenn Sie den R-Befehl verwenden, um Objekte aus Ihrem Arbeitsbereich zu entfernen, während R-Code in einem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Rechenkontext ausgeführt wird, oder wenn Sie den Arbeitsbereich im Rahmen eines R-Skripts löschen, das mit [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)aufgerufen wird, erhalten Sie möglicherweise die folgende Fehlermeldung: *Arbeitsbereichsobjekt 'RevoScriptConnection' wurde nicht gefunden*.

`revoScriptConnection` ist ein Objekt im R-Arbeitsbereich, das Informationen über eine R-Sitzung enthält, die aus [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]aufgerufen wird. Wenn Ihr R-Code jedoch einen Befehl zum Löschen des Arbeitsbereichs enthält (wie z.B. `rm(list=ls()))`), werden alle Informationen über die Sitzung und andere Objekte im R-Arbeitsbereich ebenfalls gelöscht.

Um dieses Problem zu umgehen, sollten Sie willkürliches Löschen von Variablen und anderen Objekten während der Ausführung von R in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]vermeiden. Das Löschen des Arbeitsbereichs ist bei der Arbeit auf der R-Konsole zwar üblich, kann aber zu unerwarteten Ergebnissen führen.

+ Um bestimmte Variablen zu löschen, verwenden Sie die Funktion *remove* von R: `remove('name1', 'name2', ...)`.
+ Wenn mehrere zu löschende Variablen vorhanden sind, speichern Sie die Namen temporärer Variablen in einer Liste und führen eine regelmäßige automatische Speicherbereinigung durch.

### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>Einschränkungen von Daten, die als Eingabe für ein R-Skript bereitgestellt werden können

Sie können die folgenden Typen von Abfrageergebnissen nicht in einem R-Skript verwenden:

- Daten aus einer [!INCLUDE[tsql](../includes/tsql-md.md)] -Abfrage, die auf „AlwaysEncrypted“-Spalten verweist.
  
- Daten aus einer [!INCLUDE[tsql](../includes/tsql-md.md)] -Abfrage, die auf maskierte Spalten verweist.
  
     Wenn Sie maskierte Daten in einem R-Skript verwenden müssen, ist eine mögliche Problemumgehung das Erstellen einer Kopie der Daten in einer temporären Tabelle und anschließende Verwenden dieser Daten.

### <a name="arguments-varstokeep-and-varstodrop-not-supported-for-sql-server-data-sources"></a>Argumente *VarsToKeep* und *VarsToDrop* für SQL Server-Datenquellen nicht unterstützt.

Wenn Sie die RxDataStep-Funktion verwenden, um die Ergebnisse in eine Tabelle zu schreiben, verwenden die *VarsToKeep* und *VarsToDrop* ist eine praktische Möglichkeit der Angabe der Spalten ein-oder Ausschluss im Rahmen des Vorgangs. Diese Argumente werden derzeit nicht für SQL Server-Datenquellen unterstützt.

Diese Einschränkung wird in einer späteren Version entfernt.

### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>Eingeschränkte Unterstützung für SQL-Datentypen in`sp_execute_external_script`

Nicht alle Datentypen, die in SQL unterstützt werden, können in R verwendet werden. Um dieses Problem zu umgehen, sollten Sie es in Erwägung ziehen, den nicht unterstützten Datentyp in einen unterstützten Datentypen umzuwandeln, bevor die Daten an sp_execute_external_script übergeben werden.

Weitere Informationen finden Sie unter [R-Bibliotheken und Datentypen](r/r-libraries-and-data-types.md).

### <a name="possible-string-corruption"></a>Mögliche Zeichenfolgenbeschädigung

Roundtrips von Zeichenfolgen von [!INCLUDE[tsql](../includes/tsql-md.md)] zu R und anschließend zurück zu [!INCLUDE[tsql](../includes/tsql-md.md)] können zu Beschädigungen führen. Grund sind die verschiedenen Codierungen, die in R und [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]verwendet werden, sowie die unterschiedlichen Sortierungen und unterstützten Sprachen, die von R und [!INCLUDE[tsql](../includes/tsql-md.md)]unterstützt werden. Zeichenfolgen mit einer Nicht-ASCII-Codierung werden möglicherweise nicht ordnungsgemäß verarbeitet.

Beim Senden von Zeichenfolgendaten an R konvertieren Sie diese nach Möglichkeit in eine ASCII-Darstellung.

### <a name="only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>Nur ein Wert vom Typ `raw` zurückgegeben werden`sp_execute_external_script`

Wenn ein binärer Datentyp (der R-Datentyp **raw** ) von R zurückgegeben wird, muss der Wert dem Wert im Ausgabedatenrahmen entsprechen.

Unterstützung für mehrere **raw** -Ausgaben werden in künftigen Versionen hinzugefügt.

Eine mögliche Problemumgehung, falls mehrere Ausgaberesultsets gewünscht sind, ist das mehrfache Aufrufen der gespeicherten Prozedur und Senden der Resultsets zurück an [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mithilfe von ODBC.

Beachten Sie, dass Sie Parameterwerte zusammen mit den Ergebnissen der gespeicherten Prozedur zurückgeben können, indem Sie das Schlüsselwort OUTPUT hinzufügen. Weitere Informationen finden Sie unter [Zurückgeben von Daten mithilfe von OUTPUT-Parametern](https://technet.microsoft.com/library/ms187004.aspx).

### <a name="loss-of-precision"></a>Genauigkeitsverlust

[!INCLUDE[tsql](../includes/tsql-md.md)] und R unterstützen unterschiedliche Datentypen. Aus diesem Grund kann es bei der Konvertierung numerischer Datentypen zu einem Genauigkeitsverlust kommen.

Weitere Informationen zur impliziten Datentypkonvertierung finden Sie unter [Working with R Data Types](r/r-libraries-and-data-types.md).

### <a name="variable-scoping-error-the-sample-data-set-for-the-analysis-has-no-variables-when-using-the-transformfunc-parameter"></a>Fehler bei der Bereichsdefinition von Variablen „Der Beispieldatensatz für die Analyse enthält keine Variablen“ bei Verwenden des „transformFunc“-Parameters.

Sie können ein *transfodermFunc* -Argument in einer Funktion wie `rxLinmod` oder `rxLogit` to transfoderm the data while modelling. Allerdings können Aufrufe geschachtelter Funktionen im SQL Server-Rechenkontext zu Fehlern bei der Bereichsdefinition führen, selbst wenn die Aufrufe im lokalen Rechenkontext ordnungsgemäß funktionieren.

Angenommen, Sie haben die beiden Funktionen `f` und `g` in Ihrer lokalen globalen Umgebung definiert, und `g` ruft `f`auf. Bei verteilten oder Remoteaufrufen unter Verwendung von `g`kann der Aufruf von `g` misslingen, da `f` nicht gefunden werden kann, selbst wenn Sie `f` und `g` an den Remoteaufruf übergeben haben.

Wenn dieses Problem auftritt, können Sie es umgehen, indem Sie die Definition von `f` innerhalb der Definition von `g`an einer Stelle einbetten, vor der `g` normalerweise `f`aufrufen würde.

Beispiel:

```  
f <- function(x) { 2*x + 3 }  
g <- function(y) {   
              a <- 10 * y  
               f(a)  
}  
  
```  


Um den Fehler zu vermeiden, Schreiben Sie wie folgt aus:

```  
g <- function(y){  
              f <- function(x) { 2*x +3}  
              a <- 10 * y  
              f(a)  
}  
  
```  

### <a name="data-import-and-manipulation-using-revoscaler"></a>Importieren und Bearbeiten von Daten mithilfe von RevoScaleR

Beim Lesen von **varchar** -Spalten aus einer Datenbank werden Leerzeichen abgeschnitten. Um dies zu verhindern, schließen Sie Zeichenfolgen in Zeichen ein, die keine Leerzeichen sind.

Wenn Sie Funktionen wie `rxDataStep` zum Erstellen von Tabellen mit **varchar** -Spalten nutzen, wird die Spaltenbreite basierend auf einer Stichprobe der Daten geschätzt. Wenn die Breite variieren kann, kann es notwendig sein, alle Zeichenfolgen so aufzufüllen, dass ihre Länge gleich ist.

Das Verwenden einer Transformation zum Ändern des Datentyps einer Variablen wird nicht unterstützt, wenn wiederholte Aufrufe von `rxImport` oder `rxTextToXdf` zum Importieren und Anfügen von Zeilen verwendet werden, wobei mehrere Eingabedateien zu einer einzelnen XDF-Datei kombiniert werden.

### <a name="limited-support-for-rxexec"></a>Eingeschränkte Unterstützung für rxExec

In SQL Server 2016 wird die `rxExec` durch die "revoscaler"-Paket bereitgestellte Funktion kann nur im Singlethread-Modus verwendet werden.

Parallelität für `rxExec` über mehrere Prozesse wird in einer künftigen Version hinzugefügt werden.

### <a name="increase-maximum-parameter-size-to-support-rxgetvarinfo"></a>Erhöhen der maximale Parametergröße zur Unterstützung von rxGetVarInfo

Wenn Sie Datensätze mit einer sehr großen Anzahl von Variablen (z. B. über 40.000) verwenden, legen Sie das `max-ppsize` -Flag beim Starten von R fest, um Funktionen wie z. B. `rxGetVarInfo`zu verwenden.  Das `max-ppsize` -Flag gibt die maximale Pointer Protection Stack-Größe an.

Wenn Sie die R-Konsole verwenden (z. B. in „rgui.exe“ oder „rterm.exe“), können Sie den Wert von „max-ppsize“ auf 500.000 festlegen, indem Sie Folgendes eingeben:

```  
R --max-ppsize=500000  
```  
  
Bei Verwendung der [!INCLUDE[rsql_developr](../includes/rsql-developr-md.md)] -Umgebung, können Sie das `max-ppsize` -Flag festlegen, indem Sie diesen Aufruf an die ausführbare RevoIDE-Datei richten:

```  
RevoIDE.exe /RCommandLine --max-ppsize=500000  
```  

### <a name="issues-with-the-rxdtree-function"></a>Probleme mit der RxDTree-Funktion

Die `rxDTree` -Funktion unterstützt derzeit keine formelinternen Transformationen. Insbesondere das Verwenden der `F()` -Syntax zum Erstellen von Faktoren bei laufendem Betrieb wird nicht unterstützt. Numerische Daten werden jedoch automatisch klassifiziert.

Geordnete Faktoren werden in allen RevoScaleR-Analysefunktionen außer `rxDTree`genauso wie Faktoren behandelt.

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise und Microsoft R Open

In diesem Abschnitt werden Probleme aufgeführt, die speziell von Revolution Analytics bereitgestellte Konnektivitäts-, Entwicklungs- und Leistungstools für R betreffen. Diese Tools wurden in früheren Vorabversionen von  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]bereitgestellt. 

Im Allgemeinen wird empfohlen, dass Sie diese frühere Versionen deinstallieren und installieren die neueste Version von SQL Server oder Microsoft R Server.

### <a name="running-side-by-side-versions-of-revolution-r-enterprise"></a>Paralleles Ausführen verschiedener Versionen von Revolution R Enterprise

Das parallele Installieren von Revolution R Enterprise mit einer beliebigen Version von [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] wird nicht unterstützt.

Wenn Sie eine Lizenz für eine andere Version von Revolution R Enterprise haben, müssen Sie diese auf einem Computer verwenden, der sowohl von der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz als auch allen Arbeitsstationen getrennt ist, über die Sie eine Verbindung mit der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Instanz herstellen möchten.

### <a name="use-of-r-productivity-environment-not-supported"></a>Verwendung von R-Produktivitätsumgebung nicht unterstützt.

Einige Vorabversionen von [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] enthalten eine R-Entwicklungsumgebung für Windows, die von Revolution Analytics erstellt wurde. Dieses Tool wird nicht mehr bereitgestellt und wird nicht unterstützt.

Um die Kompatibilität mit [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)], es wird dringend empfohlen, Microsoft R-Client oder Microsoft R Server anstelle von Revolution Analytics-Tools zu installieren. [R-Tools für Visual Studio](https://www.visualstudio.com/vs/rtvs/) ist ein weiterer empfohlener Client, der Microsoft R-Lösungen unterstützt.

### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>Kompatibilitätsprobleme mit SQLite-ODBC-Treiber und RevoScaleR

Version 0.92 des SQLite-ODBC-Treibers ist nicht kompatibel mit RevoScaleR. Die Revisionen 0.88 0.91 und 0.93 und später sind bekanntermaßen kompatibel.

## <a name="see-also"></a>Siehe auch

[Neues in SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)


