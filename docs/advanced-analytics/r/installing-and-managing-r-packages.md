---
title: R-Pakete, die mit SQL Server installiert | Microsoft Docs
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 2783d4ce6ca9cd25b41c1e658f5e3bf2a4f05f24
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="r-packages-installed-with-sql-server"></a>R-Pakete, die mit SQL Server installiert

Dieser Artikel beschreibt die R-Pakete, die mit SQL Server installiert sind, wenn Sie installieren und Aktivieren von Machine Learning-Funktionen. Dieser Artikel beschreibt auch Informationen zum Verwalten und Anzeigen von vorhandenen Paketen oder Hinzufügen neuer Pakete mit einer SQL Server-Instanz.

**Gilt für:** SQL Server 2017 Machine Learning Services (Datenbankintern), SQL Server 2016 R Services (Datenbankintern)

## <a name="what-is-the-instance-library-and-where-is-it"></a>Was ist die Instanz-Bibliothek und, sofern diese sind?

Alle R-Lösung, die in SQL Server ausgeführt wird, können nur Pakete, die in der Standardeinstellung R-Bibliothek, die der Instanz zugeordneten installiert sind. Bei der Installation von R-Funktionen in SQL Server befindet sich die R-Paket-Bibliothek in den instanzordner.

+ Standardinstanz *MSSQLSERVER* 

    SQLServer 2017:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library` 
    
    SQLServer 2016:`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`

+ Benannte Instanz *MyNamedInstance* 

    SQLServer 2017:`C:\Program Files\Microsoft SQL Server\MSSQL14.MyNamedInstance\R_SERVICES\library` 
    
    SQLServer 2016:`C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library`

Sie können die folgende Anweisung ausführen, um die Standardbibliothek für die aktuelle Instanz von R zu überprüfen.

```sql
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

Alternatiely, können Sie die neue [RxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) Funktion, wenn das Ausführen von sp\_ausführen\_externen\_Skript direkt auf dem Zielcomputer installiert. Die Funktion kann nicht für Remoteverbindungen Bibliothekspfade zurück.

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
```

> [!NOTE]
> Wenn Sie die Bindung verwenden, die R-Komponenten in einer Instanz aktualisiert, können den Pfad zur Bibliothek Instanz ändern. Achten Sie darauf, um zu überprüfen, ob die Bibliothek von SQL Server verwendet wird.

## <a name="r-packages-installed-with-sql-server"></a>R-Pakete, die mit SQL Server installiert

Standardmäßig R **Basis** Pakete installiert sind. Basis-Pakete enthalten Kernfunktionalität von Paketen bereitgestellt, z. B. `stats` und `utils`.

Bei der Installation von R in SQL Server 2016 oder SQL Server-2017 werden immer beinhaltet die **"revoscaler"** Pakets sowie verwandte verbesserten Pakete und Anbieter, die unterstützt remote rechenkontexte, streaming, parallele Ausführung Rx-Funktion und viele weitere Funktionen. Um die RevoScaleR-Paket zu aktualisieren, verwenden Sie entweder Bindung nur Machine learning-Komponenten, aktualisieren oder gepatcht oder aktualisieren Sie die Instanz auf eine neuere Version von SQL Server.

+ Einen Überblick über die erweiterten R-Funktionen finden Sie unter [zu Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/what-is-microsoft-r-server)

+ Informationen zum Herunterladen der Bibliotheken "revoscaler" auf einem Clientcomputer installieren [Microsoft R-Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

## <a name="permissions-required-for-installing-r-packages"></a>Erforderliche Berechtigungen für die Installation von R-Pakete

Ein Administrator musste in SQL Server 2016 neue R-Pakete auf einer Instanz serverweit zu installieren. 

SQL Server-2017 eingeführte neue Features für Paketinstallation und Verwaltung:

+ Sie können R-Befehle von einem Remoteclient aus verwenden, zum Installieren der Pakete, die über private oder freigegebene Bereich. Diese Funktion erfordert entweder [Microsoft R Server](https://docs.microsoft.com/machine-learning-server/install/r-server-install) oder [Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), sowie der Dbo-Berechtigungen für die Instanz.
+ Neue Funktionen wurden hinzugefügt zur Unterstützung der paketverwaltung von Datenbankadministratoren ohne Verwendung von T-SQL. In Zukunft stellen diese Funktionen Datenbankadministratoren die Möglichkeit, die meisten Aspekte der paketverwaltung für privilegierte Benutzer zu delegieren.

In diesem Abschnitt werden die erforderlichen Berechtigungen zum Installieren und Verwalten von Paketen, je nach Version beschrieben.

+ SQL Server 2016 R Services (Datenbankintern)

    Um ein neues R-Paket auf einem Computer installieren, auf denen ausgeführt wird, ist [!INCLUDE [ssCurrent](..\..\includes\sscurrent-md.md)], benötigen Sie Administratorrechte auf dem Computer. Es ist die Aufgabe der Datenbankadministrator oder anderer Administrator auf dem Server, um sicherzustellen, dass alle erforderlichen Pakete installiert sind, auf die [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] Instanz.

    Wenn Sie nicht über Administratorrechte auf dem Computer, der als Host verfügen die [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] Instanz, Sie ermöglichen dem Administrator Informationen zum Installieren von R-Pakete und ermöglichen den Zugriff auf eine sichere paketrepository, in denen Pakete angefordert von Benutzer abgerufen werden können.

+ SQL Server 2017-Machine Learning-Dienste

    Wenn Sie Administrator auf dem SQL Server-Instanz sind, können Sie neue Pakete werden installieren. Seien Sie sicher, dass die Standardbibliothek verwenden, die der Instanz zugeordnet ist. Pakete, die an anderen Speicherorten installiert können nicht ausgeführt werden, wenn von einer gespeicherten Prozedur aufgerufen. Alle R-Code, der ausgeführt wird, auch mithilfe der SQL Server als computekontext erfordert, dass Pakete in der Instanz-Bibliothek verfügbar ist.

    Diese Version enthält auch einige neuen Funktionen zur Unterstützung von vereinfacht die paketverwaltung von von DBAs in einer späteren Version vorgesehen. Jetzt wird empfohlen, dass Sie weiterhin so installieren Sie R-Pakete auf einer Instanz serverweit.

+ R-Server (eigenständig)

    Sie benötigen Administratorrechte auf dem Computer zum neuen R-Pakete installieren.

+ Andere Client-Umgebungen

    Wenn Sie installieren ein neues R-Paket auf einem Computer, der als R-Arbeitsstation verwendet wird und der Computer führt **nicht** eine Instanz von [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] installiert, Sie benötigen Sie Administratorrechte für den Computer Installieren Sie das Paket an. Nachdem Sie das Paket installiert haben, können Sie es lokal ausführen.

## <a name="managing-or-viewing-installed-packages"></a>Verwalten von oder das Anzeigen von installierte Pakete

Es gibt mehrere Möglichkeiten, die Sie eine vollständige Liste der installierten Pakete abrufen können. Weitere Informationen finden Sie unter [zu bestimmen, welche Pakete in SQL Server installiert sind](determine-which-packages-are-installed-on-sql-server.md).
