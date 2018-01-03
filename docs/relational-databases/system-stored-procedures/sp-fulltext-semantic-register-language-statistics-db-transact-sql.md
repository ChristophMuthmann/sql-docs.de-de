---
title: Sp_fulltext_semantic_register_language_statistics_db (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_fulltext_semantic_register_language_statistics_db
- sp_fulltext_semantic_register_language_statistics_db_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_fulltext_semantic_register_language_statistics_db
ms.assetid: bef1b104-5a44-4327-9ae4-45eae3000f7e
caps.latest.revision: "12"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7036aeab4ff8573e07d27aae1b1b486bd5b34fe0
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="spfulltextsemanticregisterlanguagestatisticsdb-transact-sql"></a>sp_fulltext_semantic_register_language_statistics_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registriert eine im Voraus aufgefüllte semantische Sprachstatistikdatenbank in der aktuellen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Sie können eine semantische Extraktion nur initiieren, nachdem Sie diese Sprachstatistikdatenbank angefügt und sie mit dieser gespeicherten Prozedur registriert haben. Sie müssen nur zum Ausführen dieser Aufgabe einmal für jede Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db  
    [ @dbname = ] ‘database_name’;  
GO  
```  
  
##  <a name="Arguments"></a> Argumente  
 [ @dbname =] '*Database_name*"  
 Der Name der Semantic Language Statistics-Datenbank für die aktuelle Instanz der zu registrierende [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die Datenbank muss bereits angefügt sein. *database_name* ist vom Datentyp **sysname**und kann nicht NULL sein.  
  
## <a name="return-code-value"></a>Rückgabecodewert  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-set"></a>Resultset  
 Keine.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Die semantische Sprachstatistikdatenbank enthält sprachbezogene Statistiken, die für die semantische Verarbeitung von Textinhalt erforderlich sind.  
  
 **sp_fulltext_semantic_register_language_statistics_db** führt die folgenden Schritte aus:  
  
1.  Überprüft, ob die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist eine Version, die semantische Verarbeitung unterstützt.  
  
2.  Überprüft, ob die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] noch keine Semantic Language Statistics-Datenbank definiert.  
  
3.  Überprüft, ob die Datenbank eine gültige semantische Sprachstatistikdatenbank ist.  
  
4.  Legt Berechtigungen für die semantische Sprachstatistikdatenbank fest, um den Zugriff auf die Datenbank durch Benutzer einzuschränken.  
  
5.  Fügt die Metadaten, die den Namen der semantischen sprachstatistikdatenbank für die Instanz von definiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
6.  Fügt die Metadaten ein, die die Zuordnungen zwischen der installierten semantischen Sprachstatistikdatenbank und den internen Sprachenmodelltabellen definieren.  
  
7.  Führt eine Überprüfung durch, um sicherzustellen, dass die Datenbank zur Verwendung bereitsteht.  
  
 Weitere Informationen finden Sie unter [Installieren und Konfigurieren der semantischen Suche](../../relational-databases/search/install-and-configure-semantic-search.md).  
  
## <a name="metadata"></a>Metadaten  
 Informationen über die Semantic Language Statistics-Datenbank auf einer Instanz von installiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Fragen Sie die Katalogsicht [Sys. fulltext_semantic_language_statistics_database &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md).  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert CONTROL SERVER-Berechtigungen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird gezeigt, wie die semantische Sprachstatistikdatenbank durch den Aufruf von **sp_fulltext_semantic_register_language_statistics_db**registriert wird.  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = 'semanticsDb';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Installieren und Konfigurieren der semantischen Suche](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
