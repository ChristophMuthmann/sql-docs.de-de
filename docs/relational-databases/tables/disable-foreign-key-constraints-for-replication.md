---
title: "Deaktivieren von Fremdschlüsseleinschränkungen für die Replikation | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- constraints [SQL Server], foreign keys
- foreign keys [SQL Server], disabling constraints
- disabling constraints
ms.assetid: 4211f2fd-d16a-4081-995c-43f1f0827f0b
caps.latest.revision: "20"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c7d304cbd4b5768c81177567170da2c6a050aee4
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="disable-foreign-key-constraints-for-replication"></a>Deaktivieren von Fremdschlüsseleinschränkungen für die Replikation
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Sie können Fremdschlüsseleinschränkungen für die Replikation in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]deaktivieren. Dies kann nützlich sein, wenn Sie Daten einer früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]veröffentlichen.  
  
> [!NOTE]  
>  Wird eine Tabelle mithilfe einer Replikation veröffentlicht, werden Fremdschlüsseleinschränkungen automatisch für die Operationen deaktiviert, die von Replikations-Agents ausgeführt werden. Wenn ein Replikations-Agent eine Einfügung, ein Update oder eine Löschung auf einem Abonnenten ausführt, wird die Einschränkung nicht überprüft; wenn ein Benutzer eine Einfügung, ein Update oder eine Löschung ausführt, wird die Einschränkung überprüft. Die Einschränkung wird für den Replikations-Agent deaktiviert, da die Einschränkung bereits auf dem Verleger überprüft wurde, als die Daten ursprünglich eingefügt, aktualisiert oder gelöscht wurden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Security](#Security)  
  
-   **So deaktivieren Sie eine Fremdschlüsseleinschränkung für die Replikation mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Tabelle.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-disable-a-foreign-key-constraint-for-replication"></a>So deaktivieren Sie eine Fremdschlüsseleinschränkung für die Replikation  
  
1.  Erweitern Sie im **Objekt-Explorer**die Tabelle mit der Fremdschlüsseleinschränkung, die geändert werden soll, und erweitern Sie dann den Ordner **Schlüssel** .  
  
2.  Klicken Sie mit der rechten Maustaste auf die Fremdschlüsseleinschränkung, und klicken Sie anschließend auf **Ändern**.  
  
3.  Wählen Sie im Dialogfeld **Fremdschlüsselbeziehungen** den Wert **Nein** für **Für Replikation erzwingen**aus.  
  
4.  Klicken Sie auf **Schließen**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-disable-a-foreign-key-constraint-for-replication"></a>So deaktivieren Sie eine Fremdschlüsseleinschränkung für die Replikation  
  
1.  Um diesen Task in [!INCLUDE[tsql](../../includes/tsql-md.md)]auszuführen, löschen Sie die Fremdschlüsseleinschränkung. Fügen Sie dann eine neue Fremdschlüsseleinschränkung hinzu, und geben Sie die Option NOT FOR REPLICATION an.  
  
 Weitere Informationen finden Sie unter [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  
