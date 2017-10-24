---
title: "Ressourcenkontrolle für R Services | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 18c9978a-aa55-42bd-9ab3-8097030888c9
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5475c2258971c48c2e19bba69d9ec962ae48be87
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="resource-governance-for-r-services"></a>Ressourcenkontrolle für R Services
  Ein Problem mit R ist, dass für das Analysieren von großen Datenmengen in der Produktion zusätzliche Hardware erforderlich ist und Daten häufig auf Computer außerhalb der Datenbank verschoben werden, die nicht von der IT-Abteilung kontrolliert werden.  Zur Durchführung erweiterter Analysevorgänge möchten Kunden Datenbankserverressourcen nutzen. Um ihre Daten dabei zu schützen, müssen solche Vorgänge die Kompatibilitätsrichtlinien auf Unternehmensebene wie Sicherheit und Leistung erfüllen.  
  
 Dieser Abschnitt enthält Informationen zum Verwalten von Ressourcen, die von der R-Laufzeit und von laufenden R-Aufträgen verwendet werden, die die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz als Rechenkontext verwenden.  
  
## <a name="what-is-resource-governance"></a>Was ist die Ressourcenkontrolle?  
 Die Ressourcenkontrolle dient dem Identifizieren und Verhindern von Problemen, die häufig in einer Datenbankserverumgebung auftreten, in der sich oft mehrere abhängige Programme befinden und mehrere Dienste unterstützt und ausgeglichen werden müssen. Für [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] beinhaltet die Ressourcenkontrolle folgende Aufgaben:  
  
-   Identifizieren von Skripts, die übermäßig viele Serverressourcen in Anspruch nehmen.  
  
     Der Administrator muss in der Lage sein, Aufträge zu beenden oder einzuschränken, die zu viele Ressourcen in Anspruch nehmen.  
  
-   Reduzieren unvorhersehbarer Arbeitsauslastungen.  
  
     Wenn gleichzeitig mehrere R-Aufträge auf dem Server ausgeführt werden und die Aufträge nicht mithilfe von Ressourcenpools voneinander isoliert werden, kann der resultierende Ressourcenkonflikt zu unvorhersehbarer Leistung führen oder den Abschluss der Arbeitsauslastung gefährden.  
  
-   Priorisieren von Arbeitsauslastungen.  
  
     Der Administrator oder Architekt muss Arbeitsauslastungen festlegen können, die Vorrang haben, oder garantieren können, dass bei einem Ressourcenkonflikt bestimmte Arbeitsauslastungen abschließen.  
  
 In [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] können Sie den [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) zur Verwaltung der Ressourcen verwenden, die von der R-Laufzeit und von R-Remoteaufträgen verwendet werden.  
  
## <a name="how-to-use-resource-governor-to-manage-r-jobs"></a>Verwenden des Resource Governor zur Verwaltung von R-Aufträgen  
 In der Regel verwalten Sie R-Aufträgen zugeordnete Ressourcen durch Erstellen eines *externen Ressourcenpools* und Zuweisen von Arbeitsauslastungen an den oder die Pools. Ein externer Ressourcenpool ist ein neuer Typ von Ressourcenpool, der in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] eingeführt wurde, um bei der Verwaltung der R-Laufzeit und anderen Prozessen außerhalb des Datenbankmoduls zu helfen.  
  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] stehen nun drei Arten von Standardressourcenpools zur Verfügung.  
  
-   Der *interne Pool* stellt die Ressourcen dar, die von SQL Server selbst verwendet werden, und kann nicht geändert oder eingeschränkt werden.  
  
-   Der *Standardpool* ist ein vordefinierter Benutzerpool, den Sie verwenden können, um die Ressourcenverwendung für den Server als Ganzes zu ändern. Sie können auch Benutzergruppen definieren, die zu diesem Pool gehören, um den Zugriff auf Ressourcen zu verwalten.  
  
-   Der *externe Standardpool* ist ein vordefinierter Benutzerpool für externe Ressourcen. Des Weiteren können Sie neue externe Ressourcenpools erstellen und Benutzergruppen definieren, die zu diesem Pool gehören.  
  
 Darüber hinaus können Sie *benutzerdefinierte Ressourcenpools* erstellen, um Ressourcen dem Datenbankmodul oder anderen Anwendungen zuzuweisen, sowie *benutzerdefinierte externe Ressourcenpools* erstellen, um R und andere externe Prozesse zu verwalten.  
  
 Eine gute Einführung in die Terminologie und allgemeinen Konzepte finden Sie unter [Ressourcenpool für die Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-resource-pool.md).  

  
## <a name="resource-management-using-resource-governor"></a>Ressourcenmanagement mit dem Resource Governor 

   Wenn Sie mit dem Resource Governor noch nicht vertraut sind, finden Sie eine kurze exemplarische Vorgehensweise zum Ändern der Standardressourcen einer Instanz und zum Erstellen eines neuen externen Ressourcenpools unter [Vorgehensweise: Erstellen eines Ressourcenpools für R](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md).   
  
 Sie können mit dem *externen Ressourcenpool* die Ressourcen verwalten, die von den folgenden ausführbaren R-Dateien verwendet werden:  
  
-   Rterm.exe und Satellitenprozesse  
  
-   BxlServer.exe und Satellitenprozesse  
  
-   Satellitenprozesse, die von LaunchPad gestartet werden  
  
 Die direkte Verwaltung des Launchpad-Diensts mithilfe des Resource Governor wird jedoch nicht unterstützt. Das liegt daran, dass [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] ein vertrauenswürdiger Dienst ist, der so entworfen wurde, dass er nur Startprogramme hostet, die von Microsoft bereitgestellt werden. Vertrauenswürdige Startprogramme sind auch dafür konfiguriert, übermäßigen Ressourcenverbrauch zu vermeiden.  
  
 Es wird empfohlen, Satellitenprozesse mit dem Resource Governor zu verwalten und sie entsprechend den Bedürfnissen der individuellen Datenbankkonfiguration und Arbeitsauslastung zu optimieren.  Zum Beispiel kann jeder einzelne Satellitenprozess während der Ausführung bei Bedarf erstellt oder gelöscht werden.  
  
## <a name="disable-external-script-execution"></a>Deaktivieren der Ausführung des externen Skripts  
 Die Unterstützung externer Skripts ist bei der Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] optional. Selbst nach der Installation von [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] ist die Möglichkeit zum Ausführen externer Skripts standardmäßig deaktiviert, und Sie müssen die Eigenschaft manuell neu konfigurieren und die Instanz neu starten, um die Ausführung von Skripts zu aktivieren.  
  
 Wenn nun ein Sicherheitsproblem auftritt oder ein Ressourcenproblem, das sofort behoben werden muss, kann ein Administrator die Ausführung externer Skripts sofort deaktivieren, indem er [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) verwendet und die Eigenschaft `external scripts enabled` auf FALSE oder 0 festlegt.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten und Überwachen von R-Lösungen](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
 [Vorgehensweise: Erstellen eines Ressourcenpools für R](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)  
 [Ressourcenpool für die Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
  


