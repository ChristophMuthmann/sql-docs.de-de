---
title: -Verwaltungsprogramm | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- administration program [ODBC]
- ODBC administrator [ODBC]
ms.assetid: a6c8248a-7a01-42e7-aaed-99dc94d50028
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 476c4710a4265214235bdd7b80a330fad5b37f34
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="administration-program"></a>-Verwaltungsprogramm
> [!NOTE]  
>  Ab Windows XP und Windows Server 2003, ist ODBC in der Windows-Betriebssystem enthalten. Sie sollten nur explizit ODBC in früheren Versionen von Windows installieren.  
  
 Eine ODBC-Administrator-Verwaltungsprogramms ist im Windows SDK/MDAC SDK enthalten. Dieses Programm und kann von Benutzern des SDK verteilt werden. Darüber hinaus können Entwickler ihre eigenen Verwaltungsprogrammen schreiben. Im Allgemeinen schreiben Entwickler eigene Verwaltungsprogrammen nur, wenn sie vollständige Kontrolle über die Datenquellenkonfiguration beibehalten werden soll, oder wenn sie Datenquellen direkt von einer Anwendung konfigurieren, die als Verwaltungsprogramm dient. Ein Tabellenkalkulationsprogramm kann z. B. Benutzer hinzufügen und verwenden Sie Datenquellen zur Laufzeit ermöglichen.  
  
 Das Verwaltungsprogramm lädt zuerst das Installationsprogramm DLL. Er ruft dann die Funktionen im Installationsprogramm DLL-Datei die folgenden Aufgaben ausführen:  
  
-   **Hinzufügen, ändern oder Löschen von Datenquellen interaktiv.** Rufen Sie das Verwaltungsprogramm kann **SQLManageDataSources**, **SQLCreateDataSource**, oder **SQLConfigDataSource**.  
  
     **SQLManageDataSources** zeigt ein Dialogfeld, mit denen der Benutzer kann hinzufügen, ändern oder Löschen von Datenquellen und Ablaufverfolgungsoptionen angeben; diese Funktion wird aufgerufen, wenn das Installationsprogramm DLL direkt in der Systemsteuerung aufgerufen wird. **SQLCreateDataSource** zeigt ein Dialogfeld, mit denen der Benutzer nur von Datenquellen hinzufügen kann, an. **SQLConfigDataSource** übergibt den Aufruf direkt an den Treiber-Setup-DLL.  
  
     In allen Fällen ruft der Installer DLL **ConfigDSN** in der Treiber-Setup-DLL, tatsächlich hinzuzufügen, ändern oder löschen Sie die Datenquelle. Der Setup-DLL für Treiber möglicherweise zusätzliche Informationen vom Benutzer aufgefordert.  
  
-   **Hinzufügen, ändern oder Löschen von Datenquellen im Hintergrund.** Ruft die Administration **SQLConfigDataSource** in der DLL-Installer und übergibt es ein null-Fenster zu behandeln, den Namen einer Datenquelle hinzufügen, ändern oder löschen und eine Liste von Werten für die Registrierung. Der Installer DLL ruft **ConfigDSN** in der Treiber-Setup-DLL, tatsächlich hinzuzufügen, ändern oder löschen Sie die Datenquelle.  
  
-   **Hinzufügen, ändern oder Löschen einer Standard-Datenquelle.** Die Standarddatenquelle ist identisch mit einer anderen Datenquelle, mit dem Unterschied, dass standardmäßig ist der Anzeigename. Es wird hinzugefügt, geändert oder gelöscht werden, auf die gleiche Weise wie jede andere Datenquelle.

