---
title: "SQL Serverintegration Services (SSIS) Dezentrales Skalieren Unterstützung für hohe Verfügbarkeit | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2405235bcfa09d2cc49e007f4eae6975d9ebf7a5
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="scale-out-support-for-high-availability"></a>Horizontales Skalieren-Unterstützung für hohe Verfügbarkeit

Im SSIS-horizontal skalieren wird die hoher Verfügbarkeit für Worker-Seite durch Ausführen von Paketen mit mehreren Scale Out Worker bereitgestellt.
Hoher Verfügbarkeit der Master-Seite erfolgt mit [AlwaysOn für SSIS-Katalog](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) und Windows-Failovercluster. In einem Windows-Failovercluster werden mehrere Instanzen von Scale-Out-Master gehostet. Wenn Scale-Out-Master-Dienstes oder SSISDB auf primären Knoten ausgefallen ist, wird den Dienst oder die SSISDB sekundären Knoten weiterhin benutzeranforderungen akzeptieren und kommunizieren mit Scale-Out-Worker. 

Um die hohe Verfügbarkeit der Master-Seite einzurichten, führen Sie die folgenden Schritte aus.

## <a name="1-prerequisites"></a>1. Erforderliche Komponenten
Erstellen Sie einen Windows-Failovercluster. Weitere Anweisungen finden Sie im Blogbeitrag [Installing the Failover Cluster Feature and Tools for Windows Server 2012](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) (Failoverclusterfunktion und Tools für Windows Server 2012 installieren). Sie sollten die Funktion und die Tools auf allen Clusterknoten installieren.

## <a name="2-install-scale-out-master-on-primary-node"></a>2. Installieren Sie Scale-Out-Master auf primären Knoten
Installieren Sie Database Engine Services, Integration Services und Scale-Out-Master auf dem primären Knoten für den Scale-Out-Master. 

Während der Installation sollten Sie 
### <a name="21-set-the-account-running-scale-out-master-service-to-a-domain-account"></a>2.1 festgelegt, das Konto, Scale-Out-Master-Dienst zu einem Domänenkonto ausgeführt wird.
Dieses Konto sollte auf SSISDB in der Zukunft auf dem sekundären Knoten in der Windows-Failovercluster zugreifen können. Wie Scale-Out-Master-Dienst und SSISDB Failover separat können, können sie nicht auf demselben Knoten werden.

![HA-Serverkonfiguration](media/ha-server-config.PNG)

### <a name="22-include-scale-out-master-service-dns-host-name-in-the-cns-of-scale-out-master-certificate"></a>2.2 Scale Out Master enthalten Dienst DNS-Hostnamen im Zertifikat CNs Scale Out Master.

Dieser Hostname wird in Scale-Out-Master-Endpunkt verwendet werden. 

![Master HA-Konfiguration](media/ha-master-config.PNG)

## <a name="3-install-scale-out-master-on-secondary-node"></a>3. Installieren Sie Scale-Out-Master auf sekundären Knoten
Installieren Sie Database Engine Services, Integration Services und Scale-Out-Master auf dem sekundären Knoten für den Scale-Out-Master. 

Sie sollten das gleiche Zertifikat für den Scale-Out-Master mit primären Knoten verwenden. Exportieren Sie die Skalierung Out Master SSL-Zertifikat auf primären Knoten mit privaten Schlüssel und installieren sie den Stammzertifikatspeicher des Loacl Computers am sekundären Knoten. Wählen Sie dieses Zertifikat bei der Installation Scale-Out-Master.

![Master HA-Konfiguration 2](media/ha-master-config2.PNG)

> [!Note]
> Sie können mehrere Sicherung Scale-Out-Master festlegen, durch die Vorgänge für sekundäre Scale Out Master wiederholen.

## <a name="4-set-up-ssisdb-always-on"></a>4. SSISDB immer auf einrichten

Die Anweisungen immer auf Einrichten für SSISDB kann, zur angezeigt werden [AlwaysOn für SSIS-Katalog (SSISDB)](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb).

Darüber hinaus müssen Sie einen Verfügbarkeit Gourp Listener für die verfügbarkeitsgruppe erstellen, die SSISDB hinzugefügt. Finden Sie unter [erstellen oder konfigurieren ein Verfügbarkeitsgruppenlisteners](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).

## <a name="5-update-scale-out-master-service-configuration-file"></a>5. Aktualisieren der Dienstkonfigurationsdatei Scale-Out-Master
Update Scale-Out-Master Dienstkonfigurationsdatei \<Treiber\>: \Programme\Microsoft SQL-Server\140\DTS\Binn\MasterSettings.config auf primären und sekundären Knoten. Update **SqlServerName** auf *[Availability Group Listener DNS-Name], [Port]*.

## <a name="6-enable-package-execution-logging"></a>6. Aktivieren der paketprotokollierung-Ausführung

In der SSISDB Protokollierung erfolgt durch die Anmeldung **"# MS_SSISLogDBWorkerAgentLogin"**, dessen Kennwort wird automatisch generiert. Um die Protokollierung funktioniert für alle Replikate von SSISDB zu machen, Verfahren Sie wie folgt.

### <a name="61-change-the-password-of-msssislogdbworkeragentlogin-on-primary-sql-server"></a>6.1 Ändern des Kennworts der **"# MS_SSISLogDBWorkerAgentLogin"** auf primären Sql-Server.
### <a name="62-add-the-login-to-secondary-sql-server"></a>6.2 Hinzufügen der sekundären Sql-Server.
### <a name="63-update-connection-string-of-logging"></a>6.3 aktualisieren Sie 6.3 die Verbindungszeichenfolge der Protokollierung.
Rufen Sie die gespeicherte Prozedur [Catalog]. [Update_logdb_info] mit 

@server_name= "*[Availability Group Listener DNS-Name], [Port]*" 

und @connection_string = "Data Source =*[Availability Group Listener DNS-Name]*,*[Port]*; Initial Catalog = SSISDB; Benutzer-Id = "# MS_SSISLogDBWorkerAgentLogin"; Kennwort =*[Kennwort]*]; ".

## <a name="7-congifure-scale-out-master-service-role-of-windows-failover-cluster"></a>7. Congifure Scale Out Master Dienstrolle des Windows-Failoverclusters

Failover-cluster-Manager, die für horizontales Skalieren eine Verbindung mit Cluster herstellen. Wählen Sie den Cluster, und klicken Sie auf **Aktion** im Menü und dann **Rolle konfigurieren...** .

In der ausgelesene einrichten **Assistenten für hohe Verfügbarkeit**Option **allgemeiner Dienst** in **Rolle auswählen** Seite, und wählen Sie SQL Server Integration Services Scale Out Master 14.0 in **Dienst auswählen** Seite.

In der **Clientzugriffspunkt** geben die Scale-Out-Master-Dienst-DNS-Hostnamen ein.

![Virtuelle Maschinen mit hoher Assistent 1](media/ha-wizard1.PNG)

Beenden Sie den Assistenten.

## <a name="8-update-master-address-in-ssisdb"></a>8. Aktualisieren von Master Adresse in der SSISDB

Führen Sie auf dem primären SQL Server gespeicherte Prozedur [SSIS] ein. [Catalog]. [Update_master_address] mit Parameter @MasterAddress = N'https: / / [Authentication-Dienst skalieren, dem DNS-Hostname]: [Port Master] ". 

## <a name="9-add-scale-out-worker"></a>9. Dezentrales Skalieren Worker hinzufügen

Jetzt können Sie anhand des Scale-Out-Worker hinzufügen [Scale-Out-Manager](integration-services-ssis-scale-out-manager.md). Geben Sie *[SQL Server Availability Group Listener-DNS-Name]*,*[Port]* in die Seite "Verbindung".





