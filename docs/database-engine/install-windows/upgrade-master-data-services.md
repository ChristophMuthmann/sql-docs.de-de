---
title: Aktualisieren von Master Data Services | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/21/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9c3543f3-3eb9-455d-a9bf-f17e9506ad21
caps.latest.revision: 31
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4abb0b1083aab2b944636e838586a39990e6ad06
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="upgrade-master-data-services"></a>Aktualisieren von Master Data Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  Im Folgenden sind die Szenarien zum Aktualisieren von Microsoft [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]-Master Data Services.  
  
-   [Upgrade ohne Datenbankmodulupgrade](../../database-engine/install-windows/upgrade-master-data-services.md#noengine)  
  
-   [Upgrade mit Datenbankmodulupgrade](../../database-engine/install-windows/upgrade-master-data-services.md#engine)  
  
-   [Upgrade in einem Szenario mit zwei Computern](../../database-engine/install-windows/upgrade-master-data-services.md#twocomputer)  
  
-   [Upgrade mithilfe einer Wiederherstellung einer Datenbank aus einer Sicherung](../../database-engine/install-windows/upgrade-master-data-services.md#restore)  
  
> [!IMPORTANT]  
> -   Upgrades von der [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP1-Version auf die CTP2-Version werden nicht unterstützt.  
> -   Sichern Sie die Datenbank vor dem Ausführen eines beliebigen Upgrades.  
> -   Durch den Upgradevorgang werden gespeicherte Prozeduren neu erstellt und von [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]verwendete Tabellen aktualisiert. Anpassungen, die Sie an einer dieser Komponenten vorgenommen haben, können verloren gehen.  
> -   Modellbereitstellungspakete können nur in der Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden, in der sie erstellt wurden. Sie können keine in [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]oder [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] erstellten Modellbereitstellungspakete für [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]bereitstellen.  
> -   Nachdem Data Quality Services und Master Data Services auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]aktualisiert wurden, wird keine frühere Version des Master Data Services-Add-Ins für Excel mehr funktionieren. Sie können das [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]-Master Data Services-Add-In für Excel unter [Master Data Services Add-in for Microsoft Excel (Master Data Services-Add-In für Microsoft Excel)](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md) herunterladen.  
  
##  <a name="fileLocation"></a> Dateispeicherort  
  
-   In [!INCLUDE[ss2017](../../includes/sssqlv14-md.md)] werden die Dateien standardmäßig in *Laufwerk*:\Programme\Microsoft SQL Server\140\Master Data Services installiert.  

-   In [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] werden die Dateien standardmäßig in *Laufwerk*:\Programme\Microsoft SQL Server\130\Master Data Services installiert.  
  
-   In [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]werden die Dateien standardmäßig in *Laufwerk*:\Programme\Microsoft SQL Server\120\Master Data Services installiert.  
  
-   In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]werden die Dateien standardmäßig in *Laufwerk*:\Programme\Microsoft SQL Server\110\Master Data Services installiert.  
  
-   In [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]werden die Dateien standardmäßig in *Laufwerk*:\Programme\Microsoft SQL Server\Master Data Services installiert.  
  
##  <a name="noengine"></a> Upgrade ohne Datenbankmodulupgrade  
 In diesem Szenario verwenden Sie weiterhin [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] oder [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], um die MDS-Datenbank zu hosten. Sie müssen jedoch das Schema der MDS-Datenbank aktualisieren und dann eine aktuelle [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] -Webanwendung erstellen, um auf die MDS-Datenbank zuzugreifen. Nach dem Upgrade kann auf die MDS-Datenbank nicht mehr von der früheren Webanwendung aus zugegriffen werden.  
  
 Sie können die aktuelle [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] und eine frühere Version von [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] auf demselben Computer installieren. Die Dateien werden in verschiedenen Speicherorten installiert, wie in [Dateispeicherort](#fileLocation)dargestellt.  
  
 **So upgraden Sie ohne das Upgrade des Datenbankmoduls**  
  
1.  Installieren Sie [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] und beliebige andere Funktionen.  
  
    1.  Öffnen Sie den [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] Setup-Assistenten.  
  
    2.  Klicken Sie im linken Bereich auf **Installation**.  
  
    3.  Klicken Sie im rechten Bereich auf **Neue eigenständige SQL Server-Installation oder Hinzufügen von Funktionen zu einer vorhandenen Installation**.  
  
    4.  Wählen Sie auf der Seite **Funktionsauswahl** die Funktion **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** sowie alle weiteren Funktionen aus, die Sie installieren möchten.  
  
    5.  Schließen Sie den Assistenten ab.  
  
2.  Aktualisieren Sie das MDS-Datenbankschema.  
  
    1.  Öffnen Sie den aktuellen [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
        > [!IMPORTANT]  
        >  Um das MDS-Datenbankschema zu aktualisieren, müssen Sie in dem Administratorkonto angemeldet sein, das beim Erstellen der MDS-Datenbank angegeben wurde. Dieser Benutzer weist in der MDS-Datenbank in mdm.tblUser den **ID** -Wert **1**auf.  
  
    2.  Klicken Sie im linken Bereich auf **Datenbankkonfiguration**.  
  
    3.  Klicken Sie im rechten Bereich auf **Datenbank auswählen**, und geben Sie die Informationen für Ihre [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]-, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]-, [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]- oder [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]-Datenbankinstanz an.  
  
    4.  Klicken Sie auf **Datenbank aktualisieren** , um den **Datenbankupgrade-Assistenten**zu starten. Weitere Informationen finden Sie unter [Datenbankupgrade-Assistent &#40;Konfigurations-Manager für Master Data Services&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md).  
  
3.  Erstellen Sie eine Webanwendung.  
  
    1.  Öffnen Sie den aktuellen [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
    2.  Klicken Sie im linken Bereich auf **Webkonfiguration**.  
  
    3.  Wählen Sie im rechten Bereich aus der Liste **Website** eine der folgenden Optionen aus:  
  
        -   **Standardwebsite**, klicken Sie dann auf **Anwendung erstellen**.  
  
        -   **Neue Website erstellen**. Beim Erstellen der Website wird automatisch eine neue Webanwendung erstellt.  
  
        > [!IMPORTANT]  
        >  Die vorhandene MDS-Webanwendung aus einer früheren SQL Server-Version ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] oder [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) kann in der [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Version des Konfigurations-Managers für Master Data Services ausgewählt werden. Sie dürfen nicht die vorhandene Webanwendung auswählen, sondern müssen stattdessen eine [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] -Webanwendung für MDS erstellen. Andernfalls wird beim Versuch, die Webanwendung der aktualisierten MDS-Datenbank zuzuordnen, eine Fehlermeldung mit dem Hinweis ausgegeben, dass auf die angeforderte Seite nicht zugegriffen werden kann, da die zugehörigen Konfigurationsdaten für die Seite ungültig sind.  
        >   
        >  Wenn Sie für die MDS-Webanwendung denselben Namen (Alias) wie für die vorhandene Webanwendung ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]oder [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) verwenden möchten, müssen Sie die Webanwendung und den zugehörigen Anwendungspool zunächst aus IIS löschen und dann mit der [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]-Version des Konfigurations-Managers für Master Data Services eine Webanwendung mit demselben Namen erstellen. Informationen zum Entfernen von Webanwendungen und Anwendungspools aus IIS finden Sie unter [Entfernen einer Anwendung (IIS)](http://go.microsoft.com/fwlink/?LinkId=323537) und [Entfernen eines Anwendungspools (IIS)](http://go.microsoft.com/fwlink/?LinkId=323538).  
  
4.  Ordnen Sie die neue Webanwendung nun der upgegradeten MDS-Datenbank zu.  
  
    1.  Klicken Sie im Abschnitt **Anwendung einer Datenbank zuordnen** auf **Auswählen**.  
  
    2.  Wählen Sie die MDS-Datenbank aus.  
  
    3.  Klicken Sie auf **Anwenden**.  
  
##  <a name="engine"></a> Upgrade mit Datenbankmodulupgrade  
 In diesem Szenario aktualisieren Sie sowohl das Datenbankmodul als auch die [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] -Anwendung von einer früheren Version auf [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] oder [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)].  
  
 **So upgraden Sie mit dem Upgrade des Datenbankmoduls**  
  
1.  **Nur für [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]**: Öffnen Sie **Systemsteuerung** > **Programme und Funktionen**, und deinstallieren Sie Microsoft [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
2.  Aktualisieren Sie das Datenbankmodul auf [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] oder [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)]. Weitere Informationen finden Sie unter [Auswählen einer Upgrademethode für das Datenbankmodul](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md).  
  
3.  Führen Sie alle Schritte in [Upgrade ohne Datenbankmodulupgrade](#noengine) aus.  
  
##  <a name="twocomputer"></a> Upgrade in einem Szenario mit zwei Computern  
 In diesem Szenario wird das Upgrade eines Systems durchgeführt, in dem SQL Server auf zwei Computern installiert ist: auf einem ist [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] oder [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)] installiert, auf dem anderen eine frühere Version von [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)].  
  
 Wenn eine frühere Version von [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] installiert ist, verwenden Sie weiterhin diese zum Hosten Ihrer MDS-Datenbank auf einem Computer. Sie müssen jedoch das Schema der MDS-Datenbank aktualisieren und dann die [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]- oder [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)]-Webanwendung verwenden, um auf die MDS-Datenbank zuzugreifen. Auf die MDS-Datenbank kann nicht mehr von der früheren Version der Webanwendung aus zugegriffen werden.  
  
 **So upgraden Sie in einem Szenario mit zwei Computern**  
  
-   Führen Sie alle Schritte in [Upgrade ohne Datenbankmodulupgrade](#noengine)aus.  
  
##  <a name="restore"></a> Upgrade mithilfe einer Wiederherstellung einer Datenbank aus einer Sicherung  
 In diesem Szenario ist entweder [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] oder [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)] zusammen mit einer früheren Version auf demselben Computer oder auf zwei unterschiedlichen Computern installiert. Vor dem Upgrade wurde eine Datenbank in einer früheren Version als [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] oder [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)] gesichert und muss nun wiederhergestellt werden.  
  
 **So upgraden Sie mithilfe der Wiederherstellung einer Datenbank aus einer Sicherung**  
  
1.  Installieren Sie [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] und beliebige andere Funktionen.  
  
    1.  Öffnen Sie den [!INCLUDE[sssnoversion](../../includes/ssnoversion-md.md)] Setup-Assistenten.  
  
    2.  Klicken Sie im linken Bereich auf **Installation**.  
  
    3.  Klicken Sie im rechten Bereich auf **Neue eigenständige SQL Server-Installation oder Hinzufügen von Funktionen zu einer vorhandenen Installation**.  
  
    4.  Wählen Sie auf der Seite **Funktionsauswahl** die Funktion **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** sowie alle weiteren Funktionen aus, die Sie installieren möchten.  
  
    5.  Schließen Sie den Assistenten ab.  
  
2.  Stellen Sie die Datenbank wieder her, die gesichert wurde.  
  
3.  Upgraden Sie das MDS-Datenbankschema, erstellen Sie eine Webanwendung, und ordnen Sie die neue Webanwendung der upgegradeten MDS-Datenbank zu. Anweisungen finden Sie in den Schritten 2 – 4 im Abschnitt [Upgrade ohne Datenbankmodulupgrade](#noengine).  
  
## <a name="troubleshooting"></a>Problembehandlung  
 **Problem** : Wenn Sie die [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]-, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]-, [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] oder [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] -Webanwendung öffnen, wird die Fehlermeldung „Die Clientversion ist nicht mit der Datenbankversion kompatibel“ angezeigt.  
  
 **Lösung**: Dieses Problem tritt auf, wenn eine [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]-, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]-, [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]- oder[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]-Master Data Manager-Webanwendung versucht, auf eine Datenbank zuzugreifen, die auf [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)]-Master Data Services aktualisiert wurde. Sie müssen stattdessen eine [!INCLUDE[ssSQL16](../../includes/sssqlv14-md.md)]-Webanwendung verwenden.  
  
 Dieses Problem tritt möglicherweise auch auf, wenn Sie beim Upgrade des MDS-Datenbankschemas den **MDS-Anwendungspool** in IIS nicht angehalten und neu gestartet haben. Starten Sie den **MDS-Anwendungspool** neu, um das Problem zu beheben.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Installieren von Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
