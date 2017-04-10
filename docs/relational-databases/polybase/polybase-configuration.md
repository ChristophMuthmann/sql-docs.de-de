---
title: "PolyBase-Konfiguration | Microsoft Docs"
ms.custom: ""
ms.date: "11/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 80ff73c1-2861-438b-a13f-309155f3d6e1
caps.latest.revision: 17
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 12
---
# PolyBase-Konfiguration
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Verwenden Sie die folgenden Vorgehensweisen, um PolyBase zu konfigurieren.  
  
## <a name="external-data-source-configuration"></a>Konfigurieren der externen Datenquelle  
 Sie müssen die Verbindung von SQL Server zur externen Datenquelle sicherstellen. Der Verbindungstyp wirkt sich stark auf die erwartete Abfrageleistung aus. Beispielsweise führt eine 10 GBit-Ethernet-Verbindung zu einer schnelleren Abfrageantwortzeit für PolyBase-Abfragen als eine 1 GBit-Ethernet-Verbindung.  
  
 Sie müssen SQL Server mithilfe von **sp_configure** für die Verbindung mit Ihrer Hadoop-Version oder Azure-BLOB-Speicher konfigurieren. PolyBase unterstützt zwei Hadoop-Distributionen: Hortonworks Data Platform (HDP) und Cloudera Distributed Hadoop (CDH).  Eine vollständige Liste der unterstützten externen Datenquellen finden Sie unter [Konfiguration der PolyBase-Netzwerkkonnektivität &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
  
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
 Um die Abfrageleistung zu verbessern, aktivieren Sie die Pushdown-Berechnung für einen Hadoop-Cluster:  
  
1.  Suchen Sie die Datei **yarn-site.xml** im Installationspfad von SQL Server. In der Regel lautet der Pfad:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  Suchen Sie auf dem Hadoop-Computer die analoge Datei im Hadoop-Konfigurationsverzeichnis. Suchen Sie in der Datei den Wert des Konfigurationsschlüssels „yarn.application.classpath.“, und kopieren Sie diesen.  
  
3.  Suchen Sie auf dem SQL Server-Computer in der Datei **yarn.site.xml** die Eigenschaft **yarn.application.classpath**. Fügen Sie den Wert vom Hadoop-Computer in das Element „Value“ ein.  
  
## <a name="kerberos-configuration"></a>Kerberos-Konfiguration  
 So stellen Sie eine Verbindung mit einem mit Kerberos geschützten Hadoop-Cluster [mithilfe von MIT KDC] her:  
  
1.  Suchen Sie das Hadoop-Konfigurationsverzeichnis im Installationspfad von SQL Server. In der Regel lautet der Pfad:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  Suchen Sie den hadoopseitigen Konfigurationswert der in dieser Tabelle aufgelisteten Konfigurationsschlüssel. (Suchen Sie die Dateien auf dem Hadoop-Computer im Hadoop-Konfigurationsverzeichnis.)  
  
3.  Kopieren Sie die Konfigurationswerte in die Eigenschaft „Value“ in den entsprechenden Dateien auf dem SQL Server-Computer.  
  
    |**#**|**Konfigurationsdatei**|**Konfigurationsschlüssel**|**Aktion**|  
    |------------|----------------|---------------------|----------|   
    |1|core-site.xml|polybase.kerberos.kdchost|Geben Sie den Kerberos-Bereich an. Zum Beispiel: IHR-BEREICH.DE|  
    |2|core-site.xml|polybase.kerberos.realm|Geben Sie den KDC-Hostnamen an. Zum Beispiel: kerberos.ihr-bereich.de.|  
    |3|core-site.xml|hadoop.security.authentication|Suchen Sie die hadoopseitige Konfiguration, und kopieren Sie diese auf den SQL Server-Computer. Beispiel: KERBEROS<br></br>**Sicherheitshinweis:** KERBEROS muss in Großbuchstaben geschrieben werden. Bei Kleinschreibung ist die Funktionalität nicht gewährleistet.|   
    |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Suchen Sie die hadoopseitige Konfiguration, und kopieren Sie diese auf den SQL Server-Computer. Beispiel: hdfs/_HOST@YOUR-REALM.COM|  
    |5|mapred-site.xml|mapreduce.jobhistory.address|Suchen Sie die hadoopseitige Konfiguration, und kopieren Sie diese auf den SQL Server-Computer. Beispiel: mapred/_HOST@YOUR-REALM.COM|  
    |6|mapred-site.xml|mapreduce.jobhistory.principal|Suchen Sie die hadoopseitige Konfiguration, und kopieren Sie diese auf den SQL Server-Computer. Zum Beispiel: 10.193.26.174:10020|  
    |7|yarn-site.xml yarn.|yarn.resourcemanager.principal|Suchen Sie die hadoopseitige Konfiguration, und kopieren Sie diese auf den SQL Server-Computer. Beispiel: yarn/_HOST@YOUR-REALM.COM|  
  
4.  Erstellen Sie ein datenbankweites Anmeldeinformationsobjekt, um die Authentifizierungsinformationen für jeden Hadoop-Benutzer anzugeben. Weitere Informationen finden Sie unter [PolyBase T-SQL-Objekte](../../relational-databases/polybase/polybase-t-sql-objects.md).  
  
## <a name="next-steps"></a>Nächste Schritte  
 [PolyBase T-SQL-Objekte](../../relational-databases/polybase/polybase-t-sql-objects.md)  
  
 [Erste Schritte mit PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Konfiguration der PolyBase-Netzwerkkonnektivität &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)   
 [PolyBase-Leitfaden](../../relational-databases/polybase/polybase-guide.md)  
  
  