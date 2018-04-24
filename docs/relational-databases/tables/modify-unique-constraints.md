---
title: Ändern von Unique-Einschränkungen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- modifying constraints
- UNIQUE constraints [SQL Server], modifying
- constraints [SQL Server], modifying
- constraints [SQL Server], unique
ms.assetid: fddbdc9e-958b-4614-8e88-6ca205d64a4e
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 39a75f519aa5e31aecd6a976110665fa79ec212f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="modify-unique-constraints"></a>Ändern von UNIQUE-Einschränkungen
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Sie können mit [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eine UNIQUE-Einschränkung in [!INCLUDE[tsql](../../includes/tsql-md.md)]ändern.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Security](#Security)  
  
-   **So ändern Sie eine UNIQUE-Einschränkung mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Tabelle.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-modify-a-unique-constraint"></a>So ändern Sie eine UNIQUE-Einschränkung  
  
1.  Klicken Sie im **Objekt-Explorer**mit der rechten Maustaste auf die Tabelle mit der UNIQUE-Einschränkung, und wählen Sie dann **Entwerfen**aus.  
  
2.  Klicken Sie im Menü **Tabellen-Designer** auf **Indizes/Schlüssel**.  
  
3.  Wählen Sie im Dialogfeld **Indizes/Schlüssel** unter **Ausgewählter Primärschlüssel/eindeutiger Schlüssel oder Index**die Einschränkung aus, die Sie bearbeiten möchten.  
  
4.  Führen Sie eine Aktion aus der folgenden Tabelle aus:  
  
    |Aktion|Schritte|  
    |--------|------------------------|  
    |Ändern der Spalten, denen die Einschränkung zugewiesen ist|1.) Klicken Sie im Raster unter **Allgemein**auf **Spalten** und anschließend auf die Auslassungszeichen **(…)** rechts neben der Eigenschaft.<br /><br /> 2.) Geben Sie im Dialogfeld **Indexspalten** die neue Spalte oder die Sortierreihenfolge oder beides für den Index an.|  
    |Umbenennen der Einschränkung|Geben Sie im Raster unter **Identität**im Feld **Name** einen neuen Namen ein. Vergewissern Sie sich, dass der neue Name in der Liste **Ausgewählter Primärschlüssel/eindeutiger Schlüssel oder Index** nicht bereits vorhanden ist.|  
    |Festlegen der CLUSTERED-Option|Wählen Sie im Raster unter **Tabellen-Designer**die Option **Als CLUSTERED erstellen** und in der Dropdownliste „Ja“ aus, um einen gruppierten Index zu erstellen, und „Nein“, um einen nicht gruppierten Index zu erstellen. In jeder Tabelle darf nur ein gruppierter Index vorhanden sein. Wenn in der Tabelle bereits ein gruppierter Index vorhanden ist, müssen Sie diese Einstellung zunächst für den ursprünglichen Index deaktivieren.|  
    |Definieren eines Füllfaktors|Erweitern Sie im Raster unter **Tabellen-Designer**die Kategorie **Füllspezifikation** , und geben Sie im Feld **Füllfaktor** eine ganze Zahl zwischen 0 und 100 ein.|  
  
5.  Klicken Sie im Menü **Datei** auf **Speichern** > *Tabellenname*.  
  
##  <a name="TsqlProcedure"></a> **So ändern Sie eine UNIQUE-Einschränkung**  
  
 Um eine UNIQUE-Einschränkung mit Transact-SQL ändern zu können, müssen Sie zuerst die vorhandene UNIQUE-Einschränkung löschen und sie dann mit der neuen Definition neu erstellen. Weitere Informationen finden Sie unter [Delete Unique Constraints](../../relational-databases/tables/delete-unique-constraints.md) und [Create Unique Constraints](../../relational-databases/tables/create-unique-constraints.md).  
  
###  <a name="TsqlExample"></a>  
