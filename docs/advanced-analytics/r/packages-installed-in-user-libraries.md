---
title: In Benutzerbibliotheken installierte Pakete | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 99ffd9b8-aa6d-4ac2-9840-4e66d0463978
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b4d5c7f3d1d0da5e1967140fcbdfcf60ba4571e7
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="packages-installed-in-user-libraries"></a>In Benutzerbibliotheken installierte Pakete

Wenn ein Benutzer ein neues R-Paket benötigt und kein Administrator ist, können die Pakete nicht am Standardspeicherort installiert werden und werden standardmäßig in einer privaten Benutzerbibliothek installiert. 

In einer typischen R-Entwicklungsumgebung müsste der Benutzer für das Verweisen auf das Paket im Code den Speicherort zur R-Umgebungsvariablen `libPath` hinzufügen oder wie folgt auf den vollständigen Paketpfad verweisen:  
  
~~~~
library("c:/Users/<username>/R/win-library/packagename")  
~~~~

## <a name="problems-with-packages-in-user-libraries"></a>Probleme mit Paketen in Benutzerbibliotheken

In [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] wird diese Problemumgehung jedoch **nicht** unterstützt; Pakete müssen in der Standardbibliothek installiert werden. Wenn das Paket nicht in der Standardbibliothek installiert wurde, erhalten Sie möglicherweise diese Fehlermeldung, wenn Sie versuchen, das Paket aufzurufen:

*Error in library(xxx) : there is no package called 'xxx'* (Fehler in Bibliothek(xxx) : kein Paket 'xxx' vorhanden)
 

Daher ist es bei der Migration von R-Lösungen für die Ausführung in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] wichtig, dass Sie die folgenden Aktionen ausführen:
+ Installieren Sie alle benötigten Pakete in der Standardbibliothek.
+ Bearbeiten Sie Code, um sicherzustellen, dass Pakete aus der Standardbibliothek und nicht aus Ad-hoc-Verzeichnissen oder Benutzerbibliotheken geladen werden.
+ Stellen Sie sicher, dass im Code keine Aufrufe von nicht installierten Paketen enthalten sind.
+ Ändern Sie Code, der versuchen würde, Pakete dynamisch zu installieren.
 
Wenn ein Paket in der Standardbibliothek installiert wurde, lädt die R-Laufzeit das Paket aus der Standardbibliothek, auch wenn im R-Code eine andere Bibliothek angegeben wurde.

## <a name="see-also"></a>Siehe auch
