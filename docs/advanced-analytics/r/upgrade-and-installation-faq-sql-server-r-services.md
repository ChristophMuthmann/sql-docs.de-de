---
title: "Upgrade und Installation häufig gestellte Fragen zur SQL Server-Machine Learning | Microsoft Docs"
ms.date: 10/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 001e66b9-6c3f-41b3-81b7-46541e15f9ea
caps.latest.revision: "59"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 3c4fb79f04daeff6d98856b521fa1602a2334cdd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning"></a>Upgrade und Installation häufig gestellte Fragen zur SQL Server-Machine Learning

Dieses Thema enthält Antworten auf einige häufig gestellte Fragen zur Installation von Machine learning-Funktionen in SQL Server. Außerdem werden häufige gestellte Fragen zu Upgrades behandelt.

+ Einige Probleme auftreten, nur beim Upgrade älterer Versionen. Aus diesem Grund wird empfohlen, dass Sie die Version und-Edition zuerst identifizieren, bevor diese Hinweise zu lesen.
+ Aktualisieren Sie auf die neueste Version oder die Dienstversion so bald wie möglich, so beheben Sie alle Probleme, die in neueren Versionen behoben wurden.

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Services (Datenbankintern)

## <a name="performing-setup-for-the-first-time"></a>Setup ausführt zum ersten Mal.

Führen Sie die Verfahren für die Einrichtung von [!INCLUDE[sscurrent_md](../../includes/sscurrent_md.md)] und R-Komponenten, wie hier beschrieben: 

+ [Einrichten von SQL Server R Services "oder" Machine Learning-Dienste In der Datenbank](../r/set-up-sql-server-r-services-in-database.md)
+ [Einrichten von SQL Server-2017 mit Python](../python/setup-python-machine-learning-services.md)
+ [Erstellen Sie einen eigenständigen R-Server](../r/create-a-standalone-r-server.md)

> [!IMPORTANT]
> 
> Nachdem Sie installiert haben, SQL Server und Machine learning-Funktionen, bevor Sie R oder Python-Skripts verwenden können, müssen Sie einige zusätzliche Konfigurationsschritte abschließen. Das liegt daran der externen Ausführung Skriptfunktion standardmäßig nicht aktiviert ist.

### <a name="requirements-and-restrictions"></a>Anforderungen und Einschränkungen

Abhängig von der Build von SQL Server, die installiert werden, kann die folgenden Einschränkungen gelten:

- In frühen Versionen von SQL Server 2016 R Services wurde 8.3-Notation auf dem Laufwerk erforderlich, die das Arbeitsverzeichnis enthält. Wenn Sie eine Vorabversion installiert haben, sollte ein Upgrade auf SQL Server 2016 Service Pack 1 dieses Problem beheben. Diese Anforderung gilt nicht für Versionen nach SP1.

- Derzeit kann nicht installiert werden [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] in einem Failovercluster installieren. 

- Auf einer Azure-VM möglicherweise einige zusätzliche Konfigurationsschritte erforderlich. Beispielsweise müssen Sie möglicherweise eine Firewallausnahme zur Unterstützung von Remotezugriff zu erstellen.

- Seite-an-Seite-Installation eine andere Version von R oder mit anderen Versionen von Revolution Analytics, wird nicht unterstützt.

- Neue Installationen einer Vorabversion von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] werden nicht mehr unterstützt. Wenn Sie eine Vorabversion verwenden, aktualisieren Sie so bald wie möglich.

- Deaktivieren Sie vor dem Setup Virenscan. Wenn Setup abgeschlossen ist, sollten Sie bis zum Anhalten der Scan für die Ordner, in [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]. Vorzugsweise anhalten-Überprüfung wird auf die gesamte [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)] Struktur.

### <a name="licensing-agreements-for-unattended-installs"></a>Lizenzverträge für unbeaufsichtigte Installationen

Wenn Sie die Befehlszeile zum Aktualisieren einer Instanz von SQL Server verwenden, stellen Sie sicher, dass die Befehlszeile beide enthalten den [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)] Vereinbarung-Parameter, und die neue Lizenz vereinbarungsparameter für R und Python-Lizenzierung.

### <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server"></a>Offline-Installation von Machine Learning-Komponenten für eine lokalisierte Version von SQL Server

Bei der Installation [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)] Machine Learning-Komponenten auf einem Computer, die nicht über Internetzugriff verfügt, müssen Sie einige zusätzliche Schritte ausführen:

+ Laden Sie die Installationsprogramme für R oder Python-Komponente in einen lokalen Ordner herunter, vor dem Ausführen von SQL Server-Setup.
+ In einigen Fällen müssen Sie so bearbeiten Sie die Installationsdatei, um sicherzustellen, dass die richtige Sprache installiert ist.
+ Die Sprachen-ID, die für Machine learning-Komponenten verwendet, muss die Sprache der SQL Server-Setup identisch sein, oder Sie nicht Setup abgeschlossen.

Weitere Informationen finden Sie unter [Machine Learning-Komponenten ohne Internetzugang installieren](../r/installing-ml-components-without-internet-access.md).

## <a name="post-installation-configuration"></a>Konfiguration nach der installation

Um Machine Learning mit R oder Python zu verwenden, ist zusätzlicher Konfigurationsaufwand nach dem Ausführen von SQL Server-Setup erforderlich. Die genauen Schritte, die erforderlich sind, hängen von der Sicherheitsstufe des Servers, und wie Sie die SQL Server-Instanz und die Datenbanken konfiguriert haben.

Überprüfen Sie alle Optionen in der Liste von Anweisungen nach der Installation, um festzustellen, welche zusätzlichen Schritte in Ihrer Umgebung erforderlich sein können.

+ [Einrichten von SQL Server-Machine learning-Datenbank](set-up-sql-server-r-services-in-database.md) 

## <a name="upgrades-or-uninstallation"></a>Upgrades oder deinstallieren

Dieser Abschnitt enthält detaillierte Anweisungen für bestimmte Szenarien für das Upgrade an.

### <a name="how-to-upgrade-sql-server"></a>Gewusst wie: upgrade von SQL Server

Sie können Ihre Version von SQL Server aktualisieren, indem Sie den Setup-Assistenten erneut ausführen.

+ [Aktualisieren von SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
+ [Aktualisieren von SQLServer mithilfe des Installations-Assistenten](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

Sie können nur die computerlernverfahren Komponenten mithilfe des so genannten Bindung aktualisieren: 
+ [Verwenden Sie SqlBindR Upgrade Machine Learning-Komponenten](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>Ende des Supports für direkte Upgrades von Vorabversionen

Upgrades von Vorabversionen von SQL Server 2016 werden nicht mehr unterstützt. Hierzu zählen SQL Server 2016 CTP3, CTP3. 1, CTP3. 2, RC0 oder RC1.

Die folgenden Versionen wurden mit Vorabversionen von SQL Server 2016 installiert.

| Version | Erstellen         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

Wenn Sie nur die geringste Möglichkeit haben, welche Version Sie verwenden, führen Sie `@@VERSION` in einer Abfrage in SQL Server Management Studio.

Im Allgemeinen ist der Prozess für das Upgrade wie folgt ein:

1. Sichern Sie Skripts und Daten.
2. Deinstallieren Sie die Vorabversion.
3. Installieren Sie eine veröffentlichte Version.

Deinstallieren einer Vorabversion von SQL Server von Machine Learning-Komponenten können komplex sein und erfordert unter Umständen ein spezielles Skript ausführen. Technischen Support um Unterstützung zu erhalten.

### <a name="support-for-slipstream-upgrades"></a>Unterstützung für Slipstream-Upgrades

Als Slipstream-Einrichtung wird die Möglichkeit bezeichnet, einen Patch oder ein Update auf eine fehlgeschlagene Installation einer Instanz anzuwenden, um vorhandene Probleme zu beheben. Der Vorteil dieser Methode ist, dass SQL Server gleichzeitig aktualisiert werden, dass Sie Setup ausführen, vermeiden einen separaten Neustart später.

Wenn der Server nicht über Internetzugriff verfügt, achten Sie darauf, dass Sie die SQL Server-Installationsprogramm herunterzuladen. Außerdem müssen Sie separat die entsprechenden Versionen der R-Komponenteninstaller herunterladen, *bevor* Sie mit dem Update beginnen. 

Speicherorte für den Download, finden Sie unter [Machine Learning-Komponenten ohne Internetzugang installieren](installing-ml-components-without-internet-access.md).

Wenn alle Setupdateien in ein lokales Verzeichnis kopiert wurden, starten Sie das Setuphilfsprogramm, indem Sie „setup.exe“ in die Befehlszeile eingeben.

- Verwenden der */UpdateSource* Argument, um den Speicherort einer lokalen Datei anzugeben, die das SQL Server-Update, z. B. ein kumulatives Update oder Service Pack-Version enthält.

- Verwenden der */MRCACHEDIRECTORY* Argument, um den Ordner anzugeben, die die R-Komponente CAB-Dateien enthält.

Weitere Informationen finden Sie in diesem Blog durch das Supportteam von: [Bereitstellen von R Services auf Computern ohne Internetzugang](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/).

### <a name="get-machine-learning-components-for-offline-installs"></a>Abrufen der Machine Learning-Komponenten für offline-Installationen

Wenn Sie installieren oder Aktualisieren von Servern, die nicht mit dem Internet verbunden sind, müssen Sie eine aktualisierte Version des Machine learning-Komponenten vor der Aktualisierung manuell herunterladen. 

+ [Machine Learning-Komponenten ohne Internetzugang installieren](../../advanced-analytics/r/installing-ml-components-without-internet-access.md).

### <a name="support-policy-and-schedule-for-update-of-machine-learning-components"></a>Unterstützen Sie Richtlinie und den Zeitplan für das Update von Machine Learning-Komponenten

Als Hotfixes oder Verbesserungen an SQL Server freigegeben sind, werden Machine Learning-Komponenten automatisch aktualisiert oder aktualisiert, wenn die Instanz bereits die Funktion enthält.

Ab Dezember 2016 können Sie Machine Learning-Komponenten für eine rasche als SQL Server-Releasezyklus aktualisieren. Hierzu *Bindung* einer Instanz von SQL Server für die moderne Software Lifecycle-Richtlinie. Immer eine neue Version der Machine Learning-Tools von Machine learning-Entwicklungsteam veröffentlicht wird, können die neueste Version herunterladen und wenden Sie es auf eine SQL Server-Instanz, die für Machine Learning verwendet wird.

Weitere Informationen finden Sie in den folgenden Themen:

+ [Unterstützungszeitraum für Microsoft R Server und Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/resources-servicing-support)
+ [Verwenden Sie zum Aktualisieren einer Instanz von SQL Server SqlBindR](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="r-server-standalone"></a>R-Server (eigenständig)

In diesem Abschnitt werden Probleme, die spezifisch für Installationen von Microsoft R Server (eigenständig), mit denen SQL Server 2016-Setup beschrieben. 

Probleme im Zusammenhang mit Upgrades von R-Server, auf Machine Learning-Server, finden Sie unter [Machine Learning-Server für Windows installieren](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

### <a name="problems-when-r-services-and-r-server-standalone-are-installed-on-the-same-computer"></a>Probleme bei der R-Services und eigenständigen R-Server auf demselben Computer installiert sind

Beim Installieren von R Server (eigenständig) und R Services (Datenbankintern) zur gleichen Zeit manchmal in früheren Versionen von SQL Server 2016 verursacht Setup mit der Fehlermeldung "Zugriff verweigert" fehl. Dieses Problem wurde in Service Pack 1 für SQL Server 2016 behoben.

Wenn Sie diesen Fehler und diese Funktionen zu aktualisieren müssen, führen Sie eine Slipstream-Installation von SQL Server 2016 mit SP1. Es gibt zwei Möglichkeiten zum Beheben des Problems, die beides erforderlich, deinstallieren und neu installieren.

1. Deinstallieren Sie R Services (Datenbankintern), und stellen Sie sicher, dass die Benutzerkonten für SQLRUserGroup entfernt werden.

2. Starten Sie den Server neu, und installieren Sie R-Server (eigenständig).

3. Ausführen von SQL Server setup einmal, und wählen Sie dieses Mal **Hinzufügen von Funktionen zu einer vorhandenen SQL Server**.

4. Wählen Sie die Instanz, und wählen Sie dann die **R Services (Datenbankintern)** Option zum Hinzufügen.

Wenn diese Prozedur nicht das Problem zu beheben, versuchen Sie die folgende problemumgehung:

1. Deinstallieren Sie R Services (Datenbankintern) und R-Server (eigenständig) gleichzeitig aus.

2. Entfernen Sie die lokalen Benutzerkonten (SQLRUserGroup).

3. Starten Sie den Server neu.

4. Führen Sie SQL Server-Setup, und fügen Sie nur die R-Services (Datenbankintern)-Funktion. Aktivieren Sie nicht **R Server (eigenständig)**.

Im Allgemeinen wird empfohlen, dass Sie R Services (Datenbankintern) und R-Server (eigenständig) nicht installieren auf dem gleichen Computer. Vorausgesetzt, dass der Server über ausreichend Kapazität verfügt, können Sie jedoch feststellen, dass eigenständigen R-Server als ein Entwicklungstool von Nutzen sein kann. Eine andere besteht mögliche, müssen Sie die Funktionen operationalisierung von R-Server verwenden, aber auch SQL Server-Daten ohne Verschieben von Daten zugreifen möchten.

## <a name="see-also"></a>Siehe auch

 [Erste Schritte mit SQL Server R Services](../r/getting-started-with-sql-server-r-services.md)

 [Erste Schritte mit Microsoft R Server eigenständige](../r/getting-started-with-microsoft-r-server-standalone.md)
