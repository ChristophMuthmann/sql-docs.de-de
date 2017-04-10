---
title: "Pr&#252;fpunktvorgang f&#252;r speicheroptimierte Tabellen | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 47975bd5-373f-43cd-946a-da8e8088b610
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# Pr&#252;fpunktvorgang f&#252;r speicheroptimierte Tabellen
  Für speicheroptimierte Daten in Daten- und Änderungsdateien muss in regelmäßigen Abständen ein Prüfpunkt erstellt werden, um den aktiven Teil des Transaktionsprotokolls fortzuführen. Der Prüfpunkt ermöglicht die Wiederherstellung speicheroptimierter Tabellen am letzten erfolgreichen Prüfpunkt. Anschließend wird der aktive Teil des Transaktionsprotokolls angewendet, um die speicheroptimierten Tabellen zu aktualisieren und die Wiederherstellung abzuschließen. Bei den Prüfpunktvorgängen für datenträgerbasierte und speicheroptimierte Tabellen handelt es sich um unterschiedliche Vorgänge. Im Folgenden werden verschiedene Szenarien und das Prüfpunktverhalten für datenträgerbasierte und speicheroptimierte Tabellen beschrieben:  
  
## Manueller Prüfpunkt  
 Bei Ausgabe eines manuellen Prüfpunkts wird der Prüfpunkt sowohl für datenträgerbasierte als auch für speicheroptimierte Tabellen geschlossen. Die aktive Datendatei wird geschlossen, obwohl sie möglicherweise teilweise gefüllt ist.  
  
## Automatischer Prüfpunkt  
 Automatische Prüfpunkte werden für datenträgerbasierte und speicheroptimierte Tabellen unterschiedlich implementiert, da die Beibehaltung der Daten sich bei diesen beiden Tabellentypen unterscheidet.  
  
 Für datenträgerbasierte Tabellen wird ein automatischer Prüfpunkt basierend auf der Konfigurationsoption Wiederherstellungsintervall erstellt. (Weitere Informationen finden Sie unter [Ändern der Zielwiederherstellungszeit einer Datenbank &#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md).)  
  
 Für speicheroptimierte Tabellen wird ein automatischer Prüfpunkt erstellt, wenn die Größe der Transaktionsprotokolldatei seit dem letzten Prüfpunkt um 1,5 GB gestiegen ist. In dieser Größe von 1,5 GB sind Transaktionsprotokolldatensätze sowohl für datenträgerbasierte als auch für speicheroptimierte Tabellen enthalten.  
  
## Siehe auch  
 [Erstellen und Verwalten von Speicher für speicheroptimierte Objekte](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  