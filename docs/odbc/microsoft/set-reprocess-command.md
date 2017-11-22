---
title: Die Verarbeitung wiederholen Befehl SET | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SET REPROCESS command [ODBC]
ms.assetid: b0708757-b1d7-42f3-8988-787f2a806b8b
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c8e907d01b79c314603ba87c8195e56c8710bd10
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="set-reprocess-command"></a>SET-Verarbeitung wiederholen-Befehl
Gibt an, wie viele Zeiten oder wie lang sein, um eine Datei oder ein Datensatz nach dem Versuch nicht erfolgreich Sperren zu sperren.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>Argumente  
 UM *nAttempts*[SECONDS]  
 Gibt die Häufigkeit oder die Anzahl der Sekunden, um zu versuchen, einen Datensatz oder eine Datei gesperrt wird, nachdem eine anfängliche fehlgeschlagenen versuchen. Der Standardwert ist 0; der Maximalwert ist 32.000.  
  
 Sekunden gibt an, dass Visual FoxPro Sperren einer Datei oder der Datensatz für *nAttempts* Sekunden. Es ist nur verfügbar, wenn *nAttempts* ist größer als 0 (null).  
  
 Z. B. wenn *nAttempts* = 30, Visual FoxPro versucht, einen Datensatz zu sperren oder die Datei bis zu 30 Mal. Wenn Sie auch die Sekunden (Legen Sie VERARBEITEN und 30 Sekunden) angeben, versucht Visual FoxPro fortlaufend, einen Datensatz oder eine Datei für bis zu 30 Sekunden zu sperren.  
  
 Wenn eine Routine ON ERROR aktiviert ist und versucht, die durch einen Befehl, der Datensätze oder eine Datei zu sperren, fehlgeschlagen sind, wird die ON ERROR-Routine ausgeführt. Eine Funktion, die Sperre versucht, eine Routine ON ERROR wird nicht ausgeführt, und die Funktion gibt "false" zurück (. F.).  
  
 Wenn eine ON ERROR-Routine nicht wirksam, ein Befehl versucht, den Datensatz bzw. die Datei zu sperren und die Sperre kann nicht platziert werden, wird ein Fehler generiert. Wenn eine Funktion versucht, die Sperre, die Warnung wird nicht angezeigt, und die Funktion gibt "false" zurück (. F.).  
  
 Wenn *nAttempts* ist 0 (Standardwert) und Sie veranlassen, einen Befehl oder Funktion, die versucht, einen Datensatz oder eine Datei zu sperren, Visual FoxPro versucht, den Datensatz zu sperren oder die Datei unbegrenzt. Wenn der Datensätze oder eine Datei verfügbar zu sperren, während Sie warten, die Sperre und die systemmeldung deaktiviert ist. Wenn eine Funktion versucht, die Sperre zu platzieren, die Funktion gibt "true" zurück (. T.).  
  
 Die ON ERROR-Routine hat Vorrang vor allen weitere Versuche, den Datensatz bzw. die Datei zu sperren, wenn eine Routine auf Fehler im Endeffekt dasselbe ist, und versucht, ein Befehl, der Datensätze oder eine Datei zu sperren, ist. Die ON ERROR-Routine wird sofort ausgeführt. Visual FoxPro wird nicht versucht, zusätzlichen Datensatz oder Dateisperren und die systemmeldung nicht angezeigt.  
  
 Wenn *nAttempts* 1, Visual FoxPro versucht, den Datensatz zu sperren oder die Datei auf unbestimmte Zeit und eine ON ERROR-Routine wird nicht ausgeführt.  
  
 Wenn eine Sperre, von einem anderen Benutzer auf den Datensatz bzw. die Datei, die Sie sperren möchten erteilt wurden, müssen Sie warten, bis der Benutzer die Sperre freigibt.  
  
 AUF AUTOMATISCH  
 Gibt an, dass Visual FoxPro versucht, den Datensatz zu sperren oder die Datei unbegrenzt. (Satz für die Aktualisierung-2 ist einen gleichwertigen Befehl).  
  
## <a name="remarks"></a>Hinweise  
 Der erste Versuch, einen Datensatz oder eine Datei zu Sperren nicht immer erfolgreich. In vielen Fällen ist ein Datensatz oder eine Datei von einem anderen Benutzer im Netzwerk gesperrt. Legen Sie erneut VERARBEITEN bestimmt, ob es sich bei Visual FoxPro macht zusätzliche versucht Zustandsdaten zu Sperren der Datensätze oder eine Datei, wenn der erste Versuch nicht erfolgreich ist. Sie können entweder Häufigkeit angeben, weitere Versuche werden oder für wie lange die Versuche gestellt werden. Eine ON ERROR-Routine wirkt sich auf wie fehlgeschlagenen Sperre Versuche behandelt werden.
