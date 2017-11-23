---
title: Konfigurieren Sie PolyBase-Verbindungen zu externen Daten (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6f14ac21-a086-4c05-861f-0a12bf278259
caps.latest.revision: "43"
ms.openlocfilehash: 7d486992f688b5bc914508ef000f23209b4bde89
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="configure-polybase-connectivity-to-external-data"></a>Konfigurieren Sie PolyBase-Verbindungen zu externen Daten
Erläutert das Konfigurieren von PolyBase in SQL Server PDW zur Verbindung mit externen Hadoop oder Microsoft Azure Blob-speicherdatenquellen. Die Verwendung von PolyBase zum Ausführen von Abfragen, die Daten aus mehreren Quellen, einschließlich u. a. Hadoop und Azure Blob-Speicher mit SQL Server PDW integrieren.  
  
### <a name="to-configure-connectivity"></a>Um die Konnektivität konfigurieren  
  
1.  Öffnen von einem Abfragetool, z. B. Sqlcmd oder SQL Server Data Tools (SSDT), und führen Sie Sp_configure, um die aktuellen Einstellungen für 'Hadoop Connectivity' anzuzeigen.  
  
    ![Hadoop-konnektivitätseinstellung](./media/configure-polybase-connectivity-to-external-data/APS_PDW_sp_configure.png "APS_PDW_sp_configure")  
  
2.  Entscheiden Sie, welche Hadoop-Konnektivität festgelegt haben, müssen und gibt an, ob Sie die aktuelle Einstellung ändern müssen. Diese Option gilt für die gesamte SQL Server PDW-Region. Eine vollständige Liste der Konfigurationseinstellungen und Versionen finden Sie unter [Sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
3.  Führen Sie zum Ändern der Einstellung 'Hadoop Connectivity' Sp_configure mit RECONFIGURE ein. Hier sind einige Beispiele.  
  
    ```sql  
    --Enable connectivity to Hortonworks Data Platform for Windows Server (HDP), HDInsight on Analytics Platform System, or HDInsight’s Microsoft Azure blob storage  
    EXEC sp_configure 'hadoop connectivity', 4;   
    RECONFIGURE;  
  
    -- Enable connectivity to Hortonworks Data Platform (HDP)for Linux   
    EXEC sp_configure 'hadoop connectivity', 5;   
    RECONFIGURE;  
  
    -- Enable connectivity to Cloudera CDH for Linux   
    EXEC sp_configure 'hadoop connectivity', 3;   
    RECONFIGURE;  
  
    -- Disable the Hadoop connectivity option   
    EXEC sp_configure 'hadoop connectivity', 0;  
    RECONFIGURE;  
    ```  
  
    Ausgeführte "Sp_configure" mit RECONFIGURE legt den Konfigurationswert fest. Neustarten der Region ist erforderlich, um den Ausführungswert festgelegt wird. Da ein Neustart erforderlich nach Beendigung des nächsten auch ist, müssen Sie den Neustart, bis nach dem nächsten Schritt führen Sie die Core-site.xml ändert.  
  
4.  Um Microsoft Azure Blob-Speicher als eine externe Datenquelle zu aktivieren, fügen Sie mindestens einen der Microsoft Azure-Konto-speicherzugriffsschlüsseln PDW-Core-site.xml-Datei hinzu. So fügen Sie einen Schlüssel hinzu:  
  
    1.  Suchen Sie Ihr Microsoft Azure Storage-Kontoname. So zeigen Sie Speicherkonten, melden Sie sich an den[Azure-Portal](https://portal.azure.com) , und klicken Sie auf **Speicherkonten (klassisch)**.  
  
        ![Windows Azure Storage-Kontoname](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountName.png "APS_PDW_AzureStorageAccountName")  
  
    2.  Suchen Sie Ihre Azure-Speicherkonto-Zugriffsschlüssel an. Zu diesem Zweck klicken Sie auf den Namen des Speicherkontos, und klicken Sie auf dem Blatt "Einstellungen" auf **Schlüssel**. Es werden Name und Ihre kontoschlüssel angezeigt.  
  
        ![Windows Azure-Konto-speicherzugriffsschlüsseln](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountAccessKey.png "APS_PDW_AzureStorageAccountAccessKey")  
  
    3.  Öffnen Sie eine Remotedesktopverbindung mit dem Steuerungsknoten PDW.  
  
    4.  Öffnen Sie die Datei c:\Programme\Microsoft c:\Programme\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf\core-site.xml.  
  
    5.  Core-site.xml wird die folgende Eigenschaft mit den Attributen Name und Wert hinzuzufügen.  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.<your storage account name>.blob.core.windows.net</name>  
          <value><your storage account access key></value>  
        </property>  
        ```  
  
        Dieses Beispiel verwendet die weiter oben dargestellten Konto und den Zugriffsschlüssel an.  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.CustomerX.blob.core.windows.net</name>  
          <value>yyeTfCxxxxxxxxQ5WdnapXw77W+FwzHUhX/p/f26fIpnNFGtewzyRN90e1/qmTOl1xxxxxxxxa0goG71LsNcw==</value>  
        </property>  
        ```  
  
        > [!CAUTION]  
        > Sicherheitsvorkehrungen Sie, bevor die Zugriffsschlüssel in Core-site.xml gespeichert. Jeder Benutzer mit CONTROL SERVER oder ALTER ANY EXTERNAL DATA SOURCE-Berechtigung kann mit eine externen Datenquelle erstellen, die dieses Konto greift auf. Sobald die externen Datenquelle erstellt wurde, können alle SQL Server PDW-Benutzer, die über die Berechtigung zum Erstellen von Tabellen eine externe Tabelle erstellen, die auf dieses Speicherkonto zugreift. Der Benutzer werden dann in der Lage Kontodaten zugreifen und nutzen Sie Ressourcen in das Konto.  
  
    6.  Speichern Sie die Änderungen in Core-site.xml.  
  
5.  Fügen Sie yarn.application.classpath-Eigenschaft und die Werte in die Yarn-site.xml-Datei an.  
  
    Überspringen Sie diesen Schritt, wenn Sie mit einer externen Hadoop 1.3 verbinden.  
  
    Beginnend mit Hadoop-2.0, enthält die Yarn-site.xml-Datei Konfigurationseinstellungen für Hadoop-YARN-Framework. Diese Datei befindet sich auf den Knoten unter **C:\program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf\\**.  
  
    Um PolyBase-Abfragen für eine externe Hadoop-Cluster 2.0 unter Windows oder Linux ausgeführt werden soll, müssen Sie die yarn.application.classpath-Eigenschaft und die Werte, die konsistent mit den Yarn-site.xml-Einstellungen auf dem externen Hadoop-Cluster konfigurieren. Diese Konfiguration ist erforderlich, selbst wenn die externe Hadoop-Cluster die Standardeinstellungen verwendet.  
  
    Beispiel für Standard-Einstellungen:  
  
    ```xml  
    <property>  
        <name>yarn.application.classpath</name>  
        <value>  
          %HADOOP_CONF_DIR%,  
          %HADOOP_COMMON_HOME%/share/hadoop/common/*,  
          %HADOOP_COMMON_HOME%/share/hadoop/common/lib/*,  
          %HADOOP_HDFS_HOME%/share/hadoop/hdfs/*,  
          %HADOOP_HDFS_HOME%/share/hadoop/hdfs/lib/*,  
          %HADOOP_YARN_HOME%/share/hadoop/yarn/*,  
          %HADOOP_YARN_HOME%/share/hadoop/yarn/lib/*  
         </value>  
      </property>  
    ```  
  
    Sobald eine beliebige Eigenschaft in Yarn-site.xml definiert ist, wird diese eigenschafteneinstellungen Einsatz von PolyBase beim Ausführen von Abfragen für den HDInsight-Region. Wenn PolyBase-Abfragen für den HDInsight-Region und einem externen Hadoop-Cluster 2.0 unter Windows ausgeführt werden sollen, Konsistenz aller Dateien Yarn-site.xml muss, andernfalls schlägt die PolyBase-Abfragen fehl.  
  
    Um PolyBase mit dem HDInsight-Region und einem externen Hadoop-Cluster 2.0 ausführen, verwenden Sie die Yarn-site.xml-Standardeinstellungen auf dem externen Hadoop-Cluster.  
  
6.  Starten Sie die PDW-Region an. Zu diesem Zweck verwenden Sie das Configuration Manager-Tool. Finden Sie unter [starten Sie den Konfigurations-Manager &#40; Analyseplattformsystem &#41; ](launch-the-configuration-manager.md).  
  
7.  Überprüfen Sie die Sicherheitseinstellungen für Hadoop-Verbindungen. Wenn die **schwache Authentifizierung** auf Hadoop Seite aktiviert ist, mithilfe von `dfs.permission = true`, müssen Sie einen Hadoop-Benutzer erstellen **Pdw_user** und gewähren von vollständigen Lese- und Schreibberechtigungen für diesen Benutzer. SQL Server PDW und den entsprechenden Aufrufen von SQL Server PDW werden immer als ausgegeben **Pdw_user** die ist ein fester Benutzername und kann nicht in dieser Version von Hadoop-Konnektivität und SQL Server PDW-Version nicht geändert werden. Wenn Sicherheit auf Hadoop mit deaktiviertem `dfs.permission = false`, keine weiteren Aktionen ausgeführt werden müssen.  
  
8.  Entscheiden Sie, welche Benutzer eine externe Datenquelle in der Microsoft Azure Blob-Speicher erstellen können. Geben Sie jeden Benutzer den Namen des Speicherkontos sowie **ALTER ANY EXTERNAL DATA SOURCE** oder **CONTROL SERVER** Berechtigung.  
  
9. Entscheiden Sie für Hadoop-Verbindungen, welche Benutzer auf Hadoop verlagern eine externen Datenquelle erstellen können. Geben Sie diesen Benutzern die IP-Adresse und Port der Anzahl der einzelnen Knoten der Hadoop-Namen, und stellen Sie diesen **ALTER ANY EXTERNAL DATA SOURCE** oder **CONTROL SERVER** Berechtigung.  
  
10. Herstellen einer Verbindung mit WASB erfordert auch DNS-Weiterleitung auf dem Gerät konfiguriert werden. Um DNS-Weiterleitung zu konfigurieren, erfahren Sie unter [mithilfe einer DNS-Weiterleitung zum Auflösen von Non-Appliance DNS-Namen &#40; Analyseplattformsystem &#41; ](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
Autorisierte Benutzer können jetzt externen Datenquellen und externe Dateiformate, externe Tabellen erstellen. Sie können diese verwenden, um Daten aus mehreren Quellen einschließlich Hadoop, integrieren, die Microsoft Azure Blob-Speicher und SQL Server PDW.  
  
## <a name="see-also"></a>Siehe auch  
[Appliance-Konfiguration &#40; Analyseplattformsystem &#41;](appliance-configuration.md)  
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
