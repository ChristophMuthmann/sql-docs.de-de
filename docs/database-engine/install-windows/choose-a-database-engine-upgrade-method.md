---
title: "Wählen einer Upgrademethode für das Datenbankmodul | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5e57a427-2e88-4ef6-b142-4ccad97bcecc
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 164c24f5cfd3c4120c75776764221560392ebd4d
ms.sourcegitcommit: c77a8ac1ab372927c09bf241d486e96881b61ac9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2018
---
# <a name="choose-a-database-engine-upgrade-method"></a>Wählen einer Upgrademethode für das Datenbankmodul
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Es gibt verschiedene zu prüfende Ansätze beim Planen des Upgrades von [!INCLUDE[ssDE](../../includes/ssde-md.md)] von einer früheren Version von SQL Server, um Ausfallzeiten und Risiken zu minimieren. Sie können ein direktes Upgrade ausführen, zu einer neuen Installation migrieren oder ein paralleles Upgrade vornehmen. Das folgende Diagramm hilft Ihnen, zwischen diesen Ansätzen auszuwählen. Jeder der Ansätze im Diagramm wird außerdem nachstehend erläutert. Informationen zu den Entscheidungskriterien im Diagramm finden Sie auch unter [Planen und Testen des Upgradeplans für das Datenbankmodul](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md).  
  
 ![Entscheidungsstruktur der Upgrademethode für das Datenbankmodul](../../database-engine/install-windows/media/database-engine-upgrade-method-decision-tree.png "Database Engine Upgrade Method Decision Tree")  
  
 **Download**  
  
-   Navigieren Sie zum Herunterladen von [!INCLUDE[SSnoversion](../../includes/ssnoversion-md.md)]zum  **[Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server)**.  
  
-   Sie haben ein Azure-Konto?  Wechseln Sie anschließend **[hierhin](http://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.FreeLicenseSQLServer2016SP1DeveloperWindowsServer2016)**, um einen virtuellen Computer zu starten, auf dem [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Developer Edition bereits installiert ist.  
  
> [!NOTE]  
>  Sie können auch ein Upgrade auf Azure SQL-Datenbank erwägen oder Ihre SQL Server-Umgebung als Teil Ihres Upgradeplans virtualisieren. Diese Themen liegen für diese Thema außerhalb des Gültigkeitsbereich, jedoch haben wir hier einige Links bereitgestellt:
>   - [SQL Server auf virtuellen Azure-Computern – Übersicht](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/)
>   - [Azure SQL-Datenbank](https://azure.microsoft.com/en-us/services/sql-database/) 
>   - [Selecting a SQL Server option in Azure (Auswählen einer SQL Server-Option in Azure)](https://azure.microsoft.com/documentation/articles/data-management-azure-sql-database-and-sql-server-iaas/)  
  
##  <a name="UpgradeInPlace"></a> Direktes Upgrade  
 Bei diesem Ansatz aktualisiert das SQL Server-Setup-Programm die vorhandene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Installation durch Ersetzen der vorhandenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Bits durch die neuen [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]-Bits und aktualisiert anschließend alle System- und Benutzerdatenbanken.  Der Ansatz für ein direktes Upgrade ist am einfachsten, erfordert gewisse Ausfallzeiten, erfordert nötigenfalls ein längeres Fallback und wird nicht für alle Szenarien unterstützt. Weitere Informationen zu unterstützten und nicht unterstützten direkten Aktualisierungsszenarien finden Sie unter [Unterstützte Versions- und Editionsupgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades-2017.md).  
  
 Dieser Ansatz wird häufig in den folgenden Szenarien verwendet:  
  
-   Eine Entwicklungsumgebung ohne Konfiguration mit hoher Verfügbarkeit.  
  
-   Eine nicht unternehmenswichtige Produktionsumgebung mit Toleranz für Ausfallzeiten, die auf aktueller Hardware und Software ausgeführt wird. Die Länge der Ausfallzeit ist abhängig von der Größe Ihrer Datenbank und der Geschwindigkeit des E/A-Subsystems. Wenn während des Upgrades von SQL Server 2014 speicheroptimierte Tabellen verwendet werden, erfordert das Upgrade zusätzliche Zeit. Weitere Informationen finden Sie unter [Planen und Testen des Upgradeplans für das Datenbankmodul](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md).  
  
> [!WARNING]  
>  Beim Ausführen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup-Programms wird die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz im Rahmen der vor dem Upgrade erfolgenden Überprüfungen beendet und neu gestartet.  
  
> [!CAUTION]  
>  Wenn Sie auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]aktualisieren, wird die frühere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz überschrieben und ist auf dem Computer folglich nicht mehr vorhanden. Sichern Sie vor dem Upgrade die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken und alle anderen der früheren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz zugeordneten Objekte.  
  
 Das folgende Diagramm bietet einen allgemeinen Überblick über die Schritte, die für ein direktes Upgrade des [!INCLUDE[ssDE](../../includes/ssde-md.md)]s erforderlich sind.  
  
 ![Hoch verfügbares, direktes Update für das Datenbankmodulupgrade](../../database-engine/install-windows/media/database-engine-upgrade-non-ha-in-place-upgrade.png "Database Engine Upgrade Non-HA In-Place Upgrade")  
  
 Ausführliche Schritte finden Sie unter [Upgrade von SQL Server mithilfe des Installations-Assistenten (Setup)](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md).  
  
##  <a name="NewInstallationUpgrade"></a> Migrieren zu einer neuen Installation  
 Bei diesem Ansatz behalten Sie die aktuelle Umgebung bei, während Sie eine neue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Umgebung einrichten. Dies erfolgt häufig auf neuer Hardware und mit einer neuen Version des Betriebssystems. Nach der Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in der neuen Umgebung führen Sie verschiedene Schritte aus, um die neue Umgebung so vorzubereiten, dass eine Migration der vorhandenen Benutzerdatenbanken aus der vorhandenen in die neue Umgebung bei minimierter Ausfallzeit erfolgen kann. Bei diesen Schritten wird Folgendes migriert:  
  
-   **Systemobjekte:** Einige Anwendungen sind von Informationen, Entitäten und/oder Objekten abhängig, die sich außerhalb einer einzelnen Benutzerdatenbank befinden. Normalerweise weist eine Anwendung Abhängigkeiten von den Datenbanken „master“ und „msdb“ sowie von der Benutzerdatenbank auf. Alle Daten, die außerhalb einer Benutzerdatenbank gespeichert werden und für die richtige Funktionsweise dieser Datenbank erforderlich sind, müssen auf der Zielserverinstanz bereitgestellt werden. Beispielsweise werden die Anmeldungen für eine Anwendung als Metadaten in der „master“-Datenbank gespeichert und müssen auf dem Zielserver neu erstellt werden. Wenn ein Anwendungs- oder Datenbank-Wartungsplan von Aufträgen des SQL Server-Agents abhängig ist, deren Metadaten in der „msdb“-Datenbank gespeichert sind, müssen Sie diese Aufträge auf der Zielserverinstanz neu erstellen. Analog dazu werden die Metadaten für einen Trigger auf Serverebene in der „master“-Datenbank gespeichert.  
 
   Wenn Sie die Datenbank für eine Anwendung auf eine andere Serverinstanz verschieben, müssen Sie alle Metadaten der abhängigen Entitäten und Objekte in „master“ und „msdb“ auf der Zielserverinstanz neu erstellen. Wenn für eine Datenbankanwendung beispielsweise Trigger auf Serverebene verwendet werden, genügt es nicht, die Datenbank im neuen System lediglich anzufügen oder wiederherzustellen. Die Datenbank funktioniert nicht wie erwartet, wenn Sie die Metadaten für diese Trigger in der „master“-Datenbank nicht manuell neu erstellen. Ausführliche Informationen finden Sie unter [Verwalten von Metadaten beim Bereitstellen einer Datenbank auf einer anderen Serverinstanz &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  
-   **In der „msdb“-Datenbank gespeicherte Integration Services-Pakete:** Wenn Sie Pakete in der „msdb“-Datenbank speichern, müssen Sie diese Pakete entweder per Skript mithilfe des Hilfsprogramms [dtutil](../../integration-services/dtutil-utility.md) entfernen oder sie auf dem neuen Server erneut bereitstellen. Vor der Verwendung der Pakete auf dem neuen Server müssen Sie die Pakete auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]aktualisieren. Weitere Informationen finden Sie unter [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
-   **Verschlüsselungsschlüssel für Reporting Services:** Das Erstellen einer Sicherungskopie des symmetrischen Schlüssels, der zum Verschlüsseln sensibler Informationen verwendet wird, ist ein wichtiger Bestandteil der Berichtsserverkonfiguration. Eine Sicherungskopie des Schlüssels ist für viele Routinevorgänge erforderlich und ermöglicht Ihnen das Wiederverwenden einer vorhandenen Berichtsserver-Datenbank in einer neuen Installation. Weitere Informationen finden Sie unter [Sichern und Wiederherstellen von Reporting Services-Verschlüsselungsschlüsseln](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md) und [Upgrade und Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)  
  
 Sobald die neue   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Umgebung über die gleichen Systemobjekte wie die vorhandene Umgebung verfügt, können Sie die Benutzerdatenbanken aus dem vorhandenen System in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz auf eine Weise migrieren, die Ausfallzeiten für das vorhandene System minimiert. Sie erreichen die Datenbankmigration entweder mittels Sicherung und Wiederherstellung oder indem Sie bei einer SAN-Umgebung die LUNs auf neue Ziele verweisen. Die Schritte für beide Methoden sind in den folgenden Diagrammen dargestellt.  
  
> [!CAUTION]  
>  Die Länge der Ausfallzeit ist abhängig von der Größe Ihrer Datenbank und der Geschwindigkeit des E/A-Subsystems. Wenn während des Upgrades von SQL Server 2014 speicheroptimierte Tabellen verwendet werden, erfordert das Upgrade zusätzliche Zeit. Weitere Informationen finden Sie unter [Planen und Testen des Upgradeplans für das Datenbankmodul](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md).  
  
 Nach der Migration der Benutzerdatenbanken verweisen Sie neue Benutzer mithilfe verschiedener Methoden (z. B. Umbenennen des Servers, Verwenden eines DNS-Eintrags, Ändern von Verbindungszeichenfolgen) auf die neue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz.  Durch diesen neuen Installationsansatz werden Risiken und Ausfallzeiten im Vergleich mit einem direkten Upgrade reduziert und Upgrades von Hardware und Betriebssystem im Zusammenspiel mit dem Upgrade auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erleichtert.  
  
> [!NOTE]  
>  Falls Sie eine Lösung für Hochverfügbarkeit oder eine andere Umgebung mit mehreren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanzen haben, fahren Sie mit dem [parallelen Upgrade](#RollingUpgrade)fort. Wenn keine Lösung für Hochverfügbarkeit vorhanden ist, können Sie entweder vorübergehend die [Datenbankspiegelung](http://msdn.microsoft.com/library/ms190941.aspx) konfigurieren, um Ausfallzeiten zu minimieren und dieses Upgrade zu vereinfachen, oder die Chance wahrnehmen, eine [AlwayOn-Verfügbarkeitsgruppe](http://msdn.microsoft.com/library/hh510260.aspx) als dauerhafte Lösung für Hochverfügbarkeit zu konfigurieren.  
  
 Beispielsweise können Sie diesen Ansatz befolgen, um Folgendes zu aktualisieren:  
  
-   Eine Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unter einem nicht unterstützten Betriebssystem.  
  
-   Eine x86-Installation von SQL Server, da [!INCLUDE[ss2016](../../includes/sssql15-md.md)] und höher keine x86-Installationen unterstützen.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf neue Hardware und/oder eine neue Version des Betriebssystems.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Verbindung mit einer Serverkonsolidierung.  
  
-   SQL Server 2005, da [!INCLUDE[ss2016](../../includes/sssql15-md.md)] und kein direktes Upgrade von SQL Server 2005 unterstützen. Weitere Informationen finden Sie unter [Führen Sie ein Upgrade von SQL Server 2005 aus?](../../database-engine/install-windows/are-you-upgrading-from-sql-server-2005.md).  
  
 Die erforderlichen Schritte für ein Upgrade auf eine neue Installation hängen zum Teil davon ab, ob Sie zugeordneten oder SAN-Speicher verwenden.  
  
-   **Umgebung mit zugeordnetem Speicher:** Wenn Sie eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Umgebung mit zugeordnetem Speicher haben, begleiten Sie das folgende Diagramm und die darin enthaltenen Links durch die Schritte, die für ein Upgrade auf eine neue Installation des [!INCLUDE[ssDE](../../includes/ssde-md.md)]s erforderlich sind.  
  
     ![Neue Installationsupgrademethode mithilfe einer Sicherung und der Wiederherstellung für einen angeschlossenen Speicher](../../database-engine/install-windows/media/new-installation-upgrade-method-using-backup-and-restore-for-attached-storage.png "New installation upgrade method using backup and restore for attached storage")  
  
-   **SAN-Speicherumgebung:** Wenn Sie eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Umgebung mit SAN-Speicher haben, begleiten Sie das folgende Diagramm und die darin enthaltenen Links durch die Schritte, die für ein Upgrade auf eine neue Installation des [!INCLUDE[ssDE](../../includes/ssde-md.md)]s erforderlich sind.  
  
     ![Neue Installationsupgrademethode mithilfe von Trennen und Anfügen für den SAN-Speicher](../../database-engine/install-windows/media/new-installation-upgrade-method-using-detach-and-attach-for-san-storage.png "New installation upgrade method using detach and attach for SAN storage")  
  
##  <a name="RollingUpgrade"></a> parallelen Upgrade  
 Ein paralleles Update ist in Umgebungen mit SQL Server-Lösungen mit mehreren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen erforderlich, die in einer bestimmten Reihenfolge aktualisiert werden müssen, um die Betriebszeit zu maximieren, Risiken zu minimieren und Funktionalität beizubehalten. Ein paralleles Upgrade ist im Wesentlichen die Aktualisierung mehrerer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen in einer bestimmten Reihenfolge, wobei entweder ein direktes Upgrade jeder vorhandenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz oder ein Upgrade auf eine neue Installation erfolgt, um die Aktualisierung von Hardware und/oder des Betriebssystems im Rahmen des Upgradeprojekts zu erleichtern. Es gibt eine Reihe von Szenarien, in denen der parallele Upgradeansatz befolgt werden muss. Diese Szenarien sind in den folgenden Themen dokumentiert:  
  
-   AlwaysOn-Verfügbarkeitsgruppen: Ausführliche Schritte zum Ausführen eines parallelen Upgrades in dieser Umgebung finden Sie unter [Upgraden von AlwaysOn-Verfügbarkeitsgruppen-Replikatsinstanzen](../../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).  
  
-   Failoverclusteringinstanzen: Ausführliche Schritte zum Ausführen eines parallelen Upgrades in dieser Umgebung finden Sie unter [Aktualisieren einer SQL Server-Failoverclusterinstanz](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md).  
  
-   Gespiegelte Instanzen: Ausführliche Schritte zum Ausführen eines parallelen Upgrades in dieser Umgebung finden Sie unter [Upgrade von gespiegelten Instanzen](../../database-engine/database-mirroring/upgrading-mirrored-instances.md).  
  
-   Protokollversandinstanzen: Ausführliche Schritte zum Ausführen eines parallelen Upgrades in dieser Umgebung finden Sie unter [Aktualisieren des Protokollversands für SQL Server (Transact-SQL)](../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   Replikationsumgebung: Ausführliche Schritte zum Ausführen eines parallelen Upgrades in dieser Umgebung finden Sie unter [Aktualisieren von replizierten Datenbanken](../../database-engine/install-windows/upgrade-replicated-databases.md).
  
-   Eine horizontal hochskalierte SQL Server Reporting Services-Umgebung: Ausführliche Schritte zum Ausführen eines parallelen Upgrades in dieser Umgebung finden Sie unter [Aktualisieren und Migrieren von Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
## <a name="next-steps"></a>Nächste Schritte
 [Planen und Testen des Upgradeplans für das Datenbankmodul](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)   
 [Abschließen des Datenbankmodul-Upgrades](../../database-engine/install-windows/complete-the-database-engine-upgrade.md)  
  
  
