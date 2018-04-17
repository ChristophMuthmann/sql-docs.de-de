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
ms.topic: article
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
ms.workload: Inactive
ms.openlocfilehash: cbd15cc8f2fc51d8d3c85269aad2854692ee966d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator-Funktion
**Konformität**  
 Version eingeführt: ODBC 2.5 veraltet  
  
 **Zusammenfassung**  
 In ODBC 3.0 **SQLInstallTranslator** wurde ersetzt durch [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md). Aufrufe von **SQLInstallTranslator** zugeordnet **SQLInstallTranslatorEx**. Weitere Informationen finden Sie unter **SQLInstallTranslatorEx**.  
  
 **SQLInstallTranslator** gibt "false" zurück, wenn eine Anwendung in der ODBC-3 ruft*.x* Treiber-Manager mit der *LpszInfFile* Argument auf einen anderen Wert als NULL festgelegt. Die Odbc.inf-Datei in ODBC 2. verwendet. *x* wird nicht mehr unterstützt, in ODBC 3.*.x*, dies gilt auch für die Abwärtskompatibilität.
