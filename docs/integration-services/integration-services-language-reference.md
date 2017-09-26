---
title: SQL Server Integration Services-Sprachreferenz | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
ms.assetid: c67b72f1-0a1e-42f0-878a-84e85efc915b
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9fe4120f8a5dc93517e8eb35b13e7fe5252be6b6
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="integration-services-language-reference"></a>Integration Services-Sprachreferenz
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  In diesem Abschnitt wird beschrieben, die [!INCLUDE[tsql](../includes/tsql-md.md)] -API zum Verwalten von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Projekte, die mit einer Instanz von bereitgestellt wurden [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]Speichert Objekte, Einstellungen und operative Daten in einer Datenbank als bezeichnet den [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Katalog. Der Standardname der der [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] SSISDB der Katalog wird. Die Objekte, die im Katalog gespeichert werden, umfassen Projekte, Pakete, Parameter, Umgebungen und Verwendungsverläufe.  
  
 Die Daten im [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Katalog werden in internen Tabellen gespeichert, die für Benutzer nicht sichtbar sind. Es werden jedoch Informationen verfügbar gemacht, die für einen Satz öffentlicher Sichten benötigt werden, die Sie abfragen können. Darüber hinaus wird ein Satz gespeicherter Prozeduren bereitgestellt, mit denen Sie häufige Aufgaben für den Katalog ausführen können.  
  
 In der Regel verwalten Sie [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Objekte im Katalog, indem Sie [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] öffnen. Sie können jedoch auch die Datenbanksichten und gespeicherten Prozeduren direkt verwenden oder benutzerdefinierten Code schreiben, mit dem die verwaltete API aufgerufen wird. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]und die verwaltete API die Sichten Abfragen und rufen Sie die gespeicherten Prozeduren, die beschrieben werden, in diesem Abschnitt können Sie viele Aufgaben ausführen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Sichten &#40; Integration Services-Katalog &#41;](../integration-services/system-views/views-integration-services-catalog.md)  
 Fragen Sie die Sicht, um zu überprüfen [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Objekte, Einstellungen und operative Daten.  
  
 [Gespeicherte Systemprozeduren &#40; Integration Services-Katalog &#41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
 Rufen Sie die gespeicherten Prozeduren zum Hinzufügen oder entfernen oder ändern [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Objekte und Einstellungen.  
  
 [Funktionen &#40;Integration Services-Katalog&#41;](http://msdn.microsoft.com/library/9f2aec85-3d4c-415f-b1f8-8328a60b1c7f)  
 Rufen Sie die Funktionen zum Verwalten von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Projekte.  
  
  
