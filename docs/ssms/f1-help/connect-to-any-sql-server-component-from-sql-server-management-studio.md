---
title: Herstellen einer Verbindung mit einer beliebigen SQL Server-Komponente aus SSMS | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-f1
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [SQL Server], SQL Server Management Studio
- saving connections
- components [SQL Server], connections
- SQL Server Management Studio [SQL Server], connections
ms.assetid: 5eeb41bd-b25b-4d3b-a005-a7d9e4b5978e
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 23b92903859c07351890dfd0858aaad6ed7da00e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="connect-to-any-sql-server-component-from-sql-server-management-studio"></a>Herstellen einer Verbindung mit einer beliebigen SQL Server-Komponente aus SQL Server Management Studio
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] stellt die Funktionalität zum Verwalten aller Komponenten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bereit. Mit [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] können Sie eine Verbindung zu folgenden Komponenten herstellen:  
  
-   Eine Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)].  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)]bereit.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)]bereit.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)]bereit.  
  
Obwohl [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] es Ihnen ermöglicht, mit Abfragen zu arbeiten, ohne zuerst eine Verbindung mit einer Datenquelle herzustellen, ist für die meisten anderen Aufgaben eine Verbindung erforderlich. [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] stellt das Dialogfeld **Verbindung mit Server herstellen** bereit, um Verbindungseigenschaften für [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Komponenten zu konfigurieren. Wenn [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] gestartet wird, wird das Dialogfeld **Verbindung mit Server herstellen** geöffnet, und Sie werden aufgefordert, eine Verbindung mit einem Server herzustellen. Das Dialogfeld **Verbindung mit Server herstellen** behält die Verbindungseinstellungen vom vorherigen Mal bei.  
  
> [!NOTE]  
> Diese Funktion lässt sich deaktivieren, sodass keine automatische Initialisierung einer Verbindung stattfindet. Weitere Informationen finden Sie unter [Startoptionen für den Datenbankmoduldienst](http://msdn.microsoft.com/en-us/d373298b-f6cf-458a-849d-7083ecb54ef5).  
  
## <a name="saving-connections"></a>Speichern von Verbindungen  
Sie können Verbindungen mit bestimmten Servern in der Liste der registrierten Server speichern, oder Sie können mit dem Projektmappen-Explorer Verbindungen in Projekten speichern.  
  
### <a name="saving-connections-in-registered-servers"></a>Speichern von Verbindungen in der Liste der registrierten Server  
Wenn Sie einen Server registrieren, speichert [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] die Verbindungsinformationen in der Liste der registrierten Server. Um eine Verbindung mit einem registrierten Server herzustellen, doppelklicken Sie in der Liste der registrierten Server auf den Servernamen. Daraufhin öffnet der Objekt-Explorer eine Verbindung zum Server.  
  
### <a name="saving-connections-in-solution-explorer"></a>Speichern von Verbindungen im Projektmappen-Explorer  
Mit dem Projektmappen-Explorer können Sie zugehörige Abfragen, Skripts, Verbindungen und andere Informationen in einem Projekt speichern. Jedes Skriptprojekt enthält einen Knoten namens **Verbindungen**, in dem Sie eine oder mehrere Verbindungen speichern können. Klicken Sie zum Hinzufügen einer Verbindung mit der rechten Maustaste auf **Verbindungen**, und klicken Sie dann auf **Neue Verbindung**. Erweitern Sie zum Zugreifen auf eine gespeicherte Verbindung **Verbindungen** , und doppelklicken Sie auf die Verbindung. [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] öffnet ein dieser Verbindung zugeordnetes Abfragefenster. Beim Speichern behalten Skripts die Verknüpfung zu einer bestimmten Verbindung bei.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Verwenden von SQL Server Management Studio](../../ssms/use-sql-server-management-studio.md)  
[Objekt-Explorer](../../ssms/object/object-explorer.md)  
  
