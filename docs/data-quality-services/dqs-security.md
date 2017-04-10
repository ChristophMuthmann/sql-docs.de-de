---
title: "DQS-Sicherheit | Microsoft Docs"
ms.custom: ""
ms.date: "10/01/2012"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 921927f5-1b1e-452a-a79e-c691829fd826
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# DQS-Sicherheit
  Die [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS)-Sicherheitsinfrastruktur basiert auf der SQL Server-Sicherheitsinfrastruktur. Ein Datenbankadministrator gewährt einem Benutzer einen Satz von Berechtigungen, indem er dem Benutzer eine DQS-Rolle zuordnet. Auf diese Weise wird bestimmt, auf welche DQS-Ressourcen der Benutzer Zugriff hat und welche funktionalen Aktivitäten der Benutzer ausführen kann.  
  
## DQS-Rollen  
 Es gibt vier Rollen für DQS. Eine davon ist der Datenbankadministrator (DBA), der hauptsächlich für Produktinstallation, Datenbankwartung und Benutzerverwaltung zuständig ist. Diese Rolle verwendet meist eher SQL Server Management Studio als die [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] - Anwendung. Die Serverrolle ist „sysadmin“.  
  
 Die anderen Rollen sind „Information Workers“ und „Data Stewards“, die das Produkt direkt durch in der Anwendung [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] verwenden. Zu diesen Rollen gehören:  
  
-   Die **DQS-Administrator** (Dqs_administrator-Rolle) kann alles in den Bereich des Produkts führen. Der Administrator kann ein Projekt bearbeiten und ausführen, eine Wissensdatenbank erstellen und bearbeiten, eine Aktivität beenden, einen Prozess innerhalb einer Aktivität stoppen und die Konfiguration sowie die Reference Data Services-Einstellungen ändern. Der DQS-Administrator kann jedoch nicht den Server installieren oder neue Benutzer hinzufügen. Dies ist Aufgabe des Datenbankadministrators.  
  
-   Die **DQS KB-Editor** (Rolle "Dqs_kb_editor") kann alle DQS-Aktivitäten mit Ausnahme von Verwaltungsaufgaben ausführen. Der KB-Editor kann ein Projekt bearbeiten und ausführen sowie eine Wissensdatenbank erstellen und bearbeiten. Er kann die Aktivitätsüberwachungsdaten anzeigen, die Aktivität jedoch weder abschließen noch stoppen oder Verwaltungsaufgaben ausführen.  
  
-   Die **DQS KB-Operator** (Dqs_kb_operator-Rolle) kann bearbeiten und Ausführen ein Projekts. Er kann keinerlei Wissensverwaltung ausführen und keine Wissensdatenbank erstellen oder ändern. Er kann die Aktivitätsüberwachungsdaten anzeigen, die Aktivität jedoch nicht abschließen bzw. keine Verwaltungsaufgaben ausführen.  
  
## Benutzerverwaltung  
 Der Datenbankadministrator (DBA) erstellt DQS-Benutzer und ordnet sie DQS-Rollen in SQL Server Management Studio zu. Der DBA verwaltet ihre Berechtigungen, indem er der DQS_MAIN-Datenbank SQL-Anmeldenamen als Benutzer hinzufügt und jeden Benutzer mit einer der DQS-Rollen verknüpft. Jeder Rolle werden Berechtigungen für einen Satz von gespeicherten Prozeduren in der DQS_MAIN-Datenbank gewährt. Die drei DQS-Rollen sind für die Datenbanken DQS_PROJECTS und DQS_STAGING_DATA nicht verfügbar.  
  
## Verwandte Aufgaben  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Beschreibt, wie Sie mit SQL Server Management Studio einen Benutzer erstellen und diesem DQS-Rollen gewähren.|[Verwalten von DQS-Benutzern in SSMS](../Topic/Manage%20DQS%20Users%20in%20SSMS.md)|  
  
  