---
title: "Verwalten von Oracle-Tabellenbereichen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Veröffentlichungen mit Oracle [SQL Server-Replikation], Verwalten von Tabellenbereichen"
  - "Tabellenbereiche [SQL Server-Replikation]"
ms.assetid: b8ea6c3b-01d6-4efc-bbfb-03b264530bbd
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# Verwalten von Oracle-Tabellenbereichen
  Ein Tabellenbereich ist eine Einheit des Datenbankspeicherplatzes, die in etwa einer Dateigruppe in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]entspricht. Tabellenbereiche ermöglichen das Speichern und Verwalten von Datenbankobjekten innerhalb einzelner Gruppen. Weitere Informationen finden Sie in der Oracle-Dokumentation.  
  
 Wenn Sie eine Tabelle als Teil einer Oracle-Veröffentlichung konfigurieren, können Sie optional einen vorhandenen Oracle-Tabellenbereich angeben, der beim Speichern der Replikations-Protokollinformationen verwendet wird. Wird kein spezifischer Tabellenbereich angegeben, wird für die Replikationsobjekte der Standardtabellenbereich verwendet, der mit dem Schema für den administrativen Replikationsbenutzer verknüpft ist, das beim Konfigurieren des Verlegers konfiguriert wurde.  
  
 **So geben Sie einen Tabellenbereich für eine Artikelprotokolltabelle an**:  
  
-   Geben Sie im Dialogfeld **Artikeleigenschaften** einen Tabellenbereich an. Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
-   Verwendung [Sp_changearticle & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md). Mit **Sp_changearticle**, geben Sie Folgendes:  
  
    -   Den Namen des Oracle-Verlegers für den Parameter **@publisher**.  
  
    -   Den Namen der Oracle-Veröffentlichung für den Parameter **@publication**.  
  
    -   Den Namen des Artikels für den Parameter **@article**.  
  
    -   Wert 'tablespace' für den Parameter **@property**  
  
    -   Name des Tabellenbereichs für den Parameter **@value**  
  
## Siehe auch  
 [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Auf dem Oracle-Verleger erstellte Objekte](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)  
  
  