---
title: "Öffnen einer Vorlage | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-templates
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- templates [Transact-SQL], opening
- opening templates
ms.assetid: 605b0f4c-5ba1-4249-ad1c-6341df77cd7a
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 346cfa3d8fbeaa4b85f600aa7928edebf47a7661
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="open-a-template"></a>Öffnen einer Vorlage
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Sie können eine Vorlage über den Vorlagen-Explorer öffnen.  
  
## <a name="to-open-a-template-from-template-explorer"></a>So öffnen Sie eine Vorlage über den Vorlagen-Explorer  
Vorlagen lassen sich über den Vorlagen-Explorer öffnen.  
  
1.  Klicken Sie zum Öffnen des Vorlagen-Explorers im Menü **Ansicht** auf **Vorlagen-Explorer**.  
  
2.  Erweitern Sie in der Liste mit Vorlagenkategorien die Kategorie mit der zu öffnenden Vorlage.  
  
3.  Die Vorlage lässt sich anhand von drei Methoden öffnen:  
  
    1.  Doppelklicken Sie auf die Vorlage, um sie in einem Code-Editor-Fenster zu öffnen.  
  
    2.  Klicken Sie mit der rechten Maustaste auf die Vorlage, und wählen Sie **Öffnen** aus, um die Vorlage in einem Code-Editor-Fenster zu öffnen.  
  
    3.  Ziehen Sie die Vorlage in ein Code-Editor-Fenster, um dem Inhalt des Editor-Fensters den Vorlagencode hinzuzufügen.  
  
Sobald die Vorlage geöffnet ist, können Sie im Dialogfeld **Vorlagenparameter ersetzen** die Parameter in der Vorlage durch Ihre eigenen Werte ersetzen.  
  
Wird durch das Öffnen einer Vorlage ein neues Editor-Fenster geöffnet, erfolgt dies mit den Anmeldeinformationen der aktuellen aktiven Verbindung. Ist beispielsweise beim Öffnen einer CREATE DATABASE-Vorlage eine [!INCLUDE[ssDE](../../includes/ssde_md.md)] -Instanz im Objekt-Explorer fokussiert, wird ein neues Editor-Fenster mit einer Verbindung zu dieser Instanz geöffnet. Ist keine aktive Verbindung vorhanden, gibt [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] ein Anmeldedialogfeld zurück.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Vorlagen-Explorer](../../ssms/template/template-explorer.md)  
[Vorlagenparameter ersetzen](../../ssms/template/replace-template-parameters.md)  
  
