---
title: Unicode-Funktionsargumente | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: eafe8c7e-f6d2-44d7-99ee-cf2148a30f4f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0e67f437cd629411230daed17f6a39f24b7103d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47669458"
---
# <a name="unicode-function-arguments"></a>Unicode-Funktionsargumente
Der ODBC 3.5 (oder höher)-Treiber-Manager unterstützt die ANSI- und Unicode-Versionen aller Funktionen, die Zeiger auf Zeichenfolgen oder SQLPOINTER in ihren Argumenten zu akzeptieren. Die Unicode-Funktionen werden als Funktionen implementiert (mit dem Suffix *W*) und nicht als Makros. ANSI-Funktionen (die aufgerufen werden kann, mit oder ohne Suffix *ein*) sind identisch mit der aktuellen ODBC API-Funktionen.  
  
## <a name="remarks"></a>Hinweise  
 Unicode-Funktionen, die immer zurückgeben, oder nutzen von Zeichenfolgen oder Argumente Länge werden als Anzahl von Zeichen übergeben. Für Funktionen, die von Längeninformationen für Server-Daten zurückgeben, werden die Anzeigegröße und Genauigkeit als Anzahl der Zeichen beschrieben. Wenn eine Länge (Übertragungsgröße der Daten) auf Zeichenfolgen-oder keine Zeichenfolge darstellen verweisen kann, wird die Länge in Oktett Längen beschrieben. Z. B. **SQLGetInfoW** dauert immer noch die Länge als Anzahl von Bytes, aber **SQLExecDirectW** Count-von-Zeichen verwenden.  
  
 Anzahl von Zeichen bezieht sich auf die Anzahl der Bytes (Oktette) für die ANSI-Funktionen und die Anzahl von WCHAR (16-Bit-Wörter) für UNICODE-Funktionen. Insbesondere kann eine Sequenz Doppelbyte-Zeichensatz (DBCS) oder eine Sequenz multibyte-Zeichensätze (MBCS) der mehrere Bytes bestehen. Eine Folge von UTF-16-Unicode-Zeichen kann aus mehreren WCHARs so lang wie bestehen.  
  
 Im folgenden finden eine Liste der ODBC-API-Funktionen, die sowohl Unicode (W) und ANSI (A)-Versionen unterstützt:  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagField**|  
|**SQLColAttribute**|**SQLGetDiagRec**|  
|**SQLColAttributes**|**SQLGetInfo**|  
|**SQLColumnPrivileges**|**SQLGetStmtAttr**|  
|**SQLColumns**|**SQLNativeSQL**|  
|**SQLConnect**|**SQLPrepare**|  
|**SQLDataSources**|**SQLPrimaryKeys**|  
|**SQLDescribeCol**|**SQLProcedureColumns**|  
|**SQLDriverConnect**|**SQLProcedures**|  
|**SQLDrivers**|**SQLSetConnectAttr**|  
|**SQLError**|**SQLSetConnectOption**|  
|**SQLExecDirect**|**SQLSetCursorName**|  
|**SQLForeignKeys**|**SQLSetDescField**|  
|**SQLGetConnectAttr**|**SQLSetStmtAttr**|  
|**SQLGetConnectOption**|**SQLSpecialColumns**|  
|**SQLGetCursorName**|**SQLStatistics**|  
|**SQLGetDescField**|**SQLTablePrivileges**|  
|**SQLGetDescRec**|**SQLTables**|  
  
 Im folgenden finden eine Liste der ODBC-Installationsprogramms und ODBC-Übersetzer-Funktionen, die sowohl Unicode (W) und ANSI (A)-Versionen unterstützen:  
  
|||  
|-|-|  
|**SQLConfigDataSource**|**SQLInstallDriverManager**|  
|**SQLCreateDataSource**|**SQLInstallerError**|  
|**SQLDataSourceToDriver**|**SQLInstallODBC**|  
|**SQLDriverToDataSource**|**SQLReadFileDSN**|  
|**SQLGetAvailableDrivers**|**SQLRemoveDSNFromINI**|  
|**SQLGetInstalledDrivers**|**SQLValidDSN**|  
|**SQLGetTranslator**|**SQLWriteDSNToINI**|  
|**SQLInstallDriver**||  
  
> [!NOTE]  
>  Als veraltet markierte Funktionen verfügen über Unterstützung für Unicode-in-ANSI--Zuordnung aus, da die ODBC 3.*.x* -Treiber-Manager unterstützt die erneute Kompilierung ODBC 2. *X* Anwendungen mit der Unicode- **#define**.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Unicode-Anwendungen](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Unicode-Treiber](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [Funktionszuordnung im Treiber-Manager](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
