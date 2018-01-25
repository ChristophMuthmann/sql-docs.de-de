---
title: "Problembehandlung sowie häufig gestellte Fragen für Machine Learning in SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 06/16/2017
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 640dde0a2faf43c7c5cda39789eaba759959bb99
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="troubleshoot-machine-learning"></a>Problembehandlung bei Machine learning

Dieser Artikel enthält Informationen zur Problembehandlung im Zusammenhang mit der Installation und Konfiguration von Machine Learning-Funktionen in SQL Server. Die Informationen enthält Links zu den Installationshandbüchern, bekannten Problemen und Anmerkungen zu dieser Version. Anderen Artikeln verknüpft, um von diesem Artikel Ratschläge zur leistungsoptimierung für Machine Learning-Lösungen in SQL Server bereitstellen.

Verwenden Sie diese Seite als Ausgangspunkt für die Suche nach bekannten Problemen, häufig gestellte Fragen für Setup und Verfahren zur Problembehandlung.

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Dienste (R und Python)

## <a name="known-issues"></a>Bekannte Probleme

In den folgenden Artikeln listet bekannte Probleme mit der aktuellen Version, oder es werden Probleme mit früheren Versionen beschrieben:

+ [Bekannte Probleme für R Services](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [Versionsanmerkungen zu SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
+ [SQL Server 2017 release notes (Versionsanmerkungen zu SQL Server 2017)](../sql-server/sql-server-2017-release-notes.md)

## <a name="troubleshooting-prerequisites"></a>Problembehandlung bei Komponenten

Wenn Sie haben, ist ein Fehler aufgetreten, oder ein Problem in Ihrer Umgebung kennen müssen, ist es wichtig, dass Sie systematisch Informationen sammeln. Diese Informationen umfassen die Version, Edition, Sicherheitskontext und Ausführungskontext.

Im folgende Artikel enthält eine Liste von Informationen, die zur Selbsthilfe Problembehandlung vereinfacht oder eine Anforderung für den technischen Support.

+ [Die Datensammlung für die Problembehandlung von Machine learning](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>Setup- und Konfigurations-Handbücher

Beginnen Sie hier, wenn Sie Machine Learning mit SQL Server nicht eingerichtet haben, oder wenn Sie die Funktion hinzufügen möchten:

+ [Richten Sie R Services "oder" Machine Learning-Dienste mit R](../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)
+ [Einrichten von Machine Learning-Dienste mit Python](../advanced-analytics/python/setup-python-machine-learning-services.md)
+ [Setup – häufig gestellte Fragen](../advanced-analytics/r/upgrade-and-installation-faq-sql-server-r-services.md)
+ [Verwenden Sie zum Aktualisieren einer Instanz von R Services SqlBindR](../advanced-analytics/r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

In den folgenden Artikeln wird beschrieben, die für offline Machine Learning-Funktionen in SQL Server-Setup zusätzliche Schritte:

+ [Unbeaufsichtigte Installation von R Services](../advanced-analytics/r/unattended-installs-of-sql-server-r-services.md) 
+ [Unbeaufsichtigte Installation von Machine Learning-Dienste mit Python](../advanced-analytics/python/unattended-installs-of-sql-server-python-services.md)

Wenn Sie Machine learning-Funktionen auf einem Computer ohne Internetzugang installieren müssen, verwenden Sie die Links in diesem Artikel, die R und Python-Komponenten, die vor dem Setup herunterzuladen:

+ [Installieren von Machine Learning-Komponenten ohne Internetzugriff](../advanced-analytics/r/installing-ml-components-without-internet-access.md)

### <a name="configuration"></a>Konfiguration

Die folgenden Artikel enthalten Informationen über die Standardwerte sowie zum Anpassen der Konfiguration für den Machine learning in einer Instanz:

+ [Ändern des benutzerkontenpools für SQL Server R Services](../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)  
+ [Konfigurieren und Verwalten von advanced Analytics-Erweiterungen](../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)  
+ [Vorgehensweise: erstellen ein Ressourcenpools](r/how-to-create-a-resource-pool-for-r.md)
+ [Optimierung für R-arbeitsauslastungen](r/operationalizing-your-r-code.md)

## <a name="related-tools-and-services"></a>Verwandte Tools und Dienste

+ [Einrichten von Microsoft Machine Learning einen eigenständigen Server](../advanced-analytics/r/create-a-standalone-r-server.md)
+ [R-Server auf einem virtuellen Azure-Computer einrichten](../advanced-analytics/r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
+ [Installieren von R Server für Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)
+ [Abrufen von R-Tools für Visual Studio](https://www.visualstudio.com/vs/rtvs/)
