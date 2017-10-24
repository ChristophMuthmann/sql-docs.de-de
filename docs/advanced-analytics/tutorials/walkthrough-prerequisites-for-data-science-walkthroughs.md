---
title: "Voraussetzungen für die Data sience-Vorgehensweise für SQL Server und R | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/23/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 0b0582b8-8843-4787-94a8-2e28bdc04fb2
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b9d3a579f023a7e6d9805b934edc3f0e9e5ad5e8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="prerequisites-for-the-data-science-walkthrough-for-sql-server-and-r"></a>Voraussetzungen für die Data sience-Vorgehensweise für SQL Server und R

Wir empfehlen, die Sie durchführen dieser exemplarischen Vorgehensweise auf einem Laptop oder einem anderen Computer, die Microsoft-R-Bibliotheken installiert wurde. Sie müssen möglicherweise, im selben Netzwerk zu Herstellen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer mit Machine Learning-Dienste und die Sprache R aktiviert.

Sie können die exemplarischen Vorgehensweise führen Sie auf einem Computer, die beides aufweist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und ein R-Entwicklungsumgebung, aber es ist nicht empfehlenswert, diese Konfiguration für eine produktionsumgebung.

## <a name="install-machine-learning-for-sql-server"></a>Machine Learning für SQL Server installieren

Sie benötigen Zugriff auf eine Instanz von SQL Server mit Unterstützung für R installiert ist, verwenden eines der folgenden:

+ Für SQLServer 2017 Machine Learning-Services (Datenbankintern)
+ SQL Server 2016 R Services

Weitere Informationen finden Sie unter [Einrichten von SQL Server R Services (Datenbankintern](../r/set-up-sql-server-r-services-in-database.md).

> [!IMPORTANT]
> Verwenden Sie [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oder höher. Frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützen keine Integration mit R, obwohl Sie ältere SQL-Datenbanken als ODBC-Datenquelle verwenden können.

## <a name="install-an-r-development-environment"></a>Installieren Sie eine R-Entwicklungsumgebung

In dieser exemplarischen Vorgehensweise wird empfohlen, dass Sie eine R-Entwicklungsumgebung verwenden. Hier sind einige Vorschläge:

- **R-Tools für Visual Studio** (RTVS) ist eine kostenlose plug-in, das bietet Intellisense, debugging und Unterstützung für Microsoft r Sie es mit R-Server und SQL Server-Machine Learning-Services verwenden können. Gehen Sie unter [R Tools for Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx)(R-Tools für Visual Studio), um es herunterzuladen.

- **Microsoft R Client** ist ein schlankes Entwicklungstool, das die Entwicklung in R mit den ScaleR-Paketen unterstützt. Unter [Erste Schritte mit Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-get-started)können Sie es herunterladen.

- **RStudio** ist eine der beliebtesten Umgebungen für die Entwicklung von R. Weitere Informationen finden Sie unter [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/).

    Dieses Lernprogramm, die Verwendung einer generischen Installation RStudio oder anderen Umgebung kann nicht abgeschlossen werden; Sie müssen auch das R-Pakete und verbindungsbibliotheken für Microsoft R Open installieren. Weitere Informationen finden Sie unter [Einrichten eines Data Science-Clients](../r/set-up-a-data-science-client.md).

- Grundlegende R-Tools (R.exe RTerm.exe, RScripts.exe) sind ebenfalls standardmäßig installiert, bei der Installation [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]. Wenn Sie nicht, eine IDE installieren möchten, können Sie diese Tools verwenden.

## <a name="get-permissions-on-the-sql-server-instance-and-database"></a>Abrufen von Berechtigungen für den SQL Server-Instanz und Datenbank

Für die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Ausführen von Skripts und Hochladen von Daten, benötigen Sie eine gültige Anmeldung auf dem Datenbankserver.  Sie können entweder einen SQL-Anmeldenamen oder die integrierte Windows-Authentifizierung verwenden. Bitten Sie den Datenbankadministrator so konfigurieren Sie die folgenden Berechtigungen für das Konto in der Datenbank, wo Sie r verwenden

- Erstellen von Datenbanken, Tabellen, Funktionen und gespeicherten Prozeduren
- Schreiben von Daten in Tabellen
- Möglichkeit zum Ausführen von R-Skript (`GRANT EXECUTE ANY EXTERNAL SCRIPT to <user>`)

In dieser exemplarischen Vorgehensweise haben wir die SQL-Anmeldung verwendet **RTestUser**. Im Allgemeinen wird empfohlen, dass Sie die integrierte Windows-Authentifizierung verwenden, verwenden die SQL-Anmeldung ist jedoch einfacher einige Demonstrationszwecken.

## <a name="change-list"></a>Änderungsliste

+ Dieses Beispiel wurde ursprünglich entwickelt mit SQL Server 2016-R-Services. Allerdings wurden wichtige Änderungen in der Microsoft-R-Komponenten für 2016 SP1 eingeführt. Insbesondere die _VarsToDrop_ und _VarsToKeep_ Parameter wurden für SQL Server-Datenquellen nicht mehr unterstützt. Therefre, wenn Sie eine Version des Lernprogramms Versionen vor SP1 wird heruntergeladen wird er nicht mehr mit Post-SP1-Builds funktionieren.

+ Die aktuelle Version des Beispiels wurde mit einer Vorabversion Build von SQL Server 2017 Machine Learning Services (RC1 und RC2) getestet. Im Allgemeinen sollten fast alle Schritte zwischen 2016 SP1 und 2017 unverändert ausgeführt.

## <a name="next-lesson"></a>Nächste Lektion

[Vorbereiten der Daten mithilfe von PowerShell](/walkthrough-prepare-the-data.md)

