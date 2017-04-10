---
title: "R-Paketverwaltung f&#252;r SQL Server R Services | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: 7
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 7
---
# R-Paketverwaltung f&#252;r SQL Server R Services
Um die Verwaltung von R-Paketen zu vereinfachen, die auf einer Instanz von SQL Server ausgeführt werden, enthält das **RevoScaleR**-Paket jetzt Funktionen zur Unterstützung von Installation und Verwaltung von R-Paketen. 

Diese neue Funktionalität unterstützt verschiedene Szenarien:

- Ein Datenwissenschaftler kann ein benötigtes R-Paket in SQL Server installieren, ohne über Administratorzugriff auf den SQL Server-Computer zu verfügen. Die Pakete werden datenbankweise installiert.
- Pakete können leicht für andere freigegeben werden. Richten Sie einfach ein lokales Paketverzeichnis ein, und lassen Sie jeden Datenwissenschaftler die Pakete für die einzelnen Datenbanken installieren.
- Der Datenbankadministrator braucht die Ausführung von R-Befehlen nicht zu erlernen und muss die Paketabhängigkeiten nicht verstehen. Der DBA verwendet Datenbankrollen, um zu steuern, welchen SQL Server-Benutzern das Installieren, Deinstallieren oder Verwenden von Paketen erlaubt ist.
 
**Funktionsweise**

* Der Datenbankadministrator ist für das Einrichten von Rollen und das Hinzufügen von Benutzern zu den Rollen sowie für die Kontrolle zuständig, wer über Berechtigungen zum Hinzufügen und Entfernen von R-Paketen zur bzw. aus der SQL Server-Umgebung verfügt.
* Wenn Sie über die Berechtigung zum Installieren von Paketen verfügen, führen Sie eine der Paketverwaltungsfunktionen aus Ihrem R-Code aus und geben den Rechenkontext an, zu dem Pakete hinzugefügt bzw. aus dem sie entfernt werden sollen. Der Rechenkontext kann Ihr lokaler Computer oder eine Datenbank auf der SQL Server-Instanz sein. 
* Wenn der Aufruf zum Installieren von Paketen auf SQL Server ausgeführt wird, entscheiden Ihre Anmeldeinformationen darüber, ob der Vorgang auf dem Server abgeschlossen werden kann. 
- Die Funktionen zur Paketinstallation prüfen Abhängigkeiten und stellen sicher, dass alle zugehörigen Pakete in SQL Server installiert werden können, gerade wie bei der Installation von R-Paketen im lokalen Rechenkontext.
- Die Funktion, die Pakete deinstalliert, berechnet ebenfalls Abhängigkeiten und stellt sicher, dass Pakete, die nicht mehr von anderen Paketen in SQL Server verwendet werden, entfernt werden, um Ressourcen freizugeben.
- Jeder Datenwissenschaftler kann private Pakete installieren, die für andere nicht sichtbar sind, und erhält so einen isolierten Sandkasten für die Arbeit mit den eigenen R-Paketen.
-  Da die Gültigkeit von Paketen auf eine Datenbank eingeschränkt werden kann und jeder Benutzer in jeder Datenbank einen isolierten Paketsandkasten erhält, ist es einfacher, verschiedene Versionen des gleichen R-Pakets zu installieren und zu verwenden. 

> [!NOTE]
> Aktuell wird dieses Feature nur für die Verwendung mit [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] veröffentlicht. 

## <a name="database-roles-and-database-scoping"></a>Datenbankrollen und Datenbank-Gültigkeitsbereiche

Die neuen Paketverwaltungsfunktionen stellen zwei Gültigkeitsbereiche für die Installation und Verwaltung von Paketen in SQL Server für eine bestimmte Datenbank bereit:

- **Freigegebener Bereich**

  *Freigegebener Bereich* bedeutet, dass Benutzer, denen die Berechtigung für die Rolle für den freigegebenen Bereich (**rpkgs-shared**) erteilt wurde, Pakete für eine angegebene Datenbank installieren und deinstallieren können. Ein Paket, das in einer Bibliothek des freigegebenen Bereichs installiert wurde, kann von anderen Benutzern der Datenbank auf SQL Server verwendet werden, sofern diesen Benutzern die Verwendung der installierten R-Pakete erlaubt ist. 

- **Privater Bereich** 

  *Privater Bereich* bedeutet, dass Benutzer, denen die Mitgliedschaft in der Rolle für den privaten Gültigkeitsbereich (**rpkgs-private**) erteilt wurde, Pakete an einem vom Benutzer definierten privaten Bibliotheksspeicherort installieren bzw. deinstallieren können. Daher können alle Pakete, die im privaten Bereich installiert wurden, nur von dem Benutzer verwendet werden, der sie installiert hat. Anders gesagt kann ein Benutzer von SQL Server keine privaten Pakete verwenden, die von einem anderen Benutzer installiert wurden. 

Diese Modelle für den *freigegebenen* und den *privaten* Bereich können kombiniert werden, um benutzerdefinierte Sicherheitssysteme zum Bereitstellen und Verwalten von Paketen auf SQL Server zu entwickeln. 

Beispielsweise kann dem Leiter oder Manager einer Gruppe von Datenwissenschaftlern die Berechtigung zum Installieren von Paketen erteilt werden, und diese Pakete können dann von allen anderen Benutzern oder Datenwissenschaftlern in der gleichen SQL Server-Instanz verwendet werden. 

Für ein anderes Szenario ist möglicherweise eine stärkere Abgrenzung der Benutzer untereinander oder eine andere Verwendung von Paketen erforderlich. In einem solchen Fall kann der private Bereich verwendet werden, um Datenwissenschaftlern Einzelberechtigungen zu erteilen, die nur für das Installieren und Verwenden der von ihnen benötigten Pakete verantwortlich sind. Da Pakete auf Benutzerbasis installiert werden, wirken sich die von einem Benutzer installierten Pakete nicht auf die Arbeit anderer Benutzer aus, die die gleiche SQL Server-Datenbank verwenden. 

### <a name="database-roles-for-package-management"></a>Datenbankrollen für die Paketverwaltung

Die folgenden neuen Datenbankrollen unterstützen die sichere Installation und Paketverwaltung für SQL R Services: 

- **rpkgs-users** Ermöglicht Benutzern das Verwenden aller freigegebenen Pakete, die von Mitgliedern der **rpkgs-shared**-Rolle installiert wurden.

- **rpkgs-private** Bietet Zugriff auf freigegebene Pakete mit den gleichen Berechtigungen wie die **rpkgs-users**-Rolle. Mitglieder dieser Rolle können darüber hinaus Pakete mit privatem Geltungsbereich installieren, entfernen und verwenden.

-  **rpkgs-shared** Bietet die gleichen Berechtigungen wie die Rolle **rpkgs-private**. Benutzer, die Mitglied dieser Rolle sind, können ebenfalls freigegebene Pakete installieren oder entfernen. 
 
- **db_owner**: verfügt über die gleichen Berechtigungen wie die Rolle **rpkgs-shared**. Kann darüber hinaus Benutzern das Recht zum Installieren oder Entfernen von freigegebenen und/oder privaten Paketen erteilen.



## <a name="new-package-management-functions"></a>Neue Paketverwaltungsfunktionen


+ `rxInstalledPackages`: Sucht Informationen zu den im angegebenen Rechenkontext installierten Paketen.

+ `rxInstallPackages`: Installiert Pakete in einem Rechenkontext, entweder aus einem angegebenen Repository oder durch Lesen von lokal gespeicherten ZIP-Archivpaketen.

+ `rxRemovePackages`: Entfernt installierte Pakete aus einem Rechenkontext.

+ `rxFindPackage`: Ruft den Pfad für ein oder mehrere Paket(e) im angegebenen Rechenkontext ab.

+ `rxSqlLibPaths`: Ruft den Suchpfad für die Bibliotheksbäume für Pakete während der Ausführung innerhalb von SQL Server ab.

## <a name="examples"></a>Beispiele

### <a name="get-package-location-on-sql-server-compute-context"></a>Abrufen des Paketspeicherorts für einen SQL Server-Rechenkontext

Dieses Paket ruft den Pfad für das **RevoScaleR**-Paket im Rechenkontext *sqlServer* ab.

  ```R
  sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerL)
  ```
  
  ### <a name="get-locations-for-multiple-packages"></a>Abrufen von Speicherorten für mehrere Pakete

Die folgenden Beispiele rufen die Pfade für die Pakete **RevoScaleR** und **lattice** im Rechenkontext *sqlServer* ab. Wenn Informationen über mehrere Pakete gefunden werden, wird ein Zeichenfolgenvektor übergeben, der die Paketnamen enthält.

  ```R
  packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlServer)
  ```



### <a name="list-packages-in-specified-compute-context"></a>Auflisten der Pakete im angegebenen Rechenkontext

Dieses Beispiel listet alle im Rechenkontext *sqlServer* installierten Pakete auf und zeigt sie dann auf der Konsole an.

  ```R
  myPackages <- rxInstalledPackages(computeContext = sqlServer) 
  myPackages
  ```

### <a name="get-package-versions"></a>Abrufen von Paketversionen

Dieses Beispiel ruft die Build- und Versionsnummern für ein im Rechenkontext *sqlServer* installiertes Paket ab.

  ```R
  sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer) 
```

### <a name="install-a-package-on-sql-server"></a>Installieren eines Pakets in SQL Server

In diesem Beispiel wird das Paket **ggplot2** mit seinen Abhängigkeiten im Rechenkontext *sqlServer* installiert.

  ```R
  pkgs <- c("ggplot2")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
  ```

### <a name="remove-a-package-from-sql-server"></a>Entfernen eines Pakets aus SQL Server

In diesem Beispiel wird das Paket **ggplot2** mit seinen Abhängigkeiten aus dem Rechenkontext *sqlServer* entfernt.

  ```R
  pkgs <- c("ggplot2")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
  ```

## <a name="see-also"></a>Siehe auch

[Vorgehensweise zum Deaktivieren der R-Paketverwaltung](../../advanced-analytics/r-services/how-to-enable-or-disable-r-package-management.md)