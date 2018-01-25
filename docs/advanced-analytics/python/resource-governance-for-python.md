---
title: "Die Ressourcenkontrolle für Python | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 10760026ef04284f6d0838af8ba81b0c7613645b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="resource-governance-for-python"></a>Die Ressourcenkontrolle für Python

Da Python, über aktiviert ist die die gleichen erweiterbarkeitsarchitektur, die für die Sprache "R" in SQL Server 2016 implementiert wurde, können Sie vorhandene Tools in SQL Server z. B. der Ressourcenkontrolle und DMVs erweiterter Ereignisse, die Ausführung von Python überwachen Skripts in SQL Server.

Die Ressourcenkontrolle ist insbesondere wichtig, da große Mengen von Daten in der Produktion analysieren selbst fortschrittliche Hardware steuern kann.  Um zu verhindern, dass Daten außerhalb der Datenbank verschoben wird, die auf Computern, die nicht verwaltet oder überwacht werden können, ist es wichtig, dass der Datenbankadministrator genügend Ressourcen für erweiterte Analysen Vorgänge zuweisen.

Dieser Abschnitt enthält Informationen zum Verwalten von Ressourcen, die von der Python-Laufzeit verwendet, und Überwachen der Verwendung von Ressourcen, die von Python-Skripts Aufträge der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz.

> [!NOTE]
> Python-Unterstützung ist ein neues Feature in SQL Server-2017 und befindet sich in der Vorabversion. Weitere Informationen schnell finden.
> Im Allgemeinen können Sie externes Skript überwachen, einschließlich eines, das Python ausgeführt wird, mithilfe des gleichen Frameworks, die für die Ressourcenkontrolle von R-Skripts in SQL Server 2016 bereitgestellt wurde.

## <a name="what-is-resource-governance"></a>Was ist die Ressourcenkontrolle?

Die Ressourcenkontrolle dient dem Identifizieren und Verhindern von Problemen, die häufig in einer Datenbankserverumgebung auftreten, in der sich oft mehrere abhängige Programme befinden und mehrere Dienste unterstützt und ausgeglichen werden müssen. Für [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] beinhaltet die Ressourcenkontrolle folgende Aufgaben:  

+ **Identifizieren von Skripts, die übermäßig viele Ressourcen**. Der Administrator muss in der Lage sein, Aufträge zu beenden oder einzuschränken, die zu viele Ressourcen in Anspruch nehmen.

+ **Abhilfe unvorhersehbare Arbeitslasten**. Wenn mehrere Python-Aufträge auf dem Server gleichzeitig ausgeführt werden, und die Aufträge mithilfe von Ressourcenpools nicht voneinander isoliert sind, kann der resultierende Ressourcenkonflikt zu unvorhersehbare Leistung führen oder bedrohen Abschluss der arbeitsauslastung.

+ **Priorisierung von Arbeitslasten**. Der Administrator oder Architekt muss Arbeitsauslastungen festlegen können, die Vorrang haben, oder garantieren können, dass bei einem Ressourcenkonflikt bestimmte Arbeitsauslastungen abschließen.

Sie können [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) , die von externen Laufzeiten verwendeten Ressourcen zu verwalten. Dies schließt die Python-Skripts, die über eine Remote-terminal jedoch mithilfe von SQL Server-Computers als computekontext ausgeführten gestartet werden.

> [!NOTE] 
> Die Ressourcenkontrolle ist in der Enterprise Edition verfügbar.

## <a name="how-to-use-resource-governor-to-manage-python-execution"></a>Verwendung der Ressourcenkontrolle zum Verwalten von Python-Ausführung

Im Allgemeinen Verwalten von Ressourcen, die einen beliebigen Auftrag externes Skript zugeordnet sind, durch das Erstellen einer *externen Ressourcenpool* und Pools Arbeitslasten zuweisen. Ein externen Ressourcenpool ist eine neue Art von Ressourcenpools in SQL Server 2016 zur Verwaltung von R-Laufzeitmoduls und anderen Prozessen, die mit dem Datenbankmodul externe eingeführt. Es kann verwendet werden, beginnend mit SQL Server-2017 Python-Aufträge zu überwachen.

Es gibt drei Arten von Standard-Ressourcenpools hinzu:

+ Der *interne Pool* stellt die Ressourcen dar, die von SQL Server selbst verwendet werden, und kann nicht geändert oder eingeschränkt werden.
+ Der *Standardpool* ist ein vordefinierter Benutzerpool, den Sie verwenden können, um die Ressourcenverwendung für den Server als Ganzes zu ändern. Sie können auch Benutzergruppen definieren, die zu diesem Pool gehören, um den Zugriff auf Ressourcen zu verwalten.
+ Der *externe Standardpool* ist ein vordefinierter Benutzerpool für externe Ressourcen. Des Weiteren können Sie neue externe Ressourcenpools erstellen und Benutzergruppen definieren, die zu diesem Pool gehören.

Darüber hinaus können Sie *benutzerdefinierte Ressourcenpools* erstellen, um Ressourcen dem Datenbankmodul oder anderen Anwendungen zuzuweisen, sowie *benutzerdefinierte externe Ressourcenpools* erstellen, um R und andere externe Prozesse zu verwalten.

Eine gute Einführung in die Terminologie und allgemeinen Konzepte finden Sie unter [Ressourcenpool für die Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-resource-pool.md).

## <a name="resource-management-using-resource-governor"></a>Ressourcenmanagement mit dem Resource Governor

Wenn Sie mit dem Resource Governor noch nicht vertraut sind, finden Sie eine kurze exemplarische Vorgehensweise zum Ändern der Standardressourcen einer Instanz und zum Erstellen eines neuen externen Ressourcenpools unter [Vorgehensweise: Erstellen eines Ressourcenpools für R](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md).

Sie können die *externen Ressourcenpool* Mechanismus zum Verwalten von Ressourcen der folgenden unterstützten ausführbare Dateien:

+ Python35.exe beim Aufruf von SQL Server oder Remote mit SQL Server als remote computekontext
+ BxlServer.exe und Satellitenprozesse
+ Startprogramme von Launchpad, z. B. PythonLauncher.dll gestartet

> [!NOTE]
> Die direkte Verwaltung den Launchpad-Dienst mithilfe der Ressourcenkontrolle wird nicht unterstützt. Das liegt daran, dass [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] ein vertrauenswürdiger Dienst ist, der so entworfen wurde, dass er nur Startprogramme hostet, die von Microsoft bereitgestellt werden. Vertrauenswürdige Startprogramme sind auch dafür konfiguriert, übermäßigen Ressourcenverbrauch zu vermeiden.

Es wird empfohlen, Satellitenprozesse mit dem Resource Governor zu verwalten und sie entsprechend den Bedürfnissen der individuellen Datenbankkonfiguration und Arbeitsauslastung zu optimieren.  Zum Beispiel kann jeder einzelne Satellitenprozess während der Ausführung bei Bedarf erstellt oder gelöscht werden.

## <a name="disable-or-enable-external-script-execution"></a>Deaktivieren oder Aktivieren der externen Skriptausführung

Unterstützung für externe Skripts ist optional, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einrichten und sogar nachdem Setup abgeschlossen, externen skriptausführung wird ist aus Sicherheitsgründen standardmäßig auf OFF festgelegt. Aus diesem Grund müssen Sie nach Abschluss der Installation von einer der Machine learning Sprachen und zugehöriger Dienste konfigurieren Sie die Instanz explizit neu und dann neu starten den Datenbankmodul-Dienst.

Im Falle unkontrollierter Skripts können Sie die Ausführung des Skripts deaktivieren. Nur dieser Prozess umgekehrt, und legen Sie die Eigenschaft `external scripts enabled` auf "false", oder 0, für die Instanz. Dadurch werden alle externen skriptausführung sofort deaktiviert. Reservieren Sie diese Option bei Sicherheitsproblemen mit oder Situationen, in denen ein Administrator muss Ressourcenprobleme sofort zu mindern.

## <a name="see-also"></a>Siehe auch

[Ressourcenpool für die Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-resource-pool.md)

