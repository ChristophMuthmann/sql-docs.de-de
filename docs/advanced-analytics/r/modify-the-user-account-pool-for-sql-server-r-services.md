---
title: Ändern des benutzerkontenpools für SQL Server-Machine Learning | Microsoft Docs
ms.date: 11/03/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 7c1efa87fef881a8b88b0967716ec062cf95e64f
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="modify-the-user-account-pool-for-sql-server-machine-learning"></a>Ändern des benutzerkontenpools für SQL Server-Machine learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Im Rahmen des Installationsprozesses für [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] wird ein neuer Windows-*Benutzerkontenpool* erstellt, um die Ausführung von Aufgaben vom [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]-Dienst zu unterstützen. Der Zweck dieser Worker-Konten ist gleichzeitige Ausführung externer Skripts, die von anderen SQL-Benutzer zu isolieren.

Dieser Artikel beschreibt die Standardkonfiguration, die Sicherheit und die Kapazität für die Worker-Konten und wie Sie die Standardkonfiguration ändern.

**Gilt für:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)], [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

## <a name="worker-accounts-used-for-external-script-execution"></a>Für das Ausführen des externen Skripts verwendete Worker-Konten

Windows-Kontogruppe wird erstellt, indem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup für jede Instanz auf dem Machine Learning installiert und aktiviert ist.

-   In einer Standardinstanz ist der Gruppenname **SQLRUserGroup**. Der Name entspricht dem, ob Sie R, Python oder beides verwenden.
-   In einer benannten Instanz erhält der Standardgruppenname den Instanznamen als Suffix, z.B. **SQLRUserGroupMyInstanceName**.

Standardmäßig enthält der Benutzerkontenpool 20 Benutzerkonten. In den meisten Fällen 20 ist mehr als ausreichend, um Machine Learning-Aufgaben unterstützen, aber Sie können die Anzahl der Konten ändern.
-  In einer Standardinstanz haben die einzelnen Konten Namen von **MSSQLSERVER01** bis **MSSQLSERVER20**.
-   In einer benannten Instanz sind die Konten nach dem Instanznamen benannt, z.B **MyInstanceName01** bis **MyInstanceName20**.

Wenn mehr als eine Instanz Machine Learning verwendet wird, wird der Computer mehrere Benutzergruppen haben. Eine Gruppe kann nicht über Instanzen gemeinsam genutzt werden.

### <a name = "HowToChangeGroup"> </a>So ändern Sie die Anzahl der Worker-Konten

Sie müssen die Eigenschaften des [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]-Dienstes wie unten beschrieben ändern, um die Anzahl der Benutzer im Kontenpool zu ändern.

Die jeweiligen Kennwörter der Benutzerkonten werden nach dem Zufallsprinzip generiert. Sie können Sie zu einem späteren Zeitpunkt ändern, nachdem die Konnten erstellt wurden.

1. Klicken Sie im SQL Server Configuration Manager auf **SQL Server-Dienste**.
2. Doppelklicken Sie auf den Launchpad-Dienst von SQL Server und beenden Sie den Dienst, wenn er ausgeführt wird.
3.  Achten Sie darauf, dass der Startmodus auf der Registerkarte **Dienst** auf „Automatisch“ festgelegt ist. Externe Skripts können nicht gestartet werden, wenn das Launchpad nicht ausgeführt wird.
4.  Klicken Sie auf die Registerkarte **Erweitert**, und bearbeiten Sie den Wert von **External Users Count** (Anzahl externer Benutzer), wenn nötig. Diese Einstellung steuert können wie viele verschiedene SQL-Benutzer externen Skript Sitzungen gleichzeitig ausführen. Der Standardwert ist 20 Konten.
5. Sie können die Option **Reset External Users Password** (Kennwörter externer Benutzer zurücksetzen) auch wahlweise auf _Ja_ festlegen, wenn Ihre Organisation eine Richtlinie zum regelmäßigen Ändern des Kennworts hat. Damit werden die verschlüsselten Kennwörter erneut generiert, die Launchpad für die Benutzerkonten verwaltet. Weitere Informationen finden Sie unter [Enforcing Password Policy (Erzwingen der Kennwortrichtlinie)](#bkmk_EnforcePolicy).
6.  Starten Sie den Launchpad-Dienst neu.

## <a name="managing-machine-learning-workloads"></a>Verwalten von Machine Learning-arbeitsauslastungen

Die Anzahl der Konten in diesem Pool bestimmt, wie viele externes Skript-Sitzungen gleichzeitig aktiv sein können.  Standardmäßig werden 20 Konten erstellt, was bedeutet, dass 20 unterschiedliche Benutzer R oder Python Sitzungen gleichzeitig verfügen können. Sie können die Anzahl der Worker-Konten erhöhen, wenn voraussichtlich mehr als 20 gleichzeitige Skripts ausgeführt werden.

Wenn derselbe Benutzer mehrere externe Skripts gleichzeitig ausgeführt wird, wird alles, was von diesem Benutzer die Sitzungen ausgeführt dasselbe workerkonto verwenden. Ein einzelner Benutzer möglicherweise z. B. 100 verschiedenen R-Skripts, die gleichzeitig ausgeführt werden, solange Sie Ressourcen ermöglichen, aber alle Skripts würde mit einem einzelnen Worker-Konto ausgeführt werden.

Die Anzahl der Worker-Konten, die Sie unterstützen können und die Anzahl gleichzeitiger Sitzungen, die jeder einzelner Benutzer ausgeführt werden kann, wird nur durch die Ressourcen des Servers beschränkt. Für gewöhnlich ist der Arbeitsspeicher der erste Engpass beim Verwenden der R-Laufzeit.

Die Ressourcen, die von Python oder R-Skripts verwendet werden können, werden von SQL Server gesteuert. Es wird empfohlen, dass Sie die Ressourcenauslastung mit SQL Server DMVs überwachen oder sich Leistungsindikatoren im verknüpften Windows-Auftragsobjekt anschauen; so können Sie die Arbeitsspeicherauslastung des Servers entsprechend anpassen. Wenn Sie SQL Server Enterprise Edition verfügen, können Sie Ressourcen für die Ausführung externer Skripts durch Konfigurieren von Zuordnen einer [externen Ressourcenpool](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md).

Zusätzliche Informationen zum Verwalten von Machine learning-Aufgabe-Kapazität finden Sie unter folgenden Artikeln:

- [SQL Server-Konfiguration für R Services](../../advanced-analytics/r/sql-server-configuration-r-services.md)
-  [Leistung-Fallstudie für R Services](../../advanced-analytics/r/performance-case-study-r-services.md)

## <a name="security"></a>Sicherheit

Jede Benutzergruppe wird mit dem [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]-Dienst auf einer bestimmten Instanz verknüpft und kann keine R-Aufträge unterstützen, die auf anderen Instanzen ausgeführt werden.

Während die Sitzung aktiv ist, wird für jedes Workerkonto ein temporärer Ordner zum Speichern von Skriptobjekten, Zwischenergebnissen und anderen von R und SQL Server während der Ausführung eines R-Skripts verwendeten Informationen erstellt. Auf diese Arbeitsdateien im Ordner „ExtensibilityData“ können nur Administratoren zugreifen. Sie werden von SQL Server bereinigt, nachdem das Skript abgeschlossen wurde. 

Weitere Informationen finden Sie unter [Sicherheitsübersicht](../../advanced-analytics/r-services/security-overview-sql-server-r.md).

### <a name="bkmk_EnforcePolicy"></a> Kennwortrichtlinie erzwingen

Wenn Ihre Organisation eine Richtlinie hat, die das regelmäßige Ändern von Kennwörtern erfordert, müssen Sie möglicherweise den Launchpad-Dienst zwingen, die verschlüsselten Kennwörter erneut zu generieren, die Launchpad für seine Workerkonten verwaltet.  

Öffnen Sie den Bereich **Eigenschaften** für den Launchpad-Dienst in SQL Server Configuration Manager, klicken Sie auf **Erweitert**, und ändern Sie **Reset External Users Password** (Kennwörter externer Benutzer zurücksetzen) in **Yes** (Ja). Wenn Sie diese Änderung übernehmen, werden die Kennwörter sofort für alle Benutzerkonten erneut generiert. Sie müssen den Launchpad-Dienst neu starten, um R-Skripts nach dieser Änderungen verwenden zu können; nun werden auch die neu generierten Kennwörter gelesen. 

Sie können dieses Flag entweder manuell festlegen oder dazu ein Skript verwenden.

### <a name="additional-permission-required-to-support-remote-compute-contexts"></a>Zusätzliche Berechtigung für das Unterstützen eines Remoterechenkontexts erforderlich

Standardmäßig hat die Gruppe von R-Workerkonten **keine** Anmeldeberechtigung auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz, mit der sie verknüpft ist. Dies kann zu einem Problem führen, wenn R-Benutzer von einem Remoteclient eine Verbindung mit SQL Server herstellen, um R-Skripts auszuführen, oder wenn ein Skript DBC verwendet, um zusätzliche Daten zu erhalten. 

Der Datenbankadministrator muss der Gruppe von R-Workerkonten die Anmeldeberechtigung für die SQL Server-Instanz erteilen, in der R-Skripts ausgeführt werden sollen (**Connect to**-Berechtigung (Verbinden mit)), um sicherzustellen, dass diese Szenarios unterstützt werden. Dies wird als bezeichnet *implizite Authentifizierung*, und ermöglicht SQL Server, die mit den Anmeldeinformationen des Remotebenutzers R-Skripts auszuführen.

> [!NOTE]
> Diese Einschränkung gilt nicht, wenn Sie SQL-Benutzernamen verwenden, um R-Skripts von einer Remotearbeitsstation auszuführen, da die SQL-Anmeldeinformationen explizit vom R-Client an die SQL Server-Instanz und dann an ODBC übergeben werden.


### <a name="how-to-enable-implied-authentication"></a>Aktivieren der impliziten Authentifizierung

1. Öffnen Sie SQL Server Management Studio als Administrator für die Instanz, wo Sie R oder Python-Code ausgeführt werden.

2. Führen Sie das folgende Skript aus: Achten Sie darauf, den Namen der Benutzergruppe zu bearbeiten, wenn Sie die Standardeinstellung geändert haben. Bearbeiten Sie außerdem den Namen des Computers und der Instanz.

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\SQLRUserGroup] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ````

