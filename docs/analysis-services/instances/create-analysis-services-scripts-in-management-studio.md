---
title: Erstellen von Analysis Services-Skripts in Management Studio | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Analysis Services objects, scripts
- objects [Analysis Services], scripts
- scripts [Analysis Services], objects
ms.assetid: 4f1b965c-9ca6-427b-8f4d-0ce1eea7c0fe
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 24fffa56991e411dfae93321bbe238c1bbcb4db3
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-analysis-services-scripts-in-management-studio"></a>Erstellen von Analysis Services-Skripts in Management Studio
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] schließt Skriptgenerierungsfunktionen, Vorlagen und Editoren ein, mit denen Sie Analysis Services-Objekte und Tasks schreiben können.  
  
## <a name="script-analysis-services-tasks-in-management-studio"></a>Script Analysis Services-Tasks in Management Studio  
 Sie können in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Skripts erstellen, indem auf eine der Skriptoptionen in einem taskbezogenen Dialogfeld geklickt wird. Alle Dialogfelder, die Sie zum Ausführen von Aufgaben verwenden (z. B. Sicherung oder Wiederherstellungsdatenbank, Objektverarbeitung oder Aggregationsentwurf), beinhalten oben eine Skriptoption. Durch die Auswahl einer dieser Optionen wird auf Grundlage der Informationen und der Einstellungen im Dialogfeld ein XMLA-Skript generiert.  
  
 Standardmäßig wird das Skript generiert und in einem XMLA-Abfrage-Editor eingefügt. Sie können die Skriptoptionsliste jedoch auch erweitern, um das Skript an die Windows-Zwischenablage oder eine Datei weiterzuleiten.  
  
#### <a name="to-script-an-analysis-services-task"></a>So erstellen Sie Skripts für einen Analysis Services-Task  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung zu einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]her.  
  
2.  Klicken Sie mit der rechten Maustaste auf eine Datenbank, und klicken Sie auf **Sichern**. Daraufhin wird das Dialogfeld Datenbank sichern geöffnet. Geben Sie einen Sicherungsdateinamen an, und wählen Sie die gewünschten Optionen für diese Sicherung aus.  
  
3.  Klicken Sie auf **Skript** am oberen Rand des Dialogfelds. Die Funktion Skript ist ein Teil aller taskbasierten Dialogfelder in Management Studio. Es hat die folgenden Optionen: **Skript für Aktion in Fenster 'Neue Abfrage' schreiben** , um das Abfrage-Editor-Fenster zu öffnen, **Skript für Aktion in Datei schreiben** , um das XMLA-Skript in einer Datei zu speichern, oder **Skript für Aktion in Zwischenablage schreiben** , um das XMLA-Skript in der Zwischenablage zu speichern.  
  
     Beachten Sie, dass die Option **Skript für Aktion in Auftrag schreiben** , die in Management Studio als Skriptoption aufgelistet wird, für Analysis Services-Skripts nicht unterstützt wird.  
  
4.  Wenn Sie die Standardoption **Skript für Aktion in Fenster 'Neue Abfrage' schreiben**aktivieren, wird ein generiertes Skript in einem XMLA-Abfragefenster eingefügt.  
  
     Sie können jetzt das Dialogfeld Datenbank sichern und das XMLA-Skript direkt bearbeiten oder ausführen.  
  
## <a name="script-analysis-services-objects-in-management-studio"></a>Script Analysis Services-Objekte in Management Studio  
 Die Skripterstellung für Objekte mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] wird ausgeführt durch Klicken mit der rechten Maustaste auf ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekt in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und Auswählen von entweder **CREATE in**, **ALTER in**oder **DELETE in**. Jede dieser Optionen kann für ein Fenster oder eine Datei gelten, aber unabhängig davon, wofür das Skript gilt, wird es in Form eines DDL-Skripts in einem XMLA-Wrapper erstellt. Ein großer Vorteil solcher Skripts ist, dass sie auf jedem Server ausgeführt werden können, auf den Sie sie verweisen. Namen in den Skripts können geändert werden, und sie können auf iterativer Basis zur Massenerstellung, Änderung oder zur Löschung von Objekten ausgeführt werden.  
  
 Objekte, die Sie schreiben können, schließen die Elemente einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank ein, einschließlich Datenquellen, Datenquellensichten, Cubes, Dimensionen, Miningstrukturen und Rollen.  
  
 Erforderliche Komponenten schließen ein Verständnis für XML for Analysis (XMLA) ein. Glücklicherweise verfügt [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] über eine Funktion, mit der das zum Erstellen von Objekten wie Cubes benötigte XMLA-Skript automatisch erstellt wird. Diese Automatisierungsfunktion erleichtert die Verwendung von XMLA. Weitere Informationen zur Verwendung von XMLA finden Sie unter [Entwickeln mit XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md). Weitere Informationen zur Verwendung von XMLA finden Sie unter [Entwickeln mit XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md).  
  
> [!IMPORTANT]  
>  Wenn Sie Skripts für das Role-Objekt erstellen, müssen Sie sich darüber bewusst sein, dass die Sicherheitsberechtigungen in den Objekten enthalten sind, die sie sichern, statt in der Sicherheitsrolle, der sie zugeordnet sind.  
  
#### <a name="to-script-analysis-services-objects"></a>So erstellen Sie Skripts für Analysis Services-Objekte  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung zu einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]her.  
  
2.  Suchen Sie das Objekt, für das Sie ein Skript zum Erstellen, Ändern oder Löschen von Objekten erstellen möchten.  
  
3.  Klicken Sie mit der rechten Maustaste auf das Objekt, zeigen Sie auf **Skript für Cube als**, zeigen Sie auf **CREATE in**, **ALTER in**oder **DELETE in**, und klicken Sie anschließend auf eine der folgenden Optionen: **Neues Abfrage-Editorfenster** zum Öffnen des Abfrage-Editorfensters, **Datei** zum Speichern des XMLA-Skripts in einer Datei oder **Zwischenablage** zum Speichern des XMLA-Skripts in der Zwischenablage.  
  
    > [!NOTE]  
    >  Normalerweise würden Sie **Datei** auswählen, wenn Sie mehrere verschiedene Versionen der Datei erstellen möchten.  
  
## <a name="see-also"></a>Siehe auch  
 [XMLA-Abfrage-Editor &#40; Analysis Services – mehrdimensionale Daten &#41;](http://msdn.microsoft.com/library/14623019-7839-4038-9d12-2f8953d2ec04)  
  
  

