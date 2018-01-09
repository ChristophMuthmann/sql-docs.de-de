---
title: Python-Bibliotheken | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d2f1dcd37a9e620402e299565f920f479e206ae4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="python-libraries-and-data-types"></a>Python-Bibliotheken und Datentypen

In diesem Thema wird beschrieben, die Python-Bibliotheken, die in den folgenden Produkten enthalten sind:

+ SQL Server-Machine Learning-Services (Datenbankintern)
+ Microsoft-Machine Learning-Server (eigenständig)

In diesem Thema werden auch nicht unterstützte Datentypen aufgeführt, und listet die Konvertierung von Datentypen, die möglicherweise implizit durchgeführt werden, wenn die Daten zwischen Python und SQL Server übergeben werden.

## <a name="python-version"></a>Python-Version

SQL Server 2017 CTP 2.0 umfasst einen Teil der Anaconda-Verteilung und Python-3.6.

Eine Teilmenge der Funktionen "revoscaler" (RxLinMod RxLogit, RxPredict, RxDTrees, RxBTrees, vielleicht einige andere) wird über die Python-APIS, mit der ein neues Python-Paket bereitgestellt **RevoScalePy**. Sie können diese Pakete verwenden, zum Arbeiten mit Daten, die mit Pandas Data Frames. XDF-Dateien oder SQL-Datenabfragen.

Weitere Informationen finden Sie unter [Revoscalepy Neuerungen?](what-is-revoscalepy.md).

## <a name="python-and-sql-data-types"></a>Python und SQL-Datentypen

Python unterstützt eine begrenzte Anzahl von Datentypen im Vergleich zu SQL Server.

Daher bei Verwendung von Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Python-Skripts können Daten möglicherweise implizit konvertiert werden in einen kompatiblen Datentyp. Allerdings wird häufig eine genaue Konvertierung kann nicht ausgeführt werden automatisch und ein Fehler zurückgegeben.

Diese Tabelle enthält die implizite Konvertierungen, die bereitgestellt werden. Andere Datentypen werden nicht unterstützt.

|SQLtype|Python-Typ|
|-|-|
|**bigint**|`numeric`|
|**binary**|`raw`|
|**bit**|`bool`|
|**char**|`str`|
|**float**|`float64`|
|**int**|`int32`|
|**nchar**|`str`|
|**nvarchar**|`str`|
|**nvarchar(max)**|`str`|
|**real**|`float32`|
|**smallint**|`int16`|
|**tinyint**|`uint8`|
|**varbinary**|`bytes`|
|**varbinary(max)**|`bytes`|
|**varchar(n)**|`str`|
|**varchar(max)**|`str`|



