---
title: SQLInstallTranslator Zuordnung | Microsoft Docs
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
- SQLInstallTranslator function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLInstallTranslator
ms.assetid: bcd9ba4f-7834-4bc4-876e-c7478998e524
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5de97b141f7ea2d1e3acf828f7d1b25bd77e0de7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator-Zuordnung
Wenn eine ODBC-2. *x* Anwendung ruft **SQLInstallTranslator** über einen ODBC 3.*.x* Treiber, der Treiber-Manager ordnet den Aufruf von **SQLInstallTranslatorEx**. Eine Anwendung sollte nicht aufrufen **SQLInstallTranslator** in die ODBC 3.*.x* Treiber-Manager mit der *LpszInfFile* Argument auf einen anderen Wert als NULL festgelegt. Der ODBC. INF-Datei in ODBC 2. verwendet. *x* wird nicht mehr unterstützt, in ODBC 3.*.x*, dies gilt auch für die Abwärtskompatibilität.
