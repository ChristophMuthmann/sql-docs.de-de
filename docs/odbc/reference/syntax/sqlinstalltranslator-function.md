---
title: SQLInstallTranslator Funktion | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLInstallTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslator
helpviewer_keywords:
- SQLInstallTranslator function [ODBC]
ms.assetid: 453b21ff-3c2b-4069-8ff7-5c727f062d89
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 36e1c76e85aec665e8b9554a305ccef0444d27f3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator-Funktion
**Konformität**  
 Version eingeführt: ODBC 2.5 veraltet  
  
 **Zusammenfassung**  
 In ODBC 3.0 **SQLInstallTranslator** wurde ersetzt durch [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md). Aufrufe von **SQLInstallTranslator** zugeordnet **SQLInstallTranslatorEx**. Weitere Informationen finden Sie unter **SQLInstallTranslatorEx**.  
  
 **SQLInstallTranslator** gibt "false" zurück, wenn eine Anwendung in der ODBC-3 ruft *.x* Treiber-Manager mit der *LpszInfFile* Argument auf einen anderen Wert als NULL festgelegt. Die Odbc.inf-Datei in ODBC 2. verwendet. *x* wird nicht mehr unterstützt, in ODBC 3.*.x*, dies gilt auch für die Abwärtskompatibilität.
