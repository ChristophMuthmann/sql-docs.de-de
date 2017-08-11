---
title: Reporting Services-Erweiterungen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- SQL Server Reporting Services, extending
- extensions [Reporting Services], about extensions
- SSIS, extending
- Reporting Services, extending
- extensions [Reporting Services]
ms.assetid: 2bf17ae4-2292-4a58-a1f0-56e99abd9b69
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 37adf4c09f7f23294572a17631240ad88f51fc9e
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="reporting-services-extensions"></a>Erweiterungen für Reporting Services
  Die modulare Architektur von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ermöglicht Erweiterungen. Eine verwaltete Code-API steht zur Verfügung, sodass Sie problemlos Erweiterungen entwickeln, installieren und verwalten können, die von vielen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Komponenten benötigt werden. Sie können private erstellen oder freigegebene Assemblys, die mit der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] und Hinzufügen neuer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Funktionalität, um den wachsenden betrieblichen Anforderungen zu erfüllen.  
  
 Durch die besondere Architektur für Erweiterungen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] können spezielle Erweiterungsfunktionen des Produkts und seiner Komponenten entwickelt werden. Momentan wird die Erweiterung der Datenverarbeitungsmöglichkeiten von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in großem Umfang unterstützt. Die Datenverarbeitungs-API enthält bekannte [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Datenanbieter-Konstrukte und Konventionen, die den Entwicklern die Integration zusätzlicher Datenverarbeitungsmöglichkeiten in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] bieten. Diese Datenverarbeitungserweiterungen fügen sowohl dem Berichtsserver als auch dem Berichts-Designer weitere Funktionen hinzu, sodass eine nahtlose Integration der benutzerdefinierten Daten in die bestehenden Berichte ermöglicht wird.  
  
 Eine weitere unterstützte Erweiterung ist die Übermittlungserweiterung. Die Übermittlungs-API ist komplett in die [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Architektur integriert und ermöglicht eine Vielzahl von Übermittlungsmechanismen für den Versand von Berichtsbenachrichtigungen an die Benutzer. Sie können den Berichtsserver so erweitern, dass er eine benutzerdefinierte Übermittlung an Benutzer zulässt. Und Sie können die Abonnementverwaltungsseiten des Berichts-Managers so erweitern, dass Abonnements möglich sind, die benutzerdefinierte Übermittlungserweiterungen verwenden.  
  
 Über eine weitere Berichtsservererweiterung, die RDCE-Erweiterung (Report Definition Customization Extension), kann eine Berichtsdefinition dynamisch angepasst werden, bevor Sie an das Verarbeitungsmodul geleitet wird. Sie können Berichte an verschiedene Faktoren, z. B. an andere Benutzer oder Sprachen, anpassen. Beispielsweise möchten Sie verschiedene Ansichten für verschiedene Benutzer (z. B. Manager oder Mitarbeiter einer Abteilung) implementieren. Oder Sie möchten einen Bericht so anpassen, dass er ein anderes Layout hat, wenn er auf Französisch oder Arabisch ausgegeben wird.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Security Considerations for Extensions (Überlegungen zur Sicherheit von Erweiterungen)](../../reporting-services/extensions/security-considerations-for-extensions.md)  
 Beschreibt Sicherheitsprobleme, die beim Entwickeln und Bereitstellen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Erweiterungen auftreten können.  
  
 [Implementing a Data Processing Extension (Implementieren von Datenverarbeitungserweiterungen)](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)  
 Beschreibt die Anforderungen und Schritte für die Implementierung von Datenverarbeitungserweiterungen für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Implementing a Delivery Extension (Implementieren von Übermittlungserweiterungen)](../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)  
 Beschreibt die Anforderungen und Schritte für die Implementierung von Übermittlungserweiterungen für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Implementing a Rendering Extension (Implementieren von Renderingerweiterungen)](../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)  
 Enthält eine Einführung zur Entwicklung von Renderingerweiterungen.  
  
 [Implementieren von Sicherheitserweiterungen](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)  
 Beschreibt die Anforderungen und Schritte für die Implementierung von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Sicherheitserweiterungen.  
  
 [Reporting Services-Erweiterungsbibliothek](../../reporting-services/extensions/reporting-services-extension-library.md)  
 Enthält die Programmierreferenz für die Erweiterungs-API-Bibliothek für die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Erweiterbarkeitsfunktionen.  
  
  
