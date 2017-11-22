---
title: PolyBase-Konfiguration | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: polybase
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80ff73c1-2861-438b-a13f-309155f3d6e1
caps.latest.revision: "17"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d796fb91c46e2620a80d2bedb481156657aeb539
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="polybase-configuration"></a>PolyBase-Konfiguration
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Verwenden Sie die folgenden Vorgehensweisen, um PolyBase zu konfigurieren.  
  
## <a name="external-data-source-configuration"></a>Konfigurieren der externen Datenquelle  
 Sie müssen die Verbindung von SQL Server zur externen Datenquelle sicherstellen. Der Verbindungstyp wirkt sich stark auf die Abfrageleistung aus. Beispielsweise führt eine 10 GBit-Ethernet-Verbindung zu einer schnelleren Abfrageantwortzeit für PolyBase-Abfragen als eine 1 GBit-Ethernet-Verbindung.  
  
 Sie müssen SQL Server mithilfe von **sp_configure**für die Verbindung mit Ihrer Hadoop-Version oder Azure-BLOB-Speicher konfigurieren. PolyBase unterstützt zwei Hadoop-Distributionen: Hortonworks Data Platform (HDP) und Cloudera Distributed Hadoop (CDH).  Eine vollständige Liste der unterstützten externen Datenquellen finden Sie unter [Konfiguration der PolyBase-Netzwerkkonnektivität &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
Bitte beachten Sie: PolyBase unterstützt nicht Cloudera Encrypted Zones. 
  
### <a name="run-spconfigure"></a>Ausführen von sp_configure  
  
1.  Führen Sie sp_configure ‘hadoop connectivity’ aus, und legen Sie einen geeigneten Wert fest.  Informationen zum Ermitteln des Werts finden Sie unter [Konfiguration der PolyBase-Netzwerkkonnektivität &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
  
    ```tsql  
    -- Values map to various external data sources.  
    -- Example: value 7 stands for Azure blob storage and Hortonworks HDP 2.3 on Linux.  
    sp_configure @configname = 'hadoop connectivity', @configvalue = 7;   
    GO   
  
    RECONFIGURE   
    GO   
    ```  
  
2.  Sie müssen SQL Server mithilfe von **services.msc** neu starten. Durch den Neustart von SQL Server werden folgende Dienste neu gestartet:  
  
    -   SQL Server PolyBase-Datenverschiebungsdienst  
  
    -   SQL Server PolyBase-Modul  
  
## <a name="pushdown-configuration"></a>Pushdown-Konfiguration  
 Aktivieren Sie zur Verbesserung der Abfrageleistung die Pushdown-Berechnung für einen Hadoop-Cluster, den Sie benötigen, um SQL Server spezifische Konfigurationsparameter für Ihre Hadoop-Umgebung zur Verfügung zu stellen:  
  
1.  Suchen Sie die Datei **yarn-site.xml** im Installationspfad von SQL Server. In der Regel lautet der Pfad:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  Suchen Sie auf dem Hadoop-Computer die analoge Datei im Hadoop-Konfigurationsverzeichnis. Suchen Sie in der Datei den Wert des Konfigurationsschlüssels „yarn.application.classpath.“, und kopieren Sie diesen.  
  
3.  Suchen Sie auf dem SQL Server-Computer in der Datei **yarn.site.xml** die Eigenschaft **yarn.application.classpath** . Fügen Sie den Wert vom Hadoop-Computer in das Element „Value“ ein.  

4. Fügen Sie für alle CDH 5.X-Versionen die Konfigurationsparameter **mapreduce.application.classpath** entweder an das Ende Ihrer **yarn.site.xml-Datei** oder innerhalb der **mapred-site.xml-Datei** an. HortonWorks enthält diese Konfigurationen innerhalb der **yarn.application.classpath**-Konfigurationen.

## <a name="connecting-to-hadoop-cluster-with-hadooprpcprotection-setting"></a>Herstellen einer Verbindung mit einem Hadoop-Cluster mit der Einstellung „Hadoop.RPC.Protection“
Eine gängige Methode zum Sichern der Kommunikation in einem Hadoop-Cluster ist das Ändern der Konfiguration „hadoop.rpc.protection“ zu „Datenschutz“ oder „Integrität“. Standardmäßig geht PolyBase davon aus, dass die Konfiguration auf „Authentifizieren“ festgelegt ist. Um diese Standardeinstellung zu überschreiben, müssen Sie folgende Eigenschaft zur Datei „core-site.xml“ hinzufügen. Das Ändern dieser Konfiguration ermöglicht eine sichere Datenübertragung zwischen Hadoop-Knoten und eine SSL-Verbindung zu SQL Server.

```
<!-- RPC Encryption information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG -->
  <property>
    <name>hadoop.rpc.protection</name>
    <value></value>
  </property> 
```




## <a name="example-yarn-sitexml-and-mapred-sitexml-files-for-cdh-5x-cluster"></a>Beispiel: „yarn-site.xml“- und „mapred-site.xml“-Dateien für CDH 5.X-Cluster



„Yarn-site.xml“ mit der Konfiguration „yarn.application.classpath“ und „mapreduce.application.classpath“
```
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
  <property>
     <name>yarn.resourcemanager.connect.max-wait.ms</name>
     <value>40000</value>
  </property>
  <property>
     <name>yarn.resourcemanager.connect.retry-interval.ms</name>
     <value>30000</value>
  </property>
<!-- Applications' Configuration-->
  <property>
    <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
     <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
     <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
     <name>yarn.application.classpath</name>
     <value>$HADOOP_CLIENT_CONF_DIR,$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/*,$HADOOP_COMMON_HOME/lib/*,$HADOOP_HDFS_HOME/*,$HADOOP_HDFS_HOME/lib/*,$HADOOP_YARN_HOME/*,$HADOOP_YARN_HOME/lib/,$HADOOP_MAPRED_HOME/*,$HADOOP_MAPRED_HOME/lib/*,$MR2_CLASSPATH*</value>
  </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
  <property>
     <name>yarn.resourcemanager.principal</name>
     <value></value>
  </property>
-->
</configuration>

```
Wenn Sie die beiden Konfigurationseinstellungen in mapred-site.xml und yarn-site.xml aufteilen, erhalten Sie die folgenden beiden Dateien:

**yarn-site.xml**
```
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
  <property>
     <name>yarn.resourcemanager.connect.max-wait.ms</name>
     <value>40000</value>
  </property>
  <property>
     <name>yarn.resourcemanager.connect.retry-interval.ms</name>
     <value>30000</value>
  </property>
<!-- Applications' Configuration-->
  <property>
    <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
     <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
     <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
     <name>yarn.application.classpath</name>
     <value>$HADOOP_CLIENT_CONF_DIR,$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/*,$HADOOP_COMMON_HOME/lib/*,$HADOOP_HDFS_HOME/*,$HADOOP_HDFS_HOME/lib/*,$HADOOP_YARN_HOME/*,$HADOOP_YARN_HOME/lib/*</value>
  </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
  <property>
     <name>yarn.resourcemanager.principal</name>
     <value></value>
  </property>
-->
</configuration>
```

**mapred-site.xml**

Beachten Sie, dass die Eigenschaft mapreduce.application.classpath hinzugefügt wurde. In CDH 5.x finden Sie die Konfigurationswerte unter derselben Namenskonvention in Ambari.

```
<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
<configuration xmlns:xi="http://www.w3.org/2001/XInclude">
  <property>
    <name>mapred.min.split.size</name>
      <value>1073741824</value>
  </property>
  <property>
    <name>mapreduce.app-submission.cross-platform</name>
    <value>true</value>
  </property>
<property>
    <name>mapreduce.application.classpath</name>
    <value>$HADOOP_MAPRED_HOME/*,$HADOOP_MAPRED_HOME/lib/*,$MR2_CLASSPATH</value>
  </property>


<!--kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
  <property>
    <name>mapreduce.jobhistory.principal</name>
    <value></value>
  </property>
  <property>
    <name>mapreduce.jobhistory.address</name>
    <value></value>
  </property>
-->
</configuration>
  
```
  
## <a name="kerberos-configuration"></a>Kerberos-Konfiguration  
Bitte beachten Sie, dass es zur Authentifizierung von PolyBase bei einem gesicherten Kerberos-Cluster erforderlich ist, die Einstellung hadoop.rpc.protection auf Authentifizierung festzulegen. Dadurch bleibt die Datenkommunikation zwischen den Hadoop-Knoten unverschlüsselt. 

 So stellen Sie eine Verbindung mit einem mit Kerberos geschützten Hadoop-Cluster [mithilfe von MIT KDC] her:
   
  
1.  Suchen Sie das Hadoop-Konfigurationsverzeichnis im Installationspfad von SQL Server. In der Regel lautet der Pfad:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  Suchen Sie den hadoopseitigen Konfigurationswert der in dieser Tabelle aufgelisteten Konfigurationsschlüssel. (Suchen Sie die Dateien auf dem Hadoop-Computer im Hadoop-Konfigurationsverzeichnis.)  
  
3.  Kopieren Sie die Konfigurationswerte in die Eigenschaft „Value“ in den entsprechenden Dateien auf dem SQL Server-Computer.  
  
    |**#**|**Konfigurationsdatei**|**Konfigurationsschlüssel**|**Aktion**|  
    |------------|----------------|---------------------|----------|   
    |1|core-site.xml|polybase.kerberos.kdchost|Geben Sie den KDC-Hostnamen an. Zum Beispiel: kerberos.ihr-bereich.de.|  
    |2|core-site.xml|polybase.kerberos.realm|Geben Sie den Kerberos-Bereich an. Zum Beispiel: IHR-BEREICH.DE|  
    |3|core-site.xml|hadoop.security.authentication|Suchen Sie die hadoopseitige Konfiguration, und kopieren Sie diese auf den SQL Server-Computer. Beispiel: KERBEROS<br></br>**Sicherheitshinweis:** KERBEROS muss in Großbuchstaben geschrieben werden. Bei Kleinschreibung ist die Funktionalität nicht gewährleistet.|   
    |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Suchen Sie die hadoopseitige Konfiguration, und kopieren Sie diese auf den SQL Server-Computer. Beispiel: hdfs/_HOST@YOUR-REALM.COM|  
    |5|mapred-site.xml|mapreduce.jobhistory.principal|Suchen Sie die hadoopseitige Konfiguration, und kopieren Sie diese auf den SQL Server-Computer. Beispiel: mapred/_HOST@YOUR-REALM.COM|  
    |6|mapred-site.xml|mapreduce.jobhistory.address|Suchen Sie die hadoopseitige Konfiguration, und kopieren Sie diese auf den SQL Server-Computer. Zum Beispiel: 10.193.26.174:10020|  
    |7|yarn-site.xml yarn.|yarn.resourcemanager.principal|Suchen Sie die hadoopseitige Konfiguration, und kopieren Sie diese auf den SQL Server-Computer. Beispiel: yarn/_HOST@YOUR-REALM.COM|  
  
4.  Erstellen Sie ein datenbankweites Anmeldeinformationsobjekt, um die Authentifizierungsinformationen für jeden Hadoop-Benutzer anzugeben. Weitere Informationen finden Sie unter [PolyBase T-SQL-Objekte](../../relational-databases/polybase/polybase-t-sql-objects.md).  
  
## <a name="next-steps"></a>Nächste Schritte  
 [PolyBase T-SQL-Objekte](../../relational-databases/polybase/polybase-t-sql-objects.md)  
  
 [Erste Schritte mit PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Konfiguration der PolyBase-Netzwerkkonnektivität &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)   
 [PolyBase-Leitfaden](../../relational-databases/polybase/polybase-guide.md)  
  
  
