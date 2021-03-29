# Practice GitHub Flavered Markdown Exensions

## 1. table

### Table이란?  
행과 열이 있는 데이터 배열.

### Table의 구성요소 :  
단일 헤더 행, 데이터로 부터 헤더를 구분하는 구분자 행, 0개 이상의 데이터 행

### Table 특징 :  
- 각 행은 임의의 텍스트를 포함하는 셀로 구성되며, 이 셀에서는 텍스트들이 파이프(|)로 구분된다. 이 때 판독의 명확성을 위해 선행 파이프와 후행 파이프가 권장되며, 그렇지 않은 경우 구문 분석 모호성이 있다. 파이프와 셀의 내용 사이의 공백은 잘리며 테이블에 블록 수준 요소를 삽입할 수 없다. 
-  구분 기호의 행은 하이픈(-)과 선행 또는 후행 콜론(:) 또는 둘 다에 해당하는(양쪽 콜론) 셀로 구성되어 각각 왼쪽, 오른쪽 또는 가운데 정렬을 나타낸다.

### EXAMPLE 1 : Table  

Markdown :  

      | foo | bar |  
      | --- | --- |  
      | baz | bim |

Rendered Output :  

| foo | bar |
| --- | --- |
| baz | bim |

HTML :  

\<table\>  
\<thead\>  
\<tr\>  
\<th\>foo\</th\>  
\<th\>bar\</th\>  
\</tr\>  
\</thead\>  
\<tbody\>  
\<tr\>  
\<td\>baz\</td\>  
\<td\>bim\</td\>  
\</tr\>  
\</tbody\>  
\</table\>  

### EXAMPLE 2 : 한 열의 셀은 길이가 일치할 필요는 없지만, 셀의 길이가 일치하면 더 쉽게 읽을 수 있다. 마찬가지로 선행 및 후행 파이프의 사용도 일관되지 않을 수 있다.  

Markdown :  

      | abc | defghi |  
      :-: | -----------:  
      bar | baz

Rendered Output :  

| abc | defghi |
:-: | -----------:
bar | baz

### EXAMPLE 3 : 다른 inline span을 포함하여 이스케이핑을 통해 셀 내용물에 파이프를 포함할 수 있다.  

Markdown :  

      | f\|oo  |  
      | ------ |  
      | b `|` az |  
      | b **\|\** im \|  

Rendered Output :  

| f\|oo  |
| ------ |
| b `\|` az |
| b **\|** im |

### EXAMPLE 4 : 테이블은 첫 번째 빈 라인 또는 다른 블록 레벨 구조의 시작 부분에서 파손된다.  

Markdown :  

      | abc | def |  
      | --- | --- |  
      | bar | baz |  
      > bar

Rendered Output :  

| abc | def |
| --- | --- |
| bar | baz |
> bar

### EXAMPLE 5 : 머리글 행은 셀 수에 있는 구분자 행과 일치해야 한다. 그렇지 않으면 테이블이 인식되지 않는다.  
  

Markdown :  

      | abc | def |
      | --- |  
      | bar |  

Rendered Output :  

| abc | def |  
| --- |  
| bar |

### EXAMPLE 6 : 표의 나머지 행은 셀 수에 따라 다를 수 있다. 헤더 행에 셀 수보다 적은 셀 수가 있다면 빈 셀이 삽입된다. 크기가 클 경우는 무시된다.  

Markdown :  

      | abc | def |  
      | --- | --- |  
      | bar |  
      | bar | baz | boo |  

Rendered Output :  

| abc | def |
| --- | --- |
| bar |
| bar | baz | boo |

### EXAMPLE 7 : 본문에 행이 없는 경우 HTML 출력에 <tbody>가 생성되지 않는다.  

Markdown :  

      | abc | def |  
      | --- | --- |  

Rendered Output :  

| abc | def |
| --- | --- |

HTML :  

\<table\>
\<thead\>
\<tr\>
\<th\>abc\</th\>
\<th\>def\</th\>
\</tr\>
\</thead\>
\</table\>

## 2. Task list items

### Task list items란? 
첫 번째 블록이 작업 목록 항목 마커로 시작하는 단락. 다른 내용보다 공백 문자가 먼저 하나 이상 있는 항목.

### Task list items의 구성요소 :  
선택적 공백 수, 왼쪽 괄호([), 공백 문자 또는 소문자 또는 대문자 x, 오른쪽 괄호(])

### 특징:  
- 랜더링 시, task list item 마커는 의미 확인란 요소로 대체된다. HTML 출력에서 이것은 <input type="checkbox">이 된다.  
- 관호 사이의 문자가 공백 문자인 경우 확인란은 선택 취소된다. 그렇지 않으면 확인란이 선택된다.
- 이 규격은 체크박스 요소가 상호작용하는 방식을 정의하지 않는다. 실제로 구현자는 확인란을 비활성화 또는 불변 요소로 자유롭게 렌더링하거나 최종 렌더링 된 문서에서 동적 상호 작용(즉, 체크, 선택 해제)을 동적으로 처리할 수 있다.  

### EXAMPLE 1 : Task list items

Markdown :  

      - [ ] foo  
      - [x] bar  

Rendered Output :  

- [ ] foo
- [x] bar

HTML :  

\<ul>  
\<l\>\<input disabled="" type="checkbox"\> foo\</li\>  
\<li\>\<input checked="" disabled="" type="checkbox"\> bar\</li\>  
\</ul\>  

### EXAMPLE 2 : Task list는 임의로 중첩될 수 있다.  

Markdown :  

      - [x] foo  
        - [ ] bar  
        - [x] baz  
      - [ ] bim  

Rendered Output :  

- [x] foo
  - [ ] bar
  - [x] baz
- [ ] bim

HTML :  

\<ul\>  
\<li\>\<input checked="" disabled="" type="checkbox"\> foo  
\<ul\>  
\<li\>\<input disabled="" type="checkbox"\> bar\</li\>  
\<li\>\<input checked="" disabled="" type="checkbox"\> baz\</li\>  
\</ul\>  
\</li\>  
\<li\>\<input disabled="" type="checkbox"\> bim\</li\>  
\</ul\>  

## 3. Strikethrough

### Strikethrough란?
두 개의 타일(~)로 묶어 사용하는 추가적인 강조 유형.

### Strikethrough의 구성요소 :  
두 개의 타일(~), 텍스트

### EXAMPLE 1 :  Strikehrough

Markdown :  

      ~~Hi~~ Hello, world!

Rendered Output :  

~~Hi~~ Hello, world!

HTML :  

\<p\>\<del\>Hi\</del\> Hello, world!\</p\>

### EXAMPLE 2 : 일반 강조 구분 기호와 마찬가지로, 새로운 단락은 구문 분석을 통해 strikethrough를 중단한다.

Markdown :  

      This ~~has a  

      new paragraph~~.  

Rendered Output :  

This ~~has a

new paragraph~~.

HTML :  

\<p\>This \~\~has a\</p\>  
\<p\>new paragraph\~\~.\</p\>  

## 4. Autolinks

### Autolinks란?

### Autolinks의 구성요소 :  <and to> 그리고, 더 작은 환경에서 인식될지라도, <and to>를 사용하지 않고도 구성할 수 있다.

### Autolink 특징 1 :  
- 인식된 모든 autolink는 선의 시작 부분, 공백 뒤 또는 구분문자\(\* \_ \~ \.)에만 사용할 수 있다.  
- 확장된 www 자동 링크는 텍스트 wwww.가 검색되고 유효한 도메인이 검색되면 인식된다. 유효한 도메인은 마침표(.)로 구분된 alphanumeric characters의 segments, 밑줄\(\_\) 및 하이픈(-)으로 구성된다. 기간이 하나 이상 있어야 하며 도메인의 마지막 두 segment에 밑줄이 없을 수 있다.

### EXAMPLE 1 : 스키마 http는 자동으로 삽입된다.  

Markdown :  

      www.commonmark.org

Rendered Output :  

www.commonmark.org

HTML :  

\<p\>\<a href="http://www.commonmark.org"\>www.commonmark.org\</a\>\</p\>  

### EXAMPLE 2 : 유효한 도메인 후 공백이 아닌 0자 이상의 문자가 다음에 올 수 있다.  

Markdown :  

      Visit www.commonmark.org/help for more information.  

Rendered Output :  

Visit www.commonmark.org/help for more information.

### EXAMPLE 3 : 그런 다음 확장 자동 링크 경로 검증을 적용한다. 후행 punctuation\(특히, \? \! \. \, \: \* \_ \~ \)은 링크 내부에 포함될 수 있지만 자동 링크의 일부로 간주되지 않는다.  

Markdown :  

      Visit www.commonmark.org.  

      Visit www.commonmark.org/a.b.  

Rendered Output :  

Visit www.commonmark.org.

Visit www.commonmark.org/a.b.

### EXAMPLE 4 : autolink가 \) 안에서 종ㄹ되면 전체 자동 링크에서 괄호 총 수를 scan한다. 여는 괄호보다 닫히는 괄호 수가 더 많은 경오, 괄호 안에 autolink를 포함하기 위해 autolink의 일치하지 않는 후행 괄호 부분은 고려하지 않는다.  

Markdown :  

      www.google.com/search?q=Markup+(business)  

      www.google.com/search?q=Markup+(business)))  

      (www.google.com/search?q=Markup+(business))  

      (www.google.com/search?q=Markup+(business)  

Rendered Output :  

www.google.com/search?q=Markup+(business)

www.google.com/search?q=Markup+(business)))

(www.google.com/search?q=Markup+(business))

(www.google.com/search?q=Markup+(business)

### EXAMPLE 5 : 위의 검사는 링크가 닫히는 괄호로 끝날 때만 수행되므로, autolink 내부에 parenthesis만 있는 경우 EXAMPLE 4와 같은 특별한 규칙이 적용되지 않는다.  

Markdown :  

      www.google.com/search?q=(business))+ok  

Rendered Output :  

www.google.com/search?q=(business))+ok

### EXAMPLE 6 : Autolink가 세미콜론\(/;/)으로 끝나는 경우 entity reference와 유사한지 확인한다. if the preceding text is & followed by one or more alphanumeric characters. 그렇다면 autolink에서 제외된다.  

Markdown :  

      www.google.com/search?q=commonmark&hl=en

      www.google.com/search?q=commonmark&hl;

Rendered Output :  

www.google.com/search?q=commonmark&hl=en

www.google.com/search?q=commonmark&hl;

### EXAMPLE 7 : \<는 autolink를 즉시 종료한다.  

Markdown :  

      www.commonmark.org/he<lp


Rendered Output :  

www.commonmark.org/he<lp

### EXAMPLE 8 : 확장돤 URL autolink는 경로 검증에 따라 scheme 중 하나가 http:// 또는 https:/ 뒤에 유효한 도메인이 있는 다음 zero or more non-space non-\< 문자를 사용할 때 인식된다.  

Markdown :  

      http://commonmark.org

      (Visit https://encrypted.google.com/search?q=Markup+(business))

Rendered Output :  

http://commonmark.org

(Visit https://encrypted.google.com/search?q=Markup+(business))

### Autolink 특징 2 :  
- 텍스트 노드 내에서 이메일 주소가 인식되면 확장된 이메일 autolink가 인식된다. 이메일 주소는 다음 규칙에 따라 인식된다.  
   1. Alphanumeric 또는 /., \-, \_, \+ 인 하나 이상의 문자이다.
   2. @ 기호이다.
   3. Alphanumeric 또는 \- 또는 마침표(.)로 구분된 하나 이상의 문자이다. 적어도 하나의 period가 있어야 한다. 마지막 문자는 \- 또는 \_ 중 하나일 수 없다.

### EXAMPLE 9 : The scheme mailto가 생성된 링크에 자동으로 추가된다.  

Markdown :  

      foo@bar.baz

Rendered Output :  

foo@bar.baz

### EXAMPLE 10 : \+는 \@ 앞에 쓸 수 있지만, 그 후에는 나타날 수 없다.  

Markdown :  

      hello@mail+xyz.example isn't valid, but hello+xyz@mail.example is.

Rendered Output :  

hello@mail+xyz.example isn't valid, but hello+xyz@mail.example is.

### EXAMPLE 11 :  \.\, \-\, 및 \_는 \@의 양쪽에 위치할 수 있지만, \.만 전자 메일 주소 끝에 발생할 수 있다. 이 경우에는 주소의 일부로 간주되지 않는다.  

Markdown :  

      a.b-c_d@a.b

      a.b-c_d@a.b.

      a.b-c_d@a.b-

      a.b-c_d@a.b_

Rendered Output :  

a.b-c_d@a.b

a.b-c_d@a.b.

a.b-c_d@a.b-

a.b-c_d@a.b_

## 5. Disallowed Raw HTML

### Disallowed Raw HTML이란?  
HTML 출력을 렌더링 할 때 다음과 같은 HTML 태그가 필터링 된다. \(tagfilter\)  
- \<title\>
- \<textarea\>
- \<style\>
- \<xpm\>
- \<iframe\>
- \<noembed\>
- \<script\>
- \<plaintext\>

### Disallowed Raw HTML 특징 :  
- Filtering is done by replacing the leading \< with the entity \&lt\;. 이러한 태그들은 특히 HTML이 그들 고유의 방식으로 해석되는 방법을 변경할 때 선택되며, 이것은 일반적으로 다른 랜더링된 Markdown 컨텐츠의 맥락에서 바람직하지 않다.  
- 다른 모든 HTML 태그는 그대로 유지된다.  

### EXAMPLE 1 :  

Markdown :  

      <strong> <title> <style> <em>  

      <blockquote>  
        <xmp> is disallowed.  <XMP> is also disallowed.  
      </blockquote>  

Rendered Output :  

<strong> <title> <style> <em>

<blockquote>
  <xmp> is disallowed.  <XMP> is also disallowed.
</blockquote>

HTML :  

\<p\>\<strong\> \&lt\;title\> \&lt\;style\> \<em\>\</p\>  
\<blockquote\>  
  \&lt\;xmp\> is disallowed.  \&lt\;XMP\> is also disallowed.  
\</blockquote\>
