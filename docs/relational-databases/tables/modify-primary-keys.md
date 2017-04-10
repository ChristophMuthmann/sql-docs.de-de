---
title: "&#196;ndern von Prim&#228;rschl&#252;sseln | Microsoft Docs"
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
  - "Ändern von Primärschlüsseln"
  - "Primärschlüssel [SQL Server], ändern"
ms.assetid: 8e2a15ba-1cd1-4408-b860-16c3ee37d635
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# &#196;ndern von Prim&#228;rschl&#252;sseln
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Sie können mit [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] einen Primärschlüssel in [!INCLUDE[tsql](../../includes/tsql-md.md)]ändern. Sie können den Primärschlüssel einer Tabelle ändern, indem Sie die Spaltenreihenfolge, den Indexnamen, die CLUSTERED-Option oder den Füllfaktor bearbeiten.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **So ändern Sie einen Primärschlüssel mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Tabelle.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So ändern Sie einen Primärschlüssel  
  
1.  Öffnen Sie den Tabellen-Designer für die Tabelle, deren Primärschlüssel Sie ändern möchten. Klicken Sie mit der rechten Maustaste auf den Tabellen-Designer, und wählen Sie im Kontextmenü den Befehl **Indizes/Schlüssel** aus.  
  
2.  Wählen Sie im Dialogfeld **Indizes/Schlüssel** aus der Liste **Ausgewählter Primärschlüssel/eindeutiger Schlüssel oder Index** den Primärschlüsselindex aus.  
  
3.  Führen Sie eine Aktion aus der folgenden Tabelle aus:  
  
    |Aktion|Schritte|  
    |--------|------------------------|  
    |Umbenennen des Primärschlüssels|Geben Sie im Feld **Name** einen neuen Namen ein. Vergewissern Sie sich, dass der neue Name in der Liste **Ausgewählter Primärschlüssel/eindeutiger Schlüssel oder Index** nicht bereits vorhanden ist.|  
    |Festlegen der CLUSTERED-Option|Um einen gruppierten Index für den Primärschlüssel zu erstellen, wählen Sie **Als CLUSTERED erstellen** aus, und wählen Sie die Option im Dropdown-Listenfeld aus. In jeder Tabelle darf nur ein gruppierter Index vorhanden sein. Wenn diese Option für einen Index nicht verfügbar ist, müssen Sie zunächst diese Einstellung für den vorhandenen gruppierten Index deaktivieren.<br /><br /> Wenn diese Option nicht aktiviert wird, wird ein eindeutiger nicht gruppierter Index erstellt.|  
    |Definieren eines Füllfaktors|Erweitern Sie die Kategorie **Füllspezifikation** , und geben Sie im Feld **Füllfaktor** einen ganzzahligen Wert zwischen 0 und 100 ein. Weitere Informationen über Füllfaktoren und deren Verwendung finden Sie unter [Angeben des Füllfaktors für einen Index](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).|  
    |Ändern der Spaltenreihenfolge|Wählen Sie **Spalten** aus, und klicken Sie dann auf das Auslassungszeichen **(…)** rechts neben der Eigenschaft. Entfernen Sie im Dialogfeld  **Indexspalten** die Spalten aus dem Primärschlüssel. Fügen Sie die Spalten in der gewünschten Reihenfolge wieder ein. Zum Entfernen einer Spalte aus dem Schlüssel können Sie den Spaltennamen einfach aus der Namensliste der **Spalten** entfernen.|  
  
4.  Klicken Sie im Menü **Datei** auf **Speichern***table name*.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So ändern Sie einen Primärschlüssel**  
  
 Um eine PRIMARY KEY-Einschränkung mit Transact-SQLzu ändern, müssen Sie zuerst die vorhandene PRIMARY KEY-Einschränkung löschen und sie dann mit der neuen Definition neu erstellen. Weitere Informationen finden Sie unter [Delete Primary Keys](../../relational-databases/tables/delete-primary-keys.md) und [Create Primary Keys](../../relational-databases/tables/create-primary-keys.md).  
  
###  <a name="TsqlExample"></a>  