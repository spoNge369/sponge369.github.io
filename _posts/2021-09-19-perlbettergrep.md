---
layout: single
title: greperl
author: spoNge
title: Perl as a Better grep - Linux
excerpt: "Usando Perl como un grep mejorado"
date : 2021-09-19
classes: wide
header:
  teaser: /assets/images/greperl/perl.png
  teaser_home_page: true
categories:
  - Perl
  - grep
tags:
  - perl
---

`$>` -> terminal.<br>
`#>` -> terminal con acceso root.

## Contrapartes de grep en Perl

`$>perl -wnl -e 'code' file`

 grep | Perl | Uso 
 :----: | :----: | :----:
 `grep 'RE' file`  		    | `perl -wnl -e '/RE/ and print;' file`  				  			 		  | Imprime la linea donde esta 'RE' dentro de `file`
 `grep -v 'RE' file` 		 | `perl -wnl -e '/RE/ or  print;' file`  							 		  | Imprime la linea donde NO esta 'RE' dentro de `file`
 `grep -i 'RE' file` 		 | `perl -wnl -e '/RE/i and print;' file` 							    	  | Case `i`nsensitive
 `grep -l 'RE' file1 file2` | `perl -wnl -e '/RE/ and print $ARGV and close ARGV;' file1 file2`   | Imprime los archivos donde encuentre la coincidencia
 `fgrep 'string' file`      | `perl -wnl -e '/\Qstring\E/ and print'; file`                       |
 `egrep 'RE' file`          | `perl -wnl -e '/RE/ and print;' file`  									  |

 `RE`: Expresion Regular, que es una cadena de caracteres que define un patron, pueden ser simples caracteres literales o metacaracteres.

## Parametros perl
 `-w:` Habilitar las warnings.<br>
 `-n:` Processing input - Bucle que recorre cada linea de `file` y cuyo bloque es `code`.<br>
 `-l:` Un salto de linea para cada registro de salida.<br>
 `-e 'code':` Execute el `code`.<br>


## files de pruebas


{%capture code%}direcciones.txt
Halchal Punter:1234 Disk Drive:Milpitas:ca:95035
Mooshi Pomalus:4242 Wafer Lane:San Jose:CA:95134
Thor Iverson:4789 Coffee Circle:Seattle:WA:981O7{%endcapture%}{%include code1.html code=code lang = "dat" copyable=true%}

{%capture code%}miembros.txt
Bruce Cockburn M5T 1A1
Imrat Khan 400076
Matthew Stull 98115
Torbin Ulrich 98107{%endcapture%}{%include code1.html code=code lang = "dat" copyable=true%}

{%capture code%}projects.txt
area51: ET,CYA,NOYB,UFO,NSA
glorp:  FYI,INGY,ESR 
slurm:  URI,INGY,TFM,ESR,SRV
yabl:   URL,SRV,INGY,ESR{%endcapture%}{%include code1.html code=code lang = "dat" copyable=true%}


## Algunos ejemplos

{%capture code%}❯ perl -wnl -e '/root/ and print;' /etc/passwd
root:x:0:0:root:/root:/usr/bin/zsh
nm-openvpn:x:126:131:NetworkManager OpenVPN,,,:/var/lib/openvpn/chroot:/usr/sbin/nologin{%endcapture%}
{%include code1.html code=code lang = "bash" copyable=false %}



{%capture code%}❯ perl -wnl -e '/ROot/i and print;' /etc/passwd
root:x:0:0:root:/root:/usr/bin/zsh
nm-openvpn:x:126:131:NetworkManager OpenVPN,,,:/var/lib/openvpn/chroot:/usr/sbin/nologin{%endcapture%}{%include code1.html code=code lang = "bash" copyable=false%}




{%capture code%}#Imprime solo las lineas donde aparecen 'ESR' y 'SRV'
❯ perl -wnl -e '/\bESR\b/ and /\bSRV\b/ and print;' projects.txt
slurm:  URI,INGY,TFM,ESR,SRV
yabl:   URL,SRV,INGY,ESR{%endcapture%}{%include code1.html code=code lang = "bash" copyable=false%}
