---
title: Globale Einstellungen (Dialogfelder) (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 6df20fbb-e92d-475f-a94d-aaf70b06eb9b
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: bbe4fbc8674f442ef23baea110701e24d54ac631
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="global-settings-dialogs-mysqltosql"></a>Globale Einstellungen (Dialogfelder) (MySQLToSQL)
Mithilfe der Dialogfelder Seite der **globale Einstellungen** (Dialogfeld), um die Standardaktion für Benutzer und die Warnung-Einstellungen für SSMA anzugeben.  
  
Die Einstellungen des Dialogfelds für den Zugriff auf die **Tools** klicken Sie im Menü **globale Einstellungen**, klicken Sie auf **GUI** am unteren Rand des linken Bereich, und klicken Sie dann wählen **Dialoge**.  
  
## <a name="options"></a>enthalten  
**Warnhinweis anzeigen, vor dem Überschreiben von Objekten**  
Wenn SSMA Objekte in SQL Server konvertiert werden, eventuell einige Objekte in SQL Server-Metadaten für das Projekt bereits vorhanden. Diese Objekte möglicherweise bereits konvertiert wurden, oder die Objekte möglicherweise einfach denselben Namen in das Zielschema als Objekte, die Sie konvertieren möchten.  
  
Verwenden Sie diese Option, um anzugeben, ob SSMA Aufforderung zum Überschreiben von doppelten Objektdefinitionen sollten:  
  
-   Bei Auswahl des **"true"**, SSMA wird ein Warnungsdialogfeld angezeigt, wenn ein doppeltes Objekt gefunden wird. In diesem Dialogfeld können Sie einzelne Objekte oder alle doppelten Objekte überschrieben werden sollen, oder überspringen Sie einzelne Objekte oder alle doppelten Objekte angeben.  
  
-   Bei Auswahl des **"false"**, **-Objekt überschreiben Standardaktion** Option wird angezeigt, in dem Sie die Standardaktion anzugeben.  
  
**Standardaktion des Objekts überschreiben**  
Diese Option wird angezeigt, wenn Sie die Option **"false"** für die **warnen vor dem Überschreiben Objekte** Option.  
  
Verwenden Sie diese Option, um anzugeben, das Standardobjekt überschreiben Verhalten:  
  
-   Bei Auswahl des **"true"**, SSMA werden Objekte in den Metadaten der SQL Server-Projekt, die denselben Namen aufweisen und in das gleiche Zielschema das Objekt, das konvertiert werden automatisch überschrieben.  
  
-   Bei Auswahl des **"false"**, SSMA Objektmetadaten während der Konvertierung wird nicht überschrieben werden.  
  
