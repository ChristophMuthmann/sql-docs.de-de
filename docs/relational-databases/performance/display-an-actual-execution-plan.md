---
title: "Anzeigen eines tats&#228;chlichen Ausf&#252;hrungsplans | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Anzeigen von Ausführungsplänen"
  - "Tatsächliche Ausführungspläne"
  - "Darstellen von Ausführungsplänen"
  - "Ausführungspläne [SQL Server], anzeigen"
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# Anzeigen eines tats&#228;chlichen Ausf&#252;hrungsplans
  In diesem Thema wird das Generieren tatsächlicher grafischer Ausführungspläne mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]beschrieben. Beim Generieren tatsächlicher Ausführungspläne werden die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfragen oder -Batches ausgeführt. Der generierte Ausführungsplan zeigt den tatsächlichen Abfrageausführungsplan an, der von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] zur Ausführung der Abfragen verwendet wird.  
  
 Benutzer müssen zum Verwenden dieser Funktion die entsprechenden Berechtigungen zum Ausführen der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfragen besitzen, für die ein grafischer Ausführungsplan generiert wird. Darüber hinaus muss ihnen die SHOWPLAN-Berechtigung für alle Datenbanken erteilt werden, auf die die Abfrage verweist.  
  
### So schließen Sie einen Ausführungsplan für eine Abfrage bei der Ausführung ein  
  
1.  Klicken Sie auf der Symbolleiste von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] auf **Datenbankmodul-Abfrage**. Sie können auch eine vorhandene Abfrage öffnen und den geschätzten Ausführungsplan anzeigen, indem Sie auf die Symbolleisten-Schaltfläche **Datei öffnen** klicken und die vorhandene Abfrage suchen.  
  
2.  Geben Sie die Abfrage ein, für die Sie den tatsächlichen Ausführungsplan anzeigen möchten.  
  
3.  Klicken Sie im Menü **Abfrage** auf **Tatsächlichen Ausführungsplan einschließen** , oder klicken Sie auf die Symbolleistenschaltfläche **Tatsächlichen Ausführungsplan einschließen** .  
  
4.  Führen Sie die Abfrage aus, indem Sie auf die Symbolleistenschaltfläche **Ausführen** klicken. Der vom Abfrageoptimierer verwendete Plan wird im Ergebnisbereich auf der Registerkarte **Ausführungsplan** angezeigt. Positionieren Sie die Maus über die logischen und physischen Operatoren, um deren Beschreibung und Eigenschaften in der QuickInfo anzuzeigen.  
  
     Sie können die Operatoreigenschaften auch im Eigenschaftenfenster anzeigen. Falls die Eigenschaften nicht sichtbar sind, klicken Sie mit der rechten Maustaste auf einen Operator, und wählen Sie **Eigenschaften** aus. Wählen Sie einen Operator aus, um seine Eigenschaften anzuzeigen.  
  
5.  Sie können die Anzeige des Ausführungsplans ändern, indem Sie mit der rechten Maustaste auf den Ausführungsplan klicken und **Vergrößern**, **Verkleinern**, **Vergrößern/Verkleinern** oder **Zoom anpassen** auswählen. Mit**Vergrößern** und **Verkleinern** können Sie den Ausführungsplan vergrößern bzw. verkleinern. Mit **Vergrößern/Verkleinern** können Sie dagegen einen eigenen Zoomfaktor definieren, z. B. 80 Prozent. Mit**Zoom anpassen** können Sie den Ausführungsplan an die Größe des Ergebnisbereichs anpassen.  
  
  