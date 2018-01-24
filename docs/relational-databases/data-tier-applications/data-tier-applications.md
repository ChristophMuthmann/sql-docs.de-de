---
title: Datenebenenanwendungen| Microsoft-Dokumentation
ms.custom: 
ms.date: 08/12/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: data-tier-applications
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- designing DACs
- How to [DAC]
- data-tier application [SQL Server], designing
- wizard [DAC]
ms.assetid: a04a2aba-d07a-4423-ab8a-0a31658f6317
caps.latest.revision: "31"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d42c7d587e18e306a15a95e4576e312a0e7c31c0
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="data-tier-applications"></a>Datenebenenanwendungen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Eine Datenebenenanwendung (DAC) ist eine logische Datenbankverwaltungsentität, die alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Objekte definiert, beispielsweise Tabellen, Sichten und Instanzobjekte, einschließlich Anmeldenamen, die mit der Datenbank eines Benutzers verknüpft sind. Eine DAC ist eine in sich geschlossene Einheit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbankbereitstellung, mit der Datenebenenentwickler und Datenbankadministratoren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Objekte in ein portables Artefakt, das sog. "DAC-Paket", packen können. Selbiges ist auch als DACPAC bekannt.  
  
 Ein BACPAC ist ein verwandtes Artefakt, das das Datenbankschema sowie die in der Datenbank gespeicherten Daten kapselt.  
  
## <a name="benefits-of-data-tier-applications"></a>Vorteile von Datenebenenanwendungen  
 Der Lebenszyklus der meisten Datenbankanwendungen zwingt Entwickler und Datenbankadministratoren dazu, Skripts und Ad-hoc-Integrationsbenachrichtigungen für Anwendungsaktualisierungen und Wartungsaktivitäten freizugeben und auszutauschen. Dies stellt bei wenigen Datenbanken kein Problem dar. Es kann jedoch schnell dazu führen, dass sie nicht mehr skalierbar sind, wenn die Datenbanken in puncto Anzahl, Größe und Komplexität wachsen.  
  
 Eine DAC ist ein Datenbank-Lebenszyklusverwaltungs- und Produktivitätstool, womit die Entwicklung deklarativer Datenbanken ermöglicht wird, um Entwicklung und Verwaltung zu vereinfachen. Ein Entwickler kann eine Datenbank in einem SQL Server Data Tools-Datenbankprojekt erstellen und die Datenbank anschließend in einem DACPAC erstellen, um sie an einen Datenbankadministrator zu übergeben. Der Datenbankadministrator kann die DAC mit SQL Server Management Studio auf einer Test- oder Produktionsinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] bereitstellen. Der Datenbankadministrator kann alternativ mit SQL Server Management Studio mithilfe des DACPAC eine zuvor bereitgestellte Datenbank aktualisieren. Zum Abschließen des Lebenszyklus kann der Datenbankadministrator die Datenbank in einen DACPAC extrahieren und sie einem Entwickler übergeben, damit entweder Test- oder Produktionsanpassungen reflektiert werden oder weitere Datenbankentwurfsänderungen als Reaktion auf Änderungen in der Anwendung ermöglicht werden können.  
  
 Der Vorteil einer DAC-gesteuerten Bereitstellung im Gegensatz zu einer skriptgesteuerten Bereitstellung besteht darin, dass das Tool dem Datenbankadministrator beim Identifizieren und Überprüfen von Verhaltensweisen verschiedener Quell- und Zieldatenbanken behilflich ist. Während der Upgrades warnt das Tool den Datenbankadministrator, wenn das Upgrade Datenverlust verursachen könnte, und es stellt auch einen Upgradeplan bereit. Der Datenbankadministrator kann den Plan auswerten und dann das Tool verwenden, um mit dem Upgrade fortzufahren.  
  
 Der DAC unterstützt auch die Versionsverwaltung, um dem Entwickler und dem Datenbankadministrator zu helfen, die Datenbankherkunft während des Lebenszyklus zu warten und zu verwalten.  
  
## <a name="dac-concepts"></a>Konzepte von DAC  
 Eine DAC vereinfacht die Entwicklung, Bereitstellung und Verwaltung der Datenebenenelemente, die eine Anwendung unterstützen:  
  
-   Eine Datenebenenanwendung (DAC) ist eine logische Datenbankverwaltungsentität, die alle SQL Server-Objekte definiert, beispielsweise Tabellen, Sichten und Instanzobjekte, einschließlich Anmeldenamen, die mit der Datenbank eines Benutzers verknüpft sind. Sie ist eine in sich geschlossene Einheit der SQL Server-Datenbankbereitstellung, mit der Datenebenenentwickler und Datenbankadministratoren SQL Server-Objekte in ein portables Artefakt, das sog. "DAC-Paket" oder die sog. DACPAC-Datei, packen können.  
  
-   Damit eine SQL Server-Datenbank als DAC behandelt wird, muss sie registriert werden, und zwar entweder explizit durch einen Benutzervorgang oder implizit durch eine der DAC-Vorgänge. Wenn eine Datenbank registriert wird, werden die DAC-Version und andere Eigenschaften als Teil der Metadaten der Datenbank aufgezeichnet. Umgekehrt kann die Registrierung einer Datenbank auch aufgehoben werden, wodurch die DAC-Eigenschaften entfernt werden.  
  
-   Im Allgemeinen können DAC-Tools DACPAC-Dateien lesen, die von DAC-Tools früherer SQL Server-Versionen generiert wurden. Zudem können von den DAC-Tools DACPAC-Dateien für frühere Versionen von SQL Server bereitgestellt werden. Demgegenüber können DAC-Tools früherer Versionen keine DACPAC-Dateien lesen, die mit höheren DAC-Tool-Versionen generiert wurden. Dies gilt insbesondere in folgenden Fällen:  
  
    -   DAC-Vorgänge wurden in SQL Server 2008 R2 eingeführt. Zusätzlich zu SQL Server 2008 R2-Datenbanken unterstützen die Tools die Generierung der DACPAC-Dateien von SQL Server 2008, SQL Server 2005 und SQL Server 2000-Datenbanken.  
  
    -   Zusätzlich zu SQL Server 2016-Datenbanken können die im Lieferumfang von SQL Server 2016 enthaltenen Tools durch DAC-Tools, die im Lieferumfang von SQL Server 2008 R2 oder SQL Server 2012 enthalten sind, generierte DACPAC-Dateien lesen. Dies schließt Datenbanken von SQL Server 2014, 2012, 2008 R2, 2008 und 2005 ein, aber **nicht** SQL Server 2000.  
  
    -   DAC-Tools von SQL Server 2008 R2 können keine DACPAC-Dateien lesen, die von [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]- oder [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Tools generiert wurden.  
  
-   Ein DACPAC ist eine Windows-Datei mit einer Erweiterung DACPAC. Die Datei unterstützt ein offenes Format. Es besteht aus mehreren XML-Abschnitten, die Details der DACPAC-Herkunft bereitstellen, sowie den Objekten in der Datenbank und anderen Eigenschaften. Ein erfahrener Benutzer kann die Datei mit dem Hilfsprogramm "DacUnpack.exe" entpacken, das mit dem Produkt geliefert wird, um jeden Abschnitt genauer zu überprüfen.  
  
-   Der Benutzer muss ein Mitglied der dbmanager-Rolle sein, oder er muss der CREATE DATABASE-Berechtigung zugeordnet sein, um eine Datenbank zu erstellen, einschließlich dem Erstellen einer Datenbank durch Bereitstellen eines DAC-Pakets. Der Benutzer muss ein Mitglied der dbmanager-Rolle sein, oder er muss der DROP DATABASE-Berechtigung zugeordnet sein, um eine Datenbank löschen zu können.  
  
## <a name="dac-tools"></a>DAC-Tools  
 Ein DACPAC kann nahtlos von mehreren Tools, die im Lieferumfang von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] enthalten sind, verwendet werden. Diese Tools erfüllen die Anforderungen verschiedener physischer Benutzer, indem DACPAC als interoperable Einheit verwendet wird.  
  
-   Anwendungsentwickler:  
  
    -   Sie können mithilfe eines SQL Server-Datentools-Datenbankprojekts eine Datenbank entwerfen. Eine erfolgreiche Erstellung dieses Projekts ergibt sich in der Generierung von einem DACPAC, der in einer DACPAC-Datei enthalten hat.  
  
    -   Sie können einen DACPAC in ein Datenbankprojekt importieren und weiterhin die Datenbank entwerfen.  
  
        SQL Server Data Tools unterstützt auch Local DB für eine nicht verbundene, clientseitige Datenbankanwendungsentwicklung. Der Entwickler kann eine Momentaufnahme dieser lokalen Datenbank erstellen, um in einer DACPAC-Datei enthaltenen DACPAC zu erstellen.  
  
    -   Unabhängig davon kann der Entwickler ein Datenbankprojekt direkt in einer Datenbank veröffentlichen, und zwar ohne ein DACPAC zu generieren. Der Veröffentlichungsvorgang weist ein ähnliches Verwalten auf wie der Bereitstellungsvorgang anderer Tools.  
  
-   Datenbankadministratoren:  
  
    -   Sie können einen DACPAC mithilfe von SQL Server Management Studio aus einer vorhandenen Datenbank extrahieren und auch andere DAC-Vorgänge ausführen.  
  
    -   Außerdem kann der Datenbankadministrator für eine [!INCLUDE[ssSDS](../../includes/sssds-md.md)] das Verwaltungsportal für SQL Azure für DAC-Vorgänge verwenden.  
  
-   Unabhängige Softwareanbieter:  
  
    -   Hostende Dienste und andere Datenverwaltungsprodukte für SQL Server können die DACFx-API für DAC-Vorgänge verwenden.  
  
-   IT-Administratoren:  
  
    -   IT-Systemintegratoren und -Administratoren können das Befehlszeilentool "SqlPackage.exe" für DAC-Vorgänge verwenden.  
  
## <a name="dac-operations"></a>DAC-Vorgänge  
 Ein DAC unterstützt die folgenden Vorgänge:  
  
-   **EXTRACT**: Der Benutzer kann eine Datenbank in eine DACPAC-Datei extrahieren.  
  
-   **DEPLOY**: Der Benutzer kann eine DACPAC-Datei auf einem Hostserver bereitstellen. Wenn die Bereitstellung in einem Verwaltbarkeitstool wie SQL Server Management Studio oder dem Verwaltungsportal für SQL Azure ausgeführt wird, wird die resultierende Datenbank im Hostserver implizit als Datenebenenanwendung registriert.  
  
-   **REGISTER**: Der Benutzer kann eine Datenbank als Datenebenenanwendung registrieren.  
  
-   **UNREGISTER**: Die Registrierung einer zuvor als DAC registrierten Datenbank kann aufgehoben werden.  
  
-   **UPGRADE**: Eine Datenbank kann mit einer DACPAC-Datei aktualisiert werden. Ein Upgrade wird sogar auf Datenbanken, die zuvor nicht als Datenebenenanwendungen registriert waren, unterstützt, doch aufgrund des Upgrades wird die Datenbank implizit registriert.  
  
## <a name="bacpac"></a>BACPAC  
 Eine BACPAC-Datei ist eine Windows-Datei mit der Erweiterung ".bacpac", die das Schema und die Daten einer Datenbank kapselt. Der Hauptzweck einer BACPAC-Datei besteht darin, eine Datenbank von einem Server auf einen anderen zu verschieben – oder eine [Datenbank von einem lokalen Server zur Cloud zu migrieren](https://azure.microsoft.com/documentation/articles/sql-database-cloud-migrate/) – und eine vorhandene Datenbank in einem offenen Format zu archivieren.  
  
 Das BACPAC-Dateiformat ist ein offenes Dateiformat (vergleichbar mit DACPAC). Die Schemainhalte von BACPAC sind mit DACPAC identisch. Die Daten in einer BACPAC-Datei werden im JSON-Format gespeichert.  
  
 DACPAC und BACPAC sind ähnlich, aber sie zielen auf andere Szenarien ab. Ein DACPAC dient zum Erfassen und Bereitstellen von Schemas, einschließlich der Aktualisierung einer vorhandenen Datenbank. DACPAC-Dateien werden primär zum Bereitstellen eines streng definierten Schemas für die Entwicklung, Tests und anschließenden Produktionsumgebungen genutzt. Umgekehrt kann das Produktionsschema erfasst und erneut in Test- und Entwicklungsumgebungen angewendet werden.  
  
 Eine BACPAC-Datei dient andererseits der Erfassung von Schemas und Daten. Dabei werden zwei Hauptoperationen unterstützt.  
  
-   **EXPORT**: Der Benutzer kann das Schema und die Daten einer Datenbank in eine BACPAC-Datei exportieren.  
  
-   **IMPORT**: Der Benutzer kann das Schema und die Daten in eine neue Datenbank auf dem Hostserver importieren.  
  
 Beide Funktionen werden von den Datenbankverwaltungstools unterstützt: SQL Server Management Studio, das Azure-Portal und die DACFx-API.  
  
## <a name="permissions"></a>Berechtigungen  
 Der Benutzer muss Mitglied der **dbmanager**-Rolle sein oder **CREATE DATABASE**-Berechtigungen erhalten haben, um eine Datenbank erstellen zu können. Dies gilt auch für das Erstellen einer Datenbank durch Bereitstellen eines DAC-Pakets. Der Benutzer muss Mitglied der **dbmanager**-Rolle sein oder **DROP DATABASE**-Berechtigungen erhalten haben, um eine Datenbank löschen zu können.  
  
## <a name="data-tier-application-tasks"></a>Tasks der Datenebenenanwendung  
  
|Task|Themenlink|  
|----------------------|-----------|  
|Beschreibt, wie eine DAC-Paketdatei zum Erstellen einer neuen DAC-Instanz verwendet wird.|[Bereitstellen einer Datenebenenanwendung](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)|  
|Beschreibt, wie eine neue DAC-Paketdatei zum Aktualisieren einer Instanz auf eine neue Version der DAC verwendet wird.|[Upgrade einer Datenebenenanwendung](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md)|  
|Beschreibt, wie eine DAC-Instanz entfernt wird. Sie können auswählen, ob Sie die zugeordnete Datenbank auch trennen oder löschen möchten, oder ob die Datenbank intakt bleiben soll.|[Löschen einer Datenebenenanwendung](../../relational-databases/data-tier-applications/delete-a-data-tier-application.md)|  
|Beschreibt, wie die Integrität derzeit bereitgestellter DACs mithilfe des SQL Server-Hilfsprogramms angezeigt wird.|[Überwachen von Datenebenenanwendungen](../../relational-databases/data-tier-applications/monitor-data-tier-applications.md)|  
|Beschreibt, wie eine BACPAC-Datei erstellt wird, die ein Archiv der Daten und Metadaten einer DAC enthält.|[Exportieren einer Datenebenenanwendung](../../relational-databases/data-tier-applications/export-a-data-tier-application.md)|  
|Beschreibt, wie mit einer DAC-Archivdatei (.bacpac) entweder eine logische Wiederherstellung einer DAC ausgeführt wird oder die DAC auf einer anderen Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] oder [!INCLUDE[ssSDS](../../includes/sssds-md.md)] migriert wird.|[Importieren einer BACPAC-Datei zum Erstellen einer neuen Benutzerdatenbank](../../relational-databases/data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)|  
|Beschreibt, wie eine BACPAC-Datei importiert wird, um eine neue Benutzerdatenbank innerhalb einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu erstellen.|[Extrahieren einer DAC aus einer Datenbank](../../relational-databases/data-tier-applications/extract-a-dac-from-a-database.md)|  
|Beschreibt, wie eine vorhandene Datenbank auf eine DAC-Instanz heraufgestuft wird. Eine DAC-Definition wird in der Systemdatenbank erstellt und gespeichert.|[Registrieren einer Datenbank als DAC](../../relational-databases/data-tier-applications/register-a-database-as-a-dac.md)|  
|Beschreibt, wie vor der Verwendung eines DAC-Pakets in einem Produktionssystem sein Inhalt und die Aktionen überprüft werden, die bei einem DAC-Upgrade ausgeführt werden.|[Überprüfen eines DAC-Pakets](../../relational-databases/data-tier-applications/validate-a-dac-package.md)|  
|Beschreibt, wie der Inhalt eines DAC-Pakets in einem Ordner abgelegt wird, in dem ein Datenbankadministrator vor der Bereitstellung auf einem Produktionsserver überprüfen kann, was die DAC bewirkt.|[Entpacken eines DAC-Pakets](../../relational-databases/data-tier-applications/unpack-a-dac-package.md)|  
|Beschreibt die Verwendung eines Assistenten, um eine vorhandene Datenbank bereitzustellen. Der Assistent führt die Bereitstellung mithilfe von DACs aus.|[Bereitstellen einer Datenbank mit DAC](../../relational-databases/data-tier-applications/deploy-a-database-by-using-a-dac.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [DAC-Unterstützung für SQL Server-Objekte und -Versionen](../../relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions.md)  
  
  
