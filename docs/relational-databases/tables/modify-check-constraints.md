---
title: "&#196;ndern von CHECK-Einschr&#228;nkungen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Check-Einschränkungen, ändern"
  - "Ändern von Einschränkungen"
  - "Einschränkungen [SQL Server], CHECK"
  - "Einschränkungen [SQL Server], ändern"
ms.assetid: f22daef8-e350-40ef-8ff0-b5f87d1d9e56
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# &#196;ndern von CHECK-Einschr&#228;nkungen
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Sie können eine CHECK-Einschränkung mit [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] in [!INCLUDE[tsql](../../includes/tsql-md.md)] ändern, wenn Sie entweder den Einschränkungsausdruck oder die Optionen ändern möchten, mit denen die Einschränkung unter bestimmten Bedingungen aktiviert bzw. deaktiviert werden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **So ändern Sie eine CHECK-Einschränkung mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Tabelle.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So ändern Sie eine CHECK-Einschränkung  
  
1.  Klicken Sie im **Objekt-Explorer** mit der rechten Maustaste auf die Tabelle mit der CHECK-Einschränkung, und wählen Sie dann **Entwerfen** aus.  
  
2.  Klicken Sie im Menü **Tabellen-Designer** auf **CHECK-Einschränkungen...**.  
  
3.  Wählen Sie im Dialogfeld **CHECK-Einschränkungen** unter **Ausgewählte CHECK-Einschränkung**die Einschränkung aus, die Sie bearbeiten möchten.  
  
4.  Führen Sie eine Aktion aus der folgenden Tabelle aus:  
  
    |Aktion|Schritte|  
    |--------|------------------------|  
    |Ändern des Einschränkungsausdrucks|Geben Sie im Feld **Ausdruck** den neuen Ausdruck ein.|  
    |Umbenennen der Einschränkung|Geben Sie im Feld **Name** einen neuen Namen ein.|  
    |Anwenden der Einschränkung auf die vorhandenen Daten|Aktivieren Sie die Option **Vorhandene Daten bei Erstellung oder Aktivierung überprüfen** .|  
    |Deaktivieren der Einschränkung, wenn der Tabelle neue Daten hinzugefügt werden oder wenn die vorhandenen Daten in der Tabelle aktualisiert werden|Deaktivieren Sie die Option **Einschränkung für INSERT und UPDATE erzwingen** .|  
    |Deaktivieren Sie die Einschränkung, wenn ein Replikations-Agent Daten in die Tabelle einfügt oder darin aktualisiert.|Deaktivieren Sie die Option **Für Replikation erzwingen** .|  
  
    > [!NOTE]  
    >  Die Funktionsweise der CHECK-Einschränkung kann je nach Datenbank unterschiedlich ausfallen.  
  
5.  Klicken Sie auf **Schließen**.  
  
6.  Klicken Sie im Menü **Datei** auf **Speichern***table name*.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So ändern Sie eine CHECK-Einschränkung**  
  
 Um eine `CHECK`-Einschränkung mit [!INCLUDE[tsql](../../includes/tsql-md.md)] zu ändern, müssen Sie zuerst die vorhandene `CHECK`-Einschränkung löschen und sie dann mit der neuen Definition neu erstellen. Weitere Informationen finden Sie unter [Löschen von CHECK-Einschränkungen](../../relational-databases/tables/delete-check-constraints.md) und [Erstellen von CHECK-Einschränkungen](../../relational-databases/tables/create-check-constraints.md).  
  
###  <a name="TsqlExample"></a>  