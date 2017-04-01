---
title: "&#196;ndern von Statistiken | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-statistics"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Statistiken [SQL Server], ändern"
  - "Ändern von Statistiken"
ms.assetid: b06299ca-ed52-411a-b245-45eac4628c99
caps.latest.revision: 9
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 9
---
# &#196;ndern von Statistiken
  Sie können mit [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] vorhandene Statistiken in [!INCLUDE[tsql](../../includes/tsql-md.md)]ändern.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **So ändern Sie Statistiken mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert Folgendes:  
  
-   Der Benutzer verfügt über die ALTER-Berechtigung für die Tabelle oder Sicht.  
  
-   Der Benutzer kann Besitzer der Tabelle oder indizierten Sicht oder ein Mitglied einer der folgenden Rollen sein: feste Serverrolle **sysadmin**, feste Datenbankrolle **db_owner** oder feste Datenbankrolle **db_ddladmin**.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So ändern Sie Statistiken  
  
1.  Klicken Sie im **Objekt-Explorer**auf das Pluszeichen, um die Datenbank zu erweitern, in der Sie eine Statistik ändern möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Tabellen** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um die Tabelle zu erweitern, in der Sie die Statistik ändern möchten.  
  
4.  Klicken Sie auf das Pluszeichen, um den Ordner **Statistik** zu erweitern.  
  
5.  Klicken Sie mit der rechten Maustaste auf das Statistikobjekt, das Sie ändern möchten, und wählen Sie **Eigenschaften**.  
  
6.  Klicken Sie im Dialogfeld **Statistikeigenschaften –** *statistics_name* auf der Seite **Allgemein** auf **Hinzufügen**, **Entfernen**, **Nach oben** oder **Nach unten** bzw. eine beliebige Kombination, um die Eigenschaften der Statistiken zu ändern. Beachten Sie, dass sich die Position einer Spalte im Raster **Statistikspalten** erheblich auf die Nützlichkeit der Statistiken auswirken kann.  
  
7.  Klicken Sie auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So ändern Sie Statistiken**  
  
 Diese Aufgabe kann nicht mit Transact-SQL-Anweisungen ausgeführt werden. Um Statistiken mithilfe von Transact-SQL zu ändern, müssen Sie zuerst die vorhandene Statistik löschen und sie dann mit neuen Attributen neu erstellen.  
  
 Weitere Informationen finden Sie unter [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md) und [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md).  
  
  