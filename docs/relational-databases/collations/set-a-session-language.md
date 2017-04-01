---
title: "Festlegen einer Sitzungssprache | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Fehler [SQL Server], internationale Überlegungen"
  - "Globalisierung [SQL Server], Sitzungen"
  - "Uhrzeit [SQL Server]"
  - "Sitzungen [SQL Server], Sprachen"
  - "Internationale Überlegungen [SQL Server], Sitzungen"
  - "Datumsangaben [SQL Server], Sitzungssprachen"
  - "Globale Überlegungen [SQL Server], Sitzungen"
  - "Sitzungssprache einer clientbasierten Sitzung"
  - "Uhrzeit [SQL Server], Sitzungssprachen"
  - "Meldungen [SQL Server], internationale Überlegungen"
  - "Sitzungssprache auf Serverseite"
ms.assetid: de7f2c90-8f4f-4cfc-94cc-4933a7fd2bde
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Festlegen einer Sitzungssprache
  Die Sitzungssprache kann verwendet werden, um festzulegen, wie die folgenden Elemente abhängig von Sprache und Kultur auf dem Server angezeigt werden:  
  
-   Die Sprache, die für Fehlermeldungen und andere Systemmeldungen verwendet wird. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt das Vorhandensein mehrerer Kopien aller Systemfehler-Zeichenfolgen und Meldungen in allen Sprachen, in denen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbar ist. Diese Meldungen können mithilfe der [sys.messages](../Topic/sys.messages%20\(Transact-SQL\).md) -Katalogsicht angezeigt werden. Wenn Sie eine lokalisierte Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installieren, sind diese Systemmeldungen für die installierte Sprachversion übersetzt. Standardmäßig erhalten Sie auch die US-englischen Meldungen . Außerdem können Sie benutzerdefinierte Meldungen in einer bestimmten Sprache mithilfe von [sp_addmessage](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md) hinzufügen.  
  
-   Das Format von Datums- und Zeitdaten.  
  
-   Die Namen von Tagen und Monaten, einschließlich Abkürzungen.  
  
-   Der erste Tag der Woche.  
  
-   Währungsdaten.  
  
 Für die Sitzungseinstellungen sind 33 Sprachen verfügbar. Eine Liste der Sprachen finden Sie unter [sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md).  
  
## Festlegen der Sitzungssprache auf dem Server  
 So legen Sie die Sitzungssprache serverseitig fest. Verwenden Sie [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md).  
  
## Festlegen der Sitzungssprache auf dem Client  
 Die Sitzungssprache kann clientseitig mit OLE DB, ODBC oder ADO.NET festgelegt werden. Verwenden Sie für OLE DB die Eigenschaft SSPROP_INIT_CURRENTLANGUAGE. Weitere Informationen hierzu finden Sie unter [Initialisierungs- und Autorisierungseigenschaften](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
 Verwenden Sie für ODBC das programmiersprachliche Schlüsselwort. Weitere Informationen finden Sie unter [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md).  
  
 Verwenden Sie für ADO.NET den **Current Language** -Parameter des Objekts **ConnectionString** . Weitere Informationen finden Sie in der Dokumentation zu [!INCLUDE[msCoName](../../includes/msconame-md.md)] Data Access Components (MDAC) Software Development Kit (SDK).  
  
  