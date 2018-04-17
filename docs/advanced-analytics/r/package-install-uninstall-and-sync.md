---
title: Synchronisierung von R-Paket für SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6e0fe3fa36a5a330e1b4fee926c0d2e4b10d809f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="r-package-synchronization-for-sql-server"></a>Synchronisierung von R-Paket für SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Die Version von "revoscaler" in SQL Server-2017 enthalten bietet die Möglichkeit zum Synchronisieren von Auflistungen von R-Pakete zwischen dem Dateisystem und die Instanz und Datenbank, in denen Pakete verwendet werden.

Dieses Feature wurde bereitgestellt, um R-Paket-Sammlungen im Zusammenhang mit SQL Server-Datenbanken sichern zu vereinfachen. Mit dieser Funktion kann Administrator wiederherstellen, nicht nur die Datenbank, jedoch R-Pakete, die von Datenanalysten Arbeit in dieser Datenbank verwendet wurden.

Dieser Artikel beschreibt die Synchronisierungsfunktion Paket sowie zum Verwenden der [RxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) Funktion, um die folgenden Aufgaben ausführen:

+ Eine Liste der Pakete für eine gesamte SQL Server-Datenbank zu synchronisieren

+ Synchronisieren von Paketen, die verwendet werden, indem ein einzelner Benutzer oder eine Gruppe von Benutzern

+ Wenn ein Benutzer auf einen anderen SQL-Server verschoben werden, Sie erstellen Sie eine Sicherung der Benutzerdatenbank arbeiten und auf den neuen Server wiederherstellen können, und die Pakete für den Benutzer in das Dateisystem auf dem neuen Server gemäß der r installiert werden soll

Sie können z. B. paketsynchronisierung in diesen Szenarien verwenden:

+ Der Datenbankadministrator hat eine Instanz von SQL Server auf einem neuen Computer wiederhergestellt, und fordert die Benutzer eine Verbindung mit ihren R-Clients und führen `rxSyncPackages` zu aktualisieren, und stellen die Pakete wieder her.

+ Sie denken, ein R-Paket im Dateisystem beschädigt ist, damit Sie ausführen `rxSyncPackages` auf dem SQL Server.

## <a name="requirements"></a>Anforderungen

Bevor Sie paketsynchronisierung verwenden können, müssen Sie die entsprechende Version von Microsoft R "oder" Machine Learning-Server haben. Diese Funktion wird in Microsoft R Version 9.1.0 oder höher bereitgestellt werden. 

Außerdem müssen Sie aktivieren die [Verwaltungsfeature Paket](r-package-how-to-enable-or-disable.md) auf dem Server.

### <a name="determine-whether-your-server-supports-package-management"></a>Bestimmen Sie, ob der Server, paketverwaltung unterstützt

Diese Funktion ist in SQL Server 2017 CTP 2 oder höher verfügbar.

Sie können dieses Feature mit einer Instanz von SQL Server 2016 hinzufügen, indem Sie ein Upgrade der Instanz um die neueste Version von Microsoft R. verwenden Weitere Informationen finden Sie unter [verwenden SqlBindR.exe so aktualisieren Sie SQL Server R Services](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

### <a name="enable-the-package-management-feature"></a>Aktivieren Sie die Paket-Management-Funktion

Verwendung von paketsynchronisierung erfordert, dass das neue Paket-Feature für die SQL Server-Instanz, und klicken Sie auf einzelne Datenbanken aktiviert werden. Weitere Informationen finden Sie unter [aktivieren oder Deaktivieren der paketverwaltung für SQL Server](r-package-how-to-enable-or-disable.md).

1. Der Serveradministrator aktiviert die Funktion für SQL Server-Instanz.
2. Für jede Datenbank erteilt der Administrator einzelne Benutzer die Möglichkeit zum Installieren oder Freigeben von R-Pakete mithilfe von Datenbankrollen.

Nachdem dies geschehen ist, können Sie RevoScaleR-Funktionen, wie z. B. [RxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) Pakete in einer Datenbank zu installieren.  Informationen zu Benutzern und die Pakete, die sie verwenden können, wird in der SQL Server-Instanz gespeichert. 

Wenn Sie ein neues Paket mit den Paket-Management-Funktionen hinzufügen, werden beide Datensätze in SQL Server und dem Dateisystem aktualisiert. Diese Informationen können verwendet werden, die Paketinformationen für die gesamte Datenbank wiederherstellen.

### <a name="permissions"></a>Berechtigungen

+ Die Person, die die Paket-Synchronisierung-Funktion ausführt, muss ein Sicherheitsprinzipal auf dem SQL Server-Instanz und die Datenbank, die die Pakete gespeichert sind.

+ Der Aufrufer der Funktion muss ein Mitglied einer dieser Rollen der Paket-Management: **Rpkgs freigegebene** oder **Rpkgs Private**.

+ Pakete, die als gekennzeichnete synchronisiert **freigegebenen**, benötigen die Person, die die Funktion ausgeführt wird die Mitgliedschaft der **Rpkgs freigegebene** Rolle und die Pakete, die verschoben werden installiert werden müssen an einen freigegebenen Bereichs-Bibliothek.

+ Pakete, die als gekennzeichnete synchronisiert **private**, entweder der Besitzer des Pakets oder der Administrator muss die Funktion ausgeführt, und die Pakete müssen privat sein.

+ Um Pakete im Auftrag anderer Benutzer zu synchronisieren, muss der Besitzer Bhe ein Mitglied der **Db_owner** -Datenbankrolle.

## <a name="how-package-synchronization-works"></a>Funktionsweise von paketsynchronisierung

Rufen Sie zum Verwenden von paketsynchronisierung [RxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages), dies ist eine neue Funktion in ["revoscaler"](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler). 

Für jeden Aufruf von `rxSyncPackages`, müssen Sie eine SQL Server-Instanz und Datenbank angeben. Entweder Sie dann die Liste der Pakete zu synchronisieren, oder geben Sie Paketbereich.

1. Erstellen Sie die SQL Server-computekontext mithilfe der `RxInSqlServer` Funktion. Wenn Sie einen computekontext angeben, wird der aktuellen computekontext verwendet.

2. Geben Sie den Namen einer Datenbank, für die Instanz in der angegebenen computekontext. Pakete werden pro Datenbank synchronisiert.

3. Geben Sie die Pakete zu synchronisieren, indem Sie mit dem Bereichsargument.

    Bei Verwendung von **private** Bereich nur Pakete, die im Besitz von dem angegebenen Besitzer werden synchronisiert. Bei Angabe von **freigegebenen** Bereich, alle privaten Pakete in der Datenbank synchronisiert werden. 
    
    Wenn Sie die Funktion ausführen, ohne entweder **private** oder **freigegebenen** Bereich, alle Pakete werden synchronisiert.

4. Wenn der Befehl erfolgreich ist, werden vorhandene Pakete im Dateisystem mit dem angegebenen Bereich und der Besitzer der Datenbank hinzugefügt.

    Wenn das Dateisystem beschädigt ist, werden die Pakete basierend auf der Liste, die in der Datenbank beibehaltene wiederhergestellt.

    Wenn das Paket-Feature nicht in der Zieldatenbank verfügbar ist, wird ein Fehler ausgelöst: "die Paket-Verwaltungsfunktion entweder nicht auf dem SQLServer aktiviert, oder die Version zu alt ist"

### <a name="example-1-synchronize-all-package-by-database"></a>Beispiel 1. Synchronisieren Sie alle Paket von der Datenbank

In diesem Beispiel ruft keine neuen Pakete aus dem lokalen Dateisystem und die Pakete werden in der Datenbank [TestDB] installiert. Da kein Besitzer spezifisch ist, enthält die Liste alle Pakete, die für private und freigegebene Bereiche installiert wurden.

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="example-2-restrict-synchronized-packages-by-scope"></a>Beispiel 2. Synchronisierte Pakete durch den Bereich einschränken

In den folgenden Beispielen synchronisieren nur die Pakete im angegebenen Bereich.

```R
#Shared scope
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)

#Private scope
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="example-3-restrict-synchronized-packages-by-owner"></a>Beispiel 3. Synchronisierte Pakete vom Besitzer zu beschränken

Im folgenden Beispiel wird veranschaulicht, wie nur die Pakete zu synchronisieren, die für einen bestimmten Benutzer installiert wurden. In diesem Beispiel wird der Benutzer durch den SQL-Anmeldenamen, identifiziert *"user1"*.

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="related-resources"></a>Verwandte Ressourcen

[R-Paketverwaltung für SQL Server](r-package-management-for-sql-server-r-services.md)
