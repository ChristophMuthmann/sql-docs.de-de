---
title: "Lastenausgleich von Paketen auf Remoteservern mithilfe des SQL Server-Agents | Microsoft Docs"
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
  - "Lastenausgleich [Integration Services]"
  - "Übergeordnete Pakete [Integration Services]"
  - "SQL Server-Agent [Integration Services]"
ms.assetid: 9281c5f8-8da3-4ae8-8142-53c5919a4cfe
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# Lastenausgleich von Paketen auf Remoteservern mithilfe des SQL Server-Agents
  Müssen viele Pakete ausgeführt werden, ist es praktisch, hierfür andere verfügbare Server zu verwenden. Diese Methode, bei der zum Ausführen von Paketen andere Server verwendet werden, während die Steuerung der Pakete über ein übergeordnetes Paket erfolgt, wird als Lastenausgleich bezeichnet. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]wird der Lastenausgleich manuell ausgeführt, wobei die Struktur des Verfahrens von den Besitzern der Pakete festgelegt werden muss. Dabei wird der Lastenausgleich nicht automatisch von den Servern ausgeführt. Des Weiteren müssen die auf den Remoteservern ausgeführten Pakete vollständige Pakete sein. Einzelne Tasks anderer Pakete sind dabei nicht zulässig.  
  
 Der Lastenausgleich ist in den folgenden Szenarien nützlich:  
  
-   Die Pakete können alle gleichzeitig ausgeführt werden.  
  
-   Die Pakete sind umfangreich, und wenn sie nacheinander ausgeführt werden, kann es sein, dass die Ausführung länger dauert als die zulässige Verarbeitungszeit.  
  
 Administratoren und Architekten können bestimmen, ob das Verwenden zusätzlicher Server zum Verarbeiten zur Verbesserung der Prozesse beiträgt.  
  
## Abbildung des Lastenausgleichs  
 Im folgenden Diagramm wird ein übergeordnetes Paket auf einem Server angezeigt. Das übergeordnete Paket enthält mehrere Tasks Auftrag des SQL Server-Agents ausführen. Mit jedem Task des übergeordneten Pakets wird ein SQL Server-Agent auf einem Remoteserver aufgerufen. Diese Remoteserver enthalten SQL Server-Agent-Aufträge, die einen Schritt für den Aufruf eines Pakets auf diesem Server beinhalten.  
  
 ![Architektur für den SSIS-Lastenausgleich (Übersicht)](../../integration-services/packages/media/loadbalancingoverview.gif "Architektur für den SSIS-Lastenausgleich (Übersicht)")  
  
 Die in dieser Architektur für den Lastenausgleich erforderlichen Schritte stellen keine neuen Konzepte dar. Der Lastenausgleich wird nämlich erreicht, indem vorhandene Konzepte und allgemeine SSIS-Objekte auf neue Art und Weise verwendet werden.  
  
## Ausführen von Paketen auf einer Remoteinstanz mithilfe des SQL Server-Agents  
 In der Basisarchitektur für die Remoteausführung von Paketen befindet sich auf der SQL Server-Instanz ein zentrales Paket, mit dem andere Remotepakete gesteuert werden. Im Diagramm wird dieses zentrale Paket, das so genannte übergeordnete SSIS-Paket, angezeigt. Die Instanz, in der sich dieses übergeordnete Paket befindet, steuert die Ausführung von SQL Server-Agent-Aufträgen, mit denen die untergeordneten Pakete ausgeführt werden. Dabei werden die untergeordneten Pakete nicht nach einem festen Zeitplan ausgeführt, der vom SQL Server-Agent auf dem Remoteserver gesteuert wird. Die untergeordneten Pakete werden stattdessen beim Aufruf über das übergeordnete Paket vom SQL Server-Agent gestartet und auf derselben SQL Server-Instanz ausgeführt, auf der sich der SQL Server-Agent befindet.  
  
 Bevor Sie mit dem SQL Server-Agent ein Remotepaket ausführen können, müssen Sie das übergeordnete Paket und die untergeordneten Pakete konfigurieren und die zum Steuern der untergeordneten Pakete verwendeten SQL Server-Agent-Aufträge festlegen. In den folgenden Abschnitten werden weitere Informationen zum Erstellen, Konfigurieren, Ausführen und Verwalten von auf Remoteservern ausgeführten Paketen bereitgestellt. Dieser Prozess beinhaltet die folgenden Schritte:  
  
-   Erstellen und Installieren der untergeordneten Pakete auf Remoteservern.  
  
-   Erstellen der SQL Server-Agent-Aufträge auf Remoteinstanzen, mit denen die Pakete ausgeführt werden.  
  
-   Erstellen des übergeordneten Pakets.  
  
-   Festlegen des Protokollierungsszenarios für die untergeordneten Pakete.  
  
 In der folgenden Tabelle werden Links zu Themen bereitgestellt, mit denen Sie durch den Prozess begleitet werden.  
  
|Thema|Description|  
|-----------|-----------------|  
|[Implementierung von untergeordneten Paketen](../../integration-services/packages/implementation-of-child-packages.md)|Beschreibt die Installation von Paketen und die Erstellung der SQL Server-Agent-Aufträge zum Ausführen der Pakete.|  
|[Implementierung des übergeordneten Pakets](../../integration-services/packages/implementation-of-the-parent-package.md)|Beschreibt die Erstellung des übergeordneten Pakets, in dem viele Tasks "Auftrag des SQL Server-Agents ausführen" enthalten sind. Mit jedem dieser Tasks wird jeweils ein untergeordnetes Paket ausgeführt.|  
|[Protokollierung für Pakete auf Remoteservern, für die ein Lastenausgleich ausgeführt wurde](../../integration-services/packages/logging-for-load-balanced-packages-on-remote-servers.md)|Beschreibt das Protokollierungsszenario für die Remotepakete.|  
  
## Verwandte Aufgaben  
 [Planen eines Pakets mit dem SQL Server-Agent](../../integration-services/packages/schedule-a-package-by-using-sql-server-agent.md)  
  
  