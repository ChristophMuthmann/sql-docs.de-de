---
title: "Verwenden von Wertbeziehungen in einer Verbunddom&#228;ne | Microsoft Docs"
ms.custom: ""
ms.date: "11/22/2011"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dqs.dm.cdvaluerelations.f1"
ms.assetid: 5ee468f0-8538-4620-90e8-63f466c9000e
caps.latest.revision: 12
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 12
---
# Verwenden von Wertbeziehungen in einer Verbunddom&#228;ne
  In diesem Thema wird beschrieben, wie Wertkombinationen angezeigt werden, die während des Wissensermittlungsprozesses in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) für die Verbunddomäne gefunden wurden. Auf dieser Seite wird angezeigt, wie oft die Wertkombinationen vorkommen. Die Wertverwaltung wird nicht für Verbunddomänen unterstützt. Deshalb können Sie für die Werte keine Vorgänge ausführen.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Um Wertbeziehungen anzuzeigen, müssen Sie eine Verbunddomäne erstellt und geöffnet haben.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die dqs_kb_editor- oder dqs_administrator-Rolle in der DQS_MAIN-Datenbank verfügen, um Wertbeziehungen in einer Verbunddomäne anzuzeigen.  
  
##  <a name="Use"></a> Anzeigen von Wertbeziehungen  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Öffnen oder erstellen Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm eine Wissensdatenbank. Wählen Sie **Domänenverwaltung** als Aktivität aus, und klicken Sie dann auf **Öffnen** oder **Erstellen**. Weitere Informationen finden Sie unter [Create a Knowledge Base](../data-quality-services/create-a-knowledge-base.md) oder [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md).  
  
3.  Wählen Sie aus der **Domänenliste** auf der Seite **Domänenverwaltung** die Verbunddomäne aus, für die Sie eine Domänenregel erstellen möchten, oder erstellen Sie eine neue Verbunddomäne. Wenn Sie eine neue Domäne erstellen müssen, finden Sie unter [Create a Composite Domain](../data-quality-services/create-a-composite-domain.md)weitere Informationen.  
  
4.  Klicken Sie auf die Registerkarte **Wertbeziehungen** .  
  
5.  Zeigen Sie die Häufigkeit für jede Wertkombination an.  
  
    > [!NOTE]  
    >  In der Tabelle **Wert** wird jede Kombination von Werten angezeigt, die in der Verbunddomäne vorhanden ist. Jeder Wert wird in der einzelnen Domäne angezeigt, für die er gilt. Die Tabelle mit den Wertbeziehungen wird standardmäßig nach der Häufigkeit sortiert, aber Sie können auch auf eine andere Spalte klicken, um nach dieser Spalte zu sortieren. Nur Werte mit einer Frequenz größer gleich 20 werden angezeigt.  
  
6.  Sie können keine Werte in der Tabelle ändern. Wenn Sie andere Vorgänge ausgeführt haben, klicken Sie auf **Fertig stellen** , um die Domänenverwaltungsaktivität abzuschließen. Klicken Sie andernfalls auf **Abbrechen**.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Anzeigen von Wertbeziehungen  
 Nachdem Sie die Wertbeziehungen angezeigt haben, können Sie andere Domänenverwaltungsaufgaben in der Domäne ausführen. Sie können die Wissensermittlung durchführen, um der Domäne Wissen hinzuzufügen, oder Sie können der Domäne eine Abgleichsrichtlinie hinzufügen. Weitere Informationen finden Sie unter [Durchführen der Wissensermittlung](../data-quality-services/perform-knowledge-discovery.md), [Verwalten einer Domäne](../data-quality-services/managing-a-domain.md), oder [Erstellen einer Abgleichsrichtlinie](../data-quality-services/create-a-matching-policy.md).  
  
  