---
title: "Erneutes Generieren von Transaktionsprozeduren zur Erfassung von Schema&#228;nderungen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Benutzerdefinierte Prozeduren [SQL Server-Replikation]"
  - "Transaktionsreplikation, Replizieren von Schemaänderungen"
  - "Schemas [SQL Server-Replikation], Replizieren von Änderungen"
ms.assetid: ccf68a13-e748-4455-8168-90e6d2868098
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Erneutes Generieren von Transaktionsprozeduren zur Erfassung von Schema&#228;nderungen
  Änderungen von Daten auf den Abonnenten werden bei der Transaktionsreplikation standardmäßig mithilfe von gespeicherten Prozeduren vorgenommen, die durch interne Prozeduren für jeden Tabellenartikel in der Veröffentlichung generiert werden. Die drei Prozeduren (eine für Einfügungen, eine für Updates und eine für Löschungen) werden auf den Abonnenten kopiert und ausgeführt, wenn eine Einfügung, ein Update oder eine Löschung auf den Abonnenten repliziert wird. Wenn bei einer Tabelle auf einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Verleger eine Schemaänderung vorgenommen wird, werden diese Prozeduren bei der Replikation automatisch erneut generiert, indem derselbe Satz interner Skriptprozeduren aufgerufen wird, damit die neuen Prozeduren dem neuen Schema entsprechen (die Replikation von Schemaänderungen wird bei Oracle-Verlegern nicht unterstützt).  
  
 Es ist auch möglich, benutzerdefinierte Prozeduren anzugeben, die an die Stelle einer oder mehrerer Standardprozedur(en) treten. Benutzerdefinierte Prozeduren müssen immer dann geändert werden, wenn sich die Schemaänderung auf die jeweilige Prozedur auswirkt. Wenn eine Prozedur z. B. auf eine Spalte verweist, die in einer Schemaänderung gelöscht wurde, müssen die Verweise auf diese Spalte aus der Prozedur entfernt werden. Für die Weitergabe einer neuen benutzerdefinierten Prozedur an Abonnenten durch Replikation gibt es die folgenden beiden Möglichkeiten:  
  
-   Die erste Möglichkeit besteht in der Verwendung einer benutzerdefinierten Skriptprozedur zum Ersetzen der von der Replikation verwendeten Standardprozeduren:  
  
    1.  Beim Ausführen von [Sp_addarticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), stellen Sie sicher die **@schema_option** 0 x 02-Bit **true**.  
  
    2.  Führen Sie [Sp_register_custom_scripting & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md) und geben Sie einen Wert von 'insert', 'update' oder 'delete' für den Parameter **@type** und der Namen der benutzerdefinierten Skriptprozedur für den Parameter **@value**.  
  
     Wenn das nächste Mal eine Schemaänderung vorgenommen wird, ruft die Replikation diese gespeicherte Prozedur auf, um die Definition für die neue benutzerdefinierte gespeicherte Prozedur auszugeben. Anschließend wird die Prozedur an die einzelnen Abonnenten weitergegeben.  
  
-   Die zweite Möglichkeit besteht darin, ein Skript zu verwenden, das eine neue benutzerdefinierte Prozedurdefinition enthält:  
  
    1.  Beim Ausführen von [Sp_addarticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), legen die **@schema_option** Bit 0 x 02 **false** damit die Replikation nicht automatisch benutzerdefinierte Prozeduren auf dem Abonnenten generiert.  
  
    2.  Vor jeder schemaänderung eine neue Skriptdatei zu erstellen und registrieren Sie das Skript bei der Replikation durch Ausführen von [Sp_register_custom_scripting & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md). Geben Sie den Wert 'Custom_script' für den Parameter **@type** und den Pfad zum Skript auf dem Verleger für den Parameter **@value**.  
  
     Bei der nächsten relevanten Schemaänderung wird dieses Skript innerhalb derselben Transaktion wie der DDL-Befehl auf allen Abonnenten ausgeführt. Nach Abschluss der Schemaänderung wird die Registrierung des Skripts aufgehoben. Damit das Skript bei einer weiteren Schemaänderung wieder ausgeführt wird, müssen Sie es erneut registrieren.  
  
## Siehe auch  
 [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)   
 [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  