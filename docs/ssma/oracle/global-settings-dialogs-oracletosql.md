---
title: Globale Einstellungen (Dialogfelder) (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 43989355-cebf-4d8b-ba3d-fa8546e70230
caps.latest.revision: 3
author: sabotta
ms.author: carlasab
manager: v-pelars
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e2feffc4f4fdf2d37797bf51581eaad83580210e
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="global-settings-dialogs--oracletosql"></a>Globale Einstellungen (Dialogfelder) (OracleToSQL)
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
  

