---
title: R-Pakete, die mit SQL Server installiert | Microsoft Docs
ms.custom: 
ms.date: 09/29/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 070e1776f0a9760742e933064be569818fe200b2
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="r-packages-installed-with-sql-server"></a>R-Pakete, die mit SQL Server installiert

In diesem Artikel wird beschrieben, die R-Pakete, die mit SQL Server installiert sind, und enthält Informationen zum Verwalten und Anzeigen von vorhandenen Paketen.

Dieser Artikel enthält auch Links zu Informationen zur Vorgehensweise beim Hinzufügen neuer Pakete für die Verwendung mit SQL Server.

**Gilt für:** SQL Server 2017 Machine Learning Services (Datenbankintern), SQL Server 2016 R Services (Datenbankintern)

## <a name="what-is-the-instance-library-and-where-is-it"></a>Was ist die Instanz-Bibliothek und, sofern diese sind?

Alle R-Lösung, die in SQL Server ausgeführt wird, können nur Pakete, die in der Standardeinstellung R-Bibliothek, die der Instanz zugeordneten installiert sind.

Bei der Installation von R-Funktionen in SQL Server befindet sich die R-Paket-Bibliothek in den instanzordner.

+ Standardinstanz *MSSQLSERVER* 

    SQLServer 2017:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library` 
    
    SQLServer 2016:`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`

+ Benannte Instanz *MyNamedInstance* 

    SQLServer 2017:`C:\Program Files\Microsoft SQL Server\MSSQL14.MyNamedInstance\R_SERVICES\library` 
    
    SQLServer 2016:`C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library`

Sie können die folgende Anweisung ausführen, um die Standardbibliothek für die aktuelle Instanz von R zu überprüfen.

```SQL
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```
## <a name="r-packages-installed-with-sql-server"></a>R-Pakete, die mit SQL Server installiert

Bei der Installation die Sprache "R" in SQL Server standardmäßig der R **Basis** Pakete installiert sind. Basis-Pakete enthalten Kernfunktionalität von Paketen bereitgestellt, z. B. `stats` und `utils`.

Installation von R in SQL Server 2016 und SQL Server-2017 enthält auch die **"revoscaler"** Pakets sowie verwandte verbesserten Pakete und Anbieter, die unterstützt remote rechenkontexte, streaming, parallele Ausführung Rx-Funktion und viele weitere Funktionen.

+ Einen Überblick über die erweiterten R-Funktionen finden Sie unter [zu Machine Learning-Server](https://docs.microsoft.com/r-server/what-is-microsoft-r-server)

+ Informationen zum Herunterladen der Bibliotheken "revoscaler" auf einem Clientcomputer installieren [Microsoft R-Client](https://docs.microsoft.com/r-server/r-client/what-is-microsoft-r-client)

## <a name="permissions-required-for-installing-r-packages"></a>Erforderliche Berechtigungen für die Installation von R-Pakete

Ein Administrator musste in SQL Server 2016 neue R-Pakete auf einer Instanz serverweit zu installieren. In SQL Server 2017 wurden neue Funktionen hinzugefügt, die dem Datenbankadministrator den Zugriff auf paketverwaltung an ausgewählte Benutzer zu delegieren zu gewähren.

In diesem Abschnitt werden die erforderlichen Berechtigungen zum Installieren und Verwalten von Paketen, je nach Version beschrieben.

+ SQL Server 2016 R Services (Datenbankintern)

    Um ein neues R-Paket auf einem Computer installieren, auf denen ausgeführt wird, ist [!INCLUDE [ssCurrent](..\..\includes\sscurrent-md.md)], benötigen Sie Administratorrechte auf dem Computer. Es ist die Aufgabe der Datenbankadministrator oder anderer Administrator auf dem Server, um sicherzustellen, dass alle erforderlichen Pakete installiert sind, auf die [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] Instanz.

    Wenn Sie nicht über Administratorrechte auf dem Computer, der als Host verfügen die [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] Instanz, Sie ermöglichen dem Administrator Informationen zum Installieren von R-Pakete und ermöglichen den Zugriff auf eine sichere paketrepository, in denen Pakete angefordert von Benutzer abgerufen werden können.

+ SQL Server 2017-Machine Learning-Dienste

    Diese Version enthält die Paket-Verwaltungsfunktionen, mit die Datenbankadministrator Paket Installationsrechte an ausgewählte Benutzer zu delegieren können. Wenn diese Funktion aktiviert wurde, fordern Sie, dass Sie der Datenbankadministrator in eines der neuen Paketrollen hinzufügen. Weitere Informationen finden Sie unter [paketverwaltung für SQL Server R](r-package-management-for-sql-server-r-services.md).

    Wenn Sie Administrator auf dem SQL Server-Instanz sind, können Sie neue Pakete werden installieren. Seien Sie sicher, dass die Standardbibliothek verwenden, die der Instanz zugeordnet ist. Pakete, die an anderen Speicherorten installiert können nicht ausgeführt werden, wenn von einer gespeicherten Prozedur aufgerufen. Alle R-Code, der ausgeführt wird, auch mithilfe der SQL Server als computekontext erfordert, dass Pakete in der Instanz-Bibliothek verfügbar ist.

+ R-Server (eigenständig)

    Sie benötigen Administratorrechte auf dem Computer zum neuen R-Pakete installieren.

+ Andere Client-Umgebungen

    Wenn Sie installieren ein neues R-Paket auf einem Computer, der als R-Arbeitsstation verwendet wird und der Computer führt **nicht** eine Instanz von [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] installiert, Sie benötigen Sie Administratorrechte für den Computer Installieren Sie das Paket an. Nachdem Sie das Paket installiert haben, können Sie es lokal ausführen.

## <a name="managing-or-viewing-installed-packages"></a>Verwalten von oder das Anzeigen von installierte Pakete

Es gibt mehrere Möglichkeiten, die Sie eine vollständige Liste der installierten Pakete abrufen können. Weitere Informationen finden Sie unter [zu bestimmen, welche Pakete in SQL Server installiert sind](determine-which-packages-are-installed-on-sql-server.md).
