---
title: "COM-basierte benutzerdefinierte Konfliktl&#246;ser | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "COM-basierte Konfliktlöser [SQL Server-Replikation]"
  - "Benutzerdefinierte Konfliktlöser [SQL Server-Replikation]"
ms.assetid: 94195797-ad7a-4962-a8e3-b259cd13aa38
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# COM-basierte benutzerdefinierte Konfliktl&#246;ser
  Benutzerdefinierte Konfliktlöser ermöglichen eine höhere Flexibilität als der Standardmechanismus für die Konfliktlösung. Darüber hinaus kann mit Ihnen Geschäftslogik implementiert werden, die von den Anwendungen benötigt wird, die die replizierten Daten verwenden. Ein COM-basierter benutzerdefinierter Konfliktlöser ist eine Dynamic Link Library (DLL), die implementiert die **ICustomResolver** COM-Schnittstelle, deren Methoden und Eigenschaften, und andere unterstützende Schnittstellen und Typdefinitionen, die speziell für die Auflösung des Konflikts zwischen entwickelt.  
  
> [!NOTE]  
>  Es wird empfohlen, nach Möglichkeit einen Geschäftslogikhandler statt eines COM-basierten benutzerdefinierten Konfliktlösers zu verwenden. Weitere Informationen zu geschäftslogikhandlern finden Sie unter [führen Business Logic During Merge Synchronization](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
 Zum Erstellen eines benutzerdefinierten COM-Konfliktlösers können Sie die in der Datei replrec.dll bereitgestellte Typbibliothek verwenden. Standardmäßig wird diese Bibliothek unter [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM installiert.  
  
 Sie müssen Folgendes vor dem Schreiben eines benutzerdefinierten COM-Konfliktlösers entscheiden:  
  
-   Die Typen von Zeilenänderungen, die aufgelöst werden sollen (z. B. Updates, Einfügungen und Löschungen), und ob der Konfliktlöser beim Upload und/oder dem Download von Mergeänderungen aufgerufen werden soll. Sie können einen Änderungstyp, alle Änderungen oder eine beliebige Kombination daraus angeben. Der Standardkonfliktlöser für Mergeprozesse verarbeitet alle Konflikte, die nicht von einem benutzerdefinierten Konfliktlöser abgedeckt werden.  
  
-   Ob beim Lösen des Konflikts das Protokollieren auf Spaltenebene verwendet werden soll. Wenn das Protokollieren auf Spaltenebene aktiviert ist, werden nur Daten in den Spalten, in denen ein Konflikt vorhanden ist, als Konflikt markiert; anderenfalls werden die Daten zusammengeführt. Konflikte werden jedoch wie bei der Nachverfolgung auf Zeilenebene gelöst: Der Prioritätsgewinner überschreibt die gesamte Datenzeile (die Daten können jedoch eine Mischung aus Werten vom Verleger, Werten von den Abonnenten oder geänderten Werten sein, die weder vom Verleger noch von den Abonnenten stammen). Weitere Informationen finden Sie unter [Detect and Resolve Merge Replication Conflicts](../../../relational-databases/replication/merge/detect-and-resolve-merge-replication-conflicts.md).  
  
 Zum Implementieren eines COM-basierten benutzerdefinierten Konfliktlösers finden Sie unter [Implementieren eines benutzerdefinierten Konfliktlösers für einen Artikel Merge](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md).  
  
 Ein benutzerdefinierter Konfliktlöser wird für einen Artikel und nicht für eine vollständige Veröffentlichung angegeben. Derselbe Konfliktlöser kann mit mehreren Artikeln verwendet werden, jedoch bezieht sich die Logik in benutzerdefinierten Konfliktlösern häufig auf eine bestimmte Tabelle. Wenn der in einer Tabelle verwendete Artikel nach dem Erstellen des Konfliktlösers geändert wird (z. B. durch Umbenennen des bei der Konfliktlösung verwendeten Spaltennamens), muss der Konfliktlöser gegebenenfalls geändert und erneut kompiliert werden.  
  
 Informationen zum Angeben eines benutzerdefinierten Konfliktlösers finden Sie unter [Specify a Merge Article Resolver](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md).  
  
## Siehe auch  
 [Erweiterte Konflikterkennung und -lösung bei der Mergereplikation](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Microsoft COM-basierte Konfliktlöser](../../../relational-databases/replication/merge/microsoft-com-based-resolvers.md)  
  
  