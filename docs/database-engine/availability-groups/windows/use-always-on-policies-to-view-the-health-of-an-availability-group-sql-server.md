---
title: "Verwenden von AlwaysOn-Richtlinien zum Anzeigen des Zustands einer Verf&#252;gbarkeitsgruppe (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Verfügbarkeitsgruppen [SQL Server-HADR], Richtlinien"
ms.assetid: 6f1bcbc3-1220-4071-8e53-4b957f5d3089
caps.latest.revision: 17
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 16
---
# Verwenden von AlwaysOn-Richtlinien zum Anzeigen des Zustands einer Verf&#252;gbarkeitsgruppe (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie der Betriebsstatus einer AlwaysOn-Verfügbarkeitsgruppe in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] mithilfe einer AlwaysOn-Richtlinie in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] bzw. mit PowerShell geändert wird. Informationen zur Verwaltung auf Basis von AlwaysOn-Richtlinien finden Sie unter [AlwaysOn-Richtlinien für Betriebsprobleme mit AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always on policies for operational issues - always on availability.md).  
  
> [!IMPORTANT]  
>  Für AlwaysOn-Richtlinien werden die Kategorienamen als IDs verwendet. Durch die Änderung des Namens einer AlwaysOn-Kategorie wird deren Funktionalität zur Integritätsüberprüfung unterbrochen. Daher sollte der Name einer AlwaysOn-Kategorie nie geändert werden.  
  
-   **Vorbereitungen:** [Sicherheit](#Security)  
  
-   **Verwenden von AlwaysOn-Richtlinien zum Anzeigen des Zustands einer Verfügbarkeitsgruppe mit:**  
  
     [AlwaysOn-Dashboard](#SSMSProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert CONNECT-, VIEW SERVER STATE- und VIEW ANY DEFINITION-Berechtigungen.  
  
##  <a name="SSMSProcedure"></a> Verwenden des AlwaysOn-Dashboards  
 **So öffnen Sie das AlwaysOn-Dashboard**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit der Serverinstanz her, die eines der Verfügbarkeitsreplikate hostet. Verwenden Sie zum Anzeigen von Informationen zu allen Verfügbarkeitsreplikaten in einer Verfügbarkeitsgruppe die Serverinstanz, die das primäre Replikat hostet.  
  
2.  Klicken Sie auf den Servernamen, um die Serverstruktur zu erweitern.  
  
3.  Erweitern Sie den Knoten **Hohe Verfügbarkeit mit AlwaysOn**.  
  
     Klicken Sie entweder mit der rechten Maustaste auf den Knoten **Verfügbarkeitsgruppen**, oder erweitern Sie diesen Knoten, und klicken Sie mit der rechten Maustaste auf eine bestimmte Verfügbarkeitsgruppe.  
  
4.  Wählen Sie den Befehl **Dashboard anzeigen** aus.  
  
 Informationen zur Verwendung des AlwaysOnDashboards finden Sie unter [Verwenden des AlwaysOn-Dashboards &#40;SQL Server Management Studio&#41;](../Topic/Use%20the%20Always On%20Dashboard%20\(SQL%20Server%20Management%20Studio\).md).  
  
##  <a name="PowerShellProcedure"></a> PowerShell  
 **Verwenden von AlwaysOn-Richtlinien zum Anzeigen des Zustands einer Verfügbarkeitsgruppe**  
  
1.  Legen Sie mit **cd** eine Serverinstanz als Standard fest, auf der eines der Verfügbarkeitsreplikate gehostet wird. Verwenden Sie zum Anzeigen von Informationen zu allen Verfügbarkeitsreplikaten in einer Verfügbarkeitsgruppe die Serverinstanz, die das primäre Replikat hostet.  
  
2.  Verwenden Sie die folgenden Cmdlets:  
  
     **Test-SqlAvailabilityGroup**  
     Bewertet die Integrität einer Verfügbarkeitsgruppe durch die Auswertung der Richtlinien der richtlinienbasierten SQL Server-Verwaltung. Sie müssen über CONNECT-, VIEW SERVER STATE- und VIEW ANY DEFINITION-Berechtigungen verfügen, um dieses Cmdlet auszuführen.  
  
     Beispielsweise werden durch den folgenden Befehl alle Verfügbarkeitsgruppen im „Error“-Zustand auf der Serverinstanz angezeigt `Computer\Instance`.  
  
    ```  
    Get-ChildItem SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups `   
    | Test-SqlAvailabilityGroup | Where-Object { $_.HealthState -eq "Error" }  
    ```  
  
     **Test-SqlAvailabilityReplica**  
     Bewertet die Integrität von Verfügbarkeitsreplikaten durch die Auswertung der Richtlinien der richtlinienbasierten SQL Server-Verwaltung. Sie müssen über CONNECT-, VIEW SERVER STATE- und VIEW ANY DEFINITION-Berechtigungen verfügen, um dieses Cmdlet auszuführen.  
  
     Durch den folgenden Befehl werden beispielsweise die Integrität des Verfügbarkeitsreplikats `MyReplica` in der Verfügbarkeitsgruppe `MyAg` ausgewertet und eine kurze Zusammenfassung ausgegeben.  
  
    ```  
    Test-SqlAvailabilityReplica `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
     **Test-SqlDatabaseReplicaState**  
     Bewertet die Integrität einer Verfügbarkeitsdatenbank für alle hinzugefügten Verfügbarkeitsreplikate durch die Auswertung der Richtlinien der richtlinienbasierten SQL Server-Verwaltung.  
  
     Durch den folgenden Befehl werden beispielsweise die Integrität aller Verfügbarkeitsdatenbanken in der Verfügbarkeitsgruppe `MyAg` ausgewertet und eine kurze Zusammenfassung für jede Datenbank ausgegeben.  
  
    ```  
    Get-ChildItem SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\DatabaseReplicaStates `   
     | Test-SqlDatabaseReplicaState  
    ```  
  
     Diese Cmdlets akzeptieren die folgenden Optionen:  
  
    |Option|Beschreibung|  
    |------------|-----------------|  
    |**AllowUserPolicies **|Führt in den AlwaysOn-Richtlinienkategorien gefundene Benutzerrichtlinien aus.|  
    |**InputObject**|Eine Auflistung von Objekten, die abhängig vom verwendeten Cmdlet den Status von Verfügbarkeitsgruppen, Verfügbarkeitsreplikaten oder Verfügbarkeitsdatenbanken darstellen. Das Cmdlet berechnet die Integrität der angegebenen Objekte.|  
    |**NoRefresh**|Wenn dieser Parameter festgelegt wird, werden die vom **-Path**- oder **-InputObject**-Parameter angegebenen Objekte nicht manuell vom Cmdlet aktualisiert.|  
    |**Pfad**|Abhängig vom verwendeten Cmdlet der Pfad zur Verfügbarkeitsgruppe, zu den Verfügbarkeitsreplikaten oder zum Status des Datenbankreplikatclusters. Dies ist ein optionaler Parameter. Wird dieser Parameter nicht angegeben, wird der Wert standardmäßig auf den aktuellen Arbeitsstandort festgelegt.|  
    |**ShowPolicyDetails**|Zeigt das Ergebnis aller von diesem Cmdlet ausgeführten Richtlinienauswertungen an. Das Cmdlet gibt ein Objekt pro Richtlinienauswertung aus. Dieses Objekt verfügt über Felder, in denen die Ergebnisse der Auswertung beschrieben werden, z. B. ob die Richtlinie eingehalten wurde sowie den Richtliniennamen und die Kategorie.|  
  
     Beispielsweise gibt der folgende **Test-SqlAvailabilityGroup**-Befehl den **-ShowPolicyDetails**-Parameter an, um das Ergebnis aller von diesem Cmdlet ausgeführten Richtlinienauswertungen anzuzeigen, und zwar für jede einzelne Richtlinie der richtlinienbasierten Verwaltung (policy-based management (PBM)) die auf einer Verfügbarkeitsgruppe namens `MyAg` ausgeführt wurde.  
  
    ```  
    Test-SqlAvailabilityGroup `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\AgName `  
    -ShowPolicyDetails  
  
    ```  
  
    > [!NOTE]  
    >  Um die Syntax eines Cmdlets anzuzeigen, verwenden Sie das **Get-Help**-Cmdlet in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell-Umgebung. Weitere Informationen finden Sie unter [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Einrichten und Verwenden des SQL Server PowerShell-Anbieters**  
  
-   [SQL Server PowerShell-Anbieter](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
-   [Aufrufen der SQL Server PowerShell-Hilfe](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
 **SQL Server AlwaysOn-Teamblogs – Überwachen des AlwaysOn-Zustands mit PowerShell:**  
  
-   [Teil 1: Übersicht über grundlegende Cmdlets](http://blogs.msdn.com/b/sqlAlways%20On/archive/2012/02/13/monitoring-Always%20On-health-with-powershell-part-1.aspx)  
  
-   [Teil 2: Verwendung erweiterter Cmdlets](http://blogs.msdn.com/b/sqlAlways%20On/archive/2012/02/13/monitoring-Always%20On-health-with-powershell-part-2.aspx)  
  
-   [Teil 3: Eine einfache Überwachungsanwendung](http://blogs.msdn.com/b/sqlAlways%20On/archive/2012/02/15/monitoring-Always%20On-health-with-powershell-part-3.aspx)  
  
-   [Teil 4: Integration in SQL Server-Agent](http://blogs.msdn.com/b/sqlAlways%20On/archive/2012/02/15/the-always-on-health-model-part-4.aspx)  
  
## Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../Topic/Overview%20of%20Always On%20Availability%20Groups%20\(SQL%20Server\).md)   
 [Verwaltung einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/administration-of-an-availability-group-sql-server.md)   
 [Überwachen von Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)   
 [AlwaysOn-Richtlinien für Betriebsprobleme mit AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always on policies for operational issues - always on availability.md)  
  
  