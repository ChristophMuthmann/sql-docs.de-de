---
title: Problembehandlung sowie häufig gestellte Fragen für Machine Learning in SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 80d153baed382c95c85793e1605b700c2719e13c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="troubleshoot-machine-learning"></a>Problembehandlung bei Machine learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel enthält Links zur Problembehandlung Installationshandbüchern, bekannten Problemen und Anmerkungen zu dieser Version. Anderen Artikeln verknüpft, um von diesem Artikel Ratschläge zur leistungsoptimierung für Machine Learning-Lösungen in SQL Server bereitstellen.

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

+ [Installieren von SQL Server 2017 Machine Learning-Services (Datenbankintern)](install/sql-machine-learning-services-windows-install.md)
+ [Installieren von SQL Server 2017 Machine Learning-Server (eigenständig)](install/sql-machine-learning-standalone-windows-install.md)
+ [Installieren von SQL Server 2016 R Services (Datenbankintern)](install/sql-r-services-windows-install.md)
+ [Installieren von SQL Server 2016R Server (eigenständig)](install/sql-r-standalone-windows-install.md)
+ [Eingabeaufforderung-setup](install/sql-ml-component-commandline-install.md)
+ [Offlineeinrichtung (kein Internet)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>Konfiguration

Die folgenden Artikel enthalten Informationen über die Standardwerte sowie zum Anpassen der Konfiguration für den Machine learning in einer Instanz:

+ [Ändern des benutzerkontenpools für SQL Server R Services](r/modify-the-user-account-pool-for-sql-server-r-services.md)  
+ [Konfigurieren und Verwalten von advanced Analytics-Erweiterungen](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [Vorgehensweise: erstellen ein Ressourcenpools](r/how-to-create-a-resource-pool-for-r.md)
+ [Optimierung für R-arbeitsauslastungen](r/operationalizing-your-r-code.md)
