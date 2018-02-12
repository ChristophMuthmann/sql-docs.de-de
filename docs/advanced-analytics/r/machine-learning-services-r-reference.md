---
title: "API-Referenz für SQL Server-Machine Learning-Services | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: ab95ffe13fafa6e54d129ae155ddd58c16f07044
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2018
---
# <a name="api-reference-for-sql-server-machine-learning-services"></a>API-Referenz für SQL Server-Machine Learning-Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

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
