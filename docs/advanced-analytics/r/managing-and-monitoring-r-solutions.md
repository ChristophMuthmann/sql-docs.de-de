---
title: "Verwalten und Überwachen von Machine Learning-Lösungen | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/26/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d455f22a-190f-4a28-9088-98a843cd5db2
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 65398ab522f7a39aae08b1f438d2fa59291e4e8f
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="managing-and-monitoring-machine-learning-solutions"></a>Verwalten und Überwachen von Machine Learning-Lösungen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel beschreibt die Funktionen in SQL Server Machine Learning Services, die Datenbankadministratoren relevant sind, die mit R und Python-Lösungen arbeiten müssen.

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Dienste

## <a name="security"></a>Sicherheit

Datenbankadministratoren müssen Datenzugriff bieten, nicht nur auf die Datenanalysten sondern mit einer Vielzahl von Berichts-Entwickler, Wirtschaftsanalytikern und Nutzern von Geschäftsdaten. Die Integration von R (und nun Python) in SQL Server bietet viele Vorteile, an dem Datenbankadministrator, der die Data Science-Rolle unterstützt.

+ Die Architektur von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] gewährleistet die Sicherheit Ihrer Datenbanken und isoliert die Ausführung von R-Sitzungen vom Betrieb der Datenbankinstanz.

+ Sie können angeben, wer über die Berechtigung zum Ausführen von R-Skripts verfügt, und sicherstellen, dass die in R-Aufträgen verwendeten Daten mit den gleichen Sicherheitsrollen verwaltet werden, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]definiert sind.

+ Der Datenbankadministrator kann Rollen verwenden, um die Installation von R-Pakete und die Ausführung von R und Python-Skripts zu verwalten.

Weitere Informationen finden Sie in den folgenden Ressourcen:

+ [Überlegungen zur Sicherheit der R-Laufzeitumgebung in SQL Server](../../advanced-analytics/r/security-considerations-for-the-r-runtime-in-sql-server.md)

+ [R-Sicherheit (Übersicht)](../r/security-overview-sql-server-r.md)

+ [Python-Sicherheit (Übersicht)](../python/security-overview-sql-server-python-services.md)

+ [Installieren und Verwalten von R-Paketen](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)

## <a name="configuration-and-management"></a>Konfiguration und Verwaltung

Datenbankadministratoren müssen konkurrierende Projekte und Prioritäten in einen zentralen Kontaktpunkt integrieren: den Datenbankserver. Sie müssen Analytics Aufrechterhaltung der Integritäts der Betriebs-und berichtsdatenspeicher-Speicher unterstützen. Die Integration von Machine learning-mit SQL Server bietet viele Vorteile für dem Datenbankadministrator, der eine wichtige Rolle bei der Bereitstellung einer effizienten Infrastruktur für Data Science zunehmend dient.

+ R und Python-Sitzungen werden ausgeführt, in einem separaten Prozess, um sicherzustellen, dass der Server wie gewohnt ausgeführt wird weiterhin, selbst wenn die externe Skriptlaufzeit Probleme aufgetreten sind.

+ Physische Benutzerkonten mit geringen rechten werden verwendet, und von diesen externen Skriptaktivität isolieren.

+ Der DBA kann standard Verwaltungstools für SQL Server-Ressource verwenden, um den Umfang der Ressourcen, die R-Laufzeit zugeordnet sind, um zu verhindern, dass umfangreiche Berechnungen die gesamtleistung des Servers gefährden steuern.

Weitere Informationen finden Sie in den folgenden Ressourcen:

+ [Ressourcenkontrolle für R Services](../r/resource-governance-for-r-services.md)

+ [Konfigurieren und Verwalten von Advanced Analytics Extensions](../r/configure-and-manage-advanced-analytics-extensions.md)
