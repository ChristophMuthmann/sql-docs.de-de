---
title: "Übersicht über das Befehl | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- command object [ADO]
ms.assetid: e84a14b1-3c2a-4f7d-a966-9e08a93948df
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 175c3793a41c4502a0c558c63e4eec89b35cd02f
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="command-object-overview"></a>Command-Objekte (Übersicht)
Mit einem **Befehl** Objekt ist, können Sie wie folgt vorgehen:  
  
-   Definieren Sie die ausführbare Datei Text des Befehls (z. B. eine SQL-Anweisung oder eine gespeicherte Prozedur) mithilfe der **CommandText** Eigenschaft.  
  
-   Definieren Sie parametrisierte Abfragen oder gespeicherte Prozedurargumente mit **Parameter** Objekte und die **Parameter** Auflistung.  
  
-   Ausführen ein Befehls und zum Zurückgeben einer **Recordset** Objekt, falls zutreffend, mithilfe der **Execute** Methode.  
  
-   Geben Sie den Befehl unter Verwendung der **CommandType** Eigenschaft vor der Ausführung, um die Leistung zu optimieren.  
  
-   Geben Sie spezifische Informationen zu den Befehlstext mithilfe der **Dialekt** Eigenschaft von der **Befehl** Objekt.  
  
-   Steuern, ob der Anbieter eine vorbereitete (oder kompilierte) Version des Befehls vor der Ausführung mit speichert die **Prepared** Eigenschaft.  
  
-   Legen Sie die Anzahl der Sekunden, die ein Anbieter für einen Befehl zum Ausführen mit wartet der **CommandTimeout** Eigenschaft.  
  
-   Ordnen Sie eine offene Verbindung mit einer **Befehl** Objekt durch Festlegen seiner **ActiveConnection** Eigenschaft.  
  
-   Legen Sie die **Namen** Eigenschaft zum Identifizieren der **Befehl** als Methode für das zugeordnete Objekt **Verbindung** Objekt.  
  
-   Übergeben einer **Befehl** -Objekt an die **Quelle** Eigenschaft eine **Recordset** um Daten zu erhalten.  
  
-   Übergeben Sie eine **Stream** Objekt, das an einen Anbieter, die er unterstützt einen Befehl (z. B. eine XML-Befehl) enthält.
