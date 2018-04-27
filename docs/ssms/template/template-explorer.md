---
title: Vorlagen-Explorer | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-templates
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.templates.explorer.f1
- sql13.wb.templates.f1
helpviewer_keywords:
- templates [SQL Server]
- SQL Server Management Studio [SQL Server], Template Explorer
- Template Explorer
- templates [Transact-SQL]
- templates [SQL Server], Template Explorer
ms.assetid: b9ee55c5-bb44-4f76-90ac-792d8d83b4c8
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6f8d8a6007d27141e4cfd37afe7d17fd11d07603
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="template-explorer"></a>Template Explorer
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] stellt eine Vielzahl von Vorlagen bereit. Vorlagen sind Dateien mit Codevorlagen, die SQL-Skripts enthalten, mit deren Hilfe Sie Objekte in einer Datenbank erstellen können. Beim ersten Öffnen des Vorlagen-Explorers wird eine Kopie der Vorlagen im Benutzerordner unter „C:\Benutzer“ im Unterordner „AppData\Roaming\Microsoft\SQL Server Management Studio\130\Templates“ abgelegt.  
  
Sie können die verfügbaren Vorlagen in Vorlagen-Explorer durchsuchen und dann eine Vorlage öffnen, um den Code in einem Fenster des Code-Editors zu integrieren. Sie können auch benutzerdefinierte Vorlagen erstellen.  
  
## <a name="benefits-of-templates"></a>Vorteile von Vorlagen  
Vorlagen sind für Projektmappen, Projekte und verschiedene Arten von Code-Editoren verfügbar. Vorlagen dienen zum Erstellen von Objekten wie Datenbanken, Tabellen, Sichten, Indizes, gespeicherten Prozeduren, Trigger, Statistiken und Funktionen. Darüber hinaus sind Vorlagen vorhanden, mit denen Sie Ihren Server verwalten können, indem Sie erweiterte Eigenschaften, Verbindungsserver, Anmeldenamen, Rollen, Benutzer und Vorlagen für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)]erstellen.  
  
Die von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] bereitgestellten Vorlageskripts enthalten Parameter, die beim Anpassen von Code hilfreich sind. Verwenden Sie nach dem Öffnen einer Vorlage das Dialogfeld **Vorlagenparameter ersetzen** , um Werte in das Skript einzufügen.  
  
Für regelmäßig auszuführende Aufgaben können Sie benutzerdefinierte Vorlagen erstellen. Sie können Ihre benutzerdefinierten Skripts in die vorhandenen Ordner einfügen oder eine neue Ordnerstruktur erstellen.  
  
Der [!INCLUDE[ssDE](../../includes/ssde_md.md)] -Abfrage-Editor unterstützt darüber hinaus Codeausschnitte, die an einer bestimmten Stelle im Skript eingefügt werden können, indem Sie mit der rechten Maustaste an diese Stelle klicken.  
  
## <a name="related-tasks"></a>Related Tasks  
Erste Schritte mit Vorlagen finden Sie in den folgenden Themen:  
  
|**Description**|**Thema**|  
|-------------------|-------------|  
|Beschreibt, wie der Code aus einer Vorlage in ein Code-Editorfenster integriert wird.|[Öffnen einer Vorlage](../../ssms/template/open-a-template.md)|  
|Beschreibt, wie Vorlagenparameterwerte nach dem Öffnen einer Vorlage in einem Code-Editor ersetzt werden.|[Vorlagenparameter ersetzen](../../ssms/template/replace-template-parameters.md)|  
  
