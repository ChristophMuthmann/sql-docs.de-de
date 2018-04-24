---
title: Konfigurieren des min. Arbeitsspeichers pro Abfrage (Serverkonfigurationsoption) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/24/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- memory [SQL Server], queries
- minimum query memory
- queries [SQL Server], memory
- min memory per query option
ms.assetid: ecd3fb79-b4a6-432f-9ef5-530e0d42d5a6
caps.latest.revision: 28
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a44ef836a60524d43bd03fb33c929c19d1e90cbf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="configure-the-min-memory-per-query-server-configuration-option"></a>Konfigurieren der Serverkonfigurationsoption Min. Arbeitsspeicher pro Abfrage
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie die Serverkonfigurationsoption **Min. Arbeitsspeicher pro Abfrage** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]konfiguriert wird. Sie können mithilfe der Option **Min. Arbeitsspeicher pro Abfrage** die Mindestmenge an Arbeitsspeicher (in KB) angeben, die für das Ausführen einer Abfrage zugeordnet wird. Wenn Sie z. B. **Min. Arbeitsspeicher pro Abfrage** auf 2.048 KB festlegen, wird sichergestellt, dass der Abfrage mindestens so viel Arbeitsspeicher zugeordnet wird. Der Standardwert ist 1.024 KB. 512 KB ist der Minimalwert, und 2.147.483.647 KB (2 GB) ist der Maximalwert.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
     [Security](#Security)  
  
-   **So konfigurieren Sie die Option Min. Arbeitsspeicher pro Abfrage mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachverfolgung:**  [Nach dem Konfigurieren der Option „Min. Arbeitsspeicher pro Abfrage“](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Der unter „Min. Arbeitsspeicher pro Abfrage“ angegebene Wert hat Vorrang vor der Option [Speicher für Indexerstellung](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md). Wenn Sie beide Optionen ändern und der Wert von „index create memory“ (Speicher für Indexerstellung) den Wert von „min memory per query“ (Min. Arbeitsspeicher pro Abfrage) unterschreitet, werden die Werte zwar festgelegt, es wird jedoch eine Warnmeldung ausgegeben. Beim Ausführen der Abfrage wird eine ähnliche Warnung ausgegeben.  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Diese Option ist eine erweiterte Option und sollte ausschließlich von einem erfahrenen Datenbankadministrator oder einem zertifizierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Experten geändert werden.  
  
-   Der Abfrageprozessor von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versucht, den optimalen Umfang an Speicher zu bestimmen, der von einer Abfrage belegt werden soll. Mit der Option Min. Arbeitsspeicher pro Abfrage kann der Administrator den Umfang an Speicher angeben, der für eine einzelne Abfrage mindestens zur Verfügung gestellt wird. Abfragen erhalten im Allgemeinen mehr Speicher als hier angegeben, wenn Hash- und Sortiervorgänge für umfangreiche Datenmengen ausgeführt werden. Durch die Erhöhung des Werts für Min. Arbeitsspeicher pro Abfrage kann es bei einigen Abfragen mit geringem bis mittlerem Umfang zur Leistungssteigerung, jedoch auch zu stärkerem Wettbewerb um Speicherressourcen kommen. Die Option „Min. Arbeitsspeicher pro Abfrage“ schließt den für Sortiervorgänge zugeordneten Arbeitsspeicher ein.  

-    Legen Sie die Serverkonfigurationsoption „Min Arbeitsspeicher pro Abfrage“ nicht zu hoch fest, insbesondere auf sehr ausgelasteten Systemen, da die Abfrage warten muss, bis die minimalen Arbeitsspeicheranforderungen erfüllt werden können, oder bis der in der Serverkonfigurationsoption Abfragewartezeit angegebene Wert erreicht ist. Wenn zum Ausführen der Abfrage mehr Arbeitsspeicher als der angegebene Minimalwert vorhanden ist, darf die Abfrage den zusätzlichen Arbeitsspeicher verwenden, vorausgesetzt, der Arbeitsspeicher kann von der Abfrage effizient verwendet werden. 
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Ausführungsberechtigungen für **sp_configure** ohne Parameter oder nur mit dem ersten Parameter werden standardmäßig allen Benutzern erteilt. Zum Ausführen von **sp_configure** mit beiden Parametern zum Ändern einer Konfigurationsoption oder zum Ausführen der RECONFIGURE-Anweisung muss einem Benutzer die ALTER SETTINGS-Berechtigung auf Serverebene erteilt worden sein. Die ALTER SETTINGS-Berechtigung ist in den festen Serverrollen **sysadmin** und **serveradmin** eingeschlossen.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-configure-the-min-memory-per-query-option"></a>So konfigurieren Sie die Option Min. Arbeitsspeicher pro Abfrage  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf einen Server, und wählen Sie **Eigenschaften**aus.  
  
2.  Klicken Sie auf den **Speicher** -Knoten.  
  
3.  Geben Sie in das Feld **Minimaler Arbeitsspeicher pro Abfrage** die Mindestmenge an Arbeitsspeicher (in KB) ein, die für das Ausführen einer Abfrage zugeordnet wird.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-configure-the-min-memory-per-query-option"></a>So konfigurieren Sie die Option Min. Arbeitsspeicher pro Abfrage  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) verwendet wird, um den Wert der Option `min memory per query` auf `3500` KB festzulegen.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'min memory per query', 3500 ;  
GO  
RECONFIGURE;  
GO    
```  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Konfigurieren der Option Min. Arbeitsspeicher pro Abfrage  
 Die Einstellung tritt ohne Neustarten des Servers sofort in Kraft.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Configure the index create memory Server Configuration Option](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md)  
  
  
