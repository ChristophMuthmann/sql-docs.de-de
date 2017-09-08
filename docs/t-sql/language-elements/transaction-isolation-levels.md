---
title: Isolationsstufen von Transaktionen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], hints
- isolation levels [SQL Server], metadata access
- hints [SQL Server], locking
ms.assetid: 02bb71fa-1e92-4782-a9cf-6e256cc1f3ea
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0acd70fad20d0ad1c2727f93da52b2e938ee21fd
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="transaction-isolation-levels"></a>Transaktionsisolationsstufen
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden Sperrhinweise in Abfragen, die über Katalogsichten, Kompatibilitätssichten, Informationsschemasichten oder Metadaten ausgebende integrierte Funktionen auf Metadaten zugreifen, nicht mit Sicherheit berücksichtigt.  
  
 Intern berücksichtigt [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] beim Zugriff auf Metadaten nur die Isolationsstufe READ COMMITTED. Wenn eine Transaktion beispielsweise die Isolationsstufe SERIALIZABLE besitzt und innerhalb der Transaktion versucht wird, über Katalogsichten oder Metadaten ausgebende integrierte Funktionen auf Metadaten zuzugreifen, werden die entsprechenden Abfragen ausgeführt, bis sie als READ COMMITTED abgeschlossen sind. Bei der Momentaufnahmeisolation kann der Zugriff auf Metadaten jedoch aufgrund von gleichzeitigen DDL-Vorgängen einen Fehler erzeugen. Der Grund dafür ist, dass Metadaten nicht versionsspezifisch sind. Daher besteht das Risiko, dass bei der Momentaufnahmeisolation der Zugriff über folgende Sichten und Funktionen zu einem Fehler führt:  
  
-   Katalogsichten  
  
-   Kompatibilitätssichten  
  
-   Informationsschemasichten  
  
-   Metadaten ausgebende integrierte Funktionen  
  
-   **Sp_help** -Gruppe gespeicherter Prozeduren  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client-Katalogprozeduren  
  
-   Dynamische Verwaltungssichten (DMVs, Dynamic Management Views) und -funktionen  
  
 Weitere Informationen zu Isolationsstufen finden Sie unter [SET TRANSACTION ISOLATION LEVEL &#40; Transact-SQL &#41; ](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
 Die folgende Tabelle fasst den Zugriff auf Metadaten bei verschiedenen Isolationsstufen zusammen.  
  
|Isolationsstufe|Unterstützt|Berücksichtigt|  
|---------------------|---------------|-------------|  
|READ UNCOMMITTED|Nein|Nicht mit Sicherheit berücksichtigt|  
|READ COMMITTED|ja|ja|  
|REPEATABLE READ|Nein|Nein|  
|MOMENTAUFNAHMEN ISOLATION|Nein|Nein|  
|SERIALIZABLE|Nein|Nein|  
  
  
