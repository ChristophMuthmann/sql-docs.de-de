---
title: "Unterstützung für Scale Out mit SQL Server Integration Services (SSIS) für Hochverfügbarkeit | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2202b61a9efce26edb0edcef53204351338ecee6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="scale-out-support-for-high-availability"></a>Scale Out-Unterstützung für Hochverfügbarkeit

In SSIS Scale Out wird die Hochverfügbarkeit auf Workerseite über ausführende Pakete mit mehreren Scale Out-Workers bereitgestellt.
Die Hochverfügbarkeit auf Masterseite erfolgt über [Always On for SSIS Catalog (Always On für SSIS-Katalog)](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) und Windows-Failovercluster. In einem Windows-Failovercluster werden mehrere Instanzen des Scale Out-Masters gehostet. Wenn der Scale Out-Masterdienst oder die SSISDB auf dem Primärknoten ausfallen, akzeptieren der Dienst oder die SSISDB auf dem Sekundärknoten weiterhin Benutzeranforderungen, und beide kommunizieren mit den Scale Out-Workers. 

Führen Sie die folgenden Schritte aus, um die Hochverfügbarkeit auf Masterseite einzurichten.

## <a name="1-prerequisites"></a>1. Erforderliche Komponenten
Erstellen Sie einen Windows-Failovercluster. Weitere Anweisungen finden Sie im Blogbeitrag [Installing the Failover Cluster Feature and Tools for Windows Server 2012](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) (Failoverclusterfunktion und Tools für Windows Server 2012 installieren). Sie sollten die Funktion und die Tools auf allen Clusterknoten installieren.

## <a name="2-install-scale-out-master-on-primary-node"></a>2. Installieren des Scale Out-Masters auf dem Primärknoten
Installieren Sie Database Engine Services, Integration Services und den Scale Out-Master auf dem Primärknoten für den Scale Out-Master. 

Bei der Installation sollten Sie Folgendes beachten: 
### <a name="21-set-the-account-running-scale-out-master-service-to-a-domain-account"></a>2.1 Legen Sie das Konto, das den Scale Out-Masterdienst ausführt, auf ein Domänenkonto fest.
Dieses Konto sollte zukünftig Zugriff auf die SSISDB auf dem sekundären Knoten im Windows-Failovercluster haben. Da für den Scale Out-Masterdienst und die SSISDB unabhängig voneinander Failover ausgeführt werden können, befinden sie sich möglicherweise nicht auf demselben Knoten.

![Serverkonfiguration für Hochverfügbarkeit](media/ha-server-config.PNG)

### <a name="22-include-scale-out-master-service-dns-host-name-in-the-cns-of-scale-out-master-certificate"></a>2.2 Nehmen Sie den DNS-Hostnamen des Scale Out-Masterdiensts in den allgemeinen Namen (Common Name, CN) des Scale Out-Masterzertifikats auf.

Dieser Hostname wird im Scale Out-Masterendpunkt verwendet. 

![Masterkonfiguration für Hochverfügbarkeit](media/ha-master-config.PNG)

## <a name="3-install-scale-out-master-on-secondary-node"></a>3. Installieren Sie den Scale Out-Master auf dem Sekundärknoten.
Installieren Sie Database Engine Services, Integration Services und den Scale Out-Master auf dem Sekundärknoten für den Scale Out-Master. 

Sie sollten dasselbe Scale Out-Masterzertifikat wie für den Primärknoten verwenden. Exportieren Sie das SSL-Zertifikat für den Scale Out-Master mit dem privaten Schlüssel auf dem Primärknoten, und installieren Sie es im Stammzertifikatspeicher auf dem Sekundärknoten auf dem lokalen Computer. Wählen Sie dieses Zertifikat bei der Installation des Scale Out-Masters aus.

![Masterkonfiguration für Hochverfügbarkeit 2](media/ha-master-config2.PNG)

> [!Note]
> Sie können mehrere Sicherungskopien des Scale Out-Masters einrichten, indem Sie den Vorgang für den sekundären Scale Out-Master wiederholen.

## <a name="4-set-up-ssisdb-always-on"></a>4. Richten Sie Always On für SSISDB ein.

Die Anweisungen zur Einrichtung von Always On für SSISDB finden Sie unter [Always On for SSIS Catalog (SSISDB) (Always On für den SSIS-Katalog (SSISDB))](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb).

Außerdem müssen Sie einen Verfügbarkeitsgruppenlistener für die Verfügbarkeitsgruppe erstellen, die SSISDB hinzugefügt wurde. Vgl. [Create or Configure an Availability Group Listener (Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners)](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).

## <a name="5-update-scale-out-master-service-configuration-file"></a>5. Aktualisieren Sie die Konfigurationsdatei des Scale Out-Masterdiensts.
Aktualisieren Sie die Konfigurationsdatei des Scale Out-Masterdiensts („\<Treiber\>:\Programme\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config“) auf dem Primär- und dem Sekundärknoten. Aktualisieren Sie **SqlServerName** auf *[DNS des Verfügbarkeitsgruppenlisteners],[Port]*.

## <a name="6-enable-package-execution-logging"></a>6. Aktualisieren Sie die Ausführungsprotokollierung.

Sie können sich bei SSISDB mit der Anmelde-ID **##MS_SSISLogDBWorkerAgentLogin##** anmelden, für die ein automatisches Kennwort generiert wurde. Führen Sie die folgenden Schritte aus, damit die Protokollierung für alle SSISDB-Replikate funktioniert.

### <a name="61-change-the-password-of-msssislogdbworkeragentlogin-on-primary-sql-server"></a>6.1 Ändern Sie das Kennwort auf dem primären SQL Server auf **##MS_SSISLogDBWorkerAgentLogin##**.
### <a name="62-add-the-login-to-secondary-sql-server"></a>6.2. Fügen Sie dem sekundären SQL Server die Anmelde-ID hinzu.
### <a name="63-update-connection-string-of-logging"></a>6.3 Aktualisieren Sie die Verbindungszeichenfolge für die Protokollierung.
Rufen Sie die gespeicherte Prozedur „[Katalog].[update_logdb_info]“ über 

@server_name = *[DNS des Verfügbarkeitsgruppenlisteners],[Port]* 

und @connection_string = 'Datenquelle=*[DNS des Verfügbarkeitsgruppenlisteners]*,*[Port]*;Initial Catalog=SSISDB;User Id=##MS_SSISLogDBWorkerAgentLogin##;Password=*[Kennwort]*];' auf.

## <a name="7-congifure-scale-out-master-service-role-of-windows-failover-cluster"></a>7. Konfigurieren Sie die Rolle des Scale Out-Masterdiensts des Windows-Failoverclusters.

Stellen Sie im Failovercluster-Manager eine Verbindung mit dem Cluster für Scale Out her. Wählen Sie den Cluster aus, und klicken Sie im Menü auf **Aktion** und dann auf **Rolle konfigurieren...**.

Wählen Sie in dem Popupfenster **Assistent für Hochverfügbarkeit** **Allgemeiner Dienst** auf der Seite **Rolle auswählen** aus, und klicken Sie auf der Seite **Dienst auswählen** auf den SQL Server Integration Services Scale Out-Master 14.0.

Geben Sie auf der Seite **Clientzugriffspunkt** den DNS-Hostnamen des Scale Out-Masters ein.

![Hochverfügbarkeitsassistent 1](media/ha-wizard1.PNG)

Beenden Sie den Assistenten.

## <a name="8-update-master-address-in-ssisdb"></a>8. Aktualisieren Sie die Masteradresse in SSISDB.

Führen Sie auf dem primären SQL Server die gespeicherte Prozedur [SSIS].[Katalog].[update_master_address] mit dem Parameter @MasterAddress = N'https://[DNS-Hostname des Scale Out-Masterdiensts]:[Masterport] ein. 

## <a name="9-add-scale-out-worker"></a>9. Hinzufügen des Scale Out-Workers

Jetzt können Sie Scale Out-Workers mithilfe des [Scale Out-Managers](integration-services-ssis-scale-out-manager.md) hinzufügen. Geben Sie auf der Seite „Verbindung“ *[DNS des SQL Server-Verfügbarkeitsgruppenlisteners]*,*[Port]* ein.




