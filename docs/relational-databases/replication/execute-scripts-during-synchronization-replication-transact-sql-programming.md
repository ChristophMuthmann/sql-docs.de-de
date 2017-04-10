---
title: "Ausf&#252;hren von Skripts w&#228;hrend der Synchronisierung (Replikationsprogrammierung mit Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "Synchronisierung [SQL Server-Replikation], Skripts"
  - "Skripts [SQL Server-Replikation], Synchronisierung und"
  - "sp_addscriptexec"
ms.assetid: b58a0877-4e43-4fab-a281-24e6022d3fb1
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Ausf&#252;hren von Skripts w&#228;hrend der Synchronisierung (Replikationsprogrammierung mit Transact-SQL)
  Die Replikation unterstützt die bedarfsgesteuerte Ausführung von Skripts für Abonnenten von Transaktions- und Mergeveröffentlichungen. Diese Funktionalität kopiert das Skript in das Replikationsarbeitsverzeichnis und wendet das Skript dann mithilfe von **sqlcmd** auf dem Abonnenten an. Standardmäßig wird der Verteilungs-Agent beendet, wenn beim Anwenden des Skripts auf ein Abonnement für eine Transaktionsveröffentlichung ein Fehler auftritt. Mithilfe von gespeicherten Replikationsprozeduren können Sie ein [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skript angeben, das programmgesteuert ausgeführt werden soll.  
  
### So geben Sie ein Skript an, das für alle Abonnenten einer Momentaufnahme-, Transaktions- oder Mergeveröffentlichung ausgeführt werden soll  
  
1.  Erstellen und testen Sie das [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skript, das bedarfsgesteuert ausgeführt wird.  
  
2.  Speichern Sie die Skriptdatei an einem Speicherort, auf den der Momentaufnahme-Agent für die Veröffentlichung zugreifen kann.  
  
3.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addscriptexec & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md). Geben Sie **@publication**, den Namen der Skriptdatei mit dem vollständigen, in Schritt 2 erstellten UNC-Pfad für **@scriptfile**und einen der folgenden Werte für **@skiperror**ein:  
  
    -   **0** -der Agent beendet das Skript ausführen, wenn ein Fehler aufgetreten ist.  
  
    -   **1** – der Agent protokolliert Fehler und das Skript fortgesetzt, wenn Fehler auftreten.  
  
4.  Das angegebene Skript wird auf jedem Abonnenten ausgeführt, wenn der Agent das nächste Mal zur Synchronisierung des Abonnements ausgeführt wird.  
  
## Siehe auch  
 [Synchronisieren von Daten](../../relational-databases/replication/synchronize-data.md)  
  
  