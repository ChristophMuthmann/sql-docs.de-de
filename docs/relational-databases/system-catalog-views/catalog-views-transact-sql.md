---
title: Katalogsichten (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: sql13.SysViewExpandPortal.f1
dev_langs: TSQL
helpviewer_keywords:
- catalog metadata [SQL Server]
- system views [SQL Server], catalog
- metadata [SQL Server], views
- catalogs [SQL Server], metadata
- catalog views [SQL Server]
- Database Engine [SQL Server], metadata
- catalog views [SQL Server], about catalog views
ms.assetid: 13bccc2f-ed3c-4b58-abd0-ca8bf34a66b8
caps.latest.revision: "45"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 40d26c8b87daec4f7cea3b1ac5e6a3390d50b193
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="system-catalog-views-transact-sql"></a>System-Katalogsichten (Transact-SQL)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Katalogsichten geben Informationen zurück, die von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] verwendet werden. Sie sollten Katalogsichten verwenden, da sie die allgemeinste Schnittstelle zu den Katalogmetadaten darstellen und die effizienteste Methode zum Abrufen, Transformieren und Präsentieren dieser Informationen in benutzerdefinierter Form bereitstellen. Alle für Benutzer verfügbaren Katalogmetadaten werden über Katalogsichten verfügbar gemacht.  
  
> [!NOTE]  
>  Katalogsichten enthalten keine Informationen zu Replikation, Sicherung, Datenbank-Wartungsplan oder Katalogdaten zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent.  
  
 Einige Katalogsichten erben Zeilen von anderen Katalogsichten. Z. B. die [sys.tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) -Katalogsicht erbt von der [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) -Katalogsicht angezeigt. Die sys.objects-Katalogsicht wird als Basissicht bezeichnet, und die sys.tables-Sicht wird abgeleitete Sicht genannt. Die sys.tables-Katalogsicht gibt die Spalten zurück, die für Tabellen spezifisch sind, sowie alle Spalten, die die sys.objects-Katalogsicht zurückgibt. Die sys.objects-Katalogsicht gibt Zeilen für Objekte zurück, bei denen es sich nicht um Tabellen handelt, z. B. gespeicherte Prozeduren und Sichten. Nachdem eine Tabelle erstellt wurde, werden die Metadaten für die Tabelle in beiden Sichten zurückgegeben. Die beiden Katalogsichten geben zwar unterschiedliche Ebenen von Informationen zur Tabelle zurück, es gibt jedoch nur einen Metadateneintrag für diese Tabelle mit einem Namen und einem object_id-Wert. Dies kann wie folgt zusammengefasst werden:  
  
-   Die Basissicht enthält eine Teilmenge der Spalten und eine Obermenge der Zeilen.  
  
-   Die abgeleitete Sicht enthält eine Obermenge der Spalten und eine Teilmenge der Zeilen.  
  
> [!IMPORTANT]  
>  In zukünftigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird die Definition der Systemkatalogsichten von [!INCLUDE[msCoName](../../includes/msconame-md.md)] möglicherweise erweitert, indem am Ende der Spaltenliste Spalten hinzugefügt werden. Es wird empfohlen, für die Verwendung der Syntax SELECT \* FROM *sys.catalog_view_name* in der Produktion Code, da die Anzahl der zurückgegebenen Spalten möglicherweise ändern und Ihre Anwendung dadurch beschädigt.  
  
 Die Katalogsichten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wurden in den folgenden Kategorien organisiert:  
  
|||  
|-|-|  
|[AlwaysOn Availability Gruppen-Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)|[Nachrichten &#40; für Fehler &#41; Katalogsichten &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/8ac78c53-7b97-41b3-9cbd-5f97c179f1f2)|  
|[Azure SQL-Datenbank-Katalogsichten](../../relational-databases/system-catalog-views/azure-sql-database-catalog-views.md)|[Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)|  
|[Ändern Sie die Überwachung-Katalogsichten &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/6e8fd949-5560-4b34-879f-4e25aa24b183)|[Katalogsichten für Partitionsfunktionen &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)|  
|[CLR-Assemblykatalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)|[Sichten der richtlinienbasierten Verwaltung &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)|  
|[Sichten des Datensammlers &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)|[Katalogsichten der Ressourcenkontrolle &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)|  
|[Datenspeicher &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)|[Katalogsichten des Abfragespeichers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)|  
|[Datenbank-Mail-Sichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/database-mail-views-transact-sql.md)|[Skalare Typen Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)|  
|[Database Mirroring Witness-Katalogsichten &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/8a0c9053-5d76-4aa9-a18d-0ea1c514034d)|[Schema-Katalogsichten &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/c516fb1c-b6ed-48ae-99c7-a78bc4336c8e)|  
|[Datenbanken und Dateikatalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)|[Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)|  
|[Endpunkte-Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)|[Service Broker-Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/service-broker-catalog-views-transact-sql.md)|  
|[Katalogsichten für erweiterte Ereignisse &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)|[Serverweite Konfiguration-Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)|  
|[Katalogsichten für erweiterte Eigenschaften &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/f39fd324-efd4-4468-884c-bf77ed1a026f)|[Katalogsichten für räumliche Daten](../../relational-databases/system-catalog-views/spatial-data-catalog-views.md)|  
|[Externe Vorgänge-Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/external-operations-catalog-views-transact-sql.md)|[SQL Datawarehouse und Parallel Datawarehouse-Katalogsichten](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)|  
|[FileStream und FileTable-Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)|[Stretch-Datenbank-Katalogsichten &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/bee78e39-e07d-4b0f-b8ad-09a01a5eb795)|  
|[Volltextsuche und semantische Suche-Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/full-text-search-and-semantic-search-catalog-views-transact-sql.md)|[XML-Schemas &#40; XML-Typsystem &#41; Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)|  
|[Verbindungsserver-Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)||  
  
## <a name="see-also"></a>Siehe auch  
 [Informationsschemasichten &#40; Transact-SQL &#41;](../../relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [Systemtabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [Häufig gestellte Fragen zu Abfragen des SQL Server-Systemkatalogs](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
