---
title: Zeile Statusarray | Microsoft Docs
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
- row status array [ODBC]
- cursors [ODBC], block
- result sets [ODBC], row status array
- block cursors [ODBC]
- result sets [ODBC], block cursors
- rowset status [ODBC]
ms.assetid: 4b69f189-2722-4314-8a02-f4ffecd6dabd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b2c45b2dc5ea9326b5ae3b229a17c13207edcabc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="row-status-array"></a>Zeilenstatusarray
Zusätzlich zu den Daten **SQLFetch** und **SQLFetchScroll** kann ein Array, das den Status der einzelnen Zeilen im Rowset bietet zurückgeben. Dieses Array wird durch das SQL_ATTR_ROW_STATUS_PTR-Anweisungsattribut festgelegt. Dieses Array muss wird von der Anwendung zugeordnet und so viele Elemente wie vom Attribut SQL_ATTR_ROW_ARRAY_SIZE-Anweisung angegeben werden. Die vom festgelegten Werte im Array **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, und **SQLSetPos.** Die Werte beschreibt den Status der Zeile und gibt an, ob dieser Status seit dem letzten Abruf geändert hat.  
  
|Array-Statuswert Zeile|Description|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|Die Zeile wurde erfolgreich abgerufen und seit dem letzten Abruf nicht geändert.|  
|SQL_ROW_SUCCESS_WITH_INFO|Die Zeile wurde erfolgreich abgerufen und seit dem letzten Abruf nicht geändert. Allerdings wurde eine Warnung zur Zeile zurückgegeben.|  
|SQL_ROW_ERROR|Fehler beim Abrufen einer Zeile.|  
|SQL_ROW_UPDATED|Die Zeile wurde erfolgreich abgerufen und wurde seit dem letzten Abruf wurde aktualisiert. Wenn die Zeile erneut abgerufen oder werden, indem aktualisiert **SQLSetPos**, dessen Status auf den neuen Status geändert wird.<br /><br /> Einige Treiber können keine Änderungen an den Daten erkennen und aus diesem Grund können dieser Wert zurückgeben. Um zu bestimmen, ob ein Treiber Updates von Zeilen erneut abgerufen erkannt werden kann, eine Anwendung ruft **SQLGetInfo** mit der Option SQL_ROW_UPDATES.|  
|SQL_ROW_DELETED|Die Zeile wurde seit dem letzten Abruf wurde gelöscht.|  
|SQL_ROW_ADDED|Die Zeile eingefügt wurde, indem **SQLBulkOperations**. Wenn die Zeile erneut abgerufen oder, durch aktualisiert wird **SQLSetPos**, ihr Status wird SQL_ROW_SUCCESS.<br /><br /> Dieser Wert ist nicht festgelegt, indem **SQLFetch** oder **SQLFetchScroll**.|  
|SQL_ROW_NOROW|Das Rowset überlappt, das Ende des Resultsets und, dass, die auf dieses Element des Arrays Status Zeile zugestimmt haben, wurde keine Zeile zurückgegeben.|
