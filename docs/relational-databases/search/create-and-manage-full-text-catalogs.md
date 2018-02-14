---
title: Erstellen und Verwalten von Volltextkatalogen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text search [SQL Server], using SQL Server Management Studio
ms.assetid: 824b7131-44a6-4815-89e6-62b7bab060e3
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b3e98a00fd7f165fbd5c83b7149a8e63505116e3
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="create-and-manage-full-text-catalogs"></a>Erstellen und Verwalten von Volltextkatalogen
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Ein Volltextkatalog ist ein logischer Container für eine Gruppe von Volltextindizes. Sie müssen einen Volltextkatalog erstellen, bevor Sie einen Volltextindex erstellen können.

Ein Volltextkatalog ist ein virtuelles Objekt und gehört keiner Dateigruppe an.
  
##  <a name="creating"></a> Erstellen eines Volltextkatalogs  

### <a name="create-a-full-text-catalog-with-transact-sql"></a>Erstellen eines Volltextkatalogs mit Transact-SQL
Verwenden Sie [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md). Zum Beispiel:

```sql 
USE AdventureWorks;  
GO  
CREATE FULLTEXT CATALOG ftCatalog AS DEFAULT;  
GO  
``` 

### <a name="create-a-full-text-catalog-with-management-studio"></a>Erstellen eines Volltextkatalogs mit Management Studio
1.  Erweitern Sie im Objekt-Explorer den Server, erweitern Sie **Datenbanken**, und erweitern Sie die Datenbank, in der der Volltextkatalog erstellt werden soll.  
  
2.  Erweitern Sie **Speicher**, und klicken Sie dann mit der rechten Maustaste auf **Volltextkataloge**.  
  
3.  Wählen Sie **Neuer Volltextkatalog**aus.  
  
4.  Geben Sie im Dialogfeld **Neuer Volltextkatalog** die Informationen für den erneut zu erstellenden Volltextkatalog an. Weitere Informationen finden Sie unter [Neuer Volltextkatalog &#40;Seite „Allgemein“&#41;](http://msdn.microsoft.com/library/5ed6f7cd-d9af-4439-9f33-fc935b883d91).  
  
    > [!NOTE]  
    >  Volltextkatalog-IDs beginnen bei 00005 und werden mit jedem neu erstellten Katalog um eins erhöht.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="props"></a> Abrufen der Eigenschaften eines Volltextkatalogs  
Verwenden Sie die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktion **FULLTEXTCATALOGPROPERTY**, um den Wert verschiedener Eigenschaften des Volltextkatalogs abzurufen. Weitere Informationen finden Sie unter [FULLTEXTCATALOGPROPERTY](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md).

Führen Sie z.B. die folgende Abfrage zum Abrufen der Anzahl der Indizes im Volltextkatalog `Catalog1` aus.

```sql 
USE <database>;  
GO  
SELECT fulltextcatalogproperty('Catalog1', 'ItemCount');  
GO  
```  
  
In der folgenden Tabelle sind die Eigenschaften aufgeführt, die sich auf Volltextkataloge beziehen. Diese Informationen sind für die Verwaltung und Problembehandlung der Volltextsuche möglicherweise hilfreich. 
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**AccentSensitivity**|Einstellung für die Unterscheidung nach Akzent.|
|**ImportStatus**|Gibt an, ob der Volltextkatalog importiert wird.|  
|**IndexSize**|Größe des Volltextkatalogs in Megabytes (MB).| 
|**ItemCount**|Aktuelle Anzahl der volltextindizierten Objekte im Volltextkatalog.|  
|**MergeStatus**|Gibt an, ob eine Masterzusammenführung ausgeführt wird.| 
|**PopulateCompletionAge**|Anzahl von Sekunden, die zwischen dem 01.01.1990, 00:00:00 Uhr, und der Beendigung des letzten Auffüllens des Volltextindex verstrichen sind.| 
|**PopulateStatus**|Gibt den Auffüllungsstatus an.<br /><br /> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|**UniqueKeyCount**|Anzahl der eindeutigen Schlüssel im Volltextkatalog.| 

##  <a name="rebuildone"></a> Erneutes Erstellen eines Volltextkatalogs  

Führen Sie die Transact-SQL-Anweisung [ALTER FULLTEXT CATALOG... REBUILD](
../../t-sql/statements/alter-fulltext-catalog-transact-sql.md) aus, oder führen Sie folgende Schritte in SQL Server Management Studio (SSMS) aus.

1.  Erweitern Sie in SSMS im Objekt-Explorer den Server, erweitern Sie **Datenbanken**, und erweitern Sie die Datenbank, die den erneut zu erstellenden Volltextkatalog enthält.  
  
2.  Erweitern Sie **Speicher**und dann **Volltextkataloge**.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Namen des erneut zu erstellenden Volltextkatalogs, und wählen Sie **Neu erstellen**aus.  
  
4.  Klicken Sie auf die Frage **Möchten Sie den Volltextkatalog löschen und neu erstellen?**auf **OK**.  
  
5.  Klicken Sie im Dialogfeld **Volltextkatalog neu erstellen** auf **Schließen**.  
   
##  <a name="rebuildall"></a> Erneutes Erstellen aller Volltextkataloge für eine Datenbank  

1.  Erweitern Sie in SSMS im Objekt-Explorer den Server, erweitern Sie **Datenbanken**, und erweitern Sie die Datenbank, die die erneut zu erstellenden Volltextkataloge enthält.  
  
2.  Erweitern Sie **Speicher**, und klicken Sie dann mit der rechten Maustaste auf **Volltextkataloge**.  
  
3.  Wählen Sie **Alle neu erstellen**aus.  
  
4.  Klicken Sie bei der Frage **Möchten Sie alle Volltextkataloge löschen und neu erstellen?**auf die Option **OK**.  
  
5.  Klicken Sie im Dialogfeld **Alle Volltextkataloge neu erstellen** auf **Schließen**.  
  
  
  
##  <a name="removing"></a> Entfernen eines Volltextkatalogs aus einer Datenbank  

Führen Sie die Transact-SQL-Anweisung [DROP FULLTEXT CATALOG](
../../t-sql/statements/drop-fulltext-catalog-transact-sql.md) aus, oder führen Sie die folgenden Schritte in SQL Server Management Studio (SSMS) aus.

1.  Erweitern Sie in SSMS im Objekt-Explorer den Server, erweitern Sie **Datenbanken**, und erweitern Sie die Datenbank, die den zu entfernenden Volltextkatalog enthält.  
  
2.  Erweitern Sie **Speicher**und dann **Volltextkataloge**.  
  
3.  Klicken Sie mit der rechten Maustaste auf den zu entfernenden Katalog, und wählen Sie dann **Löschen**aus.  
  
4.  Klicken Sie im Dialogfeld **Objekte löschen** auf **OK**.  

## <a name="next-step"></a>Nächster Schritt
[Erstellen und Verwalten von Volltextindizes](../../relational-databases/search/create-and-manage-full-text-indexes.md)
