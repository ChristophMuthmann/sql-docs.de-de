---
title: Vermeiden von Fehlern in R-Paketen in benutzerbibliotheken installiert | Microsoft Docs
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 99ffd9b8-aa6d-4ac2-9840-4e66d0463978
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 0de06ebee16d903b4b00c9d8e4673bf450c485d1
ms.contentlocale: de-de
ms.lasthandoff: 10/10/2017

---
# <a name="avoiding-errors-on-r-packages-installed-in-user-libraries"></a>Vermeiden von Fehlern in R-Paketen in benutzerbibliotheken installiert

Erfahrene Benutzer von R sind daran gewöhnt, für die Installation von R-Pakete in einer Benutzerbibliothek, wenn die Standardbibliothek blockierte oder nicht verfügbar ist. Allerdings wird dieser Ansatz wird in SQL Server nicht unterstützt und Installation in einer Benutzerbibliothek endet in der Regel zu einem Fehler "Paket wurde nicht gefunden".

Dieses Thema enthält problemumgehungen, um diesen Fehler zu vermeiden. Es wird erläutert, wie Sie R-Code ändern können, und schlägt vor, Ihnen die richtige R-Paketinstallation für die Verwendung von R-Pakete von einer SQL Server-Instanz.

## <a name="why-r-user-libraries-cannot-be-accessed-from-sql-server"></a>Warum R benutzerbibliotheken von SQL Server zugegriffen werden kann

R-Entwickler, die neue R-Pakete installieren müssen, sind beim Installieren von Paketen werden, und sobald die Standardbibliothek nicht verfügbar ist, oder wenn der Entwickler kein Administrator auf dem Computer ist die Verwendung einer privaten, Benutzerbibliothek.

Z. B. in einer typischen R-Entwicklungsumgebung, die Benutzer würde Hinzufügen der Speicherort des Pakets der R-Umgebungsvariable `libPath`, oder verweisen Sie den vollständigen Paketpfad wie folgt:

```R
library("c:/Users/<username>/R/win-library/packagename")  
```

Allerdings kann diese nie arbeiten, bei der Ausführung von R-Lösungen in SQL Server, da R-Pakete in einer spezifischen Bibliothek installiert werden müssen, die mit der Instanz verknüpft ist.

Wenn das Paket nicht in der Standardbibliothek installiert wurde, erhalten Sie möglicherweise diese Fehlermeldung, wenn Sie versuchen, das Paket aufzurufen:

*Fehler in library(xxx): ist kein Paket namens "Paketname"*

Es ist auch eine fehlerhafte Entwicklung Vorgehensweise zum Installieren der erforderlichen R-Pakete in einer benutzerdefinierten-Bibliothek, da es zu Fehlern führen kann, wenn eine Lösung von einem anderen Benutzer ausgeführt wird, die keinen Zugriff auf den BibliothekenSpeicherort.

## <a name="how-to-install-r-packages-to-an-accessible-library"></a>Gewusst wie: Installieren von R-Pakete in einer Bibliothek zugegriffen werden kann

**Für SQLServer 2016**

Verwenden Sie die Paket-Bibliothek, die der Instanz zugeordnet. Weitere Informationen finden Sie unter [R-Pakete, die mit SQL Server installiert](installing-and-managing-r-packages.md)

**Für SQLServer 2017**

SQL Server bietet Funktionen, mit denen Sie mehrere Paketversionen verwalten und erteilen Benutzern die Berechtigung für einzelne Pakete, ohne dass der Benutzer mit Dateisystemzugriff haben.

Weitere Informationen zum Einrichten einer Bibliothek des Pakets für shared und Zuweisen von Benutzern zu Rollen finden Sie unter [paketverwaltung für SQL Server R](r-package-management-for-sql-server-r-services.md).

Wenn Sie die Paket-Management-Ansatz basierend auf Datenbankrollen verwenden, ist es nicht notwendig, mehrere Kopien desselben Pakets nicht in Verzeichnissen von anderen Benutzer zu installieren. Installieren Sie eine Kopie des Pakets müssen und für authentifizierte Benutzer freigeben. Da Pakete auf Datenbankebene verwaltet werden, können Sie auch Gruppen von Paketen und die zugehörigen Berechtigung zwischen Datenbanken kopieren.

## <a name="tips-for-avoiding-package-not-found-errors"></a>Tipps zur Vermeidung von Fehlern "Paket wurde nicht gefunden"

+ Ändern Sie Code aus, um Abhängigkeiten von benutzerbibliotheken zu beseitigen. Bei der Migration von R-Lösungen für die Ausführung im [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)], es ist wichtig, dass Sie die folgenden Aktionen ausführen:

    + Installieren Sie alle Pakete, die Sie benötigen, in der Standardbibliothek, die der Instanz zugeordnet.

    + Bearbeiten Sie Code, um sicherzustellen, dass Pakete aus der Bibliothek standardmäßig nicht aus ad-hoc-Verzeichnisse oder benutzerbibliotheken geladen werden.

+ Vermeiden Sie die ad-hoc-Paketinstallation als Teil einer Lösung. Checken Sie den Code, um sicherzustellen, dass es keine Aufrufe an deinstalliert Pakete oder Code, der dynamisch Pakete installiert sind. Der Code schlägt fehl, wenn Sie keine Berechtigungen haben, und wenn Sie Berechtigungen haben, sollten Sie die Pakete separat installieren, von anderem Code, der ausgeführt werden soll.

+ Ändern Sie direkte Pfade zu R-Paket-Bibliotheken. Wenn ein Paket in der Standardbibliothek installiert wurde, lädt die R-Laufzeit das Paket aus der Standardbibliothek, auch wenn im R-Code eine andere Bibliothek angegeben wurde.

