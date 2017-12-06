---
title: Globale Einstellungen (Dialogfelder) (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 43989355-cebf-4d8b-ba3d-fa8546e70230
caps.latest.revision: "3"
author: Shamikg
ms.author: Shamikg
manager: v-pelars
ms.workload: Inactive
ms.openlocfilehash: 7dd6771528c3ccf971c19cf7f26caa5d3c2f49ab
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
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
  
