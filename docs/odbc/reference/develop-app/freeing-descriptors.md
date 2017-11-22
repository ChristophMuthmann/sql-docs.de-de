---
title: Freigeben von Deskriptoren | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
- descriptors [ODBC], allocating and freeing
- freeing descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 317213f4-0ebb-4bf8-a37a-4d6b1313823f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f951b69af4ecc18dc1dcdc23d0cbd1ce115caf0b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="freeing-descriptors"></a>Freigeben von Deskriptoren
Können explizit zugewiesene Deskriptoren reserviert, entweder explizit durch Aufrufen von **SQLFreeHandle** mit *HandleType* SQL_HANDLE_DESC oder implizit, wenn das Verbindungshandle freigegeben. Wenn ein explizit reservierte Deskriptor freigegeben wird, alle Anweisungshandles auf die freigegebenen Deskriptors automatisch angewendet, die auf die Deskriptoren implizit für sie reservierten zurückgesetzt.  
  
 Implizit zugeordnete Deskriptoren freigegeben werden können, nur durch das Aufrufen **SQLDisconnect**, dem löscht alle Anweisungen oder Deskriptoren zu öffnen, für die Verbindung oder durch Aufrufen von **SQLFreeHandle** mit einem  *HandleType* von SQL_HANDLE_STMT auf, um ein Anweisungshandle und alle der Anweisung zugeordneten implizit zugeordneten Deskriptoren freizugeben. Eine implizit zugeordnete Sicherheitsbeschreibung nicht freigegeben werden, durch den Aufruf **SQLFreeHandle** mit einem *HandleType* von SQL_HANDLE_DESC.  
  
 Ein implizit zugeordneten Deskriptor bleibt gültig, sogar wenn freigegeben, und **SQLGetDescField** für ihre Felder aufgerufen werden kann.
