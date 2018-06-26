# utl_javascript_dygraph_graphics_multipanel_time_series
Javascript dygraph graphics multipanel time series.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.

    Javascript dygraph graphics multipanel time series

    This can be done is SAS with mouseover and html output and supports other graphic output.
    Dygraph only does time series?

      Solution in WPS Proc R

      Useful Javascrip Tools

        Dygraph
        Overlib

    see for static png
    https://tinyurl.com/ycojys9m
    https://github.com/rogerjdeangelis/utl_javascript_dygraph_graphics_multipanel_time_series/blob/master/utl_javascript_dygraph_graphics_multipanel_time_series.png

    interactive javascript dygraph (download to run)
    https://tinyurl.com/ybwqklx5
    https://github.com/rogerjdeangelis/utl_javascript_dygraph_graphics_multipanel_time_series/blob/master/utl_javascript_dygraph_graphics_multipanel_time_series.html

    github
    https://tinyurl.com/y7cedrll
    https://github.com/rogerjdeangelis/utl_javascript_dygraph_graphics_multipanel_time_series

    stackoverflow
    https://tinyurl.com/yblze928
    https://stackoverflow.com/questions/51007551/displaying-multiple-dygraphs-on-a-grid-in-r-markdown

    Yuri Kleb profile
    https://stackoverflow.com/users/6679071/yurikleb

    INPUT
    =====

      SD1.HAVE

            TIME    MDEATHS    FDEATHS    LDEATHS    MDEATHX

       26JUN2018      2134        901       3035       2134
       27JUN2018      1863        689       2552       1863
       28JUN2018      1877        827       2704       1877
       29JUN2018      1877        677       2554       1877
       30JUN2018      1492        522       2014       1492
       01JUL2018      1249        406       1655       1249
       02JUL2018      1280        441       1721       1280
     ....

    EXAMPLE OUTPUT ( Stacked Dygraphs)
    ===================================


      3000 +
           |               *
           |
           |   *     **     *    *     *     *
      2000 +    *    *    **    *      **
           |   *    * *          **   *     ***
           |     * **  *  * *   *       *     *
           |     ***   ***   * *   * **  * *   *  *
      1000 +             *    **    **    ***  ***
           ---+---------+---------+---------+---------+--
          25JUN2018 15JUL2018 04AUG2018 24AUG2018 13SEP2018

      1500 +
           |
           |               *
      1000 +
           |   **    **   ***   **     *     *
           |   **   * *          **   * *   * *
       500 +     ****  **** ** **  *    *****  *  *
           |     ***    **    **   ****   **    **
           |
         0 +
           ---+---------+---------+---------+---------+--
          25JUN2018 15JUL2018 04AUG2018 24AUG2018 13SEP2018

      4000 +               *
           |
           |                *
      3000 +   *     **   *      *     *     *
           |   **   *      *    *      **    **
           |        * *          **   *     *
      2000 +     * *   *  * *   *       **    *   *
           |     ***   ***   * *   * **  ****  *  *
           |             *    **    **    **    **
      1000 +
           ---+---------+---------+---------+---------+--
          25JUN2018 15JUL2018 04AUG2018 24AUG2018 13SEP2018

      3000 +
           |               *
           |
           |   *     **     *    *     *     *
      2000 +    *    *    **    *      **
           |   *    * *          **   *     ***
           |     * **  *  * *   *       *     *
           |     ***   ***   * *   * **  * *   *  *
      1000 +             *    **    **    ***  ***
           ---+---------+---------+---------+---------+--
          25JUN2018 15JUL2018 04AUG2018 24AUG2018 13SEP2018



    PROCESS  ( All the code)
    =========================

     1. Convert sas dataset to a R time series object
     2. Create a function to create one time series plot
     3. Call the function 4 times to stack the plots
     4. Output the Javascript

    %utlfkil(d:/htm/htm.html); * delete if exist;

    %utl_submit_wps64('
    libname sd1 "d:/sd1";
    options set=R_HOME "C:/Program Files/R/R-3.3.2";
    proc r;
    submit;
      ```{r graphs};
      source("C:/Program Files/R/R-3.3.2/etc/Rprofile.site", echo=T);
      library(dygraphs);
      library(htmltools);
      library(haven);
      library(xts);
      lungDeath<-as.data.frame(read_sas("d:/sd1/have.sas7bdat"));
      head(lungDeath);
      lungDeaths<- xts(lungDeath[,-1], order.by = lungDeath[,1]);
      makeGraphs = function(i){
      theGraph <- dygraph(lungDeaths[, i], main = " ", width = 1000, height = 250, group = "lung-deaths")%>%
        dyOptions(strokeWidth = 3) %>%
        dyRangeSelector(height = 20);
        htmltools::tags$div(theGraph, style = "padding:10px; width: 1000px;  padding: 1em;
           display:inline-block;  border: solid; background-color:#e9e9e9;");
      };
      res <- lapply(1:4, makeGraphs);
      htm<-htmltools::tagList(res);
      save_html(htm, "d:/htm/utl_javascript_dygraph_graphics_multipanel_time_series.html",
        background = "white", libdir = "lib");
      ```;
    endsubmit;
    run;quit;
    ');

    OUTPUT
    ======

      https://tinyurl.com/ycojys9m   * Static png
      https://tinyurl.com/ybwqklx5   * Javascript

    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
      format time date9.;
      input mdeaths fdeaths ldeaths mdeathx @@;
      time=today() + _n_;
    cards4;
    2134 901 3035 2134 1863 689 2552 1863 1877 827 2704 1877 1877 677 2554 1877 1492
    522 2014 1492 1249 406 1655 1249 1280 441 1721 1280 1131 393 1524 1131 1209 387
    1596 1209 1492 582 2074 1492 1621 578 2199 1621 1846 666 2512 1846 2103 830 2933
    2103 2137 752 2889 2137 2153 785 2938 2153 1833 664 2497 1833 1403 467 1870 1403
    1288 438 1726 1288 1186 421 1607 1186 1133 412 1545 1133 1053 343 1396 1053 1347
    440 1787 1347 1545 531 2076 1545 2066 771 2837 2066 2020 767 2787 2020 2750 1141
    3891 2750 2283 896 3179 2283 1479 532 2011 1479 1189 447 1636 1189 1160 420 1580
    1160 1113 376 1489 1113 970 330 1300 970 999 357 1356 999 1208 445 1653 1208
    1467 546 2013 1467 2059 764 2823 2059 2240 862 3102 2240 1634 660 2294 1634 1722
    663 2385 1722 1801 643 2444 1801 1246 502 1748 1246 1162 392 1554 1162 1087 411
    1498 1087 1013 348 1361 1013 959 387 1346 959 1179 385 1564 1179 1229 411 1640
    1229 1655 638 2293 1655 2019 796 2815 2019 2284 853 3137 2284 1942 737 2679 1942
    1423 546 1969 1423 1340 530 1870 1340 1187 446 1633 1187 1098 431 1529 1098 1004
    362 1366 1004 970 387 1357 970 1140 430 1570 1140 1110 425 1535 1110 1812 679
    2491 1812 2263 821 3084 2263 1820 785 2605 1820 1846 727 2573 1846 1531 612 2143
    1531 1215 478 1693 1215 1075 429 1504 1075 1056 405 1461 1056 975 379 1354 975
    940 393 1333 940 1081 411 1492 1081 1294 487 1781 1294 1341 574 1915 1341
    ;;;;
    run;quit;

    proc print data=sd1.have;
    run;quit;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    see process



