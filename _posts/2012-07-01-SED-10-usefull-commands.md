---
ID: 51
post_title: 10 Example of SED
author: Rahul Patil
post_date: 2012-07-01 15:47:00
categories: ['sed']
post_excerpt: ""
layout: post
published: true
dsq_thread_id:
- "2080350988"
---
when you are write a script and if you want to edit some file from command line, then you can use sed. 10 Basic examples that I’ve provided here, you’ll find using command line more enjoyable and fun.

About SED

sed is an Non-interactive stream editor.

Features
<ul>
<li>scripting languages</li>
<li>work primarily with text file.</li>
<li>programmable editor.</li>
<li>accept command-line option and can be scripted ( sed -f script_name )</li>
<li>GNU versions supports POSIX (Grep) and (Egrep) regexes</li>
<li>Does not operate on the source file , by default , its only print the changes in source file exept ( -i option).</li>
<li>supports address to indicate to which lines operate on : /^$/d - delete blank lines .</li>
</ul>
Usage

```shell

sed [ Options ] ' instruction ' file     | PIPE | STDIN
```

Some examples

<strong>1. Print line no. from file (it will print line 1 to 5 .)</strong>

```shell
sed -n '1,5p' filename
```

<strong>2.</strong> <strong>Print lines except  1 to 6 line.</strong>

```shell
sed -n '1,6!p'  filename
```

<strong>3. Print below two lines from matches word</strong>

```shell
sed -ne '/word/,+2p' filename
```

<strong>4. Delete two lines with matches word</strong>

```shell

sed -e '/word/,+2d' filename

```

<strong>5. Delete below 2 lines from match word</strong>

```shell
sed -e '/5/{n;N;d}' filename
```

<strong>6. search two words</strong>

```shell
sed -ne '/monkey/,/donkey/p' filename
```

<strong>7. delete blank file (-i = edit source file and backup sourch file (filename.bak))</strong>

```shell
sed -i.bak '/^$/d' filename
```

<strong>8. delete second line after first line</strong>

```shell
sed -ne '1~2p'  filename
```

<strong>9. Search and Replace</strong>

g = Global
s = search
I = incasecensitive

```shell
sed -e 's/find/replace/g' filename
```

<strong>10. Multiple instruction</strong>

it will delete blank lines then search RAM and replace SHYAM (only print not change in source file )

```shell
sed -e '/^$/d' -e 's/RAM/SHYAM/g' filename
```

or

```shell
sed -e '/^$/d' ; 's/RAM/SHYAM/g' filename
```

the line contain "NAME" in the same line search RAM and replace SHYAM.

```shell
sed -e '/NAME/s/RAM/SHYAM/g' filename
```
