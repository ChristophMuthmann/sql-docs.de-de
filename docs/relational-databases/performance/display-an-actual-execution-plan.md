---
title: "Anzeigen eines tatsächlichen Ausführungsplans | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/21/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- displaying execution plans
- actual execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d34a82e9ceb357fde6059e3259cb2be64a3e50d7
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="display-an-actual-execution-plan"></a>Anzeigen eines tatsächlichen Ausführungsplans
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] In diesem Thema wird das Generieren tatsächlicher grafischer Ausführungspläne mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] beschrieben. Tatsächliche Ausführungspläne werden nach der Ausführung der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Abfragen oder -Batches generiert. Deshalb enthält ein tatsächlicher Ausführungsplan Laufzeitinformationen wie die tatsächlichen Nutzungsmetriken der Ressourcen oder Laufzeitwarnungen (falls vorhanden). Der generierte Ausführungsplan zeigt den tatsächlichen Abfrageausführungsplan an, der von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] zur Ausführung der Abfragen verwendet wurde.  
  
 Benutzer müssen zum Verwenden dieser Funktion die entsprechenden Berechtigungen zum Ausführen der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfragen besitzen, für die ein grafischer Ausführungsplan generiert wird. Darüber hinaus muss ihnen die SHOWPLAN-Berechtigung für alle Datenbanken erteilt werden, auf die die Abfrage verweist.  
  
### <a name="to-include-an-execution-plan-for-a-query-during-execution"></a>So schließen Sie einen Ausführungsplan für eine Abfrage bei der Ausführung ein  
  
1.  Klicken Sie auf der Symbolleiste von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] auf **Datenbankmodul-Abfrage**. Sie können auch eine vorhandene Abfrage öffnen und den geschätzten Ausführungsplan anzeigen, indem Sie auf die Symbolleisten-Schaltfläche **Datei öffnen** klicken und die vorhandene Abfrage suchen. 
  
2.  Geben Sie die Abfrage ein, für die Sie den tatsächlichen Ausführungsplan anzeigen möchten.  
  
3.  Klicken Sie im Menü **Abfrage** auf **Tatsächlichen Ausführungsplan einschließen** , oder klicken Sie auf die Symbolleistenschaltfläche **Tatsächlichen Ausführungsplan einschließen** .  
  
4.  Führen Sie die Abfrage aus, indem Sie auf die Symbolleistenschaltfläche **Ausführen** klicken. Der vom Abfrageoptimierer verwendete Plan wird im Ergebnisbereich auf der Registerkarte **Ausführungsplan** angezeigt. Positionieren Sie die Maus über die logischen und physischen Operatoren, um deren Beschreibung und Eigenschaften in der QuickInfo anzuzeigen.  
  
     Sie können die Operatoreigenschaften auch im Eigenschaftenfenster anzeigen. Falls die Eigenschaften nicht sichtbar sind, klicken Sie mit der rechten Maustaste auf einen Operator, und wählen Sie **Eigenschaften**aus. Wählen Sie einen Operator aus, um seine Eigenschaften anzuzeigen.  
  
5.  Sie können die Anzeige des Ausführungsplans ändern, indem Sie mit der rechten Maustaste auf den Ausführungsplan klicken und **Vergrößern**, **Verkleinern**, **Vergrößern/Verkleinern**oder **Zoom anpassen**auswählen. Mit**Vergrößern** und **Verkleinern** können Sie den Ausführungsplan vergrößern bzw. verkleinern. Mit **Vergrößern/Verkleinern** können Sie dagegen einen eigenen Zoomfaktor definieren, z. B. 80 Prozent. Mit**Zoom anpassen** können Sie den Ausführungsplan an die Größe des Ergebnisbereichs anpassen. Verwenden Sie alternativ eine Kombination aus der STRG-Taste und Ihrem Mausrad, um den **dynamischen Zoom** zu aktivieren.  
  
 
 > [!NOTE] 
 > Verwenden Sie alternativ [SET STATISTICS XML](../../t-sql/statements/set-statistics-xml-transact-sql.md), um Informationen zum Ausführungsplan an jede Anweisung nach deren Ausführung zurückzugeben. Bei der Verwendung in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verfügt die Registerkarte *Ergebnisse* über einen Link, der den Ausführungsplan im grafischen Format öffnet.   
