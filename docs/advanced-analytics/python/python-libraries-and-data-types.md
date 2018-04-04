---
title: Python-Bibliotheken | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 70156a6b4d443c54f9b6244e5491da63ce345198
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="python-libraries-and-data-types"></a>Python-Bibliotheken und Datentypen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel beschreibt die Python-Bibliotheken, die in den folgenden Produkten enthalten sind:

+ SQL Server-Machine Learning-Services (Datenbankintern)
+ Microsoft-Machine Learning-Server (eigenständig)

In diesem Artikel werden auch nicht unterstützte Datentypen aufgeführt, und listet die Konvertierung von Datentypen, die möglicherweise implizit durchgeführt werden, wenn die Daten zwischen Python und SQL Server übergeben werden.

## <a name="python-version"></a>Python-Version

SQL Server 2017 CTP 2.0 umfasst einen Teil der Anaconda-Verteilung und Python-3.6.

Eine Teilmenge der Funktionen "revoscaler" (RxLinMod RxLogit, RxPredict, RxDTrees, RxBTrees, vielleicht einige andere) wird über die Python-APIs, mit der ein neues Python-Paket bereitgestellt **Revoscalepy**. Sie können dieses Paket verwenden, arbeiten mit Daten, die mit Pandas Datenrahmen, XDF-Dateien oder SQL-Datenabfragen.

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



