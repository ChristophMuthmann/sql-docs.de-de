---
title: MSSQLSERVER_8525 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- "8525"
helpviewer_keywords:
- 8525 (Database Engine error)
ms.assetid: 297867c1-691e-4d6b-a3be-a7575015ecfa
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3b465c4e4c7a7484413f93aa2bb547e9685297bd
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver8525"></a>MSSQLSERVER_8525
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|8525|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name||  
|Meldungstext|Die verteilte Transaktion wurde abgeschlossen. Tragen Sie diese Sitzung in eine neue Transaktion oder in die NULL-Transaktion ein.|  
  
## <a name="explanation"></a>Erklärung  
Für das Programmiermodell für die Verwendung des Distributed Transaction Coordinators mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sind Anwendungen zum expliziten Eintragen in und Austragen aus einer verteilten Transaktion erforderlich.  
  
Dieser Fehler tritt auf, wenn die folgenden vier Bedingungen erfüllt sind:  
  
-   Die Anwendung wurde in eine verteilte Transaktion eingetragen.  
  
-   Die Transaktion wurde aus irgendeinem Grund beendet (durch einen Commit oder ein Rollback).  
  
-   Die Benutzeranwendung wurde nicht explizit aus einer verteilten Transaktion ausgetragen oder explizit in eine neue verteilte Transaktion eingetragen.  
  
-   Die Anwendung versucht jeden anderen Transaktionsvorgang als das Austragen aus einer vorhandenen verteilten Transaktion oder das Eintragen in eine neue verteilte Transaktion, z. B. das Ausgeben einer Abfrage oder das Starten einer lokalen Transaktion.  
  
Der Fehlerzustand 1 wird verwendet, wenn die Anwendung einen Vorgang ausführt, mit dem lokale Transaktionen erstellt werden, und Status 2 wird verwendet, wenn die Anwendung versucht, eine Eintragung in eine gebundene Sitzung vorzunehmen.  
  
## <a name="user-action"></a>Benutzeraktion  
Nachdem eine Anwendung eine Eintragung in eine verteilte Transaktion vorgenommen hat, muss sich die Anwendung explizit aus der verteilten Transaktion austragen oder sich in eine andere verteilte Transaktion eintragen. Damit wird implizit ein Austritt aus einer vorherigen eingetragenen Transaktion vorgenommen. Informationen dazu, wie die genaue Syntax aus einer verteilten Transaktion ausgetragen oder in eine verteilte Transaktion eingetragen wird, finden Sie im Handbuch zur Programmierschnittstelle für die Anwendung.  
  

