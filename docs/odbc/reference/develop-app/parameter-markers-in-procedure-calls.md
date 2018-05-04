---
title: Parametermarkierungen in Prozeduraufrufen | Microsoft Docs
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
- SQL statements [ODBC], interoperability
- parameter markers [ODBC]
- interoperability of SQL statements [ODBC], parameter markers
ms.assetid: cda56f2b-6eec-4cbc-8dbb-36d8fa9f9216
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d21de0ce752296e1534b01c197f18934862eec85
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="parameter-markers-in-procedure-calls"></a>Parametermarkierungen in Prozeduraufrufen
Beim Aufrufen von Prozeduren, die Parameter akzeptieren, sollten interoperable Anwendungen ausführen parametermarkierungen anstelle von literalen Parameterwerte verwenden. Einige Datenquellen unterstützen nicht die Verwendung von literalen Parameterwerte in Prozeduraufrufen. Weitere Informationen zu Parametern finden Sie unter [Anweisungsparametern](../../../odbc/reference/develop-app/statement-parameters.md). Weitere Informationen über das Aufrufen von Prozeduren finden Sie unter [Prozeduraufrufe](../../../odbc/reference/develop-app/procedure-calls.md)weiter unten in diesem Abschnitt.
