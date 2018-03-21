---
title: "Problembehandlung sowie häufig gestellte Fragen für Machine Learning in SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 5b9a5c6497781ef67d9d2ef9b9032a4d9ee250e5
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
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
+ [Offline-Installation (keine Internet)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>Konfiguration

Die folgenden Artikel enthalten Informationen über die Standardwerte sowie zum Anpassen der Konfiguration für den Machine learning in einer Instanz:

+ [Ändern des benutzerkontenpools für SQL Server R Services](r/modify-the-user-account-pool-for-sql-server-r-services.md)  
+ [Konfigurieren und Verwalten von advanced Analytics-Erweiterungen](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [Vorgehensweise: erstellen ein Ressourcenpools](r/how-to-create-a-resource-pool-for-r.md)
+ [Optimierung für R-arbeitsauslastungen](r/operationalizing-your-r-code.md)
