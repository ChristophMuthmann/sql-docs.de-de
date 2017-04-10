---
title: "Aktivieren einer Datenbank f&#252;r die Replikation (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datenbanken [SQL Server-Replikation]"
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# Aktivieren einer Datenbank f&#252;r die Replikation (SQL Server Management Studio)
  Eine Datenbank wird implizit für die Replikation aktiviert, wenn ein Mitglied der festen Serverrolle **sysadmin** mit dem Assistenten für neue Veröffentlichung eine Veröffentlichung erstellt. Ein Mitglied der **Sysadmin** -Serverrolle können auch eine Datenbank für die Replikation explizit, damit ein Mitglied der **Db_owner** festen Datenbankrolle kann eine oder mehrere Veröffentlichungen in dieser Datenbank erstellen. Um eine Datenbank explizit aktivieren, verwenden die **Publikationsdatenbanken** auf der Seite der **Verlegereigenschaften - \< Publisher>** im Dialogfeld. Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
### So aktivieren Sie eine Datenbank für die Replikation  
  
1.  Auf der **Publikationsdatenbanken** auf der Seite der **Verlegereigenschaften - \< Publisher>** Wählen Sie im Dialogfeld die **Transactional** und/oder **Merge** das Kontrollkästchen für jede Datenbank, die Sie replizieren möchten. Aktivieren Sie **Transaktionsreplikation** , um die Datenbank für die Momentaufnahmereplikation zu aktivieren.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  