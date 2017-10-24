---
title: "Synchronisierung von R-Paket für SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 10/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: ed7dbf99b0f492b5ca8879bb67a7256fdfae3306
ms.contentlocale: de-de
ms.lasthandoff: 10/10/2017

---

# <a name="r-package-synchronization-for-sql-server"></a>Synchronisierung von R-Paket für SQL Server

SQL Server-2017 bietet die Möglichkeit zum Synchronisieren von Auflistungen von R-Pakete zwischen dem Dateisystem und die Instanz und Datenbank, in denen Pakete verwendet werden.
Dieses Feature wurde bereitgestellt, um R-Paket-Sammlungen im Zusammenhang mit SQL Server-Datenbanken sichern zu vereinfachen. Mit dieser Funktion kann Administrator wiederherstellen, nicht nur die Datenbank, jedoch R-Pakete, die von Datenanalysten Arbeit in dieser Datenbank verwendet wurden.

In diesem Thema wird beschrieben, die Synchronisierungsfunktion Paket sowie zum Verwenden der [RxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages) Funktion, um die folgenden Aufgaben ausführen:

+ Eine Liste der Pakete für eine gesamte SQL Server-Datenbank zu synchronisieren

+ Synchronisieren von Paketen, die verwendet werden, indem ein einzelner Benutzer oder eine Gruppe von Benutzern

+ Wenn ein Benutzer auf einen anderen SQL-Server verschoben werden, Sie erstellen Sie eine Sicherung der Benutzerdatenbank arbeiten und auf den neuen Server wiederherstellen können, und die Pakete für den Benutzer in das Dateisystem auf dem neuen Server gemäß der r installiert werden soll

Sie können z. B. paketsynchronisierung in diesen Szenarien verwenden:

+ Der Datenbankadministrator hat eine Instanz von SQL Server auf einem neuen Computer wiederhergestellt, und fordert die Benutzer eine Verbindung mit ihren R-Clients und führen `rxSyncPackages` zu aktualisieren, und stellen die Pakete wieder her.

+ Sie denken, ein R-Paket im Dateisystem beschädigt ist, damit Sie ausführen `rxSyncPackages` auf dem SQL Server.

## <a name="requirements"></a>Anforderungen

Bevor Sie die paketsynchronisierung verwenden können, Sie benötigen die entsprechende Version von Microsoft R und die zugehörige Datenbank-Funktion aktiviert haben.

### <a name="determine-whether-your-server-supports-package-management"></a>Bestimmen Sie, ob der Server, paketverwaltung unterstützt

Diese Funktion ist in SQL Server 2017 CTP 2 oder höher verfügbar.

Da diese Funktion in Microsoft R Version 9.1.0 R-Funktionen verwendet, können Sie diese Funktion mit einer Instanz von SQL Server 2016 hinzufügen, mit dem Upgrade der Instanz, um die neueste Version von Microsoft R. verwenden Weitere Informationen finden Sie unter [verwenden SqlBindR.exe zum Upgrade von SQL Server R Services](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

### <a name="enable-the-package-management-feature"></a>Aktivieren Sie die Paket-Management-Funktion

Verwendung der paketsynchronisierung erfordert, dass der neue Features für Paket auf SQL Server-Instanz, und klicken Sie auf einzelne Datenbanken, die zum Ausführen von R-Aufgaben verwendet.

1. Der Serveradministrator aktiviert die Funktion für SQL Server-Instanz.
2. Für jede Datenbank erteilt der Administrator Benutzer die Möglichkeit zum Installieren oder Freigeben von R-Pakete.

Nachdem dies geschehen ist, werden Informationen zu Benutzern und die Pakete, die sie installiert haben in der SQL Server-Instanz gespeichert. Diese Informationen kann dann angewendet werden, um die R-Pakete im Dateisystem zu aktualisieren.

Wenn Sie ein neues Paket mit den Paket-Management-Funktionen hinzufügen, werden beide Datensätze in SQL Server und dem Dateisystem aktualisiert.

> [!NOTE]
> Paketsynchronisierung können Sie R-Pakete die traditionelle installiert haben mithilfe von R-Tools zum Installieren der Pakete direkt in das Dateisystem keine.
### <a name="permissions"></a>Berechtigungen

+ Die Person, die die Paket-Synchronisierung-Funktion ausführt, muss ein Sicherheitsprinzipal auf dem SQL Server-Instanz und die Datenbank, die die Pakete gespeichert sind.

+ Der Aufrufer der Funktion muss ein Mitglied einer dieser Rollen der Paket-Management: **Rpkgs freigegebene** oder **Rpkgs Private**.

+ Pakete, die als gekennzeichnete synchronisiert **freigegebenen**, benötigen die Person, die die Funktion ausgeführt wird die Mitgliedschaft der **Rpkgs freigegebene** Rolle und die Pakete, die verschoben werden installiert werden müssen an einen freigegebenen Bereichs-Bibliothek.

+ Pakete, die als gekennzeichnete synchronisiert **private**, entweder der Besitzer des Pakets oder der Administrator muss die Funktion ausgeführt, und die Pakete müssen privat sein.

+ Um Pakete im Auftrag anderer Benutzer zu synchronisieren, muss der Besitzer Mitglied der **Db_owner** -Datenbankrolle.

## <a name="how-package-synchronization-works"></a>Funktionsweise von paketsynchronisierung

Rufen Sie zum Verwenden von paketsynchronisierung [RxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages), dies ist eine neue Funktion in ["revoscaler"](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler). Rufen Sie diese Funktion von SQL Server mithilfe von Sp_execute_external_script, oder Sie können von einem Remoteclient von R ausgeführt und geben Sie die SQL Server-computekontext. 

Da Pakete, auf der Datenbankebene für jeden Aufruf von verwaltet werden `rxSyncPackages`, geben Sie eine SQL Server-Instanz und Datenbank, und klicken Sie dann Pakete aufzulisten, oder geben Paketbereich.

1. Erstellen Sie die SQL Server-computekontext mithilfe der `RxInSqlServer` Funktion. Wenn Sie einen computekontext angeben, wird der aktuellen computekontext verwendet.

2. Geben Sie den Namen einer Datenbank, für die Instanz in der angegebenen computekontext. Pakete werden pro Datenbank verwaltet.

3. Liste der Pakete zu synchronisieren.

4.  Verwenden Sie optional die *Bereich* Argument, um anzugeben, ob Sie die Pakete für einen einzelnen Benutzer oder für eine Gruppe von Benutzern synchronisieren. Wenn Sie die Funktion ausführen, ohne entweder **private** oder **freigegebenen** Bereich, den gesamten Satz von Paketen, die für alle Bereiche und Benutzer kopiert werden.

Wenn der Befehl erfolgreich ausgeführt wird, werden vorhandene Pakete im Dateisystem mit dem angegebenen Bereich und der Besitzer der Datenbank hinzugefügt. Wenn das Dateisystem beschädigt ist, werden die Pakete basierend auf der Liste, die in der Datenbank beibehaltene wiederhergestellt.

### <a name="example-1-synchronize-all-package-by-database"></a>Beispiel 1. Synchronisieren Sie alle Paket von der Datenbank

In diesem Beispiel ruft alle Pakete, die in der Datenbank [TestDB] installiert. Da kein Besitzer spezifisch ist, enthält die Liste alle Pakete, die für private und freigegebene Bereiche installiert wurden.

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

Im folgenden Beispiel wird veranschaulicht, wie nur die installierten Pakete für einen bestimmten Benutzer abrufen. In diesem Beispiel wird der Benutzer durch den SQL-Anmeldenamen, identifiziert *"user1"*.

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

### <a name="example-4-restrict-synchronized-packages-by-owner"></a>Beispiel 4. Synchronisierte Pakete vom Besitzer zu beschränken

Im folgende Beispiel synchronisiert die Pakete installiert, die im Dateisystem mit der Liste der Pakete, die in der Datenbank verwaltet. Wenn ein Paket nicht vorhanden ist, wird es im Dateisystem installiert.

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

## <a name="related-resources"></a>Verwandte Ressourcen

[R-paketverwaltung für SQL Server](r-package-management-for-sql-server-r-services.md)

