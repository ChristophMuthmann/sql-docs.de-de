---
title: PolyBase-Erweiterungsgruppen | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 05/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PolyBase
- PolyBase, scale-out groups
- scale-out PolyBase
ms.assetid: c7810135-4d63-4161-93ab-0e75e9d10ab5
caps.latest.revision: 20
author: barbkess
ms.author: barbkess
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d297ff12aedfdbdf4e5e50c6656c3d208ecb260d
ms.lasthandoff: 04/11/2017

---
# <a name="polybase-scale-out-groups"></a>PolyBase-Erweiterungsgruppen
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Eine eigenständige SQL Server-Instanz mit PolyBase kann bei der Verarbeitung von sehr großen Datasets in Hadoop oder Azure Blob Storage zu einem Leistungsengpass werden. Die PolyBase-Gruppenfunktion ermöglicht Ihnen die Erstellung eines Clusters aus SQL Server-Instanzen, um große Datasets in einer Skalierungsart zu verarbeiten, die zu besseren Abfrageleistungen führt. Diese Datasets stammen aus externen Datenquellen, wie beispielsweise Hadoop oder Azure Blob Storage.  
  
 Siehe [Get started with PolyBase](../../relational-databases/polybase/get-started-with-polybase.md) (Erste Schritte mit PolyBase) und [PolyBase Guide](../../relational-databases/polybase/polybase-guide.md)(PolyBase-Handbuch).  
  
 ![PolyBase-Erweiterungsgruppen](../../relational-databases/polybase/media/polybase-scale-out-groups.png "PolyBase-Erweiterungsgruppen")  
  
## <a name="overview"></a>Übersicht  
  
### <a name="head-node"></a>Hauptknoten  
 Der Hauptknoten enthält die SQL Server-Instanz, an die die PolyBase-Abfragen geschickt werden. Jede PolyBase-Gruppe kann nur einen Hauptknoten haben. Ein Hauptknoten ist eine logische Gruppe aus SQL-Datenbankmodul, PolyBase-Modul und PolyBase-Datenverschiebungsdienst auf der SQL Server-Instanz.  
  
### <a name="compute-node"></a>Computeknoten  
 Ein Computeknoten enthält die SQL Server-Instanz, die bei der Verarbeitung von Hochskalierungsabfragen für externe Daten hilft. Ein Computeknoten ist eine logische Gruppe aus SQL Server und dem PolyBase-Datenverschiebungsdienst auf der SQL Server-Instanz. Eine PolyBase-Gruppe kann mehrere Computeknoten umfassen.  
  
### <a name="distributed-query-processing"></a>Verarbeiten verteilter Abfragen  
 PolyBase-Abfragen werden an den SQL Server auf dem Hauptknoten gesendet. Der Teil der Abfrage, der sich auf externe Tabellen bezieht, wird an das PolyBase-Modul übergeben.  
  
 Das PolyBase-Modul ist die zentrale Komponente von PolyBase-Abfragen. Es analysiert die Abfrage an externen Daten, erstellt den Abfrageplan und gibt die Arbeit für die Ausführung an den Datenverschiebungsdienst auf den Computeknoten weiter. Nach Abschluss der Arbeit erhält es die Ergebnisse von den Computeknoten und übergibt sie an SQL Server für die Verarbeitung und die Rückgabe an den Client.  
  
 Der PolyBase-Datenverschiebungsdienst erhält Anweisungen vom PolyBase-Modul und überträgt die Daten zwischen HDFS und SQL Server sowie zwischen SQL Server-Instanzen auf den Haupt- und Serverknoten.  
  
### <a name="editions-availability"></a>Verfügbarkeit in den einzelnen Editionen  
 Nach dem Setup von SQL Server kann die Instanz entweder als Hauptknoten oder als Computeknoten festgelegt werden.  Die Wahl hängt davon ab, auf welcher Version von SQL Server PolyBase ausgeführt wird. In einer Installation der Enterprise-Version kann die Instanz entweder als Hauptknoten oder als Computeknoten festgelegt werden. Bei einer Standard Edition kann die Instanz nur als Computeknoten festgelegt werden.  
  
## <a name="to-configure-a-polybase-group"></a>So konfigurieren Sie eine PolyBase-Gruppe  
  
### <a name="prerequisites"></a>Erforderliche Komponenten  
  
-   N Computer in der gleichen Domäne  
  
-   Ein Domänenbenutzerkonto zum Ausführen von PolyBase-Diensten  
  
### <a name="steps"></a>Schritte  
  
1.  Installieren Sie SQL Server mit PolyBase auf N Computern.  
  
2.  Wählen Sie eine SQL Server-Instanz als Hauptknoten aus. Ein Hauptknoten kann nur auf einer Instanz festgelegt werden, die SQL Server Enterprise ausführt.  
  
3.  Fügen Sie mithilfe von [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md) die verbleibenden SQL Server-Instanzen als Serverknoten hinzu.  
  
4.  Überwachen Sie Knoten in der Gruppe mit [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).  
  
5.  Optional. Entfernen Sie einen Serverknoten mit [sp_polybase_leave_group &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md).  
  
## <a name="example-walk-through"></a>Exemplarische Vorgehensweise  
 Hier erfahren Sie, wie Sie eine PolyBase-Gruppe mit den folgenden Informationen einrichten:  
  
1.  Zwei Computer in der Domäne *PQTH4A* Die Namen der Computer sind:  
  
    -   PQTH4A-CMP01  
  
    -   PQTH4A-CMP02  
  
2.  Domänenkonto: *PQTH4A\PolybaseUser*  
  
#### <a name="step-1-install-sql-server-with-polybase-on-all-machines"></a>Schritt 1: Installieren von SQL Server mit PolyBase auf allen Computern  
  
1.  Führen Sie „setup.exe“ aus.  
  
2.  Wählen Sie auf der Seite für die Funktionsauswahl **PolyBase Query Service for External Data**(PolyBase-Abfragedienst für externe Daten) aus.  
  
3.  Verwenden Sie das **Domänenkonto** PQTH4A\PolybaseUser für SQL Server PolyBase-Modul und SQL Server PolyBase-Datenverschiebungsdienst auf der Konfigurationsseite des Servers.  
  
4.  Wählen Sie auf der PolyBase-Konfigurationsseite die Option **Use the SQL Server instance as part of a PolyBase scale-out group**(SQL Server-Instanz als Teil einer PolyBase-Erweiterungsgruppe verwenden). Dies öffnet die Firewall, um eingehende Verbindungen an die PolyBase-Dienste zuzulassen.  
  
5.  Nachdem das Setup abgeschlossen ist, führen Sie **services.msc**aus. Überprüfen Sie, ob SQL Server, das PolyBase-Modul und der PolyBase-Datenverschiebungsdienst ausgeführt werden.  
  
     ![PolyBase-Dienste](../../relational-databases/polybase/media/polybase-services.png "PolyBase services")  
  
#### <a name="step-2-select-one-sql-server-as-head-node"></a>Schritt 2: Wählen eines SQL Servers als Hauptknoten  
  
-   Nachdem das Setup abgeschlossen ist, können beide Computer als PolyBase-Gruppenhauptknoten fungieren. In diesem Beispiel wählen wir MSSQLSERVER auf PQTH4A-CMP01 als den Hauptknoten.  
  
#### <a name="step-3-add-other-sql-server-instances-as-compute-nodes"></a>Schritt 3: Hinzufügen von anderen SQL Server-Instanzen als Computeknoten  
  
1.  Stellen Sie die Verbindung mit SQL Server auf PQTH4A-CMP02 her.  
  
2.  Führen Sie die gespeicherte Prozedur [sp_polybase_leave_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)aus.  
  
    ```  
    -- Enter head node details:   
    -- head node machine name, head node dms control channel port, head node sql server name  
    EXEC sp_polybase_join_group 'PQTH4A-CMP01', 16450, 'MSSQLSERVER';  
  
    ```  
  
3.  Führen Sie „services.msc“ auf den Computeknoten (PQTH4A CMP02) aus.  
  
4.  Fahren Sie das PolyBase-Modul herunter, und starten Sie den PolyBase-Datenverschiebedienst neu.  
  
#### <a name="optional-remove-a-compute-node"></a>Optional: Entfernen eines Computeknotens  
  
1.  Stellen Sie eine Verbindung mit dem Computeknoten SQL Server (PQTH4A-CMP02) her.  
  
2.  Führen Sie die gespeicherte Prozedur „sp_polybase_leave_group“ aus.  
  
    ```  
    EXEC sp_polybase_leave_group;  
    ```  
  
3.  Führen Sie „services.msc“ auf dem Computeknoten (PQTH4A CMP02) aus, der entfernt wird.  
  
4.  Starten Sie das PolyBase-Modul. Starten Sie den SQL Server PolyBase-Datenverschiebungsdienst neu.  
  
5.  Überprüfen Sie, ob der Knoten entfernt wurde, indem Sie die DMV „sys.dm_exec_compute_nodes“ auf PQTH4A CMP01 ausführen. Jetzt fungiert PQTH4A-CMP02 als eigenständiger Hauptknoten.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Informationen zur Problembehandlung finden Sie unter [PolyBase troubleshooting with dynamic management views](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80).  
  
## <a name="see-also"></a>Siehe auch  
 [Get started with PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [PolyBase Guide](../../relational-databases/polybase/polybase-guide.md)   
 [Konfiguration der PolyBase-Konnektivität &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)  
  
  

