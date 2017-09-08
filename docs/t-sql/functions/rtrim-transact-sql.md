---
title: RTRIM (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/05/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RTRIM_TSQL
- RTRIM
dev_langs:
- TSQL
helpviewer_keywords:
- RTRIM function
- character strings [SQL Server], trailing blanks
- blank characters [SQL Server]
- trailing blanks
ms.assetid: 52fd6e8d-650c-4f66-abcf-67765aa5aa83
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 838bad2a5d5434fdb3bb338ba32f75ebdfd1460c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="rtrim-transact-sql"></a>RTRIM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Zeichenfolge zurück, nachdem alle nachfolgenden Leerzeichen abgeschnitten.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
RTRIM ( character_expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *character_expression*  
 Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) von Zeichendaten. *Character_expression* kann eine Konstante, Variable oder Spalte mit Zeichen- oder Binärdaten sein.  
  
 *Character_expression* muss einen Datentyp, der implizit in **Varchar**. Verwenden Sie andernfalls [Umwandlung](../../t-sql/functions/cast-and-convert-transact-sql.md) zur expliziten Konvertierung *Character_expression*.  
  
## <a name="return-types"></a>Rückgabetypen  
 **Varchar** oder **Nvarchar**  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-simple-example"></a>A. Einfaches Beispiel  
 Im folgenden Beispiel wird eine Zeichenfolge mit Leerzeichen am Ende des Satzes genommen und der Text ohne die Leerzeichen am Ende des Satzes zurückgegeben.  
  
```  
SELECT RTRIM('Removes trailing spaces.   ');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
  `Removes trailing spaces.`  
  
### <a name="b-simple-example"></a>B: Beispiel einfache  
 Im folgenden Beispiel wird veranschaulicht, wie `RTRIM` nachfolgende Leerzeichen entfernt werden sollen. Ist die Zeit gibt es eine andere Zeichenfolge verkettet wird, an die erste Zeichenfolge an, dass die Leerzeichen entfernt sind.  
  
```  
SELECT RTRIM('Four spaces are after the period in this sentence.    ') + 'Next string.';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
`Four spaces are after the period in this sentence.Next string.`  

### <a name="c-using-rtrim-with-a-variable"></a>C. Verwenden von RTRIM mit einer Variablen  
 Im folgenden Beispiel wird verdeutlicht, wie nachfolgende Leerzeichen mit `RTRIM` aus einer Zeichenvariablen entfernt werden können.  
  
```  
DECLARE @string_to_trim varchar(60);  
SET @string_to_trim = 'Four spaces are after the period in this sentence.    ';  
SELECT @string_to_trim + ' Next string.';  
SELECT RTRIM(@string_to_trim) + ' Next string.';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```sql   
 -------------------------------------------------------------------------  
 Four spaces are after the period in this sentence.     Next string.  
 
 (1 row(s) affected)`  
 
 -------------------------------------------------------------------------  
 Four spaces are after the period in this sentence. Next string.  
 
 (1 row(s) affected)
 ```  
  

  
## <a name="see-also"></a>Siehe auch  
 [CAST und CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Zeichenfolgenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
 [TRIM &#40; Transact-SQL &#41;](../../t-sql/functions/trim-transact-sql.md)  
 [LTRIM &#40; Transact-SQL &#41;](../../t-sql/functions/ltrim-transact-sql.md)  
  
  


