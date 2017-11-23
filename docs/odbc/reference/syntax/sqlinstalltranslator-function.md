---
title: SQLInstallTranslator Funktion | Microsoft Docs
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
apiname: SQLInstallTranslator
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLInstallTranslator
helpviewer_keywords: SQLInstallTranslator function [ODBC]
ms.assetid: 453b21ff-3c2b-4069-8ff7-5c727f062d89
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ef9452b9ff442ec5ed40b7eb38957936d31d16b5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator-Funktion
**Konformität**  
 Version eingeführt: ODBC 2.5 veraltet  
  
 **Zusammenfassung**  
 In ODBC 3.0 **SQLInstallTranslator** wurde ersetzt durch [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md). Aufrufe von **SQLInstallTranslator** zugeordnet **SQLInstallTranslatorEx**. Weitere Informationen finden Sie unter **SQLInstallTranslatorEx**.  
  
 **SQLInstallTranslator** gibt "false" zurück, wenn eine Anwendung in der ODBC-3 ruft*.x* Treiber-Manager mit der *LpszInfFile* Argument auf einen anderen Wert als NULL festgelegt. Die Odbc.inf-Datei in ODBC 2. verwendet. *x* wird nicht mehr unterstützt, in ODBC 3.*.x*, dies gilt auch für die Abwärtskompatibilität.
