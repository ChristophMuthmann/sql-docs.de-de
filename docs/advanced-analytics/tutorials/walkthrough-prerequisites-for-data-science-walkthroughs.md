---
title: "Voraussetzungen für die Data sience-Vorgehensweise für SQL Server und R | Microsoft Docs"
ms.date: 11/10/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 0b0582b8-8843-4787-94a8-2e28bdc04fb2
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 35738101548f3b0790131c8106bb37e482cc7316
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="prerequisites-for-the-data-science-walkthrough-for-sql-server-and-r"></a>Voraussetzungen für die Data sience-Vorgehensweise für SQL Server und R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Wir empfehlen, die Sie durchführen dieser exemplarischen Vorgehensweise auf einem Laptop oder einem anderen Computer, die Microsoft-R-Bibliotheken installiert wurde. Sie müssen möglicherweise, im selben Netzwerk zu Herstellen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer mit Machine Learning-Dienste und die Sprache R aktiviert.

Sie können die exemplarischen Vorgehensweise führen Sie auf einem Computer, die beides aufweist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und ein R-Entwicklungsumgebung, aber es ist nicht empfehlenswert, diese Konfiguration für eine produktionsumgebung.

## <a name="install-machine-learning-for-sql-server"></a>Machine Learning für SQL Server installieren

Sie benötigen Zugriff auf eine Instanz von SQL Server mit Unterstützung für R installiert. In dieser exemplarischen Vorgehensweise wurde ursprünglich für SQL Server 2016 entwickelt und auf 2017 getestet werden, sodass Sie eine der folgenden SQL Server-Versionen verwenden sollten. (Es gibt einige geringfügige Unterschiede in der RevoScaleR-Funktionen zwischen den Versionen.)

+ Für SQLServer 2017 Machine Learning-Services (Datenbankintern)
+ SQL Server 2016 R Services

Weitere Informationen finden Sie unter [installieren Sie SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) oder [Installieren von SQL Server 2016 R Services](../install/sql-r-services-windows-install.md).

> [!IMPORTANT]
> SQL Server-Versionen vor als 2016-Integration in r unterstützen nicht Allerdings können Sie die SQL-Datenbanken, die älter sind als ODBC-Datenquelle.

## <a name="install-an-r-development-environment"></a>Installieren Sie eine R-Entwicklungsumgebung

In dieser exemplarischen Vorgehensweise wird empfohlen, dass Sie eine R-Entwicklungsumgebung verwenden. Hier sind einige Vorschläge:

- **R-Tools für Visual Studio** (RTVS) ist eine kostenlose plug-in, das bietet Intellisense, debugging und Unterstützung für Microsoft r Sie es mit R-Server und SQL Server-Machine Learning-Services verwenden können. Gehen Sie unter [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/)(R-Tools für Visual Studio), um es herunterzuladen.

- **Microsoft R Client** ist ein lightweight-Webentwicklungstool, die Entwicklung mit dem "revoscaler"-Paket r unterstützt. Unter [Erste Schritte mit Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)können Sie es herunterladen.

- **RStudio** ist eine der beliebtesten Umgebungen für die Entwicklung von R. Weitere Informationen finden Sie unter [ https://www.rstudio.com/products/RStudio/ ](https://www.rstudio.com/products/RStudio/).

    Dieses Lernprogramm, die Verwendung einer generischen Installation RStudio oder anderen Umgebung kann nicht abgeschlossen werden; Sie müssen auch das R-Pakete und verbindungsbibliotheken für Microsoft R Open installieren. Weitere Informationen finden Sie unter [Einrichten eines Data Science-Clients](../r/set-up-a-data-science-client.md).

- Grundlegende R-Tools (R.exe RTerm.exe, RScripts.exe) werden auch standardmäßig installiert, bei der Installation von R in SQL Server oder R-Client. Wenn Sie nicht, eine IDE installieren möchten, können Sie diese Tools verwenden.

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
