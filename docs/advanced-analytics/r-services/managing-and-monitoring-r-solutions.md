---
title: "Verwalten und &#220;berwachen von R-L&#246;sungen | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d455f22a-190f-4a28-9088-98a843cd5db2
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# Verwalten und &#220;berwachen von R-L&#246;sungen
  Datenbankadministratoren müssen konkurrierende Projekte und Prioritäten in einen zentralen Kontaktpunkt integrieren: den Datenbankserver. Sie müssen jedoch nicht nur Data Scientists den Zugriff auf die Daten ermöglichen, sondern einer Vielzahl von Berichtsentwicklern, Wirtschaftsanalytikern und Nutzern von Geschäftsdaten. Gleichzeitig müssen sie die Integrität der Betriebs- und Berichtsdatenspeicher aufrecht erhalten. Im Unternehmen spielt der Datenbankadministrator eine wichtige Rolle bei der Erstellung und Bereitstellung einer effektiven Data Science-Infrastruktur. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] bietet viele Vorteile an dem Datenbankadministrator, der die Data Science-Rolle unterstützt.  
  
-   **Sicherheit.** Die Architektur des [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] behält Ihrer Datenbanken sicher und isoliert die Ausführung des R-Sitzungen aus dem Vorgang der Datenbankinstanz ein.  
  
     Sie können angeben, wer über die Berechtigung zum Ausführen von R-Skripts, und stellen Sie sicher, dass die Daten in der R-Aufträge verwaltet werden mit den gleichen Sicherheitsrollen, die in definiert sind [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Zuverlässigkeit.** R-Sitzungen werden in einem separaten Prozess ausgeführt, um sicherzustellen, dass der Server weiterhin wie gewohnt ausgeführt wird, auch wenn bei der R-Sitzung Probleme auftreten. Physische Benutzerkonten mit geringen rechten werden enthalten und Isolieren von R-Instanzen verwendet.   
  
-   **Ressourcenkontrolle.** Sie können den Umfang der Ressourcen steuern, die dem R-Laufzeitmodul zugeordnet werden, um zu verhindern, dass umfangreiche Berechnungen die Gesamtleistung des Servers gefährden.  
  
  
## In diesem Abschnitt  
 [Überwachung von R-Diensten](../../advanced-analytics/r-services/monitoring-r-services.md)
 
 [Ressourcenkontrolle für R-Dienste](../../advanced-analytics/r-services/resource-governance-for-r-services.md)
 
[Installieren und Verwalten von R-Pakete](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)
  
[Konfiguration](../../advanced-analytics/r-services/configuration-sql-server-r-services.md) 

+ [Konfigurieren und Verwalten von Advanced Analytics-Erweiterungen](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md)  
  
+  [Ändern des Benutzerkontenpools für SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)  

 [Überlegungen zur Sicherheit der R-Laufzeitumgebung in SQL Server](../../advanced-analytics/r-services/security-considerations-for-the-r-runtime-in-sql-server.md)  
  
 
  
## Siehe auch  
 [SQL Server R Services – Features und Aufgaben](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)  
  
  