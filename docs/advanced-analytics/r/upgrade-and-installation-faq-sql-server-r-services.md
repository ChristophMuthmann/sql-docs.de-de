---
title: "Upgrade und Installation – häufig gestellte Fragen (SQL Server R Services) | Microsoft Docs"
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
ms.assetid: 001e66b9-6c3f-41b3-81b7-46541e15f9ea
caps.latest.revision: 59
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: 395554af6b9d014d560d8b6520d032966630c5b2
ms.contentlocale: de-de
ms.lasthandoff: 09/08/2017

---
# <a name="upgrade-and-installation-faq-sql-server-r-services"></a>Upgrade und Installation – häufig gestellte Fragen (SQL Server R Services)

Dieses Thema enthält Antworten auf einige häufig gestellte Fragen zur Installation von Machine learning-Funktionen in SQL Server. Außerdem werden häufige gestellte Fragen zu Upgrades behandelt. Einige Probleme auftreten, nur beim Upgrade älterer Versionen. Aus diesem Grund wird empfohlen, dass die Version und-Edition erste, und ein Upgrade auf die neueste Version oder die Dienstversion so bald wie möglich identifizieren.

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Services (Datenbankintern)

## <a name="performing-setup-for-the-first-time"></a>Setup ausführt zum ersten Mal.

Führen Sie die Verfahren zum Einrichten [! INCLUDEssCurrent] und der R-Komponenten, wie hier beschrieben: 

+ [Einrichten von SQL Server R Services "oder" Machine Learning-Dienste In der Datenbank](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)
+ [Einrichten von SQL Server-2017 mit Python](../python/setup-python-machine-learning-services.md)
+ [Erstellen eines eigenständigen R-Servers](create-a-standalone-r-server.md)

Nach der Installation von SQL Server, um externen R oder Python-Skripts verwenden, müssen Sie einige zusätzlichen Konfigurationen abschließen. Das liegt daran der externen Ausführung Skriptfunktion standardmäßig nicht aktiviert ist.

> [!NOTE]
> Verwenden Sie nicht setupanweisungen, die vor der Veröffentlichung von SQL Server 2016 veröffentlicht wurden. Der Setupvorgang vollständig zwischen frühen Releases und die offizielle Release-Version geändert. 

### <a name="requirements-and-restrictions"></a>Anforderungen und Einschränkungen

Je nach der Erstellung von R-Services, die Sie installieren, kann die folgenden Einschränkungen gelten:

- In frühen Versionen von SQL Server 2016 R Services wurde 8.3-Notation auf dem Laufwerk erforderlich, die das Arbeitsverzeichnis enthält. Wenn Sie eine Vorabversion installiert haben, sollten das Upgrade auf SQL Server 2016 Service Pack 1 diese Anforderung entfernen.

- Sie können [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] nicht auf einem Failovercluster installieren. 

- Auf einer Azure-VM möglicherweise einige zusätzliche Konfigurationsschritte erforderlich. Beispielsweise müssen Sie möglicherweise eine Firewallausnahme zur Unterstützung von Remotezugriff zu erstellen.

- Seite-an-Seite-Installation eine andere Version von R oder mit anderen Versionen von Revolution Analytics, wird nicht unterstützt.

- Neue Installationen einer Vorabversion von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] werden nicht mehr unterstützt. Wenn Sie eine Vorabversion verwenden, aktualisieren Sie so bald wie möglich.

- Deaktivieren Sie vor dem Setup Virenscan. Wenn Setup abgeschlossen ist, wird empfohlen, bis zum Anhalten der Scan für die Ordner, die von SQL Server (vorzugsweise die gesamte Struktur) verwendet.

### <a name="licensing-agreements-for-unattended-installs"></a>Lizenzverträge für unbeaufsichtigte Installationen

Wenn Sie die Befehlszeile zum Aktualisieren einer Instanz von SQL Server verwenden, stellen Sie sicher, dass die Befehlszeile den neue License Agreement-Parameter enthält */IACCEPTROPENLICENSEAGREEMENT*. Setup kann fehlschlagen, wenn Sie diesen Parameter nicht verwenden.

### <a name="offline-installation-of-r-components-for-a-localized-version-of-sql-server"></a>Offline-Installation von R-Komponenten für eine lokalisierte Version von SQL Server

Bei der Installation von R Services auf einem Computer, die nicht über Internetzugriff verfügt, müssen Sie zwei zusätzliche Schritte ausführen. Laden Sie in einen lokalen Ordner den R-Komponenten-Installer herunter, bevor Sie SQL Server-Setup ausführen, und bearbeiten die Installationsdatei, um sicherzustellen, dass die richtige Sprache installiert ist.

Die Sprachen-ID für die R-Komponenten verwendet, muss der SQL Server-Setup-Sprache identisch sein oder die **Weiter** Schaltfläche ist deaktiviert, und Sie können Setup nicht abgeschlossen.

Weitere Informationen finden Sie unter [Installieren von R-Komponenten ohne Internetzugang](../../advanced-analytics/r-services/installing-ml-components-without-internet-access.md).

## <a name="post-installation-configuration"></a>Konfiguration nach der installation

Um Machine Learning mit R oder Python zu verwenden, ist zusätzlicher Konfigurationsaufwand nach dem Ausführen von SQL Server-Setup erforderlich. Abhängig von der Sicherheitsstufe des Servers und Ihrer SQL Server-Instanz und die Datenbanken möglicherweise zusätzliche Schritte erforderlich. Überprüfen Sie diese Schritte aus den setupanweisungen, um zu bestimmen, ob zusätzliche Konfiguration notwendig sein kann.

[Legen Sie die SQL Server R Services In-Datenbank](set-up-sql-server-r-services-in-database.md)

- Die Funktion, die unterstützt die Ausführung externer Skripts, z. B. R oder Python, ist standardmäßig für die datenbanksicherheit deaktiviert und muss aktiviert sein.

- Stellen Sie sicher, dass der Worker-Konten, die von Launchpad, zum Ausführen von R oder Python verwendet werden Zugriff auf die Instanz verfügen.

- Möglicherweise müssen Sie Remotezugriff auf dem Server, oder erstellen eine Firewallregel, die eingehende Kommunikation mit SQL Server.

- Abhängig von der geplanten arbeitsauslastung müssen Sie den Server für den Machine learning-Aufgaben zu optimieren. 

## <a name="upgrades-or-uninstallation"></a>Upgrades oder deinstallieren

Dieser Abschnitt enthält detaillierte Anweisungen für bestimmte Szenarien für das Upgrade an.

Upgrades von einer Vorabversion von SQL Server 2016 R Services werden nicht mehr unterstützt. Es wird empfohlen, dass Sie die Vorabversion deinstallieren und installieren eine Releaseversion so bald wie möglich.

### <a name="support-for-slipstream-upgrades"></a>Unterstützung für Slipstream-Upgrades

Als Slipstream-Einrichtung wird die Möglichkeit bezeichnet, einen Patch oder ein Update auf eine fehlgeschlagene Installation einer Instanz anzuwenden, um vorhandene Probleme zu beheben. Der Vorteil dieser Methode ist, dass SQL Server gleichzeitig aktualisiert werden, dass Sie Setup ausführen, vermeiden einen separaten Neustart später.

Wenn der Server nicht über Internetzugriff verfügt, achten Sie darauf, dass Sie die SQL Server-Installationsprogramm herunterzuladen. Außerdem müssen Sie separat die entsprechenden Versionen der R-Komponenteninstaller herunterladen, *bevor* Sie mit dem Update beginnen. 

Speicherorte für den Download, finden Sie unter [Installieren von R-Komponenten ohne Internetzugang](installing-ml-components-without-internet-access.md).

Wenn alle Setupdateien in ein lokales Verzeichnis kopiert wurden, starten Sie das Setuphilfsprogramm, indem Sie „setup.exe“ in die Befehlszeile eingeben.

- Verwenden der */UpdateSource* Argument, um den Speicherort einer lokalen Datei anzugeben, die das SQL Server-Update, z. B. ein kumulatives Update oder Service Pack-Version enthält.

- Verwenden der */MRCACHEDIRECTORY* Argument, um den Ordner anzugeben, die die R-Komponente CAB-Dateien enthält.

Weitere Informationen finden Sie in diesem Blog durch das Supportteam von: [Bereitstellen von R Services auf Computern ohne Internetzugang](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/).

### <a name="upgrade-r-components-offline"></a>Aktualisieren von offline R-Komponenten

Installieren oder Aktualisieren von Servern, die nicht mit dem Internet verbunden sind, müssen Sie eine aktualisierte Version der R-Komponenten manuell herunterladen, bevor Sie mit die Aktualisierung beginnen. Weitere Informationen finden Sie unter [Installieren von R-Komponenten ohne Internetzugang](../../advanced-analytics/r-services/installing-ml-components-without-internet-access.md).

### <a name="schedule-for-update-of-r-components"></a>Zeitplan für das Update von R-Komponenten

Als Hotfixes oder Verbesserungen an SQL Server 2016 freigegeben werden, sind auch R-Komponenten aktualisiert oder aktualisiert, wenn die Instanz bereits die R-Services-Funktion enthält.

Bei Verwendung von SQL Server-2017 werden Upgrades auf R-Komponenten automatisch installiert.

Ab Dezember 2016 können Sie R-Komponenten für eine rasche als den Zyklus der SQL Server-Version aktualisieren. Zu diesem Zweck *Bindung* eine Instanz des R Services an der moderne Software Lifecycle-Richtlinie. Derzeit wird nur für ein Upgrade des 2016-Instanzen unterstützt. Wenn eine neue Version der R-Server veröffentlicht wird, werden Sie 2017 Instanzen als auch ein Upgrade ausführen können.

Weitere Informationen finden Sie unter [verwenden SqlBindR zum Aktualisieren einer Instanz von SQL Server R Services](../../advanced-analytics/r-services/use-sqlbindr-exe-to-upgrade-an-instance-of-r-services.md).

### <a name="upgrade-from-a-pre-release-version-of-sql-server-2016"></a>Upgrade von einer Vorabversion von SQL Server 2016

Direkte Upgrades werden im Allgemeinen nicht für alle Vorabversionen unterstützt.

Um erfolgreich R Services zu installieren, müssen Sie alle früheren Versionen von Deinstallieren [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] und die zugehörigen R-Komponenten. Hierzu zählen SQL Server 2016 CTP3, CTP3. 1, CTP3. 2, RC0 oder RC1.

Deinstallieren einer Vorabversion kann komplex sein und erfordern ein spezielles Skript ausführen. Technischen Support um Unterstützung zu erhalten.

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

Wenn Sie nur die geringste Möglichkeit haben, welche Version Sie verwenden, führen Sie `@@VERSION` aus SQL Server Management Studio.

### <a name="problems-with-setup-of-r-server-standalone"></a>Probleme mit der Installation von R Server (eigenständig)

In diesem Abschnitt werden Probleme, die spezifisch für Installationen von Microsoft R Server (eigenständig), mit denen SQL Server 2016-Setup beschrieben. Weitere allgemeine Probleme im Zusammenhang mit R-Server-Upgrades, finden Sie unter [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/) auf MSDN.

#### <a name="failure-to-install-localized-versions"></a>Fehler beim Installieren von lokalisierter Versionen

Wenn Sie R-Server offline installieren, lassen Vorabversionen nicht lokalisierte Sprachen verwenden.

In der Regel, wenn der Server nicht über Internetzugriff verfügt, muss vor dem Ausführen von Setup die Installationspakete für R-Server heruntergeladen werden. Dann geben Sie den Speicherort der Dateien während der Installation.

Wenn die Sprachen-ID zugeordneten das Installer-Paket nicht identisch mit der Sprache der SQL Server-Setup ist, tritt jedoch ein Problem auf. Wenn Sie die Seite für die R-Komponenteninstallation, erreichen den **Weiter** Schaltfläche ist deaktiviert, und Sie können nicht mit der Installation fortfahren. Dieses Problem zu umgehen können Sie das Paket, um ein übereinstimmender Bezeichner verwenden umbenennen.

Z. B. der Name der Installationspakete möglicherweise `SRO_3.2.2.0_1031.cab`.
Um das 104 Sprache auf SQL Server installieren möchten, benennen Sie die Datei zu `SRO_3.2.2.0_1041.cab`.

#### <a name="installing-r-services-and-r-server-standalone-on-the-same-computer"></a>Installieren von R Services und eigenständigen R-Server auf demselben computer

Im Allgemeinen Sie R Services (Datenbankintern) und R-Server (eigenständig) auf demselben Computer nicht installieren. Jedoch, wenn der Server über genügend Kapazität verfügt, kann eigenständigen R-Server als ein Entwicklungstool nützlich. Möglicherweise müssen auch die Funktionen operationalisierung von R-Server verwenden und R-Server ohne Verschieben von Daten SQL Server-Daten zugreifen.

Beachten Sie, dass bei der Installation von R-Server und R Services auf demselben Computer zwei separate Kopien derselben R-Bibliotheken installiert sind. Eine für die Verwendung von SQL Server-Instanz, und eine für die Entwicklung verwenden oder R-Server ist.

In früheren Versionen von SQL Server 2016 kann das Installieren von R Server (eigenständig) und R Services (Datenbankintern) zur gleichen Zeit mit der Fehlermeldung "Zugriff verweigert" Fehler beim Setup führen. Dieses Problem wurde in Service Pack 1 für SQL Server 2016 behoben.

Wenn Sie diesen Fehler und diese Funktionen zu aktualisieren müssen, führen Sie eine Slipstream-Installation von SQL Server 2016 mit SP1. Es gibt zwei Möglichkeiten zum Beheben des Problems, die beides erforderlich, deinstallieren und neu installieren.

1. Deinstallieren Sie R Services (Datenbankintern), und stellen Sie sicher, dass die Benutzerkonten für SQLRUserGroup entfernt werden.

2. Starten Sie den Server neu, und installieren Sie R-Server (eigenständig).

3. Ausführen von SQL Server setup einmal, und wählen Sie dieses Mal **Hinzufügen von Funktionen zu einer vorhandenen SQL Server**.

4. Wählen Sie die Instanz, und wählen Sie dann die **R Services (Datenbankintern)** Option zum Hinzufügen.

In einigen Fällen kann diese Prozedur das Problem zu beheben. Wiederholen Sie dann die folgende problemumgehung:

1. Deinstallieren Sie R Services (Datenbankintern) und R-Server (eigenständig) gleichzeitig aus.

2. Entfernen Sie die lokalen Benutzerkonten (SQLRUserGroup).

3. Starten Sie den Server neu.

4. Führen Sie SQL Server-Setup, und fügen Sie nur die R-Services (Datenbankintern)-Funktion. Aktivieren Sie nicht **R Server (eigenständig)**.

## <a name="see-also"></a>Siehe auch

 [Erste Schritte mit SQL Server R Services](../r/getting-started-with-sql-server-r-services.md)

 [Erste Schritte mit Microsoft R Server eigenständige](../r/getting-started-with-microsoft-r-server-standalone.md)

