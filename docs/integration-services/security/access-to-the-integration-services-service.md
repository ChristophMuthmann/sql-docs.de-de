---
title: "Zugriff auf den Integration Services-Dienst | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SSIS-Pakete, Sicherheit"
  - "Anzeigen von Paketen beim Ausführen"
  - "Anzeigen von Paketen beim Ausführen"
  - "Sicherheit [Integration Services], ausgeführte Pakete"
  - "Pakete [Integration Services], Sicherheit"
  - "Aktuell ausgeführte Pakete"
  - "Integration Services-Pakete, Sicherheit"
  - "SQL Server Integration Services-Pakete, Sicherheit"
ms.assetid: 1088aafc-14c5-4e7d-9930-606a24c3049b
caps.latest.revision: 16
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 16
---
# Zugriff auf den Integration Services-Dienst
  Über Paketschutzebenen kann gesteuert werden, wer ein Paket bearbeiten und ausführen darf. Zusätzlicher Schutz ist erforderlich, um die Anzahl der Personen einzuschränken, die die Liste der derzeit auf einem Server ausgeführten Pakete anzeigen und die Paketausführung in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]beenden dürfen.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst zum Auflisten der ausgeführten Pakete verwendet. Mitglieder der Gruppe der Windows-Administratoren können alle aktuell ausgeführten Pakete anzeigen und ihre Ausführung beenden. Benutzer, die nicht zur Administratoren-Gruppe gehören, können nur solche ausgeführten Pakete anzeigen und deren Ausführung beenden, wenn sie selbst die Ausführung gestartet haben.  
  
 Es ist wichtig, den Zugriff auf Computer einzuschränken, auf denen ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst ausgeführt wird. Dies gilt besonders für einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst, der Remoteordner auflisten kann. Jeder authentifizierte Benutzer kann die Auflistung von Paketen anfordern. Selbst wenn vom Dienst keine Pakete gefunden werden, listet er Ordner auf. Diese Ordnernamen können für böswillige Benutzer von Nutzen sein. Wenn ein Administrator den Dienst so konfiguriert hat, dass Ordner auf einem Remotecomputer aufgelistet werden, können die Benutzer auch Ordnernamen anzeigen, die sie normalerweise nicht anzeigen könnten.  
  
  