---
title: "Anzeigen des geschätzten Ausführungsplans | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/21/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- zoom [SQL Server]
- estimated execution plan [SQL Server]
- displaying execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
- customizing execution plan display [SQL Server]
- modifying execution plan display
- custom zoom [SQL Server]
ms.assetid: e94aa576-4c0c-4c54-ad05-6c3432cc615b
caps.latest.revision: "26"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b05bddb677c7cf707c63c003c569eb296270832d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="display-the-estimated-execution-plan"></a>Anzeigen des geschätzten Ausführungsplans
  In diesem Thema wird das Generieren grafischer geschätzter Ausführungspläne mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]beschreiben. Beim Generieren von geschätzten Ausführungsplänen werden die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfragen oder -Batches nicht ausgeführt. Deshalb enthält ein geschätzter Ausführungsplan keine Laufzeitinformationen wie die tatsächlichen Nutzungsmetriken der Ressourcen oder Laufzeitwarnungen. Stattdessen zeigt der generierte Ausführungsplan den Abfrageausführungsplan an, den [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] bei tatsächlicher Ausführung der Abfragen mit größter Wahrscheinlichkeit verwenden würde sowie die geschätzten Reihen, die durch die Operatoren im Plan fließen.  
  
 Zum Verwenden dieser Funktion müssen die Benutzer die entsprechenden Berechtigungen haben, um die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfrage auszuführen, für die ein grafischer Ausführungsplan generiert wird. Den Benutzern muss auch die SHOWPLAN-Berechtigung für alle Datenbanken erteilt werden, auf die die Abfrage verweist.  
  
### <a name="to-display-the-estimated-execution-plan-for-a-query"></a>So zeigen Sie den geschätzten Ausführungsplan für eine Abfrage an  
  
1.  Klicken Sie auf der Symbolleiste auf **Datenbankmodul-Abfrage**. Sie können auch eine vorhandene Abfrage öffnen und den geschätzten Ausführungsplan anzeigen, indem Sie auf die Symbolleisten-Schaltfläche **Datei öffnen** klicken und die vorhandene Abfrage suchen.  
  
2.  Geben Sie die Abfrage, für die Sie den geschätzten Ausführungsplan anzeigen möchten, ein.  
  
3.  Klicken Sie im Menü **Abfrage** auf **Geschätzten Ausführungsplan anzeigen** , oder klicken Sie auf die Symbolleisten-Schaltfläche **Geschätzten Ausführungsplan anzeigen** . Der geschätzte Ausführungsplan wird im Ergebnisbereich auf der Registerkarte **Ausführungsplan** angezeigt. Um weitere Informationen anzuzeigen, lassen Sie den Mauszeiger über den logischen und physischen Operatorsymbolen ruhen. Die Beschreibung und die Eigenschaften des Operators werden nun in der QuickInfo angezeigt. Sie können die Operatoreigenschaften auch im Eigenschaftenfenster anzeigen. Klicken Sie mit der rechten Maustaste auf einen Operator, und klicken Sie auf **Eigenschaften**, wenn die Eigenschaften nicht sichtbar sind. Wählen Sie einen Operator aus, um seine Eigenschaften anzuzeigen.  
  
4.  Um die Anzeige des Ausführungsplans zu ändern, klicken Sie mit der rechten Maustaste auf den Ausführungsplan, und wählen Sie **Vergrößern**, **Verkleinern**, **Vergrößern/Verkleinern**oder **Zoom anpassen**aus. Mit**Vergrößern** und **Verkleinern** können Sie den Ausführungsplan in festgelegten Schritten vergrößern oder verkleinern. **Vergrößern/Verkleinern** ermöglicht Ihnen, die Anzeigevergrößerung nach Wunsch festzulegen, etwa auf 80 Prozent. Mit**Zoom anpassen** können Sie den Ausführungsplan an die Größe des Ergebnisbereichs anpassen. Verwenden Sie alternativ eine Kombination aus der STRG-Taste und Ihrem Mausrad, um den **dynamischen Zoom** zu aktivieren.  
 
 > [!NOTE] 
 > Verwenden Sie alternativ [SET SHOWPLAN_XML](../../t-sql/statements/set-showplan-xml-transact-sql.md), um Informationen zum Ausführungsplan jeder Anweisung zurückzugeben, ohne diese ausführen zu müssen. Bei der Verwendung in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verfügt die Registerkarte *Ergebnisse* über einen Link, der den Ausführungsplan im grafischen Format öffnet.   
