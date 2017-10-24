---
title: "Mit dem Microsoft-SDK für Java | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Java (Microsoft SDK for)
- Microsoft SDK for Java [ADO]
ms.assetid: 2d7cb5b5-8307-49dd-b07e-c07069bb1626
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b7473f3a8772c53834c964071c2385736ff45cbf
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-the-microsoft-sdk-for-java"></a>Mithilfe des Microsoft-SDK für Java

> [!IMPORTANT]
> Microsoft hat die Unterstützung von Visual J++ im Januar 2004 eingestellt.

Das Microsoft-SDK für Java ist das Entwicklerkit für die Microsoft Internet Explorer-Umgebung. Tools, Informationen und Beispiele werden bereitgestellt, können Sie die Entwicklung von Java-Programmen und Applets basierend auf JDK 1.1 und die Microsoft Win32-Virtual-Machine (Microsoft VM). Das Microsoft-SDK für Java ist nicht mit Microsoft Visual J++ gebunden. Um dieses SDK herunterzuladen, klicken Sie hier.  
  
 Das Hilfsprogramm Jactivex.exe generiert Klassen aus einer Typbibliothek, jedoch kann nur über die Befehlszeile aufgerufen werden. Diese Funktion ist nicht in der Entwicklungsumgebung Visual J++ integriert. Im Gegensatz zu den von der Java-Typbibliotheks-Assistenten generierte Klassen können Sie die vom SDK erstellten Klassenwrapper schrittweise. Dies ist nützlich zum Debuggen, wie Ihr Code die ADO-Wrapperklassen verwendet.  
  
 Dieser Mechanismus liest die ADO-Typbibliothek und generiert Klassen, die innerhalb der Anwendung instanziiert werden können. Diese Klassen werden am folgenden Speicherort generiert: \\< Windows-Verzeichnis\>\Java\trustlib\msado15.  
  
 Erstellen eine ADO-Anwendung in Java, die mit dem Microsoft-SDK für Java ist im Grunde identisch, aus der Perspektive des Quellcodes, zur Verwendung des Java-Typ-Bibliothek-Assistenten. Beispielcode, finden Sie unter [ADO-Java-Klassenwrapper](../../../ado/guide/appendixes/ado-java-class-wrappers.md). Der einzige Unterschied besteht darin, wie Sie ursprünglich, wie in den folgenden Schritten veranschaulicht die Wrapperklassen generieren.  
  
### <a name="to-create-an-ado-project-with-the-microsoft-sdk-for-java"></a>So erstellen Sie ein ADO-Projekt mit dem Microsoft-SDK für Java  
  
1.  Führen Sie Folgendes an der Eingabeaufforderung ein. Sie müssen den Pfad zu das Microsoft-SDK für Java-Bin-Verzeichnis enthalten oder führen Sie den Befehl von diesem Speicherort. Das Microsoft-SDK für Java ist in der Regel am gleichen Speicherort wie Visual Studio installiert. Dies ist eine einzelne Command-Anweisung.  
  
    ```  
    \<path to DevStudio>\<path to Java SDK>\bin\JactiveX.exe /javatlb "C:\program files\common files\system\ado\msado15.dll"  
    ```  
  
2.  Führen Sie den folgenden Befehl aus, um die generierten Klassen zu kompilieren. Der Switch /g:t aktiviert die Generierung von Debugsymbolen, damit Sie in die Ablaufverfolgung können die. Java-Symbole. Entfernen Sie sie für Releasebuilds.  
  
    ```  
    jvc /g:t c:\<windows>\Java\trustlib\msado15\*.Java  
    ```  
  
3.  Um diese Dateien zu verwenden, öffnen Sie das Projekt in Visual J++. Aus der **Projekt** Menü wählen **zu Projekt hinzufügen**. Wählen Sie **Dateien**, und fügen Sie alle von der. JAVA-Dateien im Verzeichnis trustlib\msado15 zu Ihrem Projekt generiert.  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-Java-Klassen-Wrapper](../../../ado/guide/appendixes/ado-java-class-wrappers.md)   

