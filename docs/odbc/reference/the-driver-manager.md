---
title: Der Treiber-Manager | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC]
- ODBC architecture [ODBC], driver manager
- driver manager [ODBC], about driver manager
- ODBC driver manager [ODBC]
ms.assetid: 559e4de1-16c9-4998-94f5-6431122040cd
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d31dbfce3f5c5e3b09f43ec9a644e415b6d82d22
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="the-driver-manager"></a>Der Treiber-Manager
Die *Treibermanager* ist eine Bibliothek, die Kommunikation zwischen Anwendungen und-Treiber verwaltet. Beispielsweise ist der Treiber-Manager für Microsoft® Windows®-Plattformen eine Dynamic Link Library (DLL), die von Microsoft geschrieben und kann von Benutzern das verteilbare MDAC 2.8 SP1 SDK verteilt werden.  
  
 Der Treiber-Manager vorhanden ist, vor allem als Annehmlichkeit zum Anwendungsentwickler und löst eine Reihe von Problemen, die für alle Anwendungen. Dazu gehören bestimmen, welcher Treiber laden auf einen Datenquellennamen basieren, laden und Entladen von Treibern und Aufrufen von Funktionen in Treiber.  
  
 Um festzustellen, warum die zweite Datei ein Problem aufgetreten ist, erwägen Sie, was passieren würde, wenn die Anwendung Funktionen im Treiber direkt aufgerufen. Wenn die Anwendung direkt an einen bestimmten Treiber verknüpft wurde, müssen Sie eine Tabelle von Zeigern auf Funktionen in diesen Treiber zu erstellen und diese Funktionen durch Zeiger aufgerufen. Mithilfe des gleichen Codes für mehr als einen Treiber zu einem Zeitpunkt würde noch ein anderes Maß an Komplexität hinzufügen. Die Anwendung zuerst einen Funktionszeiger, zeigen Sie auf die ordnungsgemäße Funktion in der richtige Treiber festgelegt haben, und rufen Sie anschließend die Funktion über diesen Zeiger.  
  
 Der Treiber-Manager löst dieses Problem durch Bereitstellen eines einzelnen jede Funktion aufrufen. Die Anwendung wird mit Treiber-Manager und ruft ODBC-Funktionen der Treiber-Manager nicht auf den Treiber verknüpft. Die Anwendung identifiziert den Ziel-Treiber und die Datenquelle mit einem *Verbindungshandle*. Wenn sie einen Treiber geladen wird, erstellt der Treiber-Manager eine Tabelle von Zeigern auf Funktionen in diesen Treiber. Wird mit dem Verbindungshandle, die von der Anwendung übergebenen finden die Adresse der Funktion im Zieltreiber und die Adresse dieser Funktion aufgerufen.  
  
 Den meisten Fällen übergibt der Treiber-Manager nur Funktionsaufrufe von der Anwendung an den richtigen Treiber. Allerdings es implementiert auch einige Funktionen (**SQLDataSources**, **SQLDrivers**, und **SQLGetFunctions**) und führt grundlegende fehlerüberprüfung. Beispielsweise überprüft der Treiber-Manager, dass Handles keine null-Zeiger sind, dass Funktionen in der richtigen Reihenfolge aufgerufen werden und bestimmte Funktionsargumente gültig sind. Eine vollständige Beschreibung der Fehler vom Treiber-Manager überprüft werden soll, finden Sie im Verweisabschnitt "für jede Funktion und [Anhang B: ODBC-Übergang-Statustabellen](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Der letzte wichtige Rolle des Treiber-Managers ist laden und Entladen von Treibern. Die Anwendung geladen und entladen wird nur der Treiber-Manager. Wenn sie einen bestimmten Treiber verwenden möchte, ruft er eine Verbindungsfunktion (**SQLConnect**, **SQLDriverConnect**, oder **SQLBrowseConnect**) im Treiber-Manager und gibt an, der Name einer bestimmten Datenquelle oder Treiber verwenden, z. B. "Finanzwesen" oder "SQLServer". Verwenden diesen Namen, sucht der Treiber-Manager die Datenquelleninformationen für Dateinamen des Treibers, z. B. SQLSRVR. Anschließend lädt den Treiber (vorausgesetzt, dass sie nicht bereits geladen wurde), speichert die Adresse für jede Funktion in der Treiber, und ruft die Verbindungsfunktion im Treiber, die dann selbst initialisiert und eine Verbindung mit der Datenquelle her.  
  
 Wenn die Anwendung erfolgt mit dem Treiber, ruft er **SQLDisconnect** im Treiber-Manager. Der Treiber-Manager ruft diese Funktion in den Treiber, der eine Verbindung mit der Datenquelle trennt. Der Treiber-Manager behält jedoch die Treiber im Arbeitsspeicher für den Fall, dass die Anwendung, erneut eine Verbindung herstellt. Den Treiber entladen nur, wenn die Anwendung gibt die Verbindung vom Treiber verwendet wird, oder für einen anderen Treiber die Verbindung verwendet und keine weiteren Verbindungen verwenden Sie den Treiber. Eine vollständige Beschreibung der Treiber-Manager-Rolle in laden und Entladen von Treibern, finden Sie unter [Treiber-Manager-Rolle in der Verbindungsprozess](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md).
