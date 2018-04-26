---
title: Datenquellen-Steuerelement in der SQL-Vorgänge Studio (Vorschau) | Microsoft Docs
description: Informationen Sie zum Konfigurieren von Datenquellen-Steuerelement in der SQL-Vorgänge Studio (Vorschau).
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 73fec13868004469b02f3117b9b8d70e1ec26ff3
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
#  <a name="using-source-control-in-includename-sosincludesname-sos-shortmd"></a>Mithilfe der quellcodeverwaltung in [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] unterstützt Git für die Version/Datenquellen-Steuerelements an.


## <a name="git-support-in-includename-sosincludesname-sos-shortmd"></a>Git-Unterstützung in [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] umfasst eine Git Source Control-Manager (SCM), aber Sie müssen dennoch [installieren Sie Git (Version 2.0.0 oder höher)](https://git-scm.com/download) , bevor diese Funktionen verfügbar sind. 



## <a name="open-an-existing-git-repository"></a>Öffnen Sie ein vorhandenes Git-repository

1. Klicken Sie unter der **Datei** klicken Sie im Menü **Ordner öffnen...**
2. Navigieren Sie zum Ordner mit den Dateien vom Git nachverfolgt werden, und klicken Sie auf **Ordner auswählen**. Unterordner in Ihr lokales Repository sind angemessen, hier auswählen.


## <a name="initialize-a-new-git-repository"></a>Initialisiert ein neue Git-repository

1. Wählen Sie **Quellcodeverwaltung**, wählen Sie das Git-Symbol.

   ![Git-Symbol für Datenquellen-Steuerelement](media/source-control/source-control.png)

1. Geben Sie den Pfad zu dem Ordner, die Sie als ein Git-Repository und drücken Sie initialisieren möchten **EINGABETASTE**.

   ![Initialisieren von Git-repository](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>Arbeiten mit Git-Repositorys

[!INCLUDE[name-sos](../includes/name-sos-short.md)] erbt von der Git-Implementierung von VS-Code, aber zusätzliche SCM-Anbieter wird derzeit nicht unterstützt. Ausführliche Informationen zum Arbeiten mit Git, nach dem Öffnen oder ein Repository zu initialisieren, finden Sie unter [Git-Unterstützung in Visual Studio Code](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support).


## <a name="additional-resources"></a>Weitere Ressourcen
- [Git-Dokumentation](https://git-scm.com/documentation)
