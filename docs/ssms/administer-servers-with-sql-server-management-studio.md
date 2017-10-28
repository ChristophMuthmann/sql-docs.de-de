---
title: Verwalten von Servern mit SQL Server Management Studio | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], administering
ms.assetid: 938bb035-e07a-4082-9f93-229d9feb6b06
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d73b15b799fe8c52124331cfc346d3759fc860a6
ms.contentlocale: de-de
ms.lasthandoff: 08/18/2017

---
# <a name="administer-servers-with-sql-server-management-studio"></a>Verwalten von Servern mit SQL Server Management Studio
[!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] ist ein funktionsreicher integrierter Verwaltungsclient, der entsprechend den Anforderungen von [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] - und Azure SQL-Datenbank-Administratoren für die Verwaltung von Servern entworfen wurde. In [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)]werden administrative Tasks mit dem Objekt-Explorer ausgeführt, mit dem Sie eine Verbindung mit einem beliebigen Server der [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] -Produktfamilie herstellen und dessen Inhalt grafisch dargestellt durchsuchen können. Ein Server kann eine Instanz von Folgendem sein: [!INCLUDE[ssDE](../includes/ssde_md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion_md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion_md.md)] oder Azure SQL-Datenbank.  
  
Zu den Toolkomponenten von [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] zählen registrierte Server, der Objekt-Explorer, der Projektmappen-Explorer, der Vorlagen-Explorer, die Seite Details zum Objekt-Explorer und das Dokumentenfenster. Um ein Tool anzuzeigen, klicken Sie im Menü **Ansicht** auf den Namen des Tools. Um den Abfrage-Editor anzuzeigen, klicken Sie auf der Symbolleiste auf die Schaltfläche **Neue Abfrage** .  
  
> [!IMPORTANT]  
> Der Netzwerkverkehr zwischen [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] und [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] ist standardmäßig unverschlüsselt. Sie sollten in [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] nur mit vertraulichen Daten (einschließlich Kennwörtern) arbeiten, wenn Sie eine verschlüsselte Verbindung hergestellt haben. Weitere Informationen finden Sie unter [Vorgehensweise: Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](http://msdn.microsoft.com/en-us/e1e55519-97ec-4404-81ef-881da3b42006).  
  
Verwenden Sie [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] für Folgendes:  
  
-   Registrieren von Servern.  
  
-   Stellen Sie eine Verbindung mit Folgendem her: [!INCLUDE[ssDE](../includes/ssde_md.md)], [!INCLUDE[ssAS](../includes/ssas_md.md)], [!INCLUDE[ssRS](../includes/ssrs_md.md)],  [!INCLUDE[ssIS](../includes/ssis_md.md)] oder Azure SQL-Datenbank.  
  
-   Konfigurieren von Servereigenschaften.  
  
-   Verwalten von Datenbank- und [!INCLUDE[ssAS](../includes/ssas_md.md)] -Objekten wie Cubes, Dimensionen und Assemblys.  
  
-   Erstellen von Objekten wie Datenbanken, Tabellen, Cubes, Datenbankbenutzer und Anmeldenamen.  
  
-   Verwalten von Dateien und Dateigruppen.  
  
-   Anfügen oder Trennen von Datenbanken.  
  
-   Starten von Skriptingtools.  
  
-   Verwalten der Sicherheit.  
  
-   Anzeigen von Systemprotokollen.  
  
-   Überwachen der aktuellen Aktivität.  
  
-   Konfigurieren der Replikation.  
  
-   Verwalten von Volltextindizes.  
  
Um [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] oder den [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] -Agent zu starten und zu beenden, verwenden Sie den [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] -Konfigurations-Manager.  
  
## <a name="see-also"></a>Siehe auch  
[Verwenden von SQL Server Management Studio](../ssms/use-sql-server-management-studio.md)  
[Vorgehensweise: Anzeigen von Servereigenschaften (SQL Server Management Studio)](http://msdn.microsoft.com/en-us/55f3ac04-5626-4ad2-96bd-a1f1b079659d)  
  

