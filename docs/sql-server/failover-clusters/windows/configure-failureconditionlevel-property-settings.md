---
title: Konfigurieren von FailureConditionLevel-Eigenschafteneinstellungen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 513dd179-9a46-46da-9fdd-7632cf6d0816
caps.latest.revision: 29
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 46e7f2aca995373d14ce0096a4dba4204cc69ece
ms.lasthandoff: 04/11/2017

---
# <a name="configure-failureconditionlevel-property-settings"></a>Konfigurieren von FailureConditionLevel-Eigenschafteneinstellungen
  Mit der FailureConditionLevel-Eigenschaft können Sie die Bedingungen für einen Failover oder Neustart der Always On-Failoverclusterinstanz (FCI) festlegen. Änderungen an dieser Eigenschaft werden unmittelbar übernommen, ohne dass ein Neustart des Windows Server-Failoverclusterdiensts (WSFC) oder der FCI-Ressource erforderlich ist.  
  
-   **Before you begin:**  [FailureConditionLevel Property Settings](#Restrictions), [Security](#Security)  
  
-   **To configure the FailureConditionLevel property settings using,** [PowerShell](#PowerShellProcedure), [Failover Cluster Manager](#WSFC), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> FailureConditionLevel-Eigenschafteneinstellungen  
 Die Fehlerbedingungen werden auf einer ansteigenden Skala festgelegt. Auf der Ebene 1-5 enthält jede Ebene die Bedingungen der vorherigen Ebenen sowie die eigenen Bedingungen. Dies bedeutet, dass die Wahrscheinlichkeit eines Failovers oder Neustarts mit jeder Ebene zunimmt.  Weitere Informationen finden Sie im Abschnitt "Bestimmen von Fehlern" des Themas [Failover Policy for Failover Cluster Instances](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md) .  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert ALTER SETTINGS- und VIEW SERVER STATE-Berechtigungen.  
  
##  <a name="PowerShellProcedure"></a> PowerShell  
  
##### <a name="to-configure-failureconditionlevel-settings"></a>So konfigurieren Sie die FailureConditionLevel-Einstellungen  
  
1.  Starten Sie eine erhöhte Windows PowerShell mithilfe von **Als Administrator ausführen**.  
  
2.  Importieren Sie das **FailoverClusters** -Modul, um die Cluster-Cmdlets zu aktivieren.  
  
3.  Verwenden Sie das **Get-ClusterResource** -Cmdlet, um die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Ressource zu suchen, und verwenden Sie dann das **Set-ClusterParameter** -Cmdlet, um die **FailureConditionLevel** -Eigenschaft für eine Failoverclusterinstanz festzulegen.  
  
> [!TIP]  
>  Bei jedem Öffnen eines neuen PowerShell-Fensters müssen Sie das **FailoverClusters** -Modul importieren.  
  
### <a name="example-powershell"></a>Beispiel (PowerShell)  
 Im folgenden Beispiel wird die FailureConditionLevel-Einstellung auf der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Ressource "`SQL Server (INST1)`" in "Failover oder Neustart bei wichtigen Serverfehlern" geändert.  
  
```powershell  
Import-Module FailoverClusters  
  
$fci = "SQL Server (INST1)"  
Get-ClusterResource $fci | Set-ClusterParameter FailureConditionLevel 3  
  
```  
  
### <a name="related-content-powershell"></a>Verwandte Inhalte (PowerShell)  
  
-   [Clustering and High-Availability](http://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) (Clustering und hohe Verfügbarkeit) (Failoverclustering und Netzwerklastenausgleichs-Teamblog)  
  
-   [Erste Schritte mit Windows PowerShell auf einem Failovercluster](http://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [Clusterressourcenbefehle und entsprechende Windows PowerShell-Cmdlets](http://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
##  <a name="WSFC"></a> Verwenden des Failovercluster-Manager-Snap-Ins  
 **So konfigurieren Sie FailureConditionLevel-Eigenschafteneinstellungen:**  
  
1.  Öffnen Sie des Failovercluster-Manager-Snap-In.  
  
2.  Erweitern Sie **Dienste und Anwendungen** , und wählen Sie den FCI aus.  
  
3.  Klicken Sie mit der rechten Maustaste auf die **SQL Server-Ressource** unter **Sonstige Ressourcen**, und wählen Sie im Kontextmenü **Eigenschaften** aus. Das Dialogfeld **Eigenschaften** der SQL Server-Ressource wird angezeigt.  
  
4.  Wählen Sie die Registerkarte **Eigenschaften** aus, geben Sie den gewünschten Wert für die **FailureConditionLevel** -Eigenschaft ein, und klicken Sie dann auf **OK** , um die Änderung zu übernehmen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So konfigurieren Sie FailureConditionLevel-Eigenschafteneinstellungen:**  
  
 Mit der Anweisung [ALTER SERVER CONFIGURATION](../../../t-sql/statements/alter-server-configuration-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] können Sie den FailureConditionLevel-Eigenschaftswert angeben.  
  
###  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
 Im folgenden Beispiel wird die FailureConditionLevel-Eigenschaft auf 0 gesetzt. Dadurch wird angegeben, dass bei einer Fehlerbedingung nicht automatisch ein Failover oder Neustart ausgelöst wird.  
  
```  
ALTER SERVER CONFIGURATION SET FAILOVER CLUSTER PROPERTY FailureConditionLevel = 0;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)   
 [Failover Policy for Failover Cluster Instances](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)  
  
  
