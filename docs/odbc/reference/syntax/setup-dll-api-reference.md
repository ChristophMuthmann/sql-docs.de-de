---
title: Setup-DLL-API-Referenz | Microsoft Docs
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
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: f9d03f17-1c0d-4e7c-9c04-8c316e07ef25
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa09dad7423a56db064ade504f3b6598f3daf4ff
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setup-dll-api-reference"></a>Setup-DLL-API-Referenz
Dieser Abschnitt beschreibt die Syntax der Setup-Treiber-DLL-API besteht aus zwei Funktionen (**ConfigDriver** und **ConfigDSN**). **ConfigDriver** und **ConfigDSN** können entweder im Treiber-DLL oder richten Sie in einer separaten DLL.  
  
 Darüber hinaus wird in diesem Abschnitt beschrieben, die Syntax der Konvertierer Setup-DLL-API, die aus einer einzelnen Funktion besteht (**ConfigTranslator**). **ConfigTranslator** können entweder in das DLL-Konvertierungsprogramm oder richten Sie in einer separaten DLL.  
  
 Jede Funktion ist mit der ODBC-Version mit der Bezeichnung eingeführt wurde.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [ConfigDriver-Funktion](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [ConfigDSN-Funktion](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [ConfigTranslator-Funktion](../../../odbc/reference/syntax/configtranslator-function.md)
