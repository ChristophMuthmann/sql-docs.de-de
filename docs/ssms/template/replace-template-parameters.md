---
title: Ersetzen von Vorlagenparametern|Microsoft-Dokumente
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.templates.replaceparameters.f1
helpviewer_keywords:
- template parameters [Template Explorer]
- templates [Transact-SQL], replacing parameters
- Replace (Query) Template Parameters dialog box
- replacing template parameters
ms.assetid: 1234aa14-3464-4a3e-922a-5cfb8fb23627
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 46e39ef54d2caf54cf68fa3ff3823d9111c05e0d
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="replace-template-parameters"></a>Ersetzen von Vorlagenparametern
Vorlagen enthalten Parameter, die bei jeder Verwendung der betreffenden Vorlage durch implementierungsspezifische Werte ersetzt werden können. Nach dem Öffnen einer Vorlage in einem Code-Editor können Sie die Parameter durch für die Implementierung relevante Werte ersetzen.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
Das Dialogfeld **Werte für Vorlagenparameter angeben** ist ein Raster mit drei Spalten. Die Spalten **Parameter** und **Typ** sind schreibgeschützt und können nicht geändert werden. Überprüfen Sie den Inhalt der Spalte **Wert** , und ändern Sie die Standardwerte in für die Implementierung geeignete Werte.  
  
Um das Dialogfeld verwenden zu können, müssen die im Skript enthaltenen Parameter in spitze Klammern (`< >`) gesetzt und in folgendem Format angegeben werden: `<`*Parametername*`,` *Datentyp*`,` *Standardwert*`>`.  
  
## <a name="replace-template-parameters"></a>Ersetzen von Vorlagenparametern  
Nach dem Öffnen der Vorlage in einem Code-Editor-Fenster:  
  
1.  Klicken Sie im Menü **Abfrage** auf **Werte für Vorlagenparameter angeben**.  
  
2.  Im Dialogfeld **Werte für Vorlagenparameter angeben** enthält die Spalte **Werte** jeweils einen vorgeschlagenen Wert für jeden Parameter. Akzeptieren Sie den Wert, oder ersetzen Sie ihn durch einen neuen Wert.  
  
3.  Klicken Sie auf **OK** , um das Dialogfeld **Vorlagenparameter ersetzen** zu schließen und das Skript im Abfrage-Editor zu ändern.  
  
## <a name="see-also"></a>Siehe auch  
[Vorlagen-Explorer](../../ssms/template/template-explorer.md)  
[Öffnen einer Vorlage](../../ssms/template/open-a-template.md)  
  

