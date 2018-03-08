---
title: "Verhaltensänderungen und ODBC 3.x-Treibern | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sql_attr_odbc_version [ODBC]
- backward compatibility [ODBC], behavioral changes
- compatibility [ODBC], behavioral changes
ms.assetid: 88a503cc-bff7-42d9-83ff-8e232109ed06
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dc06520b8dcf2fe5686d041e1c48e50cf5555b79
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>Verhaltensänderungen und ODBC 3.x-Treiber
Das Attribut der Umgebung überprüfen, ob SQL_ATTR_ODBC_VERSION an den Treiber ODBC 2. aufweisen muss. *x* Verhalten oder die ODBC 3.*.x* Verhalten. Wie das SQL_ATTR_ODBC_VERSION Umgebung-Attribut festgelegt ist, hängt von der Anwendung ab. ODBC 3.*.x* Anwendungen müssen Aufrufen **SQLSetEnvAttr** dieses Attribut festgelegt, nachdem sie rufen **SQLAllocHandle** ein Umgebungshandle und vor dem Aufruf von  **SQLAllocHandle** ein Verbindungshandle zuordnen. Wenn sie nicht dazu, gibt der Treiber-Manager SQLSTATE HY010 (Funktion Sequenzfehler) beim letzten Aufruf von **SQLAllocHandle**.  
  
> [!NOTE]  
>  Weitere Informationen zu verhaltensänderungen und wie eine Anwendung fungiert, finden Sie unter [Verhaltensänderungen](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 ODBC-2. *x* Anwendungen und ODBC 2.. *X* Anwendungen neu kompiliert, mit der ODBC 3.*.x* Headerdateien rufen nicht **SQLSetEnvAttr**. Allerdings rufen sie **SQLAllocEnv** anstelle von **SQLAllocHandle** ein Umgebungshandle zuordnen. Daher, wenn die Anwendung ruft **SQLAllocEnv** der Treiber-Manager der Treiber-Manager ruft **SQLAllocHandle** und **SQLSetEnvAttr** im Treiber. Folglich ODBC 3.*.x* Treiber immer Zuständen dieses Attribut festgelegt wird.  
  
 Wenn eine mit Standards kompatible Anwendung mit dem Flag "ODBC_STD Kompilierung" Aufrufe kompiliert **SQLAllocEnv** (die möglicherweise auftreten, da **SQLAllocEnv** nicht veraltetes Feature in ISO), wird der Aufruf zugeordnet  **SQLAllocHandleStd** zum Zeitpunkt der Kompilierung. Zur Laufzeit ruft die Anwendung **SQLAllocHandleStd**. Der Treiber-Manager wird das SQL_ATTR_ODBC_VERSION Umgebung-Attribut auf SQL_OV_ODBC3 fest. Ein Aufruf von **SQLAllocHandleStd** ist gleichbedeutend mit einem Aufruf von **SQLAllocHandle** mit einem *HandleType* SQL_HANDLE_ENV und einem Aufruf von **SQLSetEnvAttr** SQL_ATTR_ODBC_VERSION auf SQL_OV_ODBC3 festgelegt.  
  
 Bestimmten Treiber-Architekturen ist eine erforderlich für den Treiber als ein ODBC-2 angezeigt werden. *x* Treiber oder ein ODBC 3.*.x* -Treiber verwenden, abhängig von der die Verbindung. Der Treiber in diesem Fall nicht tatsächlich möglicherweise einen Treiber jedoch eine Ebene, die zwischen der Treiber-Manager und ein anderer Treiber befindet. Es kann z. B. einen Treiber, wie ODBC Spy++ imitieren. In einem anderen Beispiel könnte es als Gateway, wie EDA/SQL fungieren. Als ein ODBC 3. angezeigt werden*.x* -Treiber verwenden, ein solchen Treibers muss vorliegen exportieren **SQLAllocHandle**, und als ein ODBC-2 angezeigt werden. *X* -Treiber verwenden, müssen in der Lage, exportieren **SQLAllocConnect**, **SQLAllocEnv**, und **SQLAllocStmt:**. Wenn eine Umgebung, die Verbindung oder die Anweisung ist zugeordnet werden soll, der Treiber-Manager überprüft, um festzustellen, ob dieser Treiber exportiert **SQLAllocHandle**. Da der Treiber der Fall ist, der Treiber-Manager ruft **SQLAllocHandle** im Treiber. Wenn der Treiber mit einer ODBC 2. arbeitet. *x* -Treiber verwenden, muss der Treiber den Aufruf von zuordnen **SQLAllocHandle** auf **SQLAllocConnect**, **SQLAllocEnv**, oder  **SQLAllocStmt:**je nach Bedarf. Sie müssen außerdem nichts mit der **SQLSetEnvAttr** aufgerufen wird, wenn Sie als ein ODBC 2. verhält. *X* Treiber.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [datetime-Datentyp](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [Abwärtskompatibilität von C-Datentypen](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [Lesezeichen mit fester Länge](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [SQLGetInfo-Unterstützung](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [Rückgabe von SQL_NO_DATA](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [Calling SQLSetPos to Insert Data (Aufrufen von SQLSetPos zum Einfügen von Daten)](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [Laden nach Ordnungszahl](../../../odbc/reference/appendixes/loading-by-ordinal.md)
