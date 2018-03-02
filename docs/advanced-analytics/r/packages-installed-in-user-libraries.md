---
title: Vermeiden von Fehlern in R-Paketen in benutzerbibliotheken installiert | Microsoft Docs
titleSuffix: SQL Server
ms.custom: 
ms.date: 02/20/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 99ffd9b8-aa6d-4ac2-9840-4e66d0463978
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: b7f640cc33cb61ab8dffc57edb3b522808129880
ms.sourcegitcommit: c08d665754f274e6a85bb385adf135c9eec702eb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/28/2018
---
# <a name="avoiding-errors-on-r-packages-installed-in-user-libraries"></a>Vermeiden von Fehlern in R-Paketen in benutzerbibliotheken installiert
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Erfahrene Benutzer von R sind daran gewöhnt, für die Installation von R-Pakete in einer Benutzerbibliothek, wenn die Standardbibliothek blockierte oder nicht verfügbar ist. Allerdings wird dieser Ansatz wird in SQL Server nicht unterstützt und Installation in einer Benutzerbibliothek endet in der Regel zu einem Fehler "Paket wurde nicht gefunden".

Dieser Artikel beschreibt problemumgehungen, um diesen Fehler zu vermeiden. Es wird erläutert, wie Sie R-Code ändern können, und schlägt vor, Ihnen die richtige R-Paketinstallation für die Verwendung von R-Pakete von einer SQL Server-Instanz.

## <a name="why-r-user-libraries-cannot-be-accessed-from-sql-server"></a>Warum R benutzerbibliotheken von SQL Server zugegriffen werden kann

R-Entwickler, die neue R-Pakete installieren müssen, sind beim Installieren von Paketen werden, eine Private, Benutzerbibliothek verwenden, wenn die Standardbibliothek nicht verfügbar ist, oder wenn der Entwickler kein Administrator auf dem Computer ist.

Z. B. in einer typischen R-Entwicklungsumgebung, die Benutzer würde Hinzufügen der Speicherort des Pakets der R-Umgebungsvariable `libPath`, oder verweisen Sie den vollständigen Paketpfad wie folgt:

```R
library("c:/Users/<username>/R/win-library/packagename")
```

Dies funktioniert nicht bei der Ausführung von R-Lösungen in SQL Server, da R-Pakete in einer spezifischen Bibliothek installiert werden müssen, die mit der Instanz verknüpft ist. Wenn ein Paket in der Standardbibliothek nicht verfügbar ist, erhalten Sie diesen Fehler, wenn Sie versuchen, das Paket abgerufen:

*Fehler in library(xxx): ist kein Paket namens "Paketname"*

## <a name="how-to-avoid-package-not-found-errors"></a>Vermeiden von Fehlern "Paket wurde nicht gefunden"

+ Beseitigen Sie Abhängigkeiten von benutzerbibliotheken 

    Es ist eine fehlerhafte Entwicklung Vorgehensweise zum Installieren der erforderlichen R-Pakete in einer benutzerdefinierten-Bibliothek, da es zu Fehlern führen kann, wenn eine Lösung von einem anderen Benutzer ausgeführt wird, die keinen Zugriff auf den BibliothekenSpeicherort.

    Auch wenn ein Paket in der Standardbibliothek installiert ist, lädt die R-Laufzeit des Pakets aus der Bibliothek standardmäßig auch wenn Sie eine andere Version in der R-Code angegeben.

+ Ändern Sie den Code in einer freigegebenen Umgebung ausgeführt.

+ Vermeiden Sie die Installation von Paketen als Teil einer Lösung. Wenn Sie nicht über Berechtigungen zum Installieren der Pakete verfügen, schlägt der Code fehl. Auch wenn Sie Berechtigungen zum Installieren der Pakete haben, sollten Sie daher separat aus anderem Code durchführen, die Sie ausführen möchten.

+ Stellen Sie sicher, dass im Code keine Aufrufe von nicht installierten Paketen enthalten sind.

+ Aktualisieren Sie den Code um direkte Verweise auf die Pfade der R-Pakete oder R-Bibliotheken zu entfernen. 

+ Wissen Sie, welche Bibliothek Paket mit der Instanz verknüpft ist. Weitere Informationen finden Sie unter [R-Pakete, die mit SQL Server installiert](installing-and-managing-r-packages.md)
