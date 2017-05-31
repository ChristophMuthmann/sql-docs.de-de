---
title: "Auswählen eines Verschlüsselungsalgorithmus | Microsoft-Dokumentation"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cryptography [SQL Server], algorithms
- encryption [SQL Server], algorithms
- security [SQL Server], encryption
- algorithms [SQL Server encryption]
ms.assetid: 8227028c-a9c9-489d-bd27-fbf8242634ae
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a3cb1a59db35025eda9cf6ea68f0897aaecc9caf
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="choose-an-encryption-algorithm"></a>Auswählen eines Verschlüsselungsalgorithmus
  Die Verschlüsselung ist eine von mehreren Maßnahmen zum sicheren Schutz, die dem Administrator zur Verfügung stehen, der eine Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]sichern möchte.  
  
 Verschlüsselungsalgorithmen definieren Datentransformationen, die von nicht autorisierten Benutzern nicht einfach umgekehrt werden können. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ermöglicht Administratoren und Entwicklern die Auswahl aus mehreren Algorithmen, einschließlich DES, Triple DES, TRIPLE_DES_3KEY, RC2, RC4, 128-Bit-RC4, DESX, 128-Bit-AES, 192-Bit-AES und 256-Bit-AES.  
  
> [!NOTE]  
>  Ab [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)]gelten alle anderen Algorithmen als AES_128, AES_192 und AES_256 als veraltet. Um ältere Algorithmen zu verwenden (was nicht empfohlen wird), müssen Sie den Kompatibilitätsgrad zwischen Datenbanken auf höchsten 120 festlegen.  
  
 Keiner der Algorithmen ist für alle Situationen ideal, und Richtlinien zu den Vorteilen der einzelnen Algorithmen würden den Rahmen der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Onlinedokumentation sprengen. Es gelten jedoch die folgenden allgemeinen Prinzipien:  
  
-   Eine starke Verschlüsselung verbraucht im Allgemeinen mehr CPU-Ressourcen als eine schwache Verschlüsselung.  
  
-   Lange Schlüssel führen in der Regel zu einer stärkeren Verschlüsselung als kurze Schlüssel.  
  
-   Eine asymmetrische Verschlüsselung ist schwächer als eine symmetrische Verschlüsselung, wenn beide die gleiche Schlüssellänge verwenden. Dabei ist eine asymmetrische Verschlüsselung relativ langsam.  
  
-   Blockchiffren mit langen Schlüsseln sind stärker als Datenstromchiffren.  
  
-   Lange, komplexe Kennwörter sind stärker als kurze Kennwörter.  
  
-   Falls Sie viele Daten verschlüsseln, sollten Sie die Daten mithilfe eines symmetrischen Schlüssels verschlüsseln und den symmetrischen Schlüssel mit einem asymmetrischen Schlüssel verschlüsseln.  
  
-   Verschlüsselte Daten können nicht komprimiert werden, aber komprimierte Daten können verschlüsselt werden. Falls Sie die Komprimierung verwenden, sollten Sie die Daten vor dem Verschlüsseln komprimieren.  
  
> [!IMPORTANT]  
>  Der RC4-Algorithmus wird nur aus Gründen der Abwärtskompatibilität unterstützt. Neues Material kann nur mit RC4 oder RC4_128 verschlüsselt werden, wenn die Datenbank den Kompatibilitätsgrad 90 oder 100 besitzt. (Nicht empfohlen.) Verwenden Sie stattdessen einen neueren Algorithmus, z. B. einen der AES-Algorithmen. In [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] und höher kann mit RC4 oder RC4_128 verschlüsseltes Material in jedem Kompatibilitätsgrad entschlüsselt werden.  
>   
>  Die wiederholte Verwendung der gleichen RC4- oder RC4_128-KEY_GUID für unterschiedliche Datenblocks führt zum gleichen RC4-Schlüssel, da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nicht automatisch eine Salt bereitstellt. Die wiederholte Verwendung des gleichen RC4-Schlüssels stellt einen bekannten Fehler dar, der zu einer sehr schwachen Verschlüsselung führt. Deshalb wurden das RC4-Schlüsselwort und das RC4_128-Schlüsselwort als veraltet festgelegt. [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)]  
  
 Weitere Informationen zu Verschlüsselungsalgorithmen und der Verschlüsselungstechnologie finden Sie unter [Key Security Concepts](http://go.microsoft.com/fwlink/?LinkId=62082) im .NET Framework Developer's Guide auf MSDN.  
  
 **Erläuterung der DES-Algorithmen:**  
  
-   DESX wurde falsch benannt. Symmetrische Schlüssel, die mit ALGORITHM = DESX erstellt sind, verwenden eigentlich die TRIPLE DES-Chiffre mit einem 192-Bit-Schlüssel. Der DESX-Algorithmus wird nicht bereitgestellt. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
-   Symmetrische Schlüssel, die mit ALGORITHM = TRIPLE_DES_3KEY erstellt sind, verwenden die TRIPLE DES-Chiffre mit einem 192-Bit-Schlüssel.  
  
-   Symmetrische Schlüssel, die mit ALGORITHM = TRIPLE_DES erstellt sind, verwenden die TRIPLE DES-Chiffre mit einem 128-Bit-Schlüssel.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|||  
|-|-|  
|Verschlüsseln von Daten mit einem symmetrischen Schlüssel|[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)|  
|Verschlüsseln von Daten mit einem asymmetrischen Schlüssel|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)|  
|Verschlüsseln von Daten mit einem Zertifikat|[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)|  
|Verschlüsseln von Datenbankdateien mit transparenter Datenverschlüsselung|[Transparente Datenverschlüsselung &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption-tde.md)|  
|So verschlüsseln sie eine Tabellenspalte|[Verschlüsseln einer Datenspalte](../../../relational-databases/security/encryption/encrypt-a-column-of-data.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Verschlüsselung](../../../relational-databases/security/encryption/sql-server-encryption.md)   
 [Verschlüsselungshierarchie](../../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

