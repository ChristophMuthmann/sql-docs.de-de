---
title: R-Tools enthalten, die mit SQL Server-Setup | Microsoft Docs
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
ms.assetid: 7c04ae30-d391-4369-9742-d2b275e14c0d
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 8178f4a1347ef58fd7ee143fbe843e3525ac4cf0
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2018
---
# <a name="r-tools-included-with-sql-server-setup"></a>R-Tools enthalten, die mit SQL Server-setup
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Bei der Installation von R mit SQL Server erhalten Sie dieselben R-Tools, die mit allen installiert sind **Basis** Installation von R, wie z. B. Rterm, "rgui.exe" und So weiter. Technisch gesehen, müssen Sie daher alle Tools, die Sie zum Entwickeln und Testen von R-Code erforderlich.

Dieses Thema enthält die Tools, mit der Installation enthalten.

> [!TIP]
> 
> In der Regel ist es einfacher, Debuggen und Testen von R-Code mithilfe einer dedizierten Umgebung. Sie müssen als einfacher R-Code in SQL Server ausgeführt wird, es im Vorfeld in ein externes Tool zum Testen, damit Sie detaillierte Fehlermeldungen zu lesen und die Lösung Debuggen können.
> 
> Finden Sie im Artikel für eine Liste kostenlose Tools, die Sie verwenden können, zum Entwickeln von R-Lösungen und deren Konfiguration mit SQL Server arbeiten: [Einrichten einer Data Science-Client](set-up-a-data-science-client.md)

**Gilt für:** SQL Server 2016 R Services (Datenbankintern) und Microsoft R Server (eigenständig); SQLServer 2017 Machine Learning-Services (Datenbankintern) und Machine Learning-Server (eigenständig)

## <a name="r-tools-included-with-installation"></a>R-Tools enthalten, mit der installation

Die folgenden standard-R-Tools sind in enthalten eine *basieren Installation* von R, und daher standardmäßig installiert sind.

+ **RTerm**: eine Befehlszeilen Terminaldienste zum Ausführen von R-Skripts

+ **RGui.exe**: einen einfachen interaktiven Editor für R. Die Befehlszeilenargumente sind identisch für RGui.exe und RTerm.

+ **RScript**: ein Befehlszeilentool zum Ausführen von R-Skripts im Batchmodus.

Um diese Tools zu suchen, ermitteln Sie die R-Bibliothek, die beim Einrichten von SQL Server oder das eigenständige-Machine learning-Funktion installiert wurde. Z. B. in einer Standardinstallation der R-Tools in diesen Ordnern befinden sich:

+ SQL Server 2016 R Services: `~\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64`
+ Microsoft R Server eigenständige:`~\Program Files\Microsoft R\R_SERVER\bin\x64`
+ SQL Server 2017 Machine Learning-Dienste:`~\Program Files\Microsoft SQL Server\MSSQL14.<instancename>\R_SERVICES\bin\x64`
+ Machine Learning-Server (eigenständig):`~\Program Files\Microsoft\ML Server\R_SERVER\bin\x64`

Wenn Sie Hilfe bei der R-Tools benötigen, öffnen Sie einfach **"rgui.exe"**, klicken Sie auf **Hilfe**, und wählen Sie eine der Optionen.

## <a name="introducing-microsoft-r-client"></a>Einführung in Microsoft R-Client

Microsoft R-Client ist kostenlos, das Ihnen den Zugriff auf die "revoscaler"-Pakete für die Verwendung der Entwicklung bietet. Indem Sie R-Client installieren, können Sie R-Lösungen erstellen, die in allen unterstützten rechenkontexte, einschließlich SQL Server in der Datenbank Analytics und verteilte R Datenverarbeitung auf Hadoop, Spark oder Linux verwenden Machine Learning-Server ausgeführt werden können.

Wenn Sie eine andere R-Entwicklungsumgebung bereits installiert haben wie RStudio, achten Sie neu konfigurieren, die Umgebung, verwenden Sie die Bibliotheken und ausführbaren Dateien von Microsoft R-Client bereitgestellt wird. Indem Sie auf diese Weise, sodass Sie alle Funktionen von der "revoscaler"-Paket verwenden können, obwohl die Leistung beschränkt sind.

Weitere Informationen finden Sie unter [was Microsoft R-Client ist?](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)
