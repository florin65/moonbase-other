prefix=/usr

gcc -O4 -march=native -o dcraw dcraw.c \
        -Wall -Wno-unused-result -Wno-array-bounds -Wno-maybe-uninitialized \
        -Wno-unused-but-set-variable \
        -lm -ljasper -ljpeg -llcms2 -s -DLOCALEDIR=\"$prefix/share/locale/\"

prepare_install &&
install -Dm755 dcraw /usr/bin/dcraw &&
install -Dm644 dcraw.1 /usr/share/man/man1/dcraw.1 &&

for langchar in \
  fr.latin1 it.latin1 de.latin1 pt.latin1 es.latin1 nl.latin1 sv.latin1 \
  ca.latin1 da.latin1 cs.latin2 hu.latin2 pl.latin2 ro.latin2 eo.latin3 \
  ru.koi8-r ja.euc-jp zh_TW.big5 zh_CN.gb2312
do
  lang=`echo $langchar | cut -d. -f1` &&
  char=`echo $langchar | cut -d. -f2-` &&
  mkdir -p -m 755 $prefix/share/man/$lang/man1 &&
  iconv -f utf-8 -t $char dcraw_$lang.1 > $prefix/share/man/$lang/man1/dcraw.1 &&
  mkdir -p -m 755 $prefix/share/man/$lang.UTF-8/man1 &&
  cp dcraw_$lang.1 $prefix/share/man/$lang.UTF-8/man1/dcraw.1 &&
  mkdir -p -m 755 $prefix/share/locale/$lang/LC_MESSAGES 
  msgfmt -o $prefix/share/locale/$lang/LC_MESSAGES/dcraw.mo dcraw_$lang.po
done
