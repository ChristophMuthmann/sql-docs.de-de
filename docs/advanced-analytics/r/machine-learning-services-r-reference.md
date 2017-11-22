---
title: "API-Referenz für SQL Server-Machine Learning-Services | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 52261d7ebb01ca4156d067ba0f25af3cd90a64bb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="api-reference-for-sql-server-machine-learning-services"></a>API-Referenz für SQL Server-Machine Learning-Services

Dieser Artikel enthält Links zur Referenzdokumentation für den Machine learning-APIs, die von SQL Server verwendet.

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Dienste

SQL Server nutzt größtenteils, die gleichen R und Python-Bibliotheken, die in Microsoft R Server und Microsoft Machine Learning-Server bereitgestellt werden. 

> [!NOTE]
> Dokumentation für alle APIs stammt aus dem Quellcode und nicht bearbeitet wurde. Wenn Fehler angezeigt wird, fügen Sie einen Kommentar in der API-Referenz-Dokumentation hinzu. 

## <a name="r"></a>R

+ [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)

    Skalierbare Algorithmen, die remote rechenkontexte und mehrere Datenquellen zu unterstützen.

+ [MicrosoftML](https://docs.microsoft.com/machine-learning-serverr-reference/microsoftml/microsoftml-package)

    Schnelle, skalierbare den Machine learning-Algorithmen und Transformationen für r erfordert "revoscaler".

+ [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr)

   Liest das Schema der OLAP-Datenquellen und MDX-Abfragen ausgeführt.

+ [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)

    Hilfsfunktionen für eine wohlgeformte gespeicherte Prozedur aus R-Code generiert.

+ [mrsdeploy](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)

   Funktionen, die zum Einrichten einer remote-Sitzungs in einer Konsolenanwendung und zum Veröffentlichen und Verwalten von einem Webdienst, der r oder Python-Code verwendet.

## <a name="python"></a>Python

+ [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)

    Python-Entsprechung von "revoscaler"-Paket für die Sprache "R". Unterstützt die gleichen Compute-Kontexte und Datenquellen.

+ [Microsoftml für Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)

    Python entspricht der MicrosoftML-Paket für r unterstützt die gleichen rechenkontexte und Datenquellen und umfasst schnelle, skalierbare Algorithmen und Transformationen von Microsoft. 

## <a name="related-apis"></a>Verwandte APIs

+ [RevoPEMAR-Funktionsreferenz](https://docs.microsoft.com/machine-learning-server/r-reference/revopemar/pemar)

    Unterstützt die Entwicklung von parallelen Algorithmen

+ [RevoUtils](https://docs.microsoft.com/machine-learning-server/r-reference/revoutils/revoutils)

    Hilfsfunktionen für die Verwendung mit "revoscaler"-Umgebungen

## <a name="other"></a>Andere

"Vorgehensweisen" und Zusammenfassungen, die speziell für das Verwenden dieser R oder Python-APIs in SQL Server finden Sie hier:

+ [ScaleR-Funktionen zum Arbeiten mit SQL Server](scaler-functions-for-working-with-sql-server-data.md)
+ [Generieren Sie eine gespeicherte Prozedur mit sqlrutils](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
+ [MDX-Daten in R über OlapR lesen](how-to-create-mdx-queries-using-olapr.md)
