---
title: Konfiguration und Verwaltung | Microsoft Docs
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e0fd4554-60c6-4181-ac4c-2e366fb434f6
caps.latest.revision: "7"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1f90cb9c8792086352403a6bb937391daf3f338f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="configuration-and-management"></a>Konfiguration und Verwaltung

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

In diesen Themen wird beschrieben, wie neue R-Pakete auf SQL Server-Instanz installieren, R-Paket-Bibliotheken verwalten und Wiederherstellen der Paket-Bibliotheken nach einer Wiederherstellung der Datenbank.

+ [Installieren und Verwalten von R-Paketen](installing-and-managing-r-packages.md)
+ [Neue R-Pakete installiert.](install-additional-r-packages-on-sql-server.md)
+ [Aktivieren Sie die Paket-Verwaltung für eine Instanz mithilfe von Datenbankrollen](r-package-how-to-enable-or-disable.md)
+ [Erstellen Sie ein lokales Paket-Repository mit miniCRAN](create-a-local-package-repository-using-minicran.md)
+ [Bestimmen Sie, dass die R-Pakete auf SQl Server installiert sind](determine-which-packages-are-installed-on-sql-server.md)
+ [Synchronisieren von R-Pakete zwischen SQLServer und dem Dateisystem](package-install-uninstall-and-sync.md)
+ [R-Paketen in Benutzerbibliotheken installiert](packages-installed-in-user-libraries.md)

## <a name="service-configuration"></a>Dienstkonfiguration

In diesen Themen wird beschrieben, wie Änderungen an der zugrunde liegenden Dienstarchitektur vornehmen und zum Verwalten von Sicherheitsprinzipalen, die der Erweiterungsdienst zugeordnet.

+ [Überlegungen zur Sicherheit](security-considerations-for-the-r-runtime-in-sql-server.md)
+ [Ändern des Benutzerkontenpools für SQL Server R Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)
+ [Konfigurieren und Verwalten von Advanced Analytics-Erweiterungen](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)
+ [Aktivieren Sie die Paket-Verwaltung für eine Instanz mithilfe von Datenbankrollen](r-package-how-to-enable-or-disable.md)
+ [Leistungsoptimierung für R Services](sql-server-r-services-performance-tuning.md)

## <a name="resource-governance"></a>Ressourcenkontrolle

In diesen Themen wird beschrieben, wie ressourcenverwaltung für R oder Python-Projekte, die mithilfe der Ressourcenkontrolle Feature nutzenden in der Enterprise Edition implementieren.

+ [Ressourcenkontrolle für R Services](../../advanced-analytics/r/resource-governance-for-r-services.md)
+ [How to Create a Resource Pool für R](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)

Siehe auch:

+ [Monitor-R, die mithilfe von benutzerdefinierten SSMS-Berichten](monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="initial-setup"></a>Anfangssetup

Zusätzliche Hilfe im Zusammenhang mit der ersten Installation und Konfiguration finden Sie in diesen Themen:

+ [Häufig gestellte Fragen zu Upgrade und Installation](../r/upgrade-and-installation-faq-sql-server-r-services.md)
+ [Überlegungen zur Sicherheit](../r/security-considerations-for-the-r-runtime-in-sql-server.md)
+ [Bekannte Probleme für R Services](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)

