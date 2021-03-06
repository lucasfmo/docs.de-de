---
title: "Anker in regul&#228;ren Ausdr&#252;cken | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Reguläre Ausdrücke von .NET Framework, Anchor"
  - "Reguläre Ausdrücke von .NET Framework, Atomare Assertionen mit einer Breite von null"
  - "Anchor, In regulären Ausdrücken"
  - "Atomare Assertionen mit einer Breite von null"
  - "Metazeichen, Anchor"
  - "Metazeichen, Atomare Assertionen mit einer Breite von null"
  - "Reguläre Ausdrücke, Anchor"
  - "Reguläre Ausdrücke, Atomare Assertionen mit einer Breite von null"
ms.assetid: 336391f6-2614-499b-8b1b-07a6837108a7
caps.latest.revision: 20
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 20
---
# Anker in regul&#228;ren Ausdr&#252;cken
<a name="top"></a> Anker, auch als atomische Nullbreitenassertionen bezeichnet, geben eine Position in der Zeichenfolge an, an der eine Übereinstimmung auftreten muss. Wenn Sie im Suchausdruck einen Anker verwenden, durchsucht das Modul für reguläre Ausdrücke nicht die Zeichenfolge oder durchläuft Zeichen, sondern sucht nur an der angegebenen Position nach einer Übereinstimmung. Beispielsweise gibt `^` an, dass die Übereinstimmung am Anfang einer Zeile oder Zeichenfolge beginnen muss. Daher stimmt der reguläre Ausdruck `^http:` nur mit "http:" überein, wenn dies am Anfang einer Zeile steht. In der folgenden Tabelle werden die von den regulären .NET Framework\-Ausdrücken unterstützten Anker aufgeführt.  
  
|Anker|Beschreibung|  
|-----------|------------------|  
|`^`|Die Übereinstimmung muss am Anfang der Zeichenfolge oder Zeile vorliegen. Weitere Informationen finden Sie unter [Anfang der Zeichenfolge oder Zeile](#Start).|  
|`$`|Die Übereinstimmung muss am Ende der Zeichenfolge oder Zeile oder vor `\n` am Ende der Zeile oder Zeichenfolge vorliegen. Weitere Informationen finden Sie unter [Ende der Zeichenfolge oder Zeile](#End).|  
|`\A`|Die Übereinstimmung darf nur am Anfang der Zeichenfolge vorliegen \(mehrere Zeilen werden nicht unterstützt\). Weitere Informationen finden Sie unter [Nur Anfang der Zeichenfolge](#StartOnly).|  
|`\Z`|Der Vergleich muss am Ende der Zeichenfolge oder vor `\n` am Ende der Zeichenfolge erfolgen. Weitere Informationen finden Sie unter [Ende der Zeichenfolge oder vor dem abschließenden Zeilenumbruch](#EndOrNOnly).|  
|`\z`|Die Übereinstimmung darf nur am Ende der Zeichenfolge vorliegen. Weitere Informationen finden Sie unter [Nur Ende der Zeichenfolge](#EndOnly).|  
|`\G`|Die Übereinstimmung muss an dem Punkt beginnen, an dem die vorherige Übereinstimmung endete. Weitere Informationen finden Sie unter [Aufeinander folgende Übereinstimmungen](#Contiguous).|  
|`\b`|Die Übereinstimmung muss an einer Wortgrenze vorliegen. Weitere Informationen finden Sie unter [Wortgrenze](#WordBoundary).|  
|`\B`|Die Übereinstimmung darf nicht an einer Wortgrenze vorliegen. Weitere Informationen finden Sie unter [Nicht\-Wortgrenze](#NonwordBoundary).|  
  
<a name="Start"></a>   
## Anfang der Zeichenfolge oder Zeile: ^  
 Der `^`\-Anker gibt an, dass das folgende Muster an der ersten Zeichenposition der Zeichenfolge beginnen muss. Wenn Sie `^` mit der <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>\-Option \(siehe [Optionen für reguläre Ausdrücke](../../../docs/standard/base-types/regular-expression-options.md)\) verwenden, muss die Übereinstimmung am Anfang jeder Zeile vorliegen.  
  
 Im folgenden Beispiel wird der `^`\-Anker in einem regulären Ausdruck verwendet, der Informationen zu den Jahren extrahiert, in denen es bestimmte professionelle Baseballteams gab. Im Beispiel werden zwei Überladungen der <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=fullName>\-Methode aufgerufen:  
  
-   Der Aufruf der <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%29>\-Überladung sucht nur die erste Teilzeichenfolge in der Eingabezeichenfolge, die mit dem Muster des regulären Ausdrucks übereinstimmt.  
  
-   Der Aufruf der <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29>\-Überladung sucht bei Festlegung des `options`\-Parameters auf <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> alle fünf Teilzeichenfolgen.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/startofstring1.cs#1)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/startofstring1.vb#1)]  
  
 Das Muster für reguläre Ausdrücke `^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+` wird entsprechend der folgenden Tabelle definiert:  
  
|Muster|Beschreibung|  
|------------|------------------|  
|`^`|Suchen Sie nach einer Übereinstimmung am Anfang der Eingabezeichenfolge \(oder am Anfang der Zeile, wenn die Methode mit der <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>\-Option aufgerufen wird\).|  
|`((\w+(\s?)){2,}`|Suchen Sie nach einer Übereinstimmung mit mindestens einem Wortzeichen, auf das genau zwei Mal eine 0 \(Null\) oder ein Leerzeichen folgt. Dies ist die erste Erfassungsgruppe. Durch diesen Ausdruck werden auch eine zweite und dritte Erfassungsgruppe definiert: Die zweite Gruppe besteht aus dem erfassten Wort, die dritte aus den erfassten Leerzeichen.|  
|`,\s`|Suchen Sie nach einer Übereinstimmung mit einem Komma gefolgt von einem Leerzeichen.|  
|`(\w+\s\w+)`|Suchen Sie nach einer Übereinstimmung mit einem oder mehreren Wortzeichen gefolgt von mindestens einem Wortzeichen. Dies ist die vierte Erfassungsgruppe.|  
|`,`|Entsprechung für ein Komma finden.|  
|`\s\d{4}`|Suchen Sie nach einer Übereinstimmung mit einem von vier Dezimalzahlen gefolgten Leerzeichen.|  
|\(\-`(\d{4}&#124;present))?`|Suchen Sie nach einer Übereinstimmung mit 0 \(Null\) oder einem Bindestrich gefolgt von vier Dezimalzahlen oder der Zeichenfolge "present". Dies ist die sechste Erfassungsgruppe. Diese Gruppe enthält auch eine siebte Erfassungsgruppe.|  
|`,?`|Suchen Sie nach einer Übereinstimmung mit 0 \(null\) oder einem Komma.|  
|`(\s\d{4}(-(\d{4}&#124;present))?,?)+`|Suchen Sie nach einer Übereinstimmung mit mindestens einem Vorkommen der folgenden Elemente: ein Leerzeichen, vier Dezimalzahlen, 0 \(Null\) oder ein Bindestrich gefolgt von vier Dezimalzahlen oder der Zeichenfolge "present" sowie 0 \(Null\) oder ein Komma. Dies ist die fünfte Erfassungsgruppe.|  
  
 [Zurück nach oben](#top)  
  
<a name="End"></a>   
## Ende der Zeichenfolge oder Zeile: $  
 Der `$`\-Anker gibt an, dass das vorangehende Muster am Ende der Eingabezeichenfolge oder vor `\n` am Ende der Eingabezeichenfolge vorliegen muss.  
  
 Wenn Sie `$` mit der <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>\-Option verwenden, kann die Übereinstimmung auch am Ende einer Zeile vorliegen. Beachten Sie, dass `$` mit `\n` übereinstimmt, nicht jedoch mit `\r\n` \(der Kombination aus Wagenrücklauf\- und Zeilenumbruchzeichen oder CR\/LF\). Zum Suchen einer Übereinstimmung mit der CR\/LF\-Zeichenkombination schließen Sie `\r?$` in das Muster des regulären Ausdrucks ein.  
  
 Im folgenden Beispiel wird der `$`\-Anker zum Muster des regulären Ausdrucks hinzugefügt, der im Beispiel im Abschnitt [Anfang der Zeichenfolge oder Zeile](#Start) verwendet wurde. Bei Verwendung mit der ursprünglichen Eingabezeichenfolge von fünf Textzeilen wird von der <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%29?displayProperty=fullName>\-Methode keine Übereinstimmung gefunden, da das Ende der ersten Zeile nicht mit dem `$`\-Muster übereinstimmt. Wenn die ursprüngliche Eingabezeichenfolge in ein Zeichenfolgenarray geteilt wird, findet die <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%29?displayProperty=fullName>\-Methode eine Übereinstimmung mit jeder der fünf Zeilen. Wenn die <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=fullName>\-Methode mit dem auf `options` festgelegten <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>\-Parameter aufgerufen wird, werden keine Übereinstimmungen gefunden, da das Wagenrücklaufelement \(\\u\+000D\) nicht Teil des Musters des regulären Ausdrucks ist. Wenn das Muster des regulären Ausdrucks jedoch geändert wird, indem `$` durch `\r?$` ersetzt wird, ergibt der Aufruf der <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=fullName>\-Methode, sofern der `options`\-Parameter auf <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> festgelegt ist, wieder fünf Übereinstimmungen.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/endofstring1.cs#2)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/endofstring1.vb#2)]  
  
 [Zurück nach oben](#top)  
  
<a name="StartOnly"></a>   
## Nur Anfang der Zeichenfolge: \\A  
 Der `\A`\-Anker gibt an, dass eine Übereinstimmung am Anfang der Eingabezeichenfolge vorliegen muss. Dies ist mit dem `^`\-Anker identisch, jedoch wird die <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>\-Option von `\A` ignoriert. Daher kann hiermit in einer mehrzeiligen Eingabezeichenfolge nur eine Übereinstimmung nur am Anfang der ersten Zeile gesucht werden.  
  
 Das folgende Beispiel ähnelt den Beispielen für den `^`\-Anker und den `$`\-Anker. Der `\A`\-Anker wird in einem regulären Ausdruck verwendet, der Informationen zu den Jahren extrahiert, in denen es bestimmte professionelle Baseballteams gab. Die Eingabezeichenfolge weist fünf Zeilen auf. Der Aufruf der <xref:System.Text.RegularExpressions.Regex.Matches%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.RegexOptions%29?displayProperty=fullName>\-Methode sucht nur die erste Teilzeichenfolge in der Eingabezeichenfolge, die mit dem Muster des regulären Ausdrucks übereinstimmt. Wie im Beispiel dargestellt, hat die <xref:System.Text.RegularExpressions.RegexOptions>\-Option keine Auswirkungen.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/startofstring2.cs#3)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/startofstring2.vb#3)]  
  
 [Zurück nach oben](#top)  
  
<a name="EndOrNOnly"></a>   
## Ende der Zeichenfolge oder vor dem abschließenden Zeilenumbruch: \\Z  
 Der `\Z`\-Anker gibt an, dass eine Übereinstimmung am Ende der Eingabezeichenfolge oder vor `\n` am Ende der Eingabezeichenfolge vorliegen muss. Dies ist mit dem `$`\-Anker identisch, jedoch wird die <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>\-Option von `\Z` ignoriert. Daher kann hiermit in einer mehrzeiligen Zeichenfolge nur nach einer Übereinstimmung mit dem Ende der letzten Zeile oder der letzten Zeile vor `\n` gesucht werden.  
  
 Beachten Sie, dass `\Z` mit `\n`, aber nicht mit `\r\n` übereinstimmt \(der CR\/LF\-Zeichenkombination\). Zum Suchen einer Übereinstimmung mit CR\/LF schließen Sie `\r?\Z` in das Muster des regulären Ausdrucks ein.  
  
 Im folgenden Beispiel wird der `\Z`\-Anker in einem regulären Ausdruck verwendet, der ähnlich wie das Beispiel aus dem Abschnitt [Anfang der Zeichenfolge oder Zeile](#Start) Informationen zu den Jahren extrahiert, in denen es bestimmte professionelle Baseballteams gab. Der Teilausdruck `\r?\Z` im regulären Ausdruck `^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+\r?\Z` stimmt sowohl mit dem Ende einer Zeichenfolge als auch mit einer Zeichenfolge überein, die mit `\n` oder `\r\n` endet. Folglich stimmt jedes Element im Array mit dem Muster des regulären Ausdrucks überein.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/endofstring2.cs#4)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/endofstring2.vb#4)]  
  
 [Zurück nach oben](#top)  
  
<a name="EndOnly"></a>   
## Nur Ende der Zeichenfolge: \\z  
 Der `\z`\-Anker gibt an, dass eine Übereinstimmung am Ende der Eingabezeichenfolge vorliegen muss. Wie das `$`\-Sprachelement ignoriert `\z` die <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>\-Option. Im Gegensatz zum `\Z`\-Sprachelement stimmt `\z` nicht mit einem `\n`\-Zeichen am Ende einer Zeichenfolge überein. Daher kann hiermit nur eine Übereinstimmung mit der letzten Zeile der Eingabezeichenfolge gesucht werden.  
  
 Im folgenden Beispiel wird der `\z`\-Anker in einem regulären Ausdruck verwendet, der ansonsten mit dem Beispiel aus dem vorherigen Abschnitt übereinstimmt und Informationen zu den Jahren extrahiert, in denen es bestimmte professionelle Baseballteams gab. Im Beispiel wird versucht, eine Übereinstimmung mit dem Muster eines regulären Ausdrucks `^((\w+(\s?)){2,}),\s(\w+\s\w+),(\s\d{4}(-(\d{4}|present))?,?)+\r?\z` für jedes der fünf Elemente in einem Zeichenfolgenarray zu finden. Zwei der Zeichenfolgen enden mit Wagenrücklauf\- und Zeilenvorschubzeichen, eine endet mit einem Zeilenvorschubzeichen, und zwei enden weder mit einem Wagenrücklauf\- noch mit einem Zeilenvorschubzeichen. Wie die Ausgabe ergibt, stimmen nur die Zeichenfolgen ohne Wagenrücklauf oder Zeilenvorschub mit dem Muster überein.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/endofstring3.cs#5)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/endofstring3.vb#5)]  
  
 [Zurück nach oben](#top)  
  
<a name="Contiguous"></a>   
## Aufeinander folgende Übereinstimmungen: \\G  
 Der `\G`\-Anker gibt an, dass eine Übereinstimmung an dem Punkt vorliegen muss, an dem die vorherige Übereinstimmung endet. Wenn Sie diesen Anker mit der <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=fullName>\-Methode oder <xref:System.Text.RegularExpressions.Match.NextMatch%2A?displayProperty=fullName>\-Methode verwenden, wird damit sichergestellt, dass alle Übereinstimmungen zusammenhängend sind.  
  
 Im folgenden Beispiel werden mithilfe eines regulären Ausdrucks die Namen von Nagetierspezies aus einer durch Trennzeichen getrennten Zeichenfolge extrahiert.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/contiguous1.cs#6)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/contiguous1.vb#6)]  
  
 Der reguläre Ausdruck `\G(\w+\s?\w*),?` wird entsprechend der Darstellung in der folgenden Tabelle interpretiert.  
  
|Muster|Beschreibung|  
|------------|------------------|  
|`\G`|Beginnt die Übereinstimmung am Ende der vorherigen.|  
|`\w+`|Übereinstimmung mit mindestens einem Wortzeichen.|  
|`\s?`|Übereinstimmung mit 0 \(Null\) oder einem Leerzeichen.|  
|`\w*`|Übereinstimmung mit keinem oder mehreren Wortzeichen.|  
|`(\w+\s?\w*)`|Übereinstimmung mit mindestens einem Wortzeichen gefolgt von 0 \(Null\) oder einem Leerzeichen, gefolgt von 0 \(Null\) oder weiteren Wortzeichen. Dies ist die erste Erfassungsgruppe.|  
|`,?`|Übereinstimmung mit 0 \(Null\) oder einem Literal\-Kommazeichen.|  
  
 [Zurück nach oben](#top)  
  
<a name="WordBoundary"></a>   
## Wortgrenze: \\b  
 Der `\b`\-Anker gibt an, dass die Übereinstimmung an einer Grenze zwischen einem Wortzeichen \(dem `\w`\-Sprachelement\) und einem Nicht\-Wortzeichen \(dem `\W`\-Sprachelement\) vorliegen muss. Wortzeichen bestehen aus alphanumerischen Zeichen und Unterstrichen. Bei Nicht\-Wortzeichen handelt es sich um alle Zeichen, die weder alphanumerisch noch Unterstriche sind. \(Weitere Informationen finden Sie unter [Zeichenklassen](../../../docs/standard/base-types/character-classes-in-regular-expressions.md).\) Die Übereinstimmung kann auch an einer Wortgrenze am Anfang oder Ende der Zeichenfolge vorliegen.  
  
 Der `\b`\-Anker wird häufig verwendet, um sicherzustellen, dass ein Teilausdruck statt nur mit Anfang oder Ende mit einem ganzen Wort übereinstimmt. Im folgenden Beispiel wird die Verwendung des regulären Ausdrucks `\bare\w*\b` veranschaulicht. Der Ausdruck stimmt mit jedem Wort überein, das mit der Teilzeichenfolge "are" beginnt. Die Ausgabe des Beispiels veranschaulicht auch, dass `\b` sowohl mit dem Anfang als auch dem Ende der Eingabezeichenfolge übereinstimmt.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/word1.cs#7)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/word1.vb#7)]  
  
 Das Muster für reguläre Ausdrücke wird entsprechend der folgenden Tabelle interpretiert.  
  
|Muster|Beschreibung|  
|------------|------------------|  
|`\b`|Der Vergleich beginnt an einer Wortgrenze.|  
|`are`|Übereinstimmung mit der Teilzeichenfolge "are".|  
|`\w*`|Übereinstimmung mit keinem oder mehreren Wortzeichen.|  
|`\b`|Der Vergleich endet an einer Wortgrenze.|  
  
 [Zurück nach oben](#top)  
  
<a name="NonwordBoundary"></a>   
## Nicht\-Wortgrenze: \\B  
 Der `\B`\-Anker gibt an, dass die Übereinstimmung nicht an einer Wortgrenze vorliegen darf. Dies ist das Gegenteil des `\b`\-Ankers.  
  
 Im folgenden Beispiel wird der `\B`\-Anker verwendet, um nach Vorkommen der Teilzeichenfolge "qu" in einem Wort zu suchen. Das Muster des regulären Ausdrucks `\Bqu\w+` stimmt mit einer Teilzeichenfolge überein, die mit "qu" beginnt, nicht der Wortbeginn ist und bis zum Ende des Worts reicht.  
  
 [!code-csharp[Conceptual.RegEx.Language.Assertions#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.assertions/cs/nonword1.cs#8)]
 [!code-vb[Conceptual.RegEx.Language.Assertions#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.assertions/vb/nonword1.vb#8)]  
  
 Das Muster für reguläre Ausdrücke wird entsprechend der folgenden Tabelle interpretiert.  
  
|Muster|Beschreibung|  
|------------|------------------|  
|`\B`|Übereinstimmung beginnt nicht an einer Wortgrenze.|  
|`qu`|Übereinstimmung mit der Teilzeichenfolge "qu".|  
|`\w+`|Übereinstimmung mit mindestens einem Wortzeichen.|  
  
## Siehe auch  
 [Sprachelemente für reguläre Ausdrücke – Kurzübersicht](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)   
 [Optionen für reguläre Ausdrücke](../../../docs/standard/base-types/regular-expression-options.md)