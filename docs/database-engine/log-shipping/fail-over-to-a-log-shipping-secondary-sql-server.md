---
title: "Failover zu einer sekund&#228;ren Datenbank f&#252;r den Protokollversand (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Primäre Datenbanken [SQL Server]"
  - "Sekundäre Datendateien [SQL Server], manuelles Failover"
  - "Protokollversand [SQL Server-Agent], Failover"
  - "Failover [SQL Server], Protokollversand"
ms.assetid: edfe5d59-4287-49c1-96c9-dd56212027bc
caps.latest.revision: 31
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 31
---
# Failover zu einer sekund&#228;ren Datenbank f&#252;r den Protokollversand (SQL Server)
  Wenn die primäre Serverinstanz ausfällt oder gewartet werden muss, kann ein Failover zu einer sekundären Datenbank für den Protokollversand ausgeführt werden.  
  
## Vorbereitungen für ein kontrolliertes Failover  
 Normalerweise sind die primäre und die sekundäre Datenbank nicht synchronisiert, da die primäre Datenbank nach dem letzten Sicherungsauftrag weiterhin aktualisiert wird. In manchen Fällen wurden möglicherweise auch die aktuellen Sicherungen des Transaktionsprotokolls nicht auf die sekundären Serverinstanzen kopiert, oder die Protokollsicherungen wurden zwar kopiert, jedoch noch nicht vollständig auf die sekundäre Datenbank angewendet. Es wird empfohlen, nach Möglichkeit zunächst alle sekundären Datenbanken mit der primären Datenbank zu synchronisieren.  
  
 Informationen zu Protokollversandaufträgen finden Sie unter [Informationen zum Protokollversand &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
## Ausführen eines Failovers  
 So führen Sie ein Failover zu einer sekundären Datenbank aus  
  
1.  Kopieren Sie alle noch nicht kopierten Sicherungsdateien aus der Sicherungsfreigabe in den für den Kopiervorgang verwendeten Zielordner jedes sekundären Servers.  
  
2.  Wenden Sie der Reihe nach alle noch nicht angewendeten Transaktionsprotokollsicherungen auf jede sekundäre Datenbank an. Weitere Informationen finden Sie unter [Anwenden von Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
3.  Sichern Sie, wenn auf die primäre Datenbank zugegriffen werden kann, das aktive Transaktionsprotokoll, und wenden Sie die Protokollsicherung auf die sekundären Datenbanken an.  
  
     Wenn die ursprüngliche, primäre Serverinstanz nicht beschädigt ist, sichern Sie das Transaktionsprotokollfragment der primären Datenbank mit der Option WITH NORECOVERY. Dadurch verbleibt die Datenbank im Wiederherstellungsstatus und steht somit Benutzern nicht zur Verfügung. Sie können letztendlich auf diese Datenbank ein Rollforward ausführen, indem Sie Transaktionsprotokollsicherungen aus der primären Ersatzdatenbank anwenden.  
  
     Weitere Informationen finden Sie unter [Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md).  
  
4.  Nach der Synchronisierung der sekundären Server können Sie auf Wunsch ein Failover zu einem von ihnen ausführen, indem Sie seine sekundäre Datenbank wiederherstellen und Clients zu dieser Serverinstanz umleiten. Beim Wiederherstellen wird die Datenbank in einen konsistenten Status versetzt und online geschaltet.  
  
    > [!NOTE]  
    >  Wenn Sie eine sekundäre Datenbank verfügbar machen, sollten Sie sicherstellen, dass die Metadaten konsistent mit den Metadaten der ursprünglichen, ersten Datenbank sind. Weitere Informationen finden Sie unter [Verwalten von Metadaten beim Bereitstellen einer Datenbank auf einer anderen Serverinstanz &#40;SQL Server&#41;](../../relational-databases/databases/manage metadata when making a database available on another server.md).  
  
5.  Nachdem Sie die sekundäre Datenbank wiederhergestellt haben, können Sie sie so konfigurieren, dass sie für die anderen sekundären Datenbanken als erste Datenbank dient.  
  
     Wenn keine andere sekundäre Datenbank verfügbar ist, siehe [Konfigurieren des Protokollversands &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Ändern der Rollen zwischen primärem und sekundärem Protokollversandserver &#40;SQL Server&#41;](../../database-engine/log-shipping/change-roles-between-primary-and-secondary-log-shipping-servers-sql-server.md)  
  
-   [Verwaltung von Anmeldenamen und Aufträgen nach einem Rollenwechsel &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)  
  
## Siehe auch  
 [Protokollversandtabellen und gespeicherte Prozeduren](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)   
 [Informationen zum Protokollversand &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Protokollfragmentsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)  
  
  