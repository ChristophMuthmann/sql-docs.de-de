---
title: "Unterstützung für Scale Out mit SQL Server Integration Services (SSIS) für Hochverfügbarkeit | Microsoft-Dokumentation"
ms.description: This article describes how to configure SSIS Scale Out for high availability
ms.custom: 
ms.date: 12/19/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 
author: haoqian
ms.author: haoqian
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 906edbe80e7c762cdd9a271218d790edc9da8f5b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="scale-out-support-for-high-availability"></a>Scale Out-Unterstützung für Hochverfügbarkeit

In SSIS Scale Out wird die Hochverfügbarkeit auf Workerseite über ausführende Pakete mit mehreren Scale Out-Workern bereitgestellt.

Sie erreichen Hochverfügbarkeit auf Masterseite mithilfe von [Always On für den SSIS-Katalog](../catalog/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) und Windows-Failoverclustering. In diesem Beispiel werden mehrere Instanzen des Scale Out-Masters in einem Windows-Failovercluster gehostet. Wenn der Scale Out-Masterdienst oder die SSISDB auf dem Primärknoten ausfallen, akzeptieren der Dienst oder die SSISDB auf dem Sekundärknoten weiterhin Benutzeranforderungen, und beide kommunizieren mit den Scale Out-Workern. 

Führen Sie die folgenden Schritte aus, um die Hochverfügbarkeit auf Masterseite einzurichten:

## <a name="1-prerequisites"></a>1. Voraussetzungen
Erstellen Sie einen Windows-Failovercluster. Weitere Anweisungen finden Sie im Blogbeitrag [Installing the Failover Cluster Feature and Tools for Windows Server 2012 (Installation des Failoverclusterfeatures und des Tools für Windows Server 2012)](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx). Installieren Sie die Funktion und die Tools auf allen Clusterknoten.

## <a name="2-install-scale-out-master-on-the-primary-node"></a>2. Installieren des Scale Out-Masters auf dem Primärknoten
Installieren Sie SQL Server Database Engine Services, Integration Services und den Scale Out-Master auf dem Primärknoten für den Scale Out-Master. 

Führen Sie bei der Installation die folgenden Schritte aus:

### <a name="21-set-the-account-running-scale-out-master-service-to-a-domain-account"></a>2.1 Legen Sie das Konto, das den Scale Out-Masterdienst ausführt, auf ein Domänenkonto fest
Dieses Konto sollte zukünftig Zugriff auf die SSISDB auf dem Sekundärknoten im Windows-Failovercluster haben. Da für den Scale Out-Masterdienst und die SSISDB unabhängig voneinander Failover ausgeführt werden können, befinden sie sich nach der Failoverausführung möglicherweise nicht auf demselben Knoten.

![Serverkonfiguration für Hochverfügbarkeit](media/ha-server-config.PNG)

### <a name="22-include-the-dns-host-name-for-the-scale-out-master-service-in-the-cns-of-the-scale-out-master-certificate"></a>2.2 Nehmen Sie den DNS-Hostnamen des Scale Out-Masterdiensts in den allgemeinen Namen des Scale Out-Masterzertifikats auf

Dieser Hostname wird im Scale Out-Masterendpunkt verwendet. 

![Masterkonfiguration für Hochverfügbarkeit](media/ha-master-config.PNG)

## <a name="3-install-scale-out-master-on-the-secondary-node"></a>3. Installieren des Scale Out-Masters auf dem Sekundärknoten
Installieren Sie SQL Server Database Engine Services, Integration Services und den Scale Out-Master auf dem Sekundärknoten für den Scale Out-Master. 

Verwenden Sie dasselbe Scale Out-Masterzertifikat wie für den Primärknoten. Exportieren Sie das SSL-Zertifikat für den Scale Out-Master mit dem privaten Schlüssel auf dem Primärknoten, und installieren Sie es im Stammzertifikatspeicher auf dem Sekundärknoten auf dem lokalen Computer. Wählen Sie dieses Zertifikat bei der Installation des Scale Out-Masters auf dem Sekundärknoten aus.

![Masterkonfiguration für Hochverfügbarkeit 2](media/ha-master-config2.PNG)

> [!NOTE]
> Sie können mehrere Sicherungskopien des Scale Out-Masters einrichten, indem Sie diese Vorgänge für die Scale Out-Master auf weiteren Sekundärknoten wiederholen.

## <a name="4-set-up-ssisdb-always-on"></a>4. Einrichten von Always On für SSISDB

Führen Sie die Anweisungen zur Einrichtung von Always On für SSISDB aus, die unter [Always On für den SSIS-Katalog](../catalog/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) beschrieben werden.

Außerdem müssen Sie einen Verfügbarkeitsgruppenlistener für die Verfügbarkeitsgruppe erstellen, zu der Sie SSISDB hinzufügen. Vgl. [Create or Configure an Availability Group Listener (Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners)](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).

## <a name="5-update-the-scale-out-master-service-configuration-file"></a>5. Aktualisieren Sie die Konfigurationsdatei des Scale Out-Masterdiensts
Aktualisieren Sie die Konfigurationsdatei des Scale Out Masterdiensts (`\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config`) auf dem Primär- und dem Sekundärknoten. Aktualisieren Sie **SqlServerName** auf *[DNS des Verfügbarkeitsgruppenlisteners],[Port]*.

## <a name="6-enable-package-execution-logging"></a>6. Aktualisieren Sie die Ausführungsprotokollierung.

Sie können sich bei SSISDB mit der Anmelde-ID **##MS_SSISLogDBWorkerAgentLogin##** anmelden, für die ein automatisches Kennwort generiert wurde. Führen Sie die folgenden Schritte aus, damit die Protokollierung für alle SSISDB-Replikate funktioniert.

### <a name="61-change-the-password-of-msssislogdbworkeragentlogin-on-the-primary-sql-server"></a>6.1 Ändern Sie das Kennwort von **##MS_SSISLogDBWorkerAgentLogin##** auf dem primären SQL Server

### <a name="62-add-the-login-to-the-secondary-sql-server"></a>6.2. Fügen Sie dem sekundären SQL Server die Anmelde-ID hinzu

### <a name="63-update-the-connection-string-used-for-logging"></a>6.3 Aktualisieren Sie die Verbindungszeichenfolge, die für die Protokollierung verwendet wird
Rufen Sie die gespeicherte Prozedur `[catalog].[update_logdb_info]` mithilfe der folgenden Parameterwerte auf:

-   `@server_name = '[Availability Group Listener DNS name],[Port]' `

-   `@connection_string = 'Data Source=[Availability Group Listener DNS name],[Port];Initial Catalog=SSISDB;User Id=##MS_SSISLogDBWorkerAgentLogin##;Password=[Password]];'`

## <a name="7-configure-the-scale-out-master-service-role-of-the-windows-failover-cluster"></a>7. Konfigurieren der Rolle des Scale Out-Masterdiensts des Windows-Failoverclusters

1.  Stellen Sie im Failovercluster-Manager eine Verbindung mit dem Cluster für Scale Out her. Wählen Sie den Cluster aus. Wählen Sie im Menü zunächst **Aktion** und dann **Rolle konfigurieren** aus.

2.  Wählen Sie im Dialogfeld **Assistent für Hochverfügbarkeit** auf der Seite **Rolle auswählen** **allgemeiner Dienst** aus. Wählen Sie den SQL Server Integration Services Scale Out-Master 14.0 auf der Seite **Dienst auswählen** aus.

3.  Geben Sie auf der Seite **Clientzugriffspunkt** den DNS-Hostnamen des Scale Out-Masterdiensts ein.

    ![Hochverfügbarkeitsassistent 1](media/ha-wizard1.PNG)

4.  Beenden Sie den Assistenten.

## <a name="8-update-the-scale-out-master-address-in-ssisdb"></a>8. Aktualisieren der Scale Out-Masteradresse in SSISDB

Führen Sie auf dem primären SQL Server die gespeicherte Prozedur `[catalog].[update_master_address]` mithilfe des Parameterwerts `@MasterAddress = N'https://[Scale Out Master service DNS host name]:[Master Port]'` aus. 

## <a name="9-add-the-scale-out-workers"></a>9. Hinzufügen des Scale Out-Workers

Jetzt können Sie Scale Out-Workers mithilfe des [Integration Services Scale Out-Managers](integration-services-ssis-scale-out-manager.md) hinzufügen. Geben Sie auf der Verbindungsseite `[SQL Server Availability Group Listener DNS name],[Port]` ein.

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen finden Sie in den folgenden Artikeln:
-   [Scale Out-Master von Integration Services (SSIS)](integration-services-ssis-scale-out-master.md)
-   [Scale Out-Worker von Integration Services (SSIS)](integration-services-ssis-scale-out-worker.md)