---
title: Paket installieren, deinstallieren und synchronisieren | Microsoft Docs
ms.custom: 
ms.date: 04/12/2017
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
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 959282395d178a090a3d447769ced4dca8882f89
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---

# <a name="r-package-synchronization-for-sql-server"></a>Synchronisierung von R-Paket für SQLServer

SQL Server 2017 CTP 2.0 umfasst eine neue Funktion für die Synchronisierung von R-Paketen zu unterstützen, Sichern und Wiederherstellen von R-Paket-Sammlungen im Zusammenhang mit SQL Server-Datenbanken. Diese Funktion wird sichergestellt, dass komplexe Sätze von R-Pakete, die von Benutzern erstellt wurden, nicht verloren und problemlos wiederhergestellt werden können.  

In diesem Thema wird beschrieben, was bewirkt, dass die Paket-Synchronisierungsfunktion sowie zum Verwenden der `rxSyncPackages()` Funktion, um die folgenden Aufgaben ausführen:

+  Eine Liste der Pakete für eine gesamte SQL Server-Datenbank zu synchronisieren
+  %NDer-Pakete, die verwendet werden, indem ein einzelner Benutzer oder eine Gruppe von Benutzern

> [!NOTE]
> Diese Funktion dient als Teil der Vorabversion der Software und unterliegt Änderungen vor der endgültigen Version.

## <a name="what-is-package-synchronization"></a>Was ist Synchronisierung Paket 

Paketsynchronisierung ist eine neue Funktion, die speziell mit SQL Server-remotecomputekontexten. Es dient zum Abrufen einer Liste von R-Pakete, die auf eine bestimmte Datenbank, für einen bestimmten Benutzer oder Gruppe installiert sind, und stellen Sie sicher, dass die Pakete in der Datei System Übereinstimmung in der Datenbank aufgeführt. 

Dies ist hilfreich, wenn Sie zum Verschieben einer Benutzerdatenbank aus, und verschieben die Pakete zusammen mit der Datenbank benötigen. Sie können auch paketsynchronisierung beim Sichern und einer SQL Server-Datenbank, die für R-Aufträge verwendet wiederherstellen.

Paketsynchronisierung verwendet eine neue Funktion `rxSyncPackages()`. Um die Liste der Pakete zu synchronisieren, öffnen Sie eine R-Eingabeaufforderung, die computekontext, der definiert, die Instanz und die Datenbank, die Sie arbeiten möchten, übergeben werden und geben Sie dann einen Paketbereich oder einen Benutzer oder Besitzer an. 

### <a name="how-packages-are-managed-in-r-and-sql-server"></a>Wie Pakete in R und SQL Server verwaltet werden.

Beim Ausführen von R-Skripts, die mit R-Standardtools sind in der Regel R-Pakete im Dateisystem installiert. Wenn mehrere Personen R auf dem gleichen Computer verwenden, können viele Kopien der gleichen Pakete, in anderen Ordnern oder in anderer benutzerbibliotheken vorhanden sein.

Allerdings muss für die Verwendung von SQL Server ein R-Paket das Paket werden in der Standardeinstellung R-Bibliothek installiert, die der Instanz zugeordnet ist. Ein Servercomputer kann mehrere Instanzen von SQL Server mit R aktiviert hostet, und jede Instanz kann in diesem Fall einen separaten Satz von R-Pakete aufweisen. 

Der Datenbankadministrator ist verantwortlich für die Installation von Paketen auf der Instanz. Allerdings kann der Administrator mit den Verwaltungsbibliotheken Paket dieser Verantwortung für Benutzer delegieren. 

+ Für jede Datenbank kann der Administrator Benutzern die Möglichkeit, kostenlos die R-Pakete installieren, die sie benötigen. Dieser Mechanismus wird sichergestellt, dass mehrere Benutzer verschiedene Versionen der R-Pakete installieren können, ohne dass Konflikte für andere Benutzer des Computers mit SQL Server. Einzelne Benutzer können Installationspakete für ihre eigenen Zwecke mit einem Speicherort im Dateisystem als gekennzeichnet **private**, wenn sie für die Datenbankrolle gehören **Rpkgs Private**.

+ Der Administrator kann eine Gruppe von Benutzern von Paket in einer Datenbank einrichten und Installationspakete, mit denen in der Gruppe von allen Benutzern gemeinsam verwendet werden. Pakete können freigegeben werden, zwischen den Mitgliedern der Datenbankrolle **Rpkgs freigegebene**. Solche Benutzer können auch Pakete an privaten Bereich installieren. 

### <a name="goal-of-package-synchronization"></a>Ziel des paketsynchronisierung

Wenn eine Datenbank auf einem Server verloren gegangen ist oder muss, verschoben werden mithilfe der paketsynchronisierung können Sie eine Datenbank, Benutzer oder Gruppe Sätze von Paketen, die bestimmte wiederherstellen. 

Die Informationen zu Benutzern und die Pakete, die sie installiert haben in der SQL Server-Instanz gespeichert und wird verwendet, um die Pakete im Dateisystem zu aktualisieren. Wenn Sie ein neues Paket mit den Paket-Management-Funktionen hinzufügen, werden beide Datensätze in SQL Server und dem Dateisystem aktualisiert. Deshalb, wenn ein Benutzer auf einen anderen SQL Server verschoben wird, können Sie erstellen Sie eine Sicherung der Datenbank für den Benutzer arbeiten und auf den neuen Server wiederherstellen und die Pakete für den Benutzer in das Dateisystem auf dem neuen Server gemäß der r installiert werden soll


### <a name="supported-versions"></a>Unterstützte Versionen

Diese Funktion ist in SQL Server 2017 CTP 2.0 enthalten.

Da diese Funktion von Microsoft R Version 9.1.0 gehört, können Sie diese Funktion mit einer Instanz von SQL Server 2016 hinzufügen, durch ein Upgrade der Instanz um die neueste Version von Microsoft R. verwenden Weitere Informationen finden Sie unter [verwenden SqlBindR.exe zum Upgrade von SQL Server R Services](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="to-synchronize-packages"></a>Um Pakete zu synchronisieren.

Rufen Sie `rxSyncPackages` nach einer Instanz von SQL Server auf einen neuen Computer wiederherstellen, oder wenn eine R-im Dateisystem Paket ist anscheinend beschädigt.

Wenn der Befehl erfolgreich ausgeführt wird, werden die Datenbank, Bereich und Besitzer wie die angegebene vorhandene Pakete im Dateisystem hinzugefügt. Wenn das Dateisystem beschädigt ist, werden die Pakete Restred anhand der Liste, die in der Datenbank verwaltet.

### <a name="syntax"></a>Syntax
`rxSyncPackages(computeContext = rxGetOption("computeContext"),  scope = c("shared", "private"), owner = c(), verbose = getOption("verbose"))`

+ Computekontext

    Definieren Sie einen SQL Server-computekontext, bestehend aus einer Instanz und Datenbank und die Pakete zu synchronisieren. Erstellen Sie den Serverkontext SQ mithilfe der `RxInSqlServer` Funktion. Wenn Sie einen computekontext angeben, wird der aktuellen computekontext verwendet. 

+ Scope

  Geben Sie, ob die Installation der Pakete für einen einzelnen Benutzer oder für eine Gruppe von Benutzern: 

    + **private** der Vorgang umfasst nur die Pakete, die für die Verwendung von einem angegebenen Besitzer installiert wurden.
    + **freigegebene** der Oepration schließt alle Pakete, die für eine Gruppe von Benutzern installiert. 

  Wenn Sie die Funktion ausführen, ohne dass private oder freigegebene Bereich, werden beide Bereiche angewendet. Daher wird der gesamte Satz von Paketen verfügbar für alle Bereiche und Benutzer kopiert werden.

+ Besitzer 

    Geben Sie den Besitzer der Pakete zu synchronisieren. Den Namen des Besitzers muss ein gültiger Benutzer der SQL-Datenbank. Wenn Sie sie leer lassen, wird der Benutzername, der in der Verbindung angegebenen SQL-Anmeldung verwendet.


### <a name="requirements"></a>Anforderungen

+ Die Person, die die Funktion ausführt, muss ein Sicherheitsprinzipal für den SQL Server-Instanz und die Datenbank, die die Pakete und muss ein Mitglied einer Rolle für die Paket: **Rpkgs freigegebene** oder **Rpkgs Private** 
  + Pakete, die als gekennzeichnete synchronisiert **freigegebenen**, benötigen die Person, die die Funktion ausgeführt wird die Mitgliedschaft der **Rpkgs freigegebene** Rolle und die Pakete, die verschoben werden installiert werden müssen an einen freigegebenen Bereichs-Bibliothek.
  + Zum Synchronisieren-Pakete, die als gekennzeichnete **private**, entweder der Besitzer des Pakets oder der Administrator muss die Funktion ausgeführt, und die Pakete müssen privat sein.
+ **Rpkgs Benutzer** -Mitglieder dieser Rolle Ausführen von Code, der auf der SQL Server-Instanz installierte Pakete verwendet, jedoch kann nicht installieren und Pakete synchronisieren können.
+ Um Pakete im Auftrag anderer Benutzer zu synchronisieren, muss der Besitzer Mitglied der **Db_owner** -Datenbankrolle.

## <a name="examples"></a>Beispiele

In den folgenden Beispielen erstellen Sie eine Verbindung mit einer bestimmten Instanz von SQL Server, geben Sie eine Datenbank, und geben Sie einen Satz von Paketen zu synchronisieren. 

Wenn der Aufruf von `rxSyncPackages` vorgenommen werden, wird das Paket aufgeführt werden zwischen dem Dateisystem und die Datenbank synchronisiert. 

### <a name="synchronize-all-by-database"></a>Alle von der Datenbank zu synchronisieren

In diesem Beispiel ruft alle Pakete, die in der Datenbank [TestDB] installiert. Da kein Besitzer spezifisch ist, enthält die Liste alle Pakete, die für private und freigegebene Bereiche installiert wurden.

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="restrict-synchronized-packages-by-scope"></a>Synchronisierte Pakete durch den Bereich einschränken 

Die folgenden Beispiele %nDer nur die Pakete im freigegebenen Bereich oder privaten Bereich.

**Freigegebener Bereich**

```R
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)
```

**Privater Bereich**

```R
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="restrict-synchronized-packages-by-owner"></a>Synchronisierte Pakete vom Besitzer zu beschränken 

Im folgenden Beispiel wird veranschaulicht, wie nur die installierten Pakete für einen bestimmten Benutzer abrufen. In diesem Beispiel wird der Benutzer durch den SQL-Anmeldenamen, identifiziert *"user1"*.

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="see-also"></a>Siehe auch

[R-Paketverwaltung für SQLServer](../r/r-package-management-for-sql-server-r-services.md)
