---
title: "Lektion 2: Vorbereiten des Momentaufnahmeordners | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "Replikation [SQL Server], Tutorials"
ms.assetid: f286cde9-c0d0-43ef-b7ba-53c3cbb8906c
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Lektion 2: Vorbereiten des Momentaufnahmeordners
In dieser Lektion erfahren Sie, wie Sie den Momentaufnahmeordner konfigurieren, in dem die Veröffentlichungsmomentaufnahme erstellt und gespeichert wird.  
  
### So erstellen Sie eine Freigabe für den Momentaufnahmeordner und weisen Berechtigungen zu  
  
1.  Navigieren Sie im Windows-Explorer zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenordner. Der Standardspeicherort lautet C:\Programme\Microsoft SQL Server\MSSQL.X\MSSQL\Data.  
  
2.  Erstellen Sie einen neuen Ordner mit dem Namen **repldata**.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Ordner, und klicken Sie anschließend auf **Eigenschaften**.  
  
4.  Klicken Sie auf der Registerkarte **Freigabe** im Dialogfeld **Eigenschaften von repldata** auf **Freigeben**.  
  
5.  Klicken Sie im Dialogfeld **Dateifreigabe** auf **Freigeben** und anschließend auf **Fertig**.  
  
6.  Klicken Sie auf der Registerkarte **Sicherheit** auf **Bearbeiten**.  
  
7.  Klicken Sie im Dialogfeld **Berechtigungen** auf **Hinzufügen**. Geben Sie im Textfeld **Benutzer, Computer, Dienstkonten oder Gruppen auswählen** den Namen des in Lektion 1 erstellten Momentaufnahme-Agentkontos ein: \<*Computername>***\repl_snapshot**, wobei \<*Computername>* den Namen des Verlegers angibt. Klicken Sie auf **Namen überprüfen** und anschließend auf **OK**.  
  
8.  Wiederholen Sie den vorherigen Schritt, um Berechtigungen für den Verteilungs-Agent (als \<*Computername>***\repl_distribution**) und für den Merge-Agent (als \<*Computername>***\repl_merge**) hinzuzufügen.  
  
9. Überprüfen Sie, ob die folgenden Berechtigungen gewährt wurden.  
  
    -   repl_snapshot - Vollzugriff  
  
    -   repl_distribution - Lesezugriff  
  
    -   repl_merge - Lesezugriff  
  
10. Klicken Sie auf **OK**, um das Dialogfeld **Eigenschaften von repldata** zu schließen und die repldata-Freigabe zu erstellen.  
  
## Nächste Schritte  
Sie haben erfolgreich eine Freigabe für den Momentaufnahmeordner konfiguriert. Im nächsten Arbeitsschritt konfigurieren Sie die Verteilung. Weitere Informationen finden Sie unter [Lektion 3: Konfigurieren der Verteilung](../../relational-databases/replication/lesson-3-configuring-distribution.md).  
  
## Siehe auch  
[Sichern des Momentaufnahmeordners](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
  
