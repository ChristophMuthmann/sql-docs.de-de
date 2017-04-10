---
title: "Arbeiten mit Facets der richtlinienbasierten Verwaltung | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Anzeigen von Facets der richtlinienbasierten Verwaltung"
  - "Facets [Richtlinienbasierte Verwaltung], kopieren"
  - "Facets [Richtlinienbasierte Verwaltung], anzeigen"
  - "Kopieren von Facets der richtlinienbasierten Verwaltung"
ms.assetid: 88d025c4-07c2-4e4d-8634-204249a8c82c
caps.latest.revision: 29
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 29
---
# Arbeiten mit Facets der richtlinienbasierten Verwaltung
  Ein Facet der richtlinienbasierten Verwaltung ist ein Satz von logischen Eigenschaften, die sich auf einen verwaltungsrelevanten Bereich beziehen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] umfasst mehrere vordefinierte Facets. Dazu gehört beispielsweise das Facet für die Oberflächenkonfiguration, das die standardmäßig deaktivierten Funktionen als Eigenschaften definiert.  
  
 Wenn Sie viele ähnliche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Umgebungen verwalten, können Sie ein Facet für eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]konfigurieren, den Status des Facets in eine Datei kopieren und diese Datei anschließend als Richtlinie in eine andere Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] importieren. Sobald der Status in eine Richtlinie umgewandelt wurde, kann die Richtlinie auf andere Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Instanzobjekte, Datenbanken oder Datenbankobjekte angewendet werden.  
  
 In diesem Thema wird beschrieben, wie der Status eines Facets in eine XML-Datei kopiert wird.  
  
##  <a name="BeforeYouBegin"></a> Berechtigungen  
 Die Verfahren in diesem Thema erfordern die Mitgliedschaft in der PolicyAdministratorRole-Rolle in der msdb-Datenbank.  
  
## Anzeigen und Kopieren von Facet-Status  
 [Anzeigen der Facets der richtlinienbasierten Verwaltung für ein SQL Server-Objekt](../../relational-databases/policy-based-management/view-the-policy-based-management-facets-on-a-sql-server-object.md)  
  
 [Kopieren eines Facet-Status der richtlinienbasierten Verwaltung in eine XML-Datei](../../relational-databases/policy-based-management/copy-a-policy-based-management-facet-state-to-an-xml-file.md)  
  
## Siehe auch  
 [Verwalten von Servern mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  