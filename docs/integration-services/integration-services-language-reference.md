---
title: Integration Services-Sprachreferenz | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
ms.assetid: c67b72f1-0a1e-42f0-878a-84e85efc915b
caps.latest.revision: "7"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b5aec18b2ef581e38c7d4c07967f8fe2787df2d8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="integration-services-language-reference"></a>Integration Services-Sprachreferenz
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  In diesem Abschnitt wird die [!INCLUDE[tsql](../includes/tsql-md.md)]-API zum Verwalten von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Projekten beschrieben, die in einer Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] bereitgestellt wurden.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] speichert Objekte, Einstellungen und operative Daten in einer Datenbank, die als [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Katalog bezeichnet wird. Der Standardname des [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Katalogs ist SSISDB. Die Objekte, die im Katalog gespeichert werden, umfassen Projekte, Pakete, Parameter, Umgebungen und Verwendungsverläufe.  
  
 Die Daten im [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Katalog werden in internen Tabellen gespeichert, die für Benutzer nicht sichtbar sind. Es werden jedoch Informationen verfügbar gemacht, die für einen Satz öffentlicher Sichten benötigt werden, die Sie abfragen können. Darüber hinaus wird ein Satz gespeicherter Prozeduren bereitgestellt, mit denen Sie häufige Aufgaben für den Katalog ausführen können.  
  
 In der Regel verwalten Sie [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Objekte im Katalog, indem Sie [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] öffnen. Sie können jedoch auch die Datenbanksichten und gespeicherten Prozeduren direkt verwenden oder benutzerdefinierten Code schreiben, mit dem die verwaltete API aufgerufen wird. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] und die verwaltete API führen zur Ausführung vieler Aufgaben eine Abfrage der Sichten durch und rufen gespeicherte Prozeduren auf.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Sichten &#40;Integration Services-Katalog&#41;](../integration-services/system-views/views-integration-services-catalog.md)  
 Abfragen der Sichten, um [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Objekte, Einstellungen und operative Daten zu überprüfen.  
  
 [Gespeicherte Prozeduren &#40;Integration Services-Katalog&#41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
 Aufrufen der gespeicherten Prozeduren, um [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Objekte und Einstellungen hinzuzufügen, zu entfernen oder zu ändern.  
  
 [Funktionen &#40;Integration Services-Katalog&#41;](http://msdn.microsoft.com/library/9f2aec85-3d4c-415f-b1f8-8328a60b1c7f)  
 Aufrufen der Funktionen, um [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Projekte zu verwalten.  
  
  
