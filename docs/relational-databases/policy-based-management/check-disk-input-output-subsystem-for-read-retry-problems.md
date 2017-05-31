---
title: "Überprüfen des Datenträger-E/A-Subsystems auf Lesewiederholungsprobleme | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: cedf4097-5b73-4964-9935-74a101847019
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c40f4c7e64d8ee022618c2d5d6bc962b1a94b398
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="check-disk-input-output-subsystem-for-read-retry-problems"></a>Überprüfen des Datenträger-E/A-Subsystems auf Lesewiederholungsprobleme
  Diese Regel überprüft das Ereignisprotokoll auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlermeldung 825. Mit dieser Meldung wird angegeben, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim ersten Versuch keine Daten vom Datenträger lesen konnte. Diese Meldung weist auf ein größeres Problem mit dem E/A-Subsystem des Datenträgers hin. Diese Meldung deutet aktuell nicht auf ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Problem hin. Durch das Datenträgerproblem werden jedoch möglicherweise Datenverluste oder Beschädigungen der Datenbank verursacht, wenn es nicht behoben wird.  
  
## <a name="best-practices-recommendations"></a>Empfehlungen zu Best Practices  
 Mit den folgenden Aktionen können Sie das zugrunde liegende Hardwareproblem möglicherweise ermitteln und lösen:  
  
-   Beachten Sie das Fehlerprotokoll und den jeweiligen Text in dieser Meldung, um Informationen zu den Ursachen für das Problem zu erfahren.  
  
-   Prüfen Sie das Datenträgersystem. Das Problem ist möglicherweise auf die Datenträger, Datenträgercontroller, Arraykarten oder Datenträgertreiber zurückzuführen.  
  
-   Die neuesten Hilfsprogramme zum Überprüfen des Status des Datenträgersystems erhalten Sie beim Hersteller des Datenträgers.  
  
-   Wenden Sie sich an den Hersteller des Datenträgers, um die neuesten Treiberupdates zu erhalten.  
  
## <a name="for-more-information"></a>Weitere Informationen  
 [MSSQLSERVER_825](http://msdn.microsoft.com/library/f69f8214-5af1-4769-878b-117ad6eaff52)  
  
 [SQL Server I/O Basics, Chapter 2 (in Englisch)](http://go.microsoft.com/fwlink/?linkid=69370)  
  
  
