---
title: "Bekannte Probleme bei SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2b37a63a-5ff5-478e-bcc2-d13da3ac241c
caps.latest.revision: 52
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 49
---
# Bekannte Probleme bei SQL Server R Services
  Dieses Thema beschreibt Einschränkungen und Probleme von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] und den zugehörigen Komponenten in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].  
  
> [!NOTE]
> Weitere Probleme im Zusammenhang mit der Einrichtung und Konfiguration sind hier aufgeführt: [Häufig gestellte Fragen zu Upgrade und Installation](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md).  
  
## <a name="r-services-in-database"></a>R Services (In-Database)  
 In diesem Abschnitt werden Probleme beschrieben, die konkret die Funktion des Datenbankmoduls betreffen, welche die Integration von R unterstützt.  

### <a name="install-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>Installieren des aktuellsten Service Release, um die Kompatibilität mit Microsoft R Client sicherzustellen

Wenn Sie die neueste Version von Microsoft R Client installieren und anschließend verwenden, um R mittels eines fernen Rechenkontexts auf SQL Server zu verwenden, erhalten Sie möglicherweise die folgende Fehlermeldung:

*Sie führen Version 9.0.0 von Microsoft R Client auf Ihrem Computer aus. Diese ist nicht mit der Microsoft R Server-Version 8.0.3 kompatibel. Laden Sie eine kompatible Version herunter und installieren Sie sie.*

In der Regel wird die Version von R, die mit SQL Server R Services installiert ist, aktualisiert, wenn Service Releases veröffentlicht werden. Installieren Sie alle Servicepacks, um sicherzustellen, dass Sie stets über die aktuellsten Versionen von R-Komponenten verfügen. Für eine Kompatibilität mit Microsoft R Client 9.0.0 müssen Sie die Updates installieren, die in diesem [Support-Artikel](https://support.microsoft.com/kb/3210262) beschrieben werden. 
  
### <a name="new-license-agreement-for-r-components-required-for-unattended-installs"></a>Neue Lizenzvereinbarung für R-Komponenten für unbeaufsichtigte Installation erforderlich  
 Wenn Sie die Befehlszeile verwenden, um eine Instanz von SQL Server zu installieren, auf der [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] installiert ist, müssen Sie die Befehlszeile bearbeiten, damit sie den neuen Lizenzvereinbarungsparameter */IACCEPTROPENLICENSEAGREEMENT* verwendet. Wenn das ordnungsgemäße Argument nicht angegeben wird, kann das Setup von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] misslingen.  
  
### <a name="warning-of-incompatible-version-when-connecting-to-older-version-of-sql-server--r-services-from-a-client-using-includesssqlv14mdtokensqlv14sssqlv14mdmd"></a>Warnung vor einer inkompatiblen Version beim Herstellen einer Verbindung zu einer älteren Version von SQL Server R Services von einem Client, der [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] verwendet 

Wenn Sie Microsoft R Server mithilfe des Setup-Assistenten für [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] oder mithilfe des neuen eigenständige Installationsprogramms für [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows) auf einen Clientcomputer installiert haben und R-Code in einem Rechenkontext ausführen, der eine frühere Version von SQL Server R Services verwendet, wird möglicherweise eine Fehlermeldung wie die folgende ausgegeben:

*Sie führen Version 9.0.0 von Microsoft R Client auf Ihrem Computer aus. Diese ist nicht mit der Microsoft R Server-Version 8.0.3 kompatibel. Laden Sie eine kompatible Version herunter und installieren Sie sie.*

Das **SqlBindR.exe**-Tool wird in Microsoft R Server Version 9.0 bereitgestellt, um ein Upgrade von SQL Server-Instanzen auf die kompatible Version 9.0 zu unterstützen. Die Unterstützung für die Aktualisierung der R Services-Instanzen auf 9.0 wird in SQL Server als Teil eines bevorstehenden Service Release hinzugefügt werden. Zu den Versionen, die für eine zukünftige Aktualisierung in Frage kommen, gehören SQL Server 2016 RTM CU3+ und SP1+ sowie SQL Server vNext CTP 1.1. 

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>Setup für SQL Server 2016 Service Releases kann unter Umständen keine neueren R-Komponenten installieren

Wenn Sie ein kumulatives Update installieren oder ein Servicepack für SQL Server 2016 auf einem Computer installieren, der nicht mit dem Internet verbunden ist, zeigt der Setup-Assistent möglicherweise nicht die Aufforderung an, mit der Sie die R-Komponenten mithilfe heruntergeladener CAB-Dateien aktualisieren können. Dieses Problem tritt üblicherweise auf, wenn mehrere Komponenten zusammen mit dem Datenbankmodul installiert werden.
 
Um dieses Problem zu umgehen, können Sie das Service Release installieren, indem Sie die Befehlszeile verwenden und das Argument /MRCACHEDIRECTORY wie in diesem Beispiel für CU1 gezeigt verwenden: 

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

Informationen zum Herunterladen der aktuellsten CAB-Dateien finden Sie unter [Installation von R-Komponenten ohne Internetzugang](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md).

### <a name="windows-group-created-for-launchpad-must-have-an-account-in-the-sql-server-instance"></a>Für Launchpad erstellte Windows-Gruppe muss über ein Konto in der SQL Server-Instanz verfügen
 Bei der Installation von SQL Server R Services wird eine Windows-Benutzergruppe mit dem Standardnamen **SQLRUsers** erstellt, die vom Trusted Launchpad für das Ausführen von R-Aufträgen verwendet wird. Wenn Sie R-Aufträge von einem Remote-Client mithilfe der integrierten Windows-Authentifizierung ausführen müssen, müssen Sie dieser Windows Benutzergruppe die Berechtigung zur Anmeldung bei der SQL Server-Instanz erteilen, auf der R aktiviert ist.

In einer Umgebung, in der die Gruppe **SQLRUsers** nicht über diese Berechtigung verfügt, werden möglicherweise die folgenden Fehlermeldungen angezeigt:  
  
-   Wenn Sie versuchen, R-Skripts auszuführen:  
  
     *Laufzeit für 'R'-Skript kann nicht gestartet werden. Überprüfen Sie die Konfiguration der 'R'-Laufzeit.*  
  
     *Ein externer Skriptfehler ist aufgetreten. Laufzeit kann nicht gestartet werden.*  
  
-   Vom [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] -Dienst generierte Fehlermeldungen:  
  
     *Fehler beim Initialisieren des Startprogramms RLauncher.dll*  
  
     *Keine Startprogramm-DLLs registriert!*  
  
-   Sicherheitsprotokolle weisen darauf hin, dass das Konto NT SERVICE\MSSQLLAUNCHPAD sich nicht anmelden konnte.  
 
> [!NOTE]
> Wenn Sie R-Aufträge in SQL Server Management Studio mithilfe von gemeinsam genutztem Speicherbereich ausführen, tritt diese Einschränkung möglicherweise erst dann auf, wenn Ihr R-Auftrag einen eingebetteten ODBC-Aufruf verwendet. 
> 
> Diese Problemumgehung ist nicht erforderlich, wenn Sie die SQL-Anmeldenamen der Remotearbeitsstation verwenden.

### <a name="launchpad-services-fails-to-start-if-version-is-different-than-r-version"></a>Launchpad-Dienste werden nicht gestartet, wenn die Version von der R-Version abweicht
Wenn Sie R Services getrennt vom Datenbankmodul installieren und sich die Versionen unterscheiden, kann im Systemereignisprotokoll die folgende Fehlermeldung angezeigt werden: _Das SQL Server Launchpad konnte aufgrund des folgenden Fehlers nicht gestartet werden: Der Dienst antwortete nicht rechtzeitig auf die Start- oder Steuerungsanforderung._

Dieser Fehler tritt möglicherweise auf, wenn Sie das Datenbankmodul mithilfe der endgültigen Produktversion installieren, einen Patch anwenden, um das Datenbankmodul zu aktualisieren, und anschließend R Services mithilfe der endgültigen Produktversion hinzufügen.

Um dieses Problem zu vermeiden, sollten Sie sicherstellen, dass alle Komponenten dieselbe Versionsnummer aufweisen. Wenn Sie eine Komponente aktualisieren, müssen Sie dasselbe Upgrade auf alle anderen installierten Komponenten anwenden.

Eine Liste der R-Versionsnummern, die für jede Version von SQL Server 2016 erforderlich sind, finden Sie unter [Installation von R-Komponenten ohne Internetzugang](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md).


### <a name="service-account-for-launchpad-requires-permission-replace-process-level-token"></a>Dienstkonto für Launchpad erfordert die Berechtigung „Ersetzen eines Tokens auf Prozessebene“
 Bei der Installation von SQL Server R Services wird das Trusted Launchpad über das Konto NT Service\MSSQLLaunchpad gestartet, das standardmäßig mit den erforderlichen Berechtigungen bereitgestellt wird. Wenn Sie jedoch ein anderes Konto verwenden oder die mit diesem Konto verknüpften Berechtigungen ändern, wird das Launchpad unter Umständen nicht gestartet.
 
 Um sicherzustellen, dass sich das Launchpad-Dienstkonto anmelden kann, gewähren Sie dem Konto die folgende Berechtigung: `Replace Process Level Token`. Weitere Informationen finden Sie unter [Ersetzen eines Tokens auf Prozessebene](https://technet.microsoft.com/itpro/windows/keep-secure/replace-a-process-level-token).

### <a name="remote-compute-contexts-blocked-by-firewall-in-sql-server-instances-running-on-azure-virtual-machines"></a>Remoterechenkontexte werden in SQL Server-Instanzen, die auf virtuellen Computern in Azure ausgeführt werden, durch die Firewall blockiert  
 Falls Sie [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] auf einem virtuellen Computer in Azure installiert haben, können Sie Rechenkontexte, die die Verwendung des Arbeitsbereichs des virtuellen Computers erfordern, möglicherweise nicht verwenden. Der Grund ist, dass die Firewall auf Azure-VMs standardmäßig eine Regel enthält, die den Netzwerkzugriff für lokale Benutzerkonten für R blockiert.  
  
 Öffnen Sie zur Umgehung dieses Problems auf der Azure-VM **Windows-Firewall mit erweiterter Sicherheit**, wählen Sie **Ausgehende Regeln**aus, und deaktivieren Sie die folgende Regel: „Netzwerkzugriff für lokale R-Benutzerkonten in der SQL Server-Instanz MSSQLSERVER blockieren“.  
  
### <a name="implied-authentication-in-sqlexpress"></a>Implizite Authentifizierung in SQLEXPRESS
Beim Ausführen von R-Aufträgen auf einer Data Science-Remotearbeitsstation mithilfe der integrierten Windows-Authentifizierung verwendet SQL Server die *implizite Authentifizierung*, um lokale ODBC-Aufrufe zu generieren, die das Skript möglicherweise benötigt. Im RTM-Build der SQL Server Express Edition funktionierte diese Funktion jedoch nicht. 

Um das Problem zu beheben, empfehlen wir die Aktualisierung auf ein neueres Service Release.

Wenn ein Upgrade nicht möglich ist, können Sie eine SQL-Anmeldung verwenden, um R-Remoteaufträge auszuführen, die unter Umständen eingebettete ODBC-Aufrufe benötigen. 

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>Einschränkungen der Prozessoraffinität für R-Aufträge 
 
Im RTM-Build von SQL Server 2016 konnte die Prozessoraffinität nur für CPUs in der ersten k-Gruppe festgelegt werden. Wenn es sich bei dem Server um einen 2-Socket-Computer mit zwei k-Gruppen handelt, werden beispielsweise nur Prozessoren der ersten k-Gruppe für die R-Prozesse verwendet. Dieselbe Einschränkung gilt beim Konfigurieren der Ressourcenkontrolle für R-Skriptaufträge.

Dieses Problem wurde in SQL Server 2016 Service Pack 1 behoben.

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
  
### <a name="resource-governance-default-values"></a>Standardwerte der Ressourcenkontrolle  
In Enterprise Edition können Sie Ressourcenpools verwenden, um externe Skriptprozesse zu verwalten. In einigen Builds betrug der maximale Arbeitsspeicher, der für die R-Prozesse zugeordnet werden konnte, 20 %. Wenn der Server über 32 GB RAM-Speicher verfügte, konnten die ausführbaren R-Dateien (RTerm.exe und BxlServer.exe) in einer einzelnen Anforderung maximal 6,4 GB verwenden. 

Wenn Sie Ressourceneinschränkungen feststellen, sollten Sie den aktuellen Standardwert überprüfen. Sollten 20 % nicht ausreichend sein, finden Sie in der Dokumentation für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Informationen, wie Sie diesen Wert ändern können.  

### <a name="avoid-clearing-workspaces-when-executing-r-code-in-a-includessnoversiontokenssnoversionmdmd-compute-context"></a>Löschen von Arbeitsbereichen vermeiden, wenn R-Code in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rechenkontext ausgeführt wird  
 Wenn Sie den R-Befehl verwenden, um Objekte aus Ihrem Arbeitsbereich zu entfernen, während R-Code in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rechenkontext ausgeführt wird, oder wenn Sie den Arbeitsbereich im Rahmen eines R-Skripts löschen, das mit [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) aufgerufen wird, erhalten Sie möglicherweise die folgende Fehlermeldung: *Arbeitsbereichsobjekt 'RevoScriptConnection' wurde nicht gefunden*.

`revoScriptConnection` ist ein Objekt im R-Arbeitsbereich, das Informationen über eine R-Sitzung enthält, die aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufgerufen wird. Wenn Ihr R-Code jedoch einen Befehl zum Löschen des Arbeitsbereichs enthält (wie z.B. `rm(list=ls()))`), werden alle Informationen über die Sitzung und andere Objekte im R-Arbeitsbereich ebenfalls gelöscht.

Um dieses Problem zu umgehen, sollten Sie willkürliches Löschen von Variablen und anderen Objekten während der Ausführung von R in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vermeiden. Das Löschen des Arbeitsbereichs ist bei der Arbeit auf der R-Konsole zwar üblich, kann aber zu unerwarteten Ergebnissen führen. 

+ Um bestimmte Variablen zu löschen, verwenden Sie die Funktion *remove* von R: `remove('name1', 'name2', ...)`. 
+ Wenn mehrere zu löschende Variablen vorhanden sind, speichern Sie die Namen temporärer Variablen in einer Liste und führen eine regelmäßige automatische Speicherbereinigung durch. 
   
### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>Einschränkungen von Daten, die als Eingabe für ein R-Skript bereitgestellt werden können  
 Sie können die folgenden Typen von Abfrageergebnissen nicht in einem R-Skript verwenden:  
  
-   Daten aus einer [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfrage, die auf „AlwaysEncrypted“-Spalten verweist.  
  
-   Daten aus einer [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfrage, die auf maskierte Spalten verweist.  
  
     Wenn Sie maskierte Daten in einem R-Skript verwenden müssen, ist eine mögliche Problemumgehung das Erstellen einer Kopie der Daten in einer temporären Tabelle und anschließende Verwenden dieser Daten.  
   
  
## <a name="microsoft-r-server-standalone"></a>Microsoft R Server (eigenständig)  
 In diesem Abschnitt werden Probleme aufgeführt, die speziell die eigenständige Version von Microsoft R Server betreffen. 
  
### <a name="multiple-r-libraries-and-executables-are-installed-if-you-install-both-standalone-and-in-database"></a>Mehrere R-Bibliotheken und ausführbare Dateien werden installiert, wenn Sie sowohl die eigenständige Version als auch die In-Database-Version installieren  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup umfasst eine Option für das Installieren von Microsoft R Server (eigenständig). Die Option „Microsoft R Server (eigenständig)“ kann in der Enterprise Edition zum Installieren eines eigenständigen Windows-Servers verwendet werden, der R unterstützt, aber keine Interaktivität mit SQL Server benötigt.    

> [!TIP] Diese eigenständige Option ist **nicht** erforderlich, um R mit [!INCLUDE[tsql](../../includes/tsql-md.md)] zu verwenden.
> 
> Wenn Sie einen Data Science-Clientcomputer einrichten müssen, der eine Verbindung zu [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] oder zu Microsoft R Server (eigenständig) herstellen kann, empfehlen wir [Microsoft R Client](http://go.microsoft.com/fwlink/?LinkId=799768).  

Wenn Sie R Services (In-Database) und Microsoft R Server (eigenständig) auf demselben Computer installieren, müssen Sie beachten, dass für jede Instanz von SQL Server, für die R aktiviert ist, eine separate Instanz von R erstellt wird; ferner wird eine separate Instanz von R für Microsoft R Server (eigenständig) erstellt.  Wenn Sie beispielsweise die Standardinstanz und eine benannte Instanz sowie R Server (eigenständig) installiert haben, befinden sich unter Umständen drei Instanzen von R auf demselben Computer:  
  
-   **Eigenständig:** C:\Programme\Microsoft SQL Server\130\R_SERVER  
  
-   **Standardinstanz:** C:\Programme\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES  
  
-   **Benannte Instanz:** C:\Programme\Microsoft SQL Server\MSSQL13.<Instanzname>\R_SERVICES  
  
> [!NOTE] 
> 
> Verwenden Sie die R-Bibliotheken und -Tools, die mit einer Datenbankinstanz verknüpft sind, nur aus dem Kontext von [!INCLUDE[tsql](../../includes/tsql-md.md)]. Wenn Sie R mit anderen R-Tools ausführen müssen, achten Sie darauf, dass Sie auf die R-Bibliotheken verweisen, die von R Server (eigenständig) verwendet werden und die standardmäßig unter C:\Programme\Microsoft SQL Server\130\R_SERVER installiert sind.  

### <a name="performance-limits-when-r-services-libraries-are-called-from-standalone-r-tools"></a>Leistungseinschränkungen, wenn R Services-Bibliotheken von eigenständigen R-Tools aufgerufen werden

Die R-Bibliotheken, die von SQL Server R Services verwendet werden, sind standardmäßig unter C:\Programme\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES installiert. Es ist *möglich*, die R-Tools und -Bibliotheken aufzurufen, die für SQL Server R Services von einer externen R-Anwendung wie RGui installiert werden. 

Dies geht jedoch mit einer Leistungseinbuße einher. Selbst wenn Sie beispielsweise die Enterprise Edition von SQL Server erworben haben, wird R im Singlethread-Modus ausgeführt, wenn Sie den R-Code mit externen Tools ausführen. Die Leistung ist höher, wenn Sie den R-Code ausführen, indem Sie eine SQL Server-Verbindung herstellen und [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) verwenden, das die R Services-Bibliotheken für Sie aufruft.

+ Vermeiden Sie es, die von SQL Server verwendeten R-Bibliotheken mit externen R-Tools aufzurufen. 
+ Wenn Sie R auf dem SQL Server-Computer mithilfe externer Tools ausführen müssen, sollten Sie eine separate Instanz von R installieren und dann sicherstellen, dass Ihre R-Tools auf die neue Bibliothek verweisen. 
+ Wenn Sie die Enterprise Edition verwenden, wird empfohlen, dass Sie Microsoft R Server (eigenständig) auf dem SQL Server-Computer installieren. Verweisen Sie dann aus dem externen Tool, mit dem Sie R-Code ausführen, auf die Bibliotheken für R Server, die standardmäßig unter C:\Programme\Microsoft SQL Server\<Versionsnummer>\R_SERVER installiert sind. 

Weitere Informationen finden Sie unter [Erstellen eines eigenständigen R-Servers](../../advanced-analytics/r-services/create-a-standalone-r-server.md).  
  
  
## <a name="general-r-issues"></a>Allgemeine R-Probleme  

 In diesem Abschnitt werden Probleme aufgeführt, die speziell die R-Konnektivität und die R-Leistungstools betreffen.  
  
### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>Eingeschränkte Unterstützung für SQL-Datentypen in sp_execute_external_script  

 Nicht alle Datentypen, die in SQL unterstützt werden, können in R verwendet werden. Um dieses Problem zu umgehen, sollten Sie es in Erwägung ziehen, den nicht unterstützten Datentyp in einen unterstützten Datentypen umzuwandeln, bevor die Daten an sp_execute_external_script übergeben werden.  
  
 Weitere Informationen finden Sie unter [Arbeiten mit R-Datentypen](../../advanced-analytics/r-services/working-with-r-data-types.md).  
  
### <a name="possible-string-corruption"></a>Mögliche Zeichenfolgenbeschädigung  

 Roundtrips von Zeichenfolgen von [!INCLUDE[tsql](../../includes/tsql-md.md)] zu R und anschließend zurück zu [!INCLUDE[tsql](../../includes/tsql-md.md)] können zu Beschädigungen führen. Grund sind die verschiedenen Codierungen, die in R und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet werden, sowie die unterschiedlichen Sortierungen und unterstützten Sprachen, die von R und [!INCLUDE[tsql](../../includes/tsql-md.md)]unterstützt werden. Zeichenfolgen mit einer Nicht-ASCII-Codierung werden möglicherweise nicht ordnungsgemäß verarbeitet.  
  
 Beim Senden von Zeichenfolgendaten an R konvertieren Sie diese nach Möglichkeit in eine ASCII-Darstellung.  
  
### <a name="only-one-raw-value-can-be-returned-from-spexecuteexternalscript"></a>sp_execute_external_script kann nur einen einzigen Rohwert zurückgeben  

 Wenn ein binärer Datentyp (der R-Datentyp **raw** ) von R zurückgegeben wird, muss der Wert dem Wert im Ausgabedatenrahmen entsprechen.  
  
 Unterstützung für mehrere **raw** -Ausgaben werden in künftigen Versionen hinzugefügt.  
  
 Eine mögliche Problemumgehung, falls mehrere Ausgaberesultsets gewünscht sind, ist das mehrfache Aufrufen der gespeicherten Prozedur und Senden der Resultsets zurück an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe von ODBC.  
  
 Beachten Sie, dass Sie Parameterwerte zusammen mit den Ergebnissen der gespeicherten Prozedur zurückgeben können, indem Sie das Schlüsselwort OUTPUT hinzufügen. Weitere Informationen finden Sie unter [Zurückgeben von Daten mithilfe von OUTPUT-Parametern](https://technet.microsoft.com/library/ms187004.aspx).
  
### <a name="loss-of-precision"></a>Genauigkeitsverlust  

 [!INCLUDE[tsql](../../includes/tsql-md.md)] und R unterstützen unterschiedliche Datentypen. Aus diesem Grund kann es bei der Konvertierung numerischer Datentypen zu einem Genauigkeitsverlust kommen.  
  
 Weitere Informationen zur impliziten Datentypkonvertierung finden Sie unter [Working with R Data Types](../../advanced-analytics/r-services/working-with-r-data-types.md).  
  
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
  
 Um den Fehler zu vermeiden, schreiben Sie den Code wie folgt um:  
  
```  
g <- function(y){  
              f <- function(x) { 2*x +3}  
              a <- 10 * y  
              f(a)  
}  
  
```  

  
## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise und Microsoft R Open 
 
 In diesem Abschnitt werden Probleme aufgeführt, die speziell von Revolution Analytics bereitgestellte Konnektivitäts-, Entwicklungs- und Leistungstools für R betreffen. Diese Tools wurden in früheren Vorabversionen von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] bereitgestellt. 

Generell wird empfohlen, dass Sie diese Vorabversionen deinstallieren und die neueste Version von SQL Server R Services, Microsoft R Server oder Microsoft R Client installieren.
  
### <a name="running-side-by-side-versions-of-revolution-r-enterprise"></a>Paralleles Ausführen verschiedener Versionen von Revolution R Enterprise  

 Das parallele Installieren von Revolution R Enterprise mit einer beliebigen Version von [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] wird nicht unterstützt.  
  
 Wenn Sie eine Lizenz für eine andere Version von Revolution R Enterprise haben, müssen Sie diese auf einem Computer verwenden, der sowohl von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz als auch allen Arbeitsstationen getrennt ist, über die Sie eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz herstellen möchten.  
  
### <a name="limited-support-for-revoscaler-rxexec"></a>Eingeschränkte Unterstützung für RevoScaleR rxExec  

 Ab RC0 kann die von `rxExec` bereitgestellte [!INCLUDE[rsql_rre-short](../../includes/rsql-rre-short-md.md)] -Funktion nur im Singlethread-Modus verwendet werden.  
  
 Parallelität für `rxExec` über mehrere Prozesse wird in einer künftigen Version hinzugefügt werden.  
  
### <a name="data-import-and-manipulation-using-revoscaler"></a>Importieren und Bearbeiten von Daten mithilfe von RevoScaleR  

 Beim Lesen von **varchar** -Spalten aus einer Datenbank werden Leerzeichen abgeschnitten. Um dies zu verhindern, schließen Sie Zeichenfolgen in Zeichen ein, die keine Leerzeichen sind.  
  
 Wenn Sie Funktionen wie `rxDataStep` zum Erstellen von Tabellen mit **varchar** -Spalten nutzen, wird die Spaltenbreite basierend auf einer Stichprobe der Daten geschätzt. Wenn die Breite variieren kann, kann es notwendig sein, alle Zeichenfolgen so aufzufüllen, dass ihre Länge gleich ist.  
  
 Das Verwenden einer Transformation zum Ändern des Datentyps einer Variablen wird nicht unterstützt, wenn wiederholte Aufrufe von `rxImport` oder `rxTextToXdf` zum Importieren und Anfügen von Zeilen verwendet werden, wobei mehrere Eingabedateien zu einer einzelnen XDF-Datei kombiniert werden.  
  
### <a name="increase-maximum-parameter-size-to-support-rxgetvarinfo"></a>Erhöhen der maximale Parametergröße zur Unterstützung von rxGetVarInfo  

 Wenn Sie Datensätze mit einer sehr großen Anzahl von Variablen (z. B. über 40.000) verwenden, legen Sie das `max-ppsize` -Flag beim Starten von R fest, um Funktionen wie z. B. `rxGetVarInfo`zu verwenden.  Das `max-ppsize` -Flag gibt die maximale Pointer Protection Stack-Größe an.  
  
 Wenn Sie die R-Konsole verwenden (z. B. in „rgui.exe“ oder „rterm.exe“), können Sie den Wert von „max-ppsize“ auf 500.000 festlegen, indem Sie Folgendes eingeben:  
  
```  
R --max-ppsize=500000  
```  
  
 Bei Verwendung der [!INCLUDE[rsql_developr](../../includes/rsql-developr-md.md)] -Umgebung, können Sie das `max-ppsize` -Flag festlegen, indem Sie diesen Aufruf an die ausführbare RevoIDE-Datei richten:  
  
```  
RevoIDE.exe /RCommandLine --max-ppsize=500000  
```  
  
### <a name="issues-with-rxdtree-function"></a>Probleme mit der rxDTree-Funktion  

 Die `rxDTree` -Funktion unterstützt derzeit keine formelinternen Transformationen. Insbesondere das Verwenden der `F()` -Syntax zum Erstellen von Faktoren bei laufendem Betrieb wird nicht unterstützt. Numerische Daten werden jedoch automatisch klassifiziert.  
  
 Geordnete Faktoren werden in allen RevoScaleR-Analysefunktionen außer `rxDTree`genauso wie Faktoren behandelt.  
  
### <a name="using-the-r-productivity-environment"></a>Verwenden der R-Produktivitätsumgebung  

Einige Vorabversionen von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] enthalten eine R-Entwicklungsumgebung für Windows, die von Revolution Analytics erstellt wurde. 

Für die Kompatibilität mit [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] wird jedoch dringend empfohlen, anstelle der Tools von Revolution Analytics Microsoft R Client oder Microsoft R Server zu installieren. [R-Tools für Visual Studio](https://www.visualstudio.com/vs/rtvs/) ist ein weiterer empfohlener Client, der Microsoft R-Lösungen unterstützt.
  
### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>Kompatibilitätsprobleme mit SQLite-ODBC-Treiber und RevoScaleR  
 Version 0.92 des SQLite-ODBC-Treibers ist nicht kompatibel mit RevoScaleR. Die Revisionen 0.88 0.91 und 0.93 und später sind bekanntermaßen kompatibel.  
  
## <a name="see-also"></a>Siehe auch  
[Neues in SQL Server 2016](../../sql-server/what-s-new-in-sql-server-2016.md)
  