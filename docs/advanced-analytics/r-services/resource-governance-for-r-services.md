---
title: "Ressourcenkontrolle f&#252;r R-Dienste | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 18c9978a-aa55-42bd-9ab3-8097030888c9
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Ressourcenkontrolle f&#252;r R-Dienste
  Ein Problem mit R ist, dass Analyse große Datenmengen in der Produktion ist zusätzliche Hardware erforderlich, und Daten werden auf Computern, die nicht von kontrolliert werden häufig außerhalb der Datenbank verschoben IT.  Um erweiterte Analyse durchzuführen, Kunden möchten-Serverressourcen nutzen, und um ihre Daten schützen, müssen solche Vorgänge auf Enterprise-Ebene, z. B. Sicherheit und Leistung Auflagen.  
  
 Dieser Abschnitt enthält Informationen zum Verwalten von Ressourcen, die von der Laufzeit R und von R-Aufträge ausgeführt und verwendet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz wie die Compute-Kontext.  
  
## Was ist die Ressourcenkontrolle?  
 Ressourcenkontrolle dient zum Identifizieren und zu verhindern, dass Probleme, die in einer Datenbank-Server-Umgebung, in denen häufig mehrere abhängige Programme sind und mehrere Dienste zur Unterstützung von und zu verteilen. Für [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], Ressourcenkontrolle sind folgende Schritte erforderlich:  
  
-   Identifizieren von Skripts, die übermäßig viele Ressourcen verwenden.  
  
     Der Administrator muss in der Lage zu beenden oder zu drosseln, Aufträge, die zu viele Ressourcen in Anspruch nehmen.  
  
-   Schadensbegrenzende unvorhersehbare Workloads.  
  
     Wenn mehrere R-Aufträge werden gleichzeitig auf dem Server ausgeführt, und die Aufträge mithilfe von Ressourcen-Pools nicht voneinander isoliert sind, kann der resultierende Ressourcenkonflikt z. B. dazu führen, dass unvorhersehbare Leistung oder Abschluss der Arbeitslast drohen.  
  
-   Priorisieren von Arbeitslasten.  
  
     Der Administrator oder der Architekt muss Arbeitslasten festzulegen, die die müssen haben Vorrang vor, oder bestimmte Arbeitslasten abgeschlossen, wenn Ressourcenkonflikt garantiert.  
  
 In [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], können Sie [Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md) die von der Laufzeit R und R Remoteaufträge verwendeten Ressourcen zu verwalten.  
  
## Vorgehensweise zum Verwenden der Ressourcenkontrolle verwalten R-Aufträge  
 In der Regel verwalten Sie R-Aufträge durch Erstellen von zugeordnete Ressourcen *externe Ressourcenpools* und die oder Ressourcenpools Arbeitslasten zuweisen. Ein externe Ressourcenpool ist ein neuer Typ des Ressourcenpools eingeführten [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], zur Verwaltung der R-Laufzeit und anderen Prozessen, die außerhalb der Datenbank-Engine.  
  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], stehen nun drei Arten von Standard-Ressourcenpools.  
  
-   Die *internen Pool* stellt die Ressourcen verwendet, die von SQL Server selbst können nicht geändert oder eingeschränkt.  
  
-   Die *Standard-Pool* ist eine vordefinierte Benutzerpool, die Sie verwenden können, um die Ressourcenverwendung für den Server als Ganzes zu ändern. Sie können auch Benutzergruppen definieren, die zu diesem Pool, zum Verwalten des Zugriffs auf Ressourcen gehören.  
  
-   Die *Standard externen Pool* ist eine vordefinierte Benutzerpool für externe Ressourcen. Darüber hinaus können Sie neue externe Ressourcen-Pools erstellen und Definieren von Benutzergruppen zu diesem Pool gehören.  
  
 Sie können darüber hinaus erstellen *benutzerdefinierte Ressourcenpools* zum Zuweisen von Ressourcen, die das Datenbankmodul oder einer anderen Anwendung und erstellen *externe Ressourcenpools* R und andere externe Prozesse zu verwalten.  
  
 Eine gute Einführung in die Terminologie und allgemeine Konzepte finden Sie unter [Ressourcenpool der Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-resource-pool.md).  
  
> [!NOTE]  
>  Die neuen Eigenschaften der Ressourcenkontrolle sind derzeit nur über DDL-Anweisungen oder Skripts zur Verfügung. externe Ressourcengruppen können nicht erstellt werden, mithilfe der Benutzeroberfläche in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
## Die Ressourcenkontrolle Ressourcenmanagement 

   Wenn Sie die Ressourcenkontrolle nicht vertraut sind, finden Sie dieses Thema enthält eine kurze exemplarische Vorgehensweise zum Erstellen eines neuen externen Ressourcenpools und ändern die Ressourcen für die Instanz:  [So wird's gemacht: Erstellen eines Ressourcenpools für R](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)   
  
 Können Sie die *externe Ressourcenpool* Mechanismus zur Verwaltung der Ressourcen, die von der folgenden R-Programmdateien verwendet:  
  
-   Rterm.exe und Satellitenassemblys Prozesse  
  
-   BxlServer.exe und Satellitenassemblys Prozesse  
  
-   Satelliten-Prozesse gestartet, indem Sie LaunchPad  
  
 Die direkte Verwaltung Launchpad-Dienst mithilfe der Ressourcenkontrolle wird jedoch nicht unterstützt. Der Grund dafür ist die [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] ist ein vertrauenswürdiger Dienst, der Entwurf kann hosten nur Startprogramme, die von Microsoft bereitgestellt werden. Vermeiden Sie übermäßige Ressourcen belegt sind auch vertrauenswürdige Startprogramme konfiguriert.  
  
 Es wird empfohlen, Satelliten-Vorgänge, die die Ressourcenkontrolle verwalten und Optimieren Sie sie entsprechend den Bedürfnissen der einzelnen Datenbankkonfiguration und Arbeitslast.  Jeder einzelne Satelliten-Prozess kann z. B. erstellt oder bei Bedarf während der Ausführung gelöscht werden.  
  
## Deaktivieren Sie die Ausführung des externen Skripts  
 Unterstützung für externe Skripts ist optional, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup. Selbst nach der Installation [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], die Möglichkeit zum Ausführen von externen Skripts ist standardmäßig deaktiviert und muss manuell neu konfigurieren die Eigenschaft und die Instanz zum Aktivieren der Ausführung des Skripts neu starten.  
  
 Daher liegt ein Problem, die sofort verhindert werden soll, oder ein Sicherheitsproblem, ein Administrator kann sofort deaktivieren jeder Ausführung des externen Skripts mit [Sp_configure & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) und die Eigenschaft `external scripts enabled` auf FALSE oder 0.  
  
## Siehe auch  
 [Verwalten und Überwachen von R-Lösungen](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
 [Gewusst wie: Erstellen eines Ressourcenpools für R](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)  
 [Ressourcenpool für die Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
  