---
title: FIPS-Modus | Microsoft Docs
ms.custom: 
ms.date: 06/28/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 1
author: v-nisidh
ms.author: v-nisidh
manager: andrela
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7f344ad84588110372ccb369ae97642ef6c42f07
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="fips-mode"></a>FIPS-Modus
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver für SQL Server unterstützt *FIPS 140-kompatiblen Modus*. Für Oracle / Sun-JVM finden Sie in der [FIPS 140-kompatiblen Modus für SunJSSE](https://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/FIPS.html) Abschnitt zur FIPS Konfigurieren von Oracle bereitgestellten aktiviert JVM. 

**Erforderliche Komponenten**:
* FIPS konfiguriert JVM
* Entsprechende SSL-Zertifikat.
* Dateien der entsprechenden Richtlinie. 
* Parameter der entsprechenden Konfiguration. 


## <a name="fips-configured-jvm"></a>FIPS konfiguriert JVM:

Um die genehmigten Module für FIPS-Konfiguration angezeigt wird, finden Sie in der [überprüft FIPS 140-1 und kryptografische Module FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/documents/140-1/1401val2016.htm). 

Anbieter müssen möglicherweise einige zusätzliche Schritte zum Konfigurieren von JVM mit FIPS.

### <a name="ensure-your-jvm-is-in-fips-mode"></a>Stellen Sie sicher, dass die JVM im FIPS-Modus ist:
Um sicherzustellen, dass Ihre JVM FIPS aktiviert ist, führen Sie den folgenden Codeausschnitt: 

````
public boolean isFIPS() throws Exception {
    Provider jsse = Security.getProvider("SunJSSE");
    return jsse != null && jsse.getInfo().contains("FIPS");
}
````

## <a name="appropriate-ssl-certificate"></a>Entsprechende SSL-Zertifikat:
Um SQL Server im FIPS-Modus eine Verbindung herzustellen, ist ein gültiges SSL-Zertifikat erforderlich. Installieren Sie, oder importieren Sie es in der Java Schlüsselspeicher auf dem Clientcomputer (JVM), in denen FIPS aktiviert ist. Falls Sie nicht importieren oder installieren Sie das entsprechende Zertifikat, konnte Sie möglicherweise nicht mit SQL Server herstellen, wie eine sichere Verbindung hergestellt werden kann.

### <a name="importing-ssl-certificate-in-java-keystore"></a>Importieren von SSL-Zertifikat in Java-Schlüsselspeicher aus:
Für FIPS fallen wahrscheinlich Importieren des Zertifikats (Cert) entweder PKCS oder in einem anbieterspezifischen-Format. Verwenden der folgende Codeausschnitt importieren Sie das SSL-Zertifikat, und speichern Sie ihn in ein Arbeitsverzeichnis, mit dem entsprechenden KeyStore-Format an. _TRUST_STORE_PASSWORD_ ist Ihr Kennwort für Java KeyStore. 

````
    public void saveGenericKeyStore(String provider, String trustStoreType, String certName, String certPath) throws KeyStoreException, CertificateException, NoSuchAlgorithmException, NoSuchProviderException, IOException {
        KeyStore ks = KeyStore.getInstance(trustStoreType, provider);
        FileOutputStream os = new FileOutputStream("./MyTrustStore_" + trustStoreType);
        ks.load(null, null);
        ks.setCertificateEntry(certName, getCertificate(certPath));
        ks.store(os, TRUST_STORE_PASSWORD.toCharArray());
        os.flush();
        os.close();
    }

    private Certificate getCertificate(String pathName) throws FileNotFoundException, CertificateException {
        FileInputStream fis = new FileInputStream(pathName);
        CertificateFactory cf = CertificateFactory.getInstance("X.509");
        return cf.generateCertificate(fis);
    }

````


Im folgenden Beispiel werden wir ein Azure SSL-Zertifikat in des PKCS12-Formats mit BouncyCastle Anbieter importieren. Das Zertifikat wird importiert, in das Arbeitsverzeichnis an, mit dem Namen _MyTrustStore_PKCS12_ mithilfe der folgende Codeausschnitt:

` saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer"); `

## <a name="appropriate-policy-files"></a>Dateien der entsprechenden Richtlinie: 
Für einige Anbieter FIPS sind uneingeschränkte Richtlinie Support erforderlich. In solchen Fällen für Sun / Oracle Java Cryptography Extension (JCE) Unlimited Strength Zuständigkeit Richtliniendateien herunterladen für [JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) oder [JRE 7](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html). 

## <a name="appropriate-configuration-parameters"></a>Parameter der entsprechenden Konfiguration: 
Um die JDBC-Treiber im FIPS-kompatiblen Modus auszuführen, konfigurieren Sie Verbindungseigenschaften, wie in der folgenden Tabelle dargestellt. 

**Eigenschaften**: 

|Eigenschaft|Typ|Standardwert|Description|Hinweise|
|---|---|---|---|---|
|encrypt|boolescher Wert ["" true "/" false ""]|"false"|FIPS-aktivierten verschlüsseln JVM Eigenschaft sollte **"true"**||
|TrustServerCertificate|boolescher Wert ["" true "/" false ""]|"false"|FIPS Zertifikatkette überprüfen müssen, daher sollten verwenden wir **"false"** Wert für diese Eigenschaft. ||
|trustStore|String|NULL|Ihre Java-Schlüsselspeicher-Dateipfad, in dem Sie Ihr Zertifikat importiert haben. Wenn Sie in Ihrem System und gibt dann nicht erforderlich, übergeben Sie nichts Zertifikat installieren. Treiber verwendet Cacerts oder Jssecacerts Dateien.||
|trustStorePassword|String|NULL|Das Kennwort, das zum Überprüfen der Integrität der trustStore-Daten verwendet wird.||
|FIPS|boolescher Wert ["" true "/" false ""]|"false"|Diese Eigenschaft sollte sein, für die Fips JVM aktiviert **"true"**|Hinzugefügt in 6.1.4||
|fipsProvider|String|NULL|FIPS-Anbieter in JVM konfiguriert. Z. B. BCFIPS oder SunPKCS11 NSS |Hinzugefügt in 6.1.2|
|trustStoreType|String|JKS|Für FIPS-Modus Trust Store Mengentyp PKCS12 oder Typ von FIPS-Anbieter definiert |Hinzugefügt in 6.1.2||



  
