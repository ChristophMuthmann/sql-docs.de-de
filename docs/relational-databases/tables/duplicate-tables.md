---
title: Duplizieren von Tabellen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- copying tables
- tables [SQL Server], duplicating
- duplicating tables
- table copying [SQL Server]
ms.assetid: c6b07423-d1e5-4e5e-8681-5088921f5df3
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2e02199d165d8d68556bd5934003f98e417e3eec
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="duplicate-tables"></a>Duplizieren von Tabellen
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Sie können mit [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eine vorhandene Tabelle in [!INCLUDE[tsql](../../includes/tsql-md.md)] duplizieren, indem Sie eine neue Tabelle erstellen und dann Spalteninformationen aus einer vorhandenen Tabelle kopieren.  
  
> [!IMPORTANT]  
>  Mit diesem Vorgang wird nur die Struktur einer Tabelle dupliziert, nicht die einzelnen Tabellenzeilen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Security](#Security)  
  
-   **So duplizieren Sie eine Tabelle mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die CREATE TABLE-Berechtigung in der Zieldatenbank.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-duplicate-a-table"></a>So duplizieren Sie eine Tabelle  
  
1.  Stellen Sie sicher, dass eine Verbindung mit der Datenbank vorhanden ist, in der Sie die Tabelle erstellen möchten, und dass die Datenbank im Objekt-Explorer ausgewählt ist.  
  
2.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf **Tabellen** , und klicken Sie dann auf **Neue Tabelle**.  
  
3.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf die Tabelle, die Sie kopieren möchten, und klicken Sie dann auf **Entwerfen**.  
  
4.  Wählen Sie in der vorhandenen Tabelle die Spalten aus, und klicken Sie im Menü **Bearbeiten** auf **Kopieren**.  
  
5.  Wechseln Sie zurück in die neue Tabelle, und markieren Sie die erste Zeile.  
  
6.  Klicken Sie im Menü **Bearbeiten** auf **Einfügen**.  
  
7.  Klicken Sie im Menü **Datei** auf **Speichern** > *Tabellenname*.  
  
8.  Geben Sie im Dialogfeld **Namen auswählen** einen Namen für die neue Tabelle ein, und klicken Sie auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-duplicate-a-table-in-query-editor"></a>So duplizieren Sie eine Tabelle im Abfrage-Editor  
  
1.  Stellen Sie sicher, dass eine Verbindung mit der Datenbank vorhanden ist, in der Sie die Tabelle erstellen möchten, und dass die Datenbank im Objekt-Explorer ausgewählt ist.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Tabelle, die Sie duplizieren möchten, zeigen Sie auf **Skript für Tabelle als**, zeigen Sie dann auf **CREATE in**, und wählen Sie **Neues Abfrage-Editor-Fenster**aus.  
  
3.  Ändern Sie den Namen der Tabelle.  
  
4.  Entfernen Sie alle Spalten, die nicht in der neuen Tabelle benötigt werden.  
  
5.  Klicken Sie auf **Ausführen**.  
  
  
