---
title: "API-Referenz für SQL Server-Machine Learning-Services | Microsoft Docs"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1c776c43d66d01a2f721b5d3d8bc540741bf8b13
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---

# <a name="api-reference-for-sql-server-machine-learning-services"></a>API-Referenz für SQL Server-Machine Learning-Services

Dieser Artikel enthält Links zur Referenzdokumentation für den Machine learning-APIs, die von SQL Server verwendet. 

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Dienste

SQL Server nutzt größtenteils, die gleichen R und Python-Bibliotheken, die in Microsoft R Server und Microsoft Machine Learning-Server bereitgestellt werden. 

> [!NOTE]
> Dokumentation für alle APIs stammt aus dem Quellcode und ist nicht nach dem bearbeiteten.

## <a name="r"></a>R

+ ["Revoscaler"](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)

    Skalierbare Algorithmen, die remote rechenkontexte und mehrere Datenquellen zu unterstützen.

+ [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)

    Schnelle, skalierbare den Machine learning-Algorithmen und Transformationen für r erfordert "revoscaler".

+ [olapR](https://docs.microsoft.com/r-server/r-reference/olapr/olapr)

   Liest das Schema der OLAP-Datenquellen und MDX-Abfragen ausgeführt.

+ [sqlrutils](https://docs.microsoft.com/r-server/r-reference/sqlrutils/sqlrutils)

    Hilfsfunktionen für eine wohlgeformte gespeicherte Prozedur aus R-Code generiert.

+ [mrsdeploy](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package)

   Funktionen, die zum Einrichten einer remote-Sitzungs in einer Konsolenanwendung und zum Veröffentlichen und Verwalten von einem Webdienst, der r oder Python-Code verwendet.

## <a name="python"></a>Python

+ [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)

    Python-Entsprechung von "revoscaler"-Paket für die Sprache "R". Unterstützt die gleichen Compute-Kontexte und Datenquellen.

+ [Microsoftml für Python](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)

    Python entspricht der MicrosoftML-Paket für r unterstützt die gleichen rechenkontexte und Datenquellen und umfasst schnelle, skalierbare Algorithmen und Transformationen von Microsoft.

## <a name="related-apis"></a>Verwandte APIs

+ [RevoPEMAR-Funktionsreferenz](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

    Unterstützt die Entwicklung von parallelen Algorithmen

+ [RevoUtils](https://docs.microsoft.com/r-server/r-reference/revoutils/revoutils)

    Hilfsfunktionen für die Verwendung mit "revoscaler"-Umgebungen

## <a name="other"></a>Andere

"Vorgehensweisen" und Zusammenfassungen, die speziell für das Verwenden dieser R oder Python-APIs in SQL Server finden Sie hier:

+ [ScaleR-Funktionen zum Arbeiten mit SQL Server](scaler-functions-for-working-with-sql-server-data.md)
+ [Generieren Sie eine gespeicherte Prozedur mit sqlrutils](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
+ [MDX-Daten in R über OlapR lesen](how-to-create-mdx-queries-using-olapr.md)

