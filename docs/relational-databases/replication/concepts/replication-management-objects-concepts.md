---
title: "Konzepte für Replikationsverwaltungsobjekte (RMO) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 11/08/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- replication [SQL Server], RMO
- programming interfaces [SQL Server replication]
- replication [SQL Server], how-to topics
- RMO [SQL Server]
- Replication Management Objects
- programming [SQL Server replication], RMO
ms.assetid: 37476d50-fb47-49e3-9504-3b163ac381d8
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a928aa42c4666bdfce9be3fcb2d35895444dd4b6
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="replication-management-objects-concepts"></a>Replication Management Objects Concepts
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Bei Replikationsverwaltungsobjekten (RMO) handelt es sich um eine verwaltete Codeassembly, die Replikationsfunktionen für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] kapselt. RMO wird durch den <xref:Microsoft.SqlServer.Replication>-Namespace implementiert.  
  
 In den folgenden Abschnitten wird beschrieben, wie Sie RMO für die programmgesteuerte Kontrolle von Replikationsaufgaben verwenden können:  
  
 [Verteilung konfigurieren](../../../relational-databases/replication/configure-distribution.md)  
 Die Themen in diesem Abschnitt veranschaulichen, wie RMO zum Konfigurieren von Veröffentlichung und Verteilung verwendet wird.  
  
 [Erstellen, Ändern und Löschen von Veröffentlichungen und Artikeln &#40;Replikation&#41;](../../../relational-databases/replication/publish/create-modify-and-delete-publications-and-articles-replication.md)  
 Die Themen in diesem Abschnitt demonstrieren, wie mit RMO Veröffentlichungen und Artikel erstellt, gelöscht und geändert werden.  
  
 [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md)  
 Die Themen in diesem Abschnitt beschreiben, wie mit RMO Abonnements erstellt, gelöscht und geändert werden.  
  
 [Sichern einer Replikationstopologie](../../../relational-databases/replication/security/secure-a-replication-topology.md)  
 Die Themen in diesem Abschnitt erläutern, wie mit RMO Sicherheitseinstellungen angezeigt und geändert werden.  
  
 [Synchronisieren von Abonnements &#40;Replikation&#41;](../../../relational-databases/replication/synchronize-subscriptions-replication.md)  
 Die Themen in diesem Abschnitt veranschaulichen, wie Abonnements synchronisiert werden.  
  
 [Überwachen der Replikation](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
 Die Themen in diesem Abschnitt beschreiben, wie eine Replikationstopologie programmgesteuert überwacht wird.  
  
## <a name="introduction-to-rmo-programming"></a>Einführung in die RMO-Programmierung  
 RMO wurde zum Programmieren aller Aspekte der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Replikation entwickelt. Der RMO-Namespace lautet <xref:Microsoft.SqlServer.Replication>. Er wird durch die Microsoft.SqlServer.Rmo.dll, eine [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework-Assembly, implementiert. Die Microsoft.SqlServer.Replication.dll-Assembly, die ebenfalls zum <xref:Microsoft.SqlServer.Replication>-Namespace gehört, implementiert eine verwaltete Codeschnittstelle zum Programmieren der verschiedenen Replikations-Agents (Momentaufnahme-Agent, Verteilungs-Agent und Merge-Agent). Der Zugriff auf die entsprechenden Klassen kann in RMO erfolgen, um Abonnements zu synchronisieren. Klassen im <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>-Namespace, die durch die Microsoft.SqlServer.Replication.BusinessLogicSupport.dll-Assembly implementiert werden, dienen zum Erstellen benutzerdefinierter Geschäftslogik für die Mergereplikation. Diese Assembly ist von RMO unabhängig.  
  
## <a name="deploying-applications-based-on-rmo"></a>Bereitstellen von Anwendungen auf Grundlage von RMO  
 RMO hängt von den Replikationskomponenten und den Clientverbindungskomponenten ab, die in allen Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mit Ausnahme von SQL Server Compact enthalten sind. Zum Bereitstellen einer Anwendung auf Grundlage von RMO müssen Sie eine Version von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], die Replikationskomponenten und Clientverbindungskomponenten enthält, auf dem Computer installieren, auf dem die Anwendung ausgeführt wird.  
  
## <a name="getting-started-with-rmo"></a>Erste Schritte mit RMO  
 In diesem Abschnitt wird beschrieben, wie ein einfaches RMO-Projekt mit [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio gestartet wird.  
  
#### <a name="to-create-a-new-microsoft-visual-c-project"></a>So erstellen Sie ein neues Microsoft Visual C#-Projekt  
  
1.  Starten Sie Visual Studio.  
  
2.  Klicken Sie im Menü **Datei** auf **Neues Projekt**. Das Dialogfeld **Neues Projekt** wird angezeigt.  
  
3.  Wählen Sie im Dialogfeld **Projekttypen** den Typ **Visual C#-Projekte** aus. Wählen Sie im Bereich **Vorlagen** die Option **Windows-Anwendung** aus.  
  
4.  (Optional) Geben Sie im Feld **Name** einen Namen für die neue Anwendung ein.  
  
5.  Klicken Sie auf **OK**, um die Visual C# Windows-Vorlage zu laden.  
  
6.  Wählen Sie im Menü **Projekt** die Option **Verweis hinzufügen** aus. Das Dialogfeld **Verweis hinzufügen** wird angezeigt.  
  
7.  Wählen Sie die folgenden Assemblys aus der Liste auf der Registerkarte **.NET** aus, und klicken Sie anschließend auf **OK**.  
  
    -   Microsoft.SqlServer.Replication .NET Programming Interface  
  
    -   Microsoft.SqlServer.ConnectionInfo  
  
    -   Replication Agent Library  
  
    > [!NOTE]  
    >  Mit gedrückter STRG-Taste können Sie mehrere Dateien gleichzeitig auswählen.  
  
8.  (Optional) Wiederholen Sie Schritt 6. Klicken Sie auf die Registerkarte **Durchsuchen**, navigieren Sie zu [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]-COM, wählen Sie Microsoft.SqlServer.Replication.BusinessLogicSupport.dll aus, und klicken Sie anschließend auf **OK**.  
  
9. Klicken Sie im Menü **Ansicht** auf **Code**.  
  
10. Geben Sie im Code vor der Namespace-Anweisung die folgenden **using**-Anweisungen ein, um die Typen in den RMO-Namespaces zu qualifizieren:  
  
    ```  
    // These namespaces are required.  
    using Microsoft.SqlServer.Replication;  
    using Microsoft.SqlServer.Management.Common;  
    // This namespace is only used when creating custom business  
    // logic for merge replication.  
    using Microsoft.SqlServer.Replication.BusinessLogicSupport;   
    ```  
  
#### <a name="to-create-a-new-microsoft-visual-basic-net-project"></a>So erstellen Sie ein neues Microsoft Visual Basic .NET-Projekt  
  
1.  Starten Sie Visual Studio.  
  
2.  Wählen Sie im Menü **Datei** die Option **Neues Projekt** aus. Das Dialogfeld **Neues Projekt** wird angezeigt.  
  
3.  Wählen Sie im Projekttypenbereich **Visual Basic** aus. Wählen Sie im Vorlagenbereich die Option **Windows-Anwendung** aus.  
  
4.  (Optional) Geben Sie im Feld **Name** einen Namen für die neue Anwendung ein.  
  
5.  Klicken Sie auf **OK**, um die Visual Basic Windows-Vorlage zu laden.  
  
6.  Wählen Sie im Menü **Projekt** die Option **Verweis hinzufügen** aus. Das Dialogfeld **Verweis hinzufügen** wird angezeigt.  
  
7.  Wählen Sie die folgenden Assemblys aus der Liste auf der Registerkarte **.NET** aus, und klicken Sie anschließend auf **OK**.  
  
    -   Microsoft.SqlServer.Replication .NET Programming Interface  
  
    -   Microsoft.SqlServer.ConnectionInfo  
  
    -   Replication Agent Library  
  
    > [!NOTE]  
    >  Mit gedrückter STRG-Taste können Sie mehrere Dateien gleichzeitig auswählen.  
  
8.  (Optional) Wiederholen Sie Schritt 6. Klicken Sie auf die Registerkarte **Durchsuchen**, navigieren Sie zu [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]-COM, wählen Sie Microsoft.SqlServer.Replication.BusinessLogicSupport.dll aus, und klicken Sie anschließend auf **OK**.  
  
9. Klicken Sie im Menü **Ansicht** auf **Code**.  
  
10. Geben Sie im Code vor möglichen Deklarationen die folgenden **Imports**-Anweisungen ein, um die Typen im RMO-Namespace zu qualifizieren.  
  
    ```  
    ' These namespaces are required.  
    Imports Microsoft.SqlServer.Replication  
    Imports Microsoft.SqlServer.Management.Common  
    ' This namespace is only used when creating custom business  
    ' logic for merge replication.  
    Imports Microsoft.SqlServer.Replication.BusinessLogicSupport   
    ```  
  
## <a name="connecting-to-a-replication-server"></a>Verbinden mit einem Replikationsserver  
 Bei RMO-Programmierobjekten ist es erforderlich, dass eine Verbindung zu einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mithilfe einer Instanz der <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Klasse erfolgt. Diese Verbindung mit dem Server erfolgt unabhängig von einem RMO-Programmierobjekt. Sie wird anschließend entweder während der Erstellung der Instanz oder durch die Zuweisung zur `P:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContex`-Eigenschaft des Objekts an das RMO-Objekt übergeben. Dadurch können ein RMO-Programmierobjekt und die Instanzen des Verbindungsobjekts getrennt erstellt und verwaltet werden. Zudem kann ein einzelnes Verbindungsobjekt mit mehreren RMO-Programmierobjekten verwendet werden. Für Verbindungen mit einem Replikationsserver gelten die folgenden Regeln:  
  
-   Alle Eigenschaften für die Verbindung werden für ein angegebenes <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Objekt definiert.  
  
-   Eine Verbindung zu jeder Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] muss über ein eigenes <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Objekt verfügen.  
  
-   Das <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Objekt ist der `P:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext`-Eigenschaft des RMO-Programmierobjekts zugewiesen, das auf dem Server erstellt oder auf das über den Server zugegriffen wird.  
  
-   Mit der <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A>-Methode wird die Verbindung mit dem Server geöffnet. Diese Methode muss aufgerufen werden, bevor Methoden aufgerufen werden, die auf den Server zugreifen, oder bevor RMO-Programmierobjekte aufgerufen werden, die diese Verbindung verwenden.  
  
-   Da sowohl RMO- als auch [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Verwaltungsobjekte (SMO) die <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Klasse für Verbindungen zu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verwenden, können RMO- und SMO-Objekte die gleiche Verbindung verwenden. Weitere Informationen finden Sie unter [Hinzufügen von Funktionen zu einer Instanz von SQL Server](../../../relational-databases/server-management-objects-smo/create-program/connecting-to-an-instance-of-sql-server.md).  
  
-   Sämtliche Authentifizierungsinformationen, die zur Herstellung der Verbindung und zur erfolgreichen Anmeldung beim Server erforderlich sind, sind im <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Objekt angegeben.  
  
-   Die Windows-Authentifizierung ist als Standard vorgegeben. Um die Authentifizierung von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verwenden zu können, müssen <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.LoginSecure%2A> auf **FALSE** und <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Login%2A> sowie <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Password%2A> auf eine gültige Kombination aus Anmeldeinformationen und Kennwort für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gesetzt sein. Anmeldeinformationen müssen stets sicher aufbewahrt und behandelt werden. Nach Möglichkeit sollte die Eingabe zur Laufzeit erfolgen.  
  
-   Für Multithreadanwendungen sollte in jedem Thread ein separates <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Objekt verwendet werden.  
  
 Rufen Sie die <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A>-Methode für das <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Objekt auf, um aktive, von RMO-Objekten verwendete Serververbindungen zu schließen.  
  
## <a name="setting-rmo-properties"></a>Festlegen von RMO-Eigenschaften  
 Die Eigenschaften von RMO-Programmierobjekten stellen die Eigenschaften dieser Replikationsobjekte auf dem Server dar. Wenn Sie neue Replikationsobjekte auf dem Server erstellen, werden diese Objekte mithilfe von RMO-Eigenschaften definiert. Für vorhandene Objekte stellen die RMO-Eigenschaften die Eigenschaften des vorhandenen Objekts dar, die nur für nicht schreibgeschützte oder festlegbare Eigenschaften geändert werden können. Eigenschaften können für neue Objekte oder vorhandene Objekte festgelegt werden.  
  
### <a name="setting-properties-for-new-replication-objects"></a>Festlegen von Eigenschaften für neue Replikationsobjekte  
 Beim Erstellen eines neuen Replikationsobjekts auf dem Server müssen Sie alle erforderlichen Eigenschaften angeben, bevor die **Create**-Methode des Objekts aufgerufen wird. Weitere Informationen zum Festlegen von Eigenschaften für ein neues Replikationsobjekt finden Sie unter [Konfigurieren der Veröffentlichung und der Verteilung](../../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
### <a name="setting-properties-for-existing-replication-objects"></a>Festlegen von Eigenschaften für vorhandene Replikationsobjekte  
 Für auf dem Server vorhandene Replikationsobjekte unterstützt RMO abhängig vom Objekt die Fähigkeit, einige oder alle Eigenschaften zu ändern. Nur nicht schreibgeschützte oder festlegbare Eigenschaften können geändert werden. Bevor Eigenschaften geändert werden können, muss entweder die **Load**-Methode oder die `M:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties`-Methode aufgerufen werden, um die aktuellen Eigenschaften vom Server abzurufen. Durch Aufrufen dieser Methoden wird angegeben, dass ein vorhandenes Objekt geändert wird.  
  
 Beim Ändern der Objekteigenschaften führt RMO standardmäßig einen Commit für diese Änderungen auf dem Server auf Grundlage des verwendeten Ausführungsmodus von <xref:Microsoft.SqlServer.Management.Common.ServerConnection> aus. Mit der `P:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject`-Methode können Sie überprüfen, ob ein Objekt auf dem Server vorhanden ist, bevor Sie versuchen, die entsprechenden Eigenschaften abzurufen oder zu ändern. Informationen zum Ändern der Eigenschaften eines Replikationsobjekts finden Sie unter [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
> [!NOTE]  
>  Wenn mehrere RMO-Clients oder mehrere Instanzen eines RMO-Programmierobjekts auf das gleiche Replikationsobjekt auf dem Server zugreifen, kann die **Refresh**-Methode des RMO-Objekts aufgerufen werden, um Eigenschaften basierend auf dem aktuellen Status des Objekts auf dem Server zu aktualisieren.  
  
### <a name="caching-property-changes"></a>Zwischenspeichern von Eigenschaftsänderungen  
 Wenn die <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes>-Eigenschaft auf <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes.CaptureSql> festgelegt ist, werden alle von RMO generierten [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Anweisungen erfasst, sodass sie manuell mit einer der Ausführungsmethoden in einem einzelnen Batch ausgeführt werden können. Mit RMO können Sie Eigenschaftsänderungen zwischenspeichern und mit der `M:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges`-Methode des Objekts einen Commit für alle Änderungen gleichzeitig in einem einzelnen Batch durchführen. Um Eigenschaftsänderungen zwischenzuspeichern, muss die `P:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges`-Eigenschaft des Objekts auf **TRUE** festgelegt werden. Beim Zwischenspeichern von Eigenschaftsänderungen in RMO wird der Zeitpunkt, wann Änderungen an den Server gesendet werden, nach wie vor vom <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Objekt gesteuert. Weitere Informationen zum Zwischenspeichern von Eigenschaftsänderungen eines Replikationsobjekts finden Sie unter [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
> [!IMPORTANT]  
>  Obwohl die <xref:Microsoft.SqlServer.Management.Common.ServerConnection>-Klasse das Deklarieren von expliziten Transaktionen beim Festlegen von Eigenschaften unterstützt, können diese Transaktionen interne Replikationstransaktionen beeinträchtigen und zu unerwarteten Ergebnissen führen und sollten daher nicht mit RMO verwendet werden.  

### <a name="enabling-tls-12-support-for-rmo-components"></a>Aktivieren von TLS 1.2-Unterstützung für RMO-Komponenten 
 Die TLS 1.2-Unterstützung für RMO-Komponenten unter Windows 2012 und niedriger lässt sich aktivieren, indem Sie das Update [KB 3140245](http://support.microsoft.com/help/3140245) installieren und die Registrierungsschlüssel wie in diesem Artikel erklärt erstellen. Unter Windows 2012 R2 und höher müssen nur die in diesem Artikel erwähnten Registrierungsschlüssel erstellt werden.
 
## <a name="example"></a>Beispiel  
 In diesem Beispiel wird das Zwischenspeichern der Eigenschaftsänderungen veranschaulicht. Änderungen an den Attributen einer Transaktionsveröffentlichung werden zwischengespeichert, bis sie explizit an den Server gesendet werden.  
  
 [!code-cs[HowTo#rmo_ChangeTranPub_cached](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changetranpub_cached)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Konzepte für die Replikationsprogrammierung](../../../relational-databases/replication/concepts/replication-programming-concepts.md)  
  
  
