---
title: "Informationsskript f&#252;r Verleger und Verteiler | Microsoft Docs"
ms.custom: ""
ms.date: "03/09/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Verleger [SQL Server-Replikation], Informationsskripts"
  - "Verteiler [SQL Server-Replikation], Informationsskripts"
ms.assetid: 8622db47-c223-48fa-87ff-0b4362cd069a
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# Informationsskript f&#252;r Verleger und Verteiler
  Dieses Skript verwendet Tabellen und gespeicherte Prozeduren für die Replikation zur Beantwortung allgemeiner Fragen in Bezug auf Objekte auf dem Verteiler und dem Verleger. Das Skript kann, so wie es ist, verwendet werden, oder es kann als Basis für benutzerdefinierte Skripts dienen. Das Skript erfordert möglicherweise zwei Änderungen, damit es in Ihrer Umgebung ausgeführt werden kann:  
  
-   Ändern Sie die Zeile `use AdventureWorks2012` so, dass sie den Namen Ihrer Veröffentlichungsdatenbank enthält.  
  
-   Entfernen Sie die Kommentare (`--`) über die Befehlszeile `exec sp_helparticle @publication='<PublicationName>'` und Ersetzen Sie \< PublicationName> mit dem Namen einer Veröffentlichung.  
  
```  
--********** Execute at the Distributor in the master database **********--  
  
USE master;  
go  
  
--Is the current server a Distributor?  
--Is the distribution database installed?  
--Are there other Publishers using this Distributor?  
EXEC sp_get_distributor  
  
--Is the current server a Distributor?  
SELECT is_distributor FROM sys.servers WHERE name='repl_distributor' AND data_source=@@servername;  
  
--Which databases on the Distributor are distribution databases?  
SELECT name FROM sys.databases WHERE is_distributor = 1  
  
--What are the Distributor and distribution database properties?  
EXEC sp_helpdistributor;  
EXEC sp_helpdistributiondb;  
EXEC sp_helpdistpublisher;  
  
--********** Execute at the Publisher in the master database **********--  
  
--Which databases are published for replication and what type of replication?  
EXEC sp_helpreplicationdboption;  
  
--Which databases are published using snapshot replication or transactional replication?  
SELECT name as tran_published_db FROM sys.databases WHERE is_published = 1;  
--Which databases are published using merge replication?  
SELECT name as merge_published_db FROM sys.databases WHERE is_merge_published = 1;  
  
--What are the properties for Subscribers that subscribe to publications at this Publisher?  
EXEC sp_helpsubscriberinfo;  
  
--********** Execute at the Publisher in the publication database **********--  
  
USE AdventureWorks2012;  
go  
  
--What are the snapshot and transactional publications in this database?   
EXEC sp_helppublication;  
--What are the articles in snapshot and transactional publications in this database?  
--REMOVE COMMENTS FROM NEXT LINE AND REPLACE <PublicationName> with the name of a publication  
--EXEC sp_helparticle @publication='<PublicationName>';  
  
--What are the merge publications in this database?   
EXEC sp_helpmergepublication;  
--What are the articles in merge publications in this database?  
EXEC sp_helpmergearticle; -- to return information on articles for a single publication, specify @publication='<PublicationName>'  
  
--Which objects in the database are published?  
SELECT name AS published_object, schema_id, is_published AS is_tran_published, is_merge_published, is_schema_published  
FROM sys.tables WHERE is_published = 1 or is_merge_published = 1 or is_schema_published = 1  
UNION  
SELECT name AS published_object, schema_id, 0, 0, is_schema_published  
FROM sys.procedures WHERE is_schema_published = 1  
UNION  
SELECT name AS published_object, schema_id, 0, 0, is_schema_published  
FROM sys.views WHERE is_schema_published = 1;  
  
--Which columns are published in snapshot or transactional publications in this database?  
SELECT object_name(object_id) AS tran_published_table, name AS published_column FROM sys.columns WHERE is_replicated = 1;  
  
--Which columns are published in merge publications in this database?  
SELECT object_name(object_id) AS merge_published_table, name AS published_column FROM sys.columns WHERE is_merge_published = 1;  
```  
  
## Siehe auch  
 [Häufig gestellte Fragen für Replikationsadministratoren](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)   
 [Sp_get_distributor & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-get-distributor-transact-sql.md)   
 [Sp_helparticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [Sp_helpdistributiondb & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [Sp_helpdistpublisher & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Sp_helpdistributor & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [Sp_helpmergearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [Sp_helpmergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [Sp_helppublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [Sp_helpreplicationdboption & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpreplicationdboption-transact-sql.md)   
 [Sp_helpsubscriberinfo & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [Sys.Columns & #40; Transact-SQL & #41;](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Sys.Databases & #40; Transact-SQL & #41;](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Sys.Procedures & #40; Transact-SQL & #41;](../../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md)   
 [Sys.Servers & #40; Transact-SQL & #41;](../../../relational-databases/system-catalog-views/sys-servers-transact-sql.md)   
 [Sys.Tables & #40; Transact-SQL & #41;](../../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [Sys.Views & #40; Transact-SQL & #41;](../../../relational-databases/system-catalog-views/sys-views-transact-sql.md)  
  
  