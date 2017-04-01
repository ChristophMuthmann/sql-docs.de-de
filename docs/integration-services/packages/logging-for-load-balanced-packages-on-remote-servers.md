---
title: "Protokollierung f&#252;r Pakete auf Remoteservern, f&#252;r die ein Lastenausgleich ausgef&#252;hrt wurde | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Protokolle [Integration Services], Remotepakete"
ms.assetid: fd571567-b625-4f9a-8b7e-42c5c588b11b
caps.latest.revision: 24
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# Protokollierung f&#252;r Pakete auf Remoteservern, f&#252;r die ein Lastenausgleich ausgef&#252;hrt wurde
  Für einen Administrator ist es einfacher, die Protokolle aller untergeordneten Pakete, die auf verschiedenen Servern ausgeführt werden, zu verwalten, wenn alle untergeordneten Pakete denselben Protokollanbieter verwenden und in dasselbe Ziel schreiben. Eine Möglichkeit zum Erstellen einer allgemeinen Protokolldatei für alle untergeordneten Pakete besteht darin, die untergeordneten Pakete für die Protokollierung ihrer Ereignisse in einem SQL Server-Protokollanbieter zu konfigurieren. Sie können alle Pakete für die Verwendung derselben Datenbank, desselben Servers und derselben Server-Instanz konfigurieren.  
  
 Zum Anzeigen der Protokolldateien muss sich der Administrator lediglich bei einem einzigen Server anmelden, um die Protokolldateien aller untergeordneten Pakete anzuzeigen.  
  
## Verwandte Aufgaben  
 Informationen über das Ermöglichen des Anmeldens in einem Paket finden Sie unter [Aktivieren der Paketprotokollierung in SQL Server Data Tools](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md).  
  
## Siehe auch  
 [Integration Services-Protokollierung &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  