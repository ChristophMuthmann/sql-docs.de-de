---
title: Konfigurieren und Verwalten von Instanzen von SQL Server-Machine Learning-Dienst | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 0b524e7e9fb24ff0296fc0e70c8bb8a462f3d199
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="configure-and-manage-machine-learning-components-in-sql-server"></a>Konfigurieren und Verwalten von Machine Learning-Komponenten in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel enthält Links zu ausführlicheren Informationen über das Konfigurieren eines Servers zur Unterstützung von Machine Learning-Dienste mit SQL Server in dieser Produkte:

+ SQL Server 2016 R Services (Datenbankintern)
+ SQL Server 2017 Machine Learning Services (Datenbankintern)

> [!NOTE]
> 
> Dieser Inhalt wurde ursprünglich für die SQLServer 2016-Version nur die R-Sprache unterstützt geschrieben.
> 
> In SQL Server 2017 die Unterstützung für Python wurde hinzugefügt, das zugrunde liegende Framework von Architektur und Diensten ist jedoch gleich aus. Aus diesem Grund können Sie konfigurieren, Sicherheit, Speicher, ressourcensteuerung und weitere Optionen für das Ausführen von Python-Skripts, die gleiche Weise unterstützt, die für R-Skripts.
> 
> Jedoch, da die Unterstützung für Python ist für die Python-arbeitsauslastung noch nicht verfügbar ist, eine neue Funktion, die detaillierte Informationen zu potenziellen Optimierungen. Überprüfen Sie es später erneut.

## <a name="r-package-management"></a>R-Paketverwaltung

In diesen Artikeln beschrieben, wie neue R-Pakete auf SQL Server-Instanz installieren, R-Paket-Bibliotheken verwalten und Wiederherstellen der Paket-Bibliotheken nach einer Wiederherstellung der Datenbank.

+ [Installieren und Verwalten von R-Paketen](installing-and-managing-r-packages.md)
+ [Neue R-Pakete installiert.](install-additional-r-packages-on-sql-server.md)
+ [Aktivieren Sie die Paket-Verwaltung für eine Instanz mithilfe von Datenbankrollen](r-package-how-to-enable-or-disable.md)
+ [Erstellen Sie ein lokales Paket-Repository mit miniCRAN](create-a-local-package-repository-using-minicran.md)
+ [Bestimmen Sie, dass die R-Pakete auf SQl Server installiert sind](determine-which-packages-are-installed-on-sql-server.md)
+ [Synchronisieren von R-Pakete zwischen SQLServer und dem Dateisystem](package-install-uninstall-and-sync.md)
+ [R-Paketen in Benutzerbibliotheken installiert](packages-installed-in-user-libraries.md)

## <a name="service-configuration"></a>Dienstkonfiguration

In diesen Artikeln wird beschrieben, wie Änderungen an der zugrunde liegenden Dienstarchitektur vornehmen und zum Verwalten von Sicherheitsprinzipalen, die der Erweiterungsdienst zugeordnet.

+ [Überlegungen zur Sicherheit](security-considerations-for-the-r-runtime-in-sql-server.md)
+ [Ändern des Benutzerkontenpools für SQL Server R Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)
+ [Konfigurieren und Verwalten von Advanced Analytics-Erweiterungen](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)
+ [Aktivieren Sie die Paket-Verwaltung für eine Instanz mithilfe von Datenbankrollen](r-package-how-to-enable-or-disable.md)
+ [Leistungsoptimierung für R Services](sql-server-r-services-performance-tuning.md)

## <a name="resource-governance"></a>Ressourcenkontrolle

In diesen Artikeln wird beschrieben, wie ressourcenverwaltung für R oder Python-Projekte, die mithilfe der Ressourcenkontrolle Feature nutzenden in der Enterprise Edition implementieren.

+ [Ressourcenkontrolle für R Services](../../advanced-analytics/r/resource-governance-for-r-services.md)
+ [How to Create a Resource Pool für R](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)

Siehe auch:

+ [Monitor-R, die mithilfe von benutzerdefinierten SSMS-Berichten](monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="initial-setup"></a>Anfangssetup

Zusätzliche Hilfe im Zusammenhang mit der ersten Installation und Konfiguration finden Sie in diesen Artikeln:

+ [Häufig gestellte Fragen zu Upgrade und Installation](../r/upgrade-and-installation-faq-sql-server-r-services.md)
+ [Überlegungen zur Sicherheit](../r/security-considerations-for-the-r-runtime-in-sql-server.md)
+ [Bekannte Probleme für R Services](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)

