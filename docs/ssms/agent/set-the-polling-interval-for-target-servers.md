---
title: Set the Polling Interval for Target Servers | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interval for polling [SQL Server]
- target servers [SQL Server], polling interval
- polling interval [SQL Server]
ms.assetid: 4ffbbefa-77fb-442e-a77c-cb8c6cab9f3c
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 98961d875eaef7e6c941212780ddcb60b44d57ac
ms.lasthandoff: 04/11/2017

---
# <a name="set-the-polling-interval-for-target-servers"></a>Set the Polling Interval for Target Servers
In diesem Thema wird das Festlegen der Frequenz für den [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent beschrieben, mit der Informationen vom Master- zu den Zielservern aktualisiert werden. Ein Auftrag ist eine festgelegte Reihe von Aktionen, die der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent ausführt. Ein Multiserverauftrag ist ein Auftrag, der von einem Masterserver auf mindestens einem Zielserver ausgeführt wird.  
  
-   **Vorbereitungen:**  [Sicherheit](#Security)  
  
-   **Festlegen des Abrufintervalls für Zielserver mit:** [SQL Server Management Studio](#SSMS), [Transact-SQL](#TSQL)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
Auf jedem Server kann gleichzeitig eine Instanz des gleichen Auftrags ausgeführt werden. Jeder Zielserver ruft in regelmäßigen Abständen den Masterserver ab, lädt eine Kopie aller neuen Aufträge herunter, die dem Zielserver zugewiesen wurden, und trennt dann die Verbindung. Der Zielserver führt den Auftrag lokal aus und stellt dann erneut eine Verbindung mit dem Masterserver her, um den Auftragsergebnisstatus hochzuladen.  
  
> [!NOTE]  
> Wenn der Zielserver versucht, den Auftragsstatus durch Hochladen zu übertragen, und dabei nicht auf den Masterserver zugreifen kann, bleibt der Auftragsstatus so lange im Spooler (in der Warteschlange), bis der Masterserver wieder zur Verfügung steht.  
  
### <a name="Security"></a>Sicherheit  
Ausführliche Informationen finden Sie unter [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md) und [Choose the Right SQL Server Agent Service Account for Multiserver Environments](../../ssms/agent/choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md).  
  
## <a name="SSMS"></a>Verwenden von SQL Server Management Studio  
**So legen Sie das Abrufintervall für Zielserver fest**  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]her, und erweitern Sie dann diese Instanz.  
  
2.  Klicken Sie mit der rechten Maustaste auf **SQL Server-Agent**, zeigen Sie auf **Multiserververwaltung**, und klicken Sie dann auf **Zielserver verwalten**.  
  
3.  Klicken Sie auf der Registerkarte **Status des Zielservers** auf **Anweisungen bereitstellen**.  
  
4.  Wählen Sie in der Liste **Anweisungstyp** die Option **Abrufintervall festlegen**aus.  
  
5.  Geben Sie im Feld **Abrufintervall** die Anzahl von Sekunden zwischen 10 und 28.800 ein, die verstreichen müssen, bevor der Zielserver den Masterserver abruft.  
  
6.  Führen Sie unter **Empfänger**eine der folgenden Aktionen aus:  
  
    1.  Klicken Sie auf **Alle Zielserver** , wenn für alle Zielserver dasselbe Abrufintervall gilt.  
  
    2.  Klicken Sie auf **Diese Zielserver** , wenn nicht für alle Zielserver dasselbe Abrufintervall gilt, und wählen Sie dann die Zielserver aus, für die dieses Abrufintervall verwendet werden soll.  
  
## <a name="TSQL"></a>Verwenden von Transact-SQL  
**So legen Sie das Abrufintervall für Zielserver fest**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit einer Instanz von Database Engine (Datenbankmodul) her, und erweitern Sie dann diese Instanz.  
  
2.  Klicken Sie auf der Symbolleiste auf **Neue Abfrage**.  
  
3.  Verwenden Sie im Abfragefenster die gespeicherte Systemprozedur [sp_post_msx_operation (Transact-SQL)](http://msdn.microsoft.com/en-us/085deef8-2709-4da9-bb97-9ab32effdacf) , um das Abrufintervall für Zielserver festzulegen.  
  
## <a name="see-also"></a>Siehe auch  
[sysdownloadlist](http://msdn.microsoft.com/en-us/71087a4c-e829-488e-aa7d-a9476e2b4779)  
  

