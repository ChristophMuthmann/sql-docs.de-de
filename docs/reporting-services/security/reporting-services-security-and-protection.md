---
title: "Sicherheit und Schutz f&#252;r Reporting Services | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Sicherheit [Reporting Services]"
  - "Reporting Services, Sicherheit"
ms.assetid: 270075c5-bf12-4467-a775-abbda3d954a5
caps.latest.revision: 21
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 21
---
# Sicherheit und Schutz f&#252;r Reporting Services
  In diesem Abschnitt wird beschrieben, welche Sicherheitsfunktionen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. In diesem Abschnitt werden auch die Autorisierungsmodelle und die Authentifizierungsanbieter erläutert, die in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]unterstützt werden.  
  
## Erweiterter Schutz für die Authentifizierung  
 Der erweiterte Schutz für die Authentifizierung wird ab [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]unterstützt. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Funktion unterstützt die Verwendung der Kanalbindung und Dienstbindung, um den Authentifizierungsschutz zu verbessern. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Funktionen müssen mit einem Betriebssystem verwendet werden, das erweiterten Schutz unterstützt. Weitere Informationen finden Sie unter [Extended Protection for Authentication with Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md).  
  
## Authentifizierung und Autorisierung  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] bietet unterschiedliche Authentifizierungstypen für Benutzer und Clientanwendungen zur Authentifizierung mit dem Berichtsserver. Mit dem richtigen Authentifizierungstyp für Ihren Berichtsserver kann Ihr Unternehmen die den Anforderungen entsprechende Sicherheitsstufe erzielen. Weitere Informationen finden Sie unter [Authentication with the Report Server](../../reporting-services/security/authentication-with-the-report-server.md).  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verwendet auch Rollen und Berechtigungen, um den Benutzerzugriff auf Inhalte des Berichtsserverkatalogs (d.h. wer worauf und wie zugreifen kann) zu steuern. Weitere Informationen finden Sie unter [Rollen und Berechtigungen &#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md).  
  
## Verwandte Aufgaben  
  
|Taskbeschreibungen|Links|  
|-----------------------|-----------|  
|Konfigurieren Sie das Secure Sockets Layer (SSL), um Clientverbindungen zum Berichtsserver zu sichern.|[Konfigurieren von SSL-Verbindungen auf einem Berichtsserver im einheitlichen Modus](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)|  
  
  