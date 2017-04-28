---
title: "Ändern der Spaltenreihenfolge einer Tabelle | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- columns [SQL Server], change order in a table
- column order, change
ms.assetid: cd99ef56-9085-431a-a0fc-58e7add5399f
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f9ab22cf6c60bd7d89ff70eba15ca65c731a1fb1
ms.lasthandoff: 04/11/2017

---
# <a name="change-column-order-in-a-table"></a>Ändern der Spaltenreihenfolge einer Tabelle
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Sie können mit [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] die Reihenfolge der Spalten im Tabellen-Designer in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ändern.  
  
> [!CAUTION]  
>  Das Ändern der Spaltenreihenfolge in einer Tabelle kann sich auf den Code und die Anwendungen auswirken, die von einer bestimmten Spaltenreihenfolge abhängig sind. Dies schließt Abfragen, Sichten, gespeicherte Prozeduren, benutzerdefinierte Funktionen und Clientanwendungen ein. Bedenken Sie sorgfältig die Konsequenzen, bevor Sie Änderungen an der Spaltenreihenfolge vornehmen. Best Practice ist, in der Anwendung oder auf der Abfrageebene die Reihenfolge anzugeben, in der die Spalten zurückgegeben werden sollen. Sie sollten sich nicht darauf verlassen, dass bei Verwendung von SELECT * alle Spalten in der Reihenfolge, in der sie in der Tabelle definiert worden sind, zurückgegeben werden. Geben Sie die Spalten in Abfragen und Anwendungen immer namentlich in der Reihenfolge an, in der sie angezeigt werden sollen.  
  
 **In diesem Thema**  
  
-   **So ändern Sie die Spaltenreihenfolge mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-change-the-column-order"></a>So ändern Sie die Spaltenreihenfolge  
  
1.  Klicken Sie im **Objekt-Explorer**mit der rechten Maustaste auf die Tabelle mit Spalten, die Sie neu anordnen möchten, und klicken Sie auf **Entwerfen**.  
  
2.  Markieren Sie das Feld links neben dem Namen der Spalte, deren Reihenfolge Sie ändern möchten.  
  
3.  Ziehen Sie die Spalte an eine andere Position innerhalb der Tabelle.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So ändern Sie die Spaltenreihenfolge**  
  
 Diese Aufgabe kann nicht mit Transact-SQL-Anweisungen ausgeführt werden.  
  
###  <a name="TsqlExample"></a>  
