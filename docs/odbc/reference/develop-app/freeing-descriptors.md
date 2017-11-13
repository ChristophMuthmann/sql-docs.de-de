---
title: Freigeben von Deskriptoren | Microsoft Docs
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
- SQLFreeHandle function [ODBC]
- descriptors [ODBC], allocating and freeing
- freeing descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 317213f4-0ebb-4bf8-a37a-4d6b1313823f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d1c70c82196907fc0bd9747a8ece089d4e4ab514
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="freeing-descriptors"></a>Freigeben von Deskriptoren
Können explizit zugewiesene Deskriptoren reserviert, entweder explizit durch Aufrufen von **SQLFreeHandle** mit *HandleType* SQL_HANDLE_DESC oder implizit, wenn das Verbindungshandle freigegeben. Wenn ein explizit reservierte Deskriptor freigegeben wird, alle Anweisungshandles auf die freigegebenen Deskriptors automatisch angewendet, die auf die Deskriptoren implizit für sie reservierten zurückgesetzt.  
  
 Implizit zugeordnete Deskriptoren freigegeben werden können, nur durch das Aufrufen **SQLDisconnect**, dem löscht alle Anweisungen oder Deskriptoren zu öffnen, für die Verbindung oder durch Aufrufen von **SQLFreeHandle** mit einem  *HandleType* von SQL_HANDLE_STMT auf, um ein Anweisungshandle und alle der Anweisung zugeordneten implizit zugeordneten Deskriptoren freizugeben. Eine implizit zugeordnete Sicherheitsbeschreibung nicht freigegeben werden, durch den Aufruf **SQLFreeHandle** mit einem *HandleType* von SQL_HANDLE_DESC.  
  
 Ein implizit zugeordneten Deskriptor bleibt gültig, sogar wenn freigegeben, und **SQLGetDescField** für ihre Felder aufgerufen werden kann.

