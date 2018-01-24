---
title: Erstellen von Skripts mit Vorlagen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: ed48014c-3fc9-48ff-8c0f-8d1822195f14
caps.latest.revision: "28"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f1972bf4ce414c66a3a4f607af859502680730ea
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="lesson-3-1---create-scripts-using-templates"></a>Lektion 3-1: Erstellen von Skripts mit Vorlagen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] stellt eine große Anzahl von Skriptvorlagen zur Verfügung, die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen für viele häufig ausgeführte Aufgaben umfassen. Diese Vorlagen enthalten Parameter für Werte, die vom Benutzer angegeben werden, wie z. B. der Tabellenname. Wenn Sie Parameter verwenden, brauchen Sie den Namen nur einmal einzugeben, er wird dann automatisch an alle erforderlichen Stellen im Skript kopiert. Sie können auch eigene, benutzerspezifische Vorlagen für die Skripts erstellen, die Sie am häufigsten benötigen. Sie können die Vorlagenstruktur neu anordnen, Vorlagen verschieben oder neue Ordner für Vorlagen anlegen. In der folgenden Übung verwenden Sie eine Vorlage zum Anlegen einer Datenbank.  
  
## <a name="using-templates"></a>Verwenden von Vorlagen  
  
#### <a name="to-create-a-script-using-a-template"></a>So erstellen Sie ein Skript mithilfe einer Vorlage  
  
1.  Klicken Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]im Menü **Ansicht** auf **Vorlagen-Explorer**.  
  
2.  Die Vorlagen im Vorlagen-Explorer sind in Gruppen angeordnet. Erweitern Sie **Datenbank**, und doppelklicken Sie anschließend auf **Datenbank erstellen**.  
  
3.  Vervollständigen Sie im Dialogfeld **Verbindung mit Datenbankmodul herstellen** die Verbindungseinstellungen, und klicken Sie anschließend auf **Verbinden**. Ein neues Fenster des Abfrage-Editors wird geöffnet, in dem der Inhalt der Vorlage **Datenbank erstellen** angezeigt wird.  
  
4.  Klicken Sie im Menü **Abfrage** auf **Werte für Vorlagenparameter angeben**.  
  
5.  Im Dialogfeld **Werte für Vorlagenparameter angeben** enthält die **Wert** -Spalte einen empfohlenen Wert für den Parameter **Database_Name** . Geben Sie im Feld des Parameters **Database_Name** den Begriff **Marketing**ein, und klicken Sie auf **OK**. "Marketing" wird jetzt im Skript an mehreren Stellen eingefügt.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in dieser Lektion  
[Erstellen von benutzerdefinierten Vorlagen](../../tools/sql-server-management-studio/lesson-3-2-create-custom-templates.md)  
  
  
  
