HTML cleaner for Galileo openbooks
==================================

This is a tool for cleaning up [Galileo Computing openbooks](http://www.galileocomputing.de/openbook)
before converting them to EPUB or PDF format. It is meant to be an improved reimplementation of my
[bash shell script using xml2](https://github.com/kriegaex/html_book_cleaner). In opposite to the
script which is just meant to be a proof of concept for two books, this tool is meant to convert
*__all__* books.

__Current state of development:__ The tool can convert all openbooks, but in opposite to the shell
script version it does not download and unpack them automatically beforehand.

__Dependencies:__ The tool was developed in Java 7, but might work in older JREs too (untested).
It also uses a few open source libraries:
  * [JTidy r938](http://jtidy.sourceforge.net/) for converting the original Galileo files from
    unclean HTML into XHTML and also for pretty-printing the final result (XOM does not pretty-print).
    *__Please note__* that *JTidy* itself needs two patches I created because otherwise it cannot
    handle all of Galileo's faulty HTML. The patched files are part of this repository, so they will
    overrule the original classes as long as they come first in the Java classpath.
    Direct JAR download: [jtidy-r938.jar](http://sourceforge.net/projects/jtidy/files/JTidy/r938/jtidy-r938.jar/download)
    You can also find the patches in the following *JTidy* bug tickets:
      * [BR within PRE rendered with additional linefeeds - ID: 3532720]
        (http://sourceforge.net/tracker/?func=detail&aid=3532720&group_id=13153&atid=113153)
      * [Non-breaking space in HEAD rejected - ID: 3532726]
        (http://sourceforge.net/tracker/?func=detail&aid=3532726&group_id=13153&atid=113153)
  * [XOM 1.2.8](http://www.xom.nu/) is an XML library used for parsing the XHTML output of *JTidy*
    into a DOM representation which can then be manipulated via XPath queries. The main part of the
    clean-up work is done using *XOM*.
    Direct JAR download: [xom-1.2.8.jar](http://www.cafeconleche.org/XOM/xom-1.2.8.jar)
  * [TagSoup 1.2.1](http://ccil.org/~cowan/XML/tagsoup/) is a SAX-compliant HTML parser which nicely
    integrates into *XOM*. Initially I had planned to use it directly for parsing the original HTML
    files, but it could not handle them well, so I added *JTidy* to the mix. Unfortunately *JTidy*
    has no direct *XOM* integration because it is not SAX-compliant, so it cannot replace *TagSoup*.
    This is how I ended up using both libraries. Maybe I will find a way to remove one of them in
    the future.
    Direct JAR download: [tagsoup-1.2.1.jar](http://ccil.org/~cowan/XML/tagsoup/tagsoup-1.2.1.jar)

__To do:__
* I want to add the missing download and unpack steps, so the tool can be used stand-alone and
  fully replace the old shell script. *[Done, available in master, not in download JAR yet.]*
* I dislike the current code structure and want to do some refactoring. Because I have not programmed
  in a long time (I used to be a full-time developer in the 1990s and am a project management coach
  now), development is not my daily work anymore, so even though I already refactored a lot of things
  before the initial upload, there is still a lot to be done to satisfy my own demands from a design
  and [software craftsmanship](http://en.wikipedia.org/wiki/Software_craftsmanship) perspective. See
  also the book [Clean Code](http://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)
  by Robert C. Martin. *[Partly done, available in master, not in download JAR yet.]*
* I am not sure about it, but I might start writing *unit tests* for the tool if I ever feel like it.
  Practicing a bit of TDD is something I have not done in a long time, except for recommending and
  introducing it to my clients as an agile coach. I would not consider myself a professional developer
  without practicing TDD, but after all I am no longer a professional developer. ;-)

Because of the missing features and open bugs as well as the *clean code* and *refactoring* stuff
mentioned above and because I want to learn about the *Git* integration in *Eclipse* (I currently only
know a bit of *Git* command-line stuff), I guess it will be nice to do this step by step, documenting
my progress in small, fine-granular *Git* changesets, so later on I can review my own progress.
*[Partly done, available in master, not in download JAR yet.]*

As you can see, I am mostly doing this little project for myself, but I like to share the results and
receive some user feedback. I hope the openbook cleaner is useful to you. Enjoy! :-)

Alexander Kriegisch
