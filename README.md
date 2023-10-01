# utl-merging-inner-join-dataframes-based-on-single-primary-key-in-wps-r-python-sql-nosql
Inner join of datasets hav1 and hav2 on primary key 'gene' 
    %let pgm=utl-merging-inner-join-dataframes-based-on-single-primary-key-in-wps-r-python-sql-nosql;

    Problem

       Inner join of datasets hav1 and hav2 on primary key 'gene'

    github
    https://tinyurl.com/5a4nw9y8
    https://github.com/rogerjdeangelis/utl-merging-inner-join-dataframes-based-on-single-primary-key-in-wps-r-python-sql-nosql

    stackoverflow
    https://tinyurl.com/5n6whnns
    https://stackoverflow.com/questions/77204849/merging-dataframes-based-on-common-rows-in-r

       SOLUTIONS

          1 wps sql (uses sql arrys)
            Paraphrase: select l.*, r.* from hav1 as l, hav2 as r where r.gene=l.gene

          2 wps r base
            want<-merge(havone, havtwo,  by = "GENE");
            https://stackoverflow.com/users/646761/margusl

          3 wps r sql
            Paraphrase: select l.*, r.* from hav1 as l, hav2 as r where r.gene=l.gene

          3 wps r sql
            Paraphrase: select l.*, r.* from hav1 as l, hav2 as r where r.gene=l.gene
    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.hav1;
    informat gene $8.;
    input
      gene    C12    C24    C48    C72    T12    T24    T48    T72;
    cards4;
    Gnai3 514 319 974 198 936 829 807 882
    Cdc45  40  22  16  33  44   0   6  32
    H19     0   0   0   0   0   0   0  10
    Scml2  28  43  25  10  79   0  26  46
    Apoh   34   0   0   0  16  16   0   2
    Narf  238 190 122 181 122  60  54 118
    Cav2  199  53  36 130  80   6  17  79
    Klf6  478 471 337 059 987 522 117 298
    Scmh1 239 464 872 254 307 799 869 959
    Cox5a 144  68  97 112 251  23 163  71
    Tbx2    8   9   4   5  13   0   8   9
    Ngfr   51  60  50  32  46  57   0  10
    ;;;;
    run;quit;


    data sd1.hav2;
    informat gene $8.;
    input
      gene   C12   C24    C48    C72    T12   T24    T48    T72;
    cards4;
    Gnai3 171 446 278 876 876  45 582 040
    Cdc45  47   9  19  41  22   0  38  78
    H19    77  52  33  36 177  34 402 458
    Scml2   2   0  10   3  12   0   0   9
    Narf   43   5   4  27  35   2  23 135
    Cav2   54  23   5  10  64   0  30  40
    Klf6  498 730 454  33 616 421 389 950
    Scmh1 591 129 260 273 457  29 303 534
    Cox5a  70  21  39  51 225  25 321  98
    Tbx2    6   0   0  10   3   0   7  11
    Tbx4    5   0   0   0   5   0   3   9
    Ngfr   14   8  21  33   9  18  22  40
    ;;;;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* INNER JOIN OF HAV1 to HAV2 on GENE                                                                                     */
    /*  _                   _                                                                                                 */
    /* (_)_ __  _ __  _   _| |_ ___                                                                                           */
    /* | | `_ \| `_ \| | | | __/ __|                                                                                          */
    /* | | | | | |_) | |_| | |_\__ \                                                                                          */
    /* |_|_| |_| .__/ \__,_|\__|___/                                                                                          */
    /*         |_|                                                                                                            */
    /*                                                                                                                        */
    /* SD1.HAV1 total obs=12                                                                                                  */
    /*                                                                                                                        */
    /* ONLY HENE Apoh is not in both datasets                                                                                 */
    /*                                                                                                                        */
    /* Obs    GENE     C12    C24    C48    C72    T12    T24    T48    T72                                                   */
    /*                                                                                                                        */
    /*   5    Apoh      34      0      0      0     16     16      0      2                                                   */
    /*                                                                                                                        */
    /* SD1.HAV1 total obs=12                                                                                                  */
    /*                                                                                                                        */
    /* Obs    GENE     C12    C24    C48    C72    T12    T24    T48    T72                                                   */
    /*                                                                                                                        */
    /*   1    Gnai3    514    319    974    198    936    829    807    882                                                   */
    /*   2    Cdc45     40     22     16     33     44      0      6     32                                                   */
    /*   3    H19        0      0      0      0      0      0      0     10                                                   */
    /*   4    Scml2     28     43     25     10     79      0     26     46                                                   */
    /*   5    Apoh      34      0      0      0     16     16      0      2                                                   */
    /*   6    Narf     238    190    122    181    122     60     54    118                                                   */
    /*   7    Cav2     199     53     36    130     80      6     17     79                                                   */
    /*   8    Klf6     478    471    337     59    987    522    117    298                                                   */
    /*   9    Scmh1    239    464    872    254    307    799    869    959                                                   */
    /*  10    Cox5a    144     68     97    112    251     23    163     71                                                   */
    /*  11    Tbx2       8      9      4      5     13      0      8      9                                                   */
    /*  12    Ngfr      51     60     50     32     46     57      0     10                                                   */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* SD1.HAV2 total obs=12                                                                                                  */
    /*                                                                                                                        */
    /* Obs    GENE     C12    C24    C48    C72    T12    T24    T48    T72                                                   */
    /*                                                                                                                        */
    /*   1    Gnai3    171    446    278    876    876     45    582     40                                                   */
    /*   2    Cdc45     47      9     19     41     22      0     38     78                                                   */
    /*   3    H19       77     52     33     36    177     34    402    458                                                   */
    /*   4    Scml2      2      0     10      3     12      0      0      9                                                   */
    /*   5    Narf      43      5      4     27     35      2     23    135                                                   */
    /*   6    Cav2      54     23      5     10     64      0     30     40                                                   */
    /*   7    Klf6     498    730    454     33    616    421    389    950                                                   */
    /*   8    Scmh1    591    129    260    273    457     29    303    534                                                   */
    /*   9    Cox5a     70     21     39     51    225     25    321     98                                                   */
    /*  10    Tbx2       6      0      0     10      3      0      7     11                                                   */
    /*  11    Tbx4       5      0      0      0      5      0      3      9                                                   */
    /*  12    Ngfr      14      8     21     33      9     18     22     40                                                   */
    /*              _               _                                                                                         */
    /*   ___  _   _| |_ _ __  _   _| |_                                                                                       */
    /*  / _ \| | | | __| `_ \| | | | __|                                                                                      */
    /* | (_) | |_| | |_| |_) | |_| | |_                                                                                       */
    /*  \___/ \__,_|\__| .__/ \__,_|\__|                                                                                      */
    /*                 |_|                                                                                                    */
    /*                                                                                                                        */
    /*                  FROM SD1.HAV1                                         FROM SD1.HAV2                                   */
    /*            ===============================================   ===============================================           */
    /* Obs GENE_1 C12_1 C24_1 C48_1 C72_1 T12_1 T24_1 T48_1 T72_1   C12_2 C24_2 C48_2 C72_2 T12_2 T24_2 T48_2 T72_2           */
    /*                                                                                                                        */
    /*   1  Gnai3   514   319   974   198   936   829   807   882     171   446   278   876   876    45   582    40           */
    /*   2  Cdc45    40    22    16    33    44     0     6    32      47     9    19    41    22     0    38    78           */
    /*   3  H19       0     0     0     0     0     0     0    10      77    52    33    36   177    34   402   458           */
    /*   4  Scml2    28    43    25    10    79     0    26    46       2     0    10     3    12     0     0     9           */
    /*   5  Narf    238   190   122   181   122    60    54   118      43     5     4    27    35     2    23   135           */
    /*   6  Cav2    199    53    36   130    80     6    17    79      54    23     5    10    64     0    30    40           */
    /*   7  Klf6    478   471   337    59   987   522   117   298     498   730   454    33   616   421   389   950           */
    /*   8  Scmh1   239   464   872   254   307   799   869   959     591   129   260   273   457    29   303   534           */
    /*   9  Cox5a   144    68    97   112   251    23   163    71      70    21    39    51   225    25   321    98           */
    /*  10  Tbx2      8     9     4     5    13     0     8     9       6     0     0    10     3     0     7    11           */
    /*  11  Ngfr     51    60    50    32    46    57     0    10      14     8    21    33     9    18    22    40           */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*                                  _
    / | __      ___ __  ___   ___  __ _| |
    | | \ \ /\ / / `_ \/ __| / __|/ _` | |
    | |  \ V  V /| |_) \__ \ \__ \ (_| | |
    |_|   \_/\_/ | .__/|___/ |___/\__, |_|
                 |_|                 |_|
    */
    %array(_rn,values=%utl_varlist(sd1.hav1));

    %put &=_rn3; /*---- _RN3=C24                                             ----*/
    %put &=_rnn; /*---- _RNN=9                                               ----*/

    %utl_submit_wps64x("
    options validvarname=any;
    libname sd1 'd:/sd1';
    proc sql;
      create
         table sd1.want as
      select
         %do_over(_rn,phrase=l.? as ?_1,between=comma)
        ,%do_over(_rn,phrase=r.? as ?_2,between=comma)
      from
         sd1.hav1 as l inner join sd1.hav2 as r
      on
         l.gene = r.gene
    ;quit;
    ");

    proc print data=sd1.want width=min;;
    run;quit;

    */ /*************************************************************************************************************************
    */ /*
    */ /* GENERATED CODE
    */ /*
    */ /* data _null_;
    */ /*   %do_over(_rn,phrase=%str(put ",l.? as ?_1";));
    */ /* run;quit;
    */ /*
    */ /* ,l.GENE as GENE_1
    */ /* ,l.C12 as C12_1
    */ /* ,l.C24 as C24_1
    */ /* ,l.C48 as C48_1
    */ /* ,l.C72 as C72_1
    */ /* ,l.T12 as T12_1
    */ /* ,l.T24 as T24_1
    */ /* ,l.T48 as T48_1
    */ /* ,l.T72 as T72_1
    */ /*
    */ /*
    */ /*                  FROM SD1.HAV1                                         FROM SD1.HAV2
    */ /*            ===============================================   ===============================================
    */ /* Obs GENE_1 C12_1 C24_1 C48_1 C72_1 T12_1 T24_1 T48_1 T72_1   C12_2 C24_2 C48_2 C72_2 T12_2 T24_2 T48_2 T72_2
    */ /*
    */ /*   1  Gnai3   514   319   974   198   936   829   807   882     171   446   278   876   876    45   582    40
    */ /*   2  Cdc45    40    22    16    33    44     0     6    32      47     9    19    41    22     0    38    78
    */ /*   3  H19       0     0     0     0     0     0     0    10      77    52    33    36   177    34   402   458
    */ /*   4  Scml2    28    43    25    10    79     0    26    46       2     0    10     3    12     0     0     9
    */ /*   5  Narf    238   190   122   181   122    60    54   118      43     5     4    27    35     2    23   135
    */ /*   6  Cav2    199    53    36   130    80     6    17    79      54    23     5    10    64     0    30    40
    */ /*   7  Klf6    478   471   337    59   987   522   117   298     498   730   454    33   616   421   389   950
    */ /*   8  Scmh1   239   464   872   254   307   799   869   959     591   129   260   273   457    29   303   534
    */ /*   9  Cox5a   144    68    97   112   251    23   163    71      70    21    39    51   225    25   321    98
    */ /*  10  Tbx2      8     9     4     5    13     0     8     9       6     0     0    10     3     0     7    11
    */ /*  11  Ngfr     51    60    50    32    46    57     0    10      14     8    21    33     9    18    22    40
    */ /*
    */ /*************************************************************************************************************************

    /*___                                _
    |___ \  __      ___ __  ___   _ __  | |__   __ _ ___  ___
      __) | \ \ /\ / / `_ \/ __| | `__| | `_ \ / _` / __|/ _ \
     / __/   \ V  V /| |_) \__ \ | |    | |_) | (_| \__ \  __/
    |_____|   \_/\_/ | .__/|___/ |_|    |_.__/ \__,_|___/\___|
                     |_|
    */

    proc datasets lib=sd1 nolist nodetails;delete want; run;quit;

    %utl_submit_wps64('
    options validvarname=upcase;
    libname sd1 "d:/sd1";
    proc r;
    export data=sd1.hav1 r=havone;
    export data=sd1.hav2 r=havtwo;
    submit;
    want<-merge(havone, havtwo,  by = "GENE");
    want;
    endsubmit;
    import data=sd1.want r=want;
    run;quit;
    ');

    proc print data=sd1.want width=min;;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* The WPS Proc R                                                                                                         */
    /*                                                                                                                        */
    /*     GENE C12.x C24.x C48.x C72.x T12.x T24.x T48.x T72.x C12.y C24.y C48.y C72.y T12.y T24.y T48.y T72.y               */
    /* 1   Cav2   199    53    36   130    80     6    17    79    54    23     5    10    64     0    30    40               */
    /* 2  Cdc45    40    22    16    33    44     0     6    32    47     9    19    41    22     0    38    78               */
    /* 3  Cox5a   144    68    97   112   251    23   163    71    70    21    39    51   225    25   321    98               */
    /* 4  Gnai3   514   319   974   198   936   829   807   882   171   446   278   876   876    45   582    40               */
    /* 5    H19     0     0     0     0     0     0     0    10    77    52    33    36   177    34   402   458               */
    /* 6   Klf6   478   471   337    59   987   522   117   298   498   730   454    33   616   421   389   950               */
    /* 7   Narf   238   190   122   181   122    60    54   118    43     5     4    27    35     2    23   135               */
    /* 8   Ngfr    51    60    50    32    46    57     0    10    14     8    21    33     9    18    22    40               */
    /* 9  Scmh1   239   464   872   254   307   799   869   959   591   129   260   273   457    29   303   534               */
    /* 10 Scml2    28    43    25    10    79     0    26    46     2     0    10     3    12     0     0     9               */
    /* 11  Tbx2     8     9     4     5    13     0     8     9     6     0     0    10     3     0     7    11               */
    /*                                                                                                                        */
    /* WPS                                                                                                                    */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* GENE  C12_X C24_X C48_X C72_X T12_X T24_X T48_X T72_X C12_Y C24_Y C48_Y C72_Y T12_Y T24_Y T48_Y T72_Y                  */
    /*                                                                                                                        */
    /* Cav2   199    53    36   130    80     6    17    79    54    23     5    10    64     0    30    40                   */
    /* Cdc45   40    22    16    33    44     0     6    32    47     9    19    41    22     0    38    78                   */
    /* Cox5a  144    68    97   112   251    23   163    71    70    21    39    51   225    25   321    98                   */
    /* Gnai3  514   319   974   198   936   829   807   882   171   446   278   876   876    45   582    40                   */
    /* H19      0     0     0     0     0     0     0    10    77    52    33    36   177    34   402   458                   */
    /* Klf6   478   471   337    59   987   522   117   298   498   730   454    33   616   421   389   950                   */
    /* Narf   238   190   122   181   122    60    54   118    43     5     4    27    35     2    23   135                   */
    /* Ngfr    51    60    50    32    46    57     0    10    14     8    21    33     9    18    22    40                   */
    /* Scmh1  239   464   872   254   307   799   869   959   591   129   260   273   457    29   303   534                   */
    /* Scml2   28    43    25    10    79     0    26    46     2     0    10     3    12     0     0     9                   */
    /* Tbx2     8     9     4     5    13     0     8     9     6     0     0    10     3     0     7    11                   */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____                                         _
    |___ /  __      ___ __  ___   _ __   ___  __ _| |
      |_ \  \ \ /\ / / `_ \/ __| | `__| / __|/ _` | |
     ___) |  \ V  V /| |_) \__ \ | |    \__ \ (_| | |
    |____/    \_/\_/ | .__/|___/ |_|    |___/\__, |_|
                     |_|                        |_|
    */
    proc datasets lib=sd1 nolist nodetails;delete want; run;quit;

    options validvarname=any;
    libname sd1 "d:/sd1";

    %utl_submit_wps64x("
    libname sd1 'd:/sd1';
    proc r;
    export data=sd1.hav1 r=hav1;
    export data=sd1.hav2 r=hav2;
    submit;
    library(sqldf);
    want<-sqldf('
      select
         %do_over(_rn,phrase=l.? as ?_1,between=comma)
        ,%do_over(_rn,phrase=r.? as ?_2,between=comma)
      from
         hav1 as l inner join hav2 as r
      on
         l.gene = r.gene

    ');
    want;
    endsubmit;
    import data=sd1.want r=want;
    run;quit;
    ");

    proc print data=sd1.want width=min;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* The WPS Proc R SQL                                                                                                     */
    /*                                                                                                                        */
    /*    GENE_1 C12_1 C24_1 C48_1 C72_1 T12_1 T24_1 T48_1 T72_1 GENE_2 C12_2 C24_2 C48_2 C72_2 T12_2 T24_2 T48_2 T72_2       */
    /* 1   Gnai3   514   319   974   198   936   829   807   882  Gnai3   171   446   278   876   876    45   582    40       */
    /* 2   Cdc45    40    22    16    33    44     0     6    32  Cdc45    47     9    19    41    22     0    38    78       */
    /* 3     H19     0     0     0     0     0     0     0    10    H19    77    52    33    36   177    34   402   458       */
    /* 4   Scml2    28    43    25    10    79     0    26    46  Scml2     2     0    10     3    12     0     0     9       */
    /* 5    Narf   238   190   122   181   122    60    54   118   Narf    43     5     4    27    35     2    23   135       */
    /* 6    Cav2   199    53    36   130    80     6    17    79   Cav2    54    23     5    10    64     0    30    40       */
    /* 7    Klf6   478   471   337    59   987   522   117   298   Klf6   498   730   454    33   616   421   389   950       */
    /* 8   Scmh1   239   464   872   254   307   799   869   959  Scmh1   591   129   260   273   457    29   303   534       */
    /* 9   Cox5a   144    68    97   112   251    23   163    71  Cox5a    70    21    39    51   225    25   321    98       */
    /* 10   Tbx2     8     9     4     5    13     0     8     9   Tbx2     6     0     0    10     3     0     7    11       */
    /* 11   Ngfr    51    60    50    32    46    57     0    10   Ngfr    14     8    21    33     9    18    22    40       */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*  _                                      _   _                             _
    | || |   __      ___ __  ___   _ __  _   _| |_| |__   ___  _ __    ___  __ _| |
    | || |_  \ \ /\ / / `_ \/ __| | `_ \| | | | __| `_ \ / _ \| `_ \  / __|/ _` | |
    |__   _|  \ V  V /| |_) \__ \ | |_) | |_| | |_| | | | (_) | | | | \__ \ (_| | |
       |_|     \_/\_/ | .__/|___/ | .__/ \__, |\__|_| |_|\___/|_| |_| |___/\__, |_|
                      |_|         |_|    |___/                                |_|
    */

    proc datasets lib=sd1 nolist nodetails;delete want; run;quit;

    options validvarname=any;
    libname sd1 "d:/sd1";

    %utl_submit_wps64x("
    libname sd1 'd:/sd1';
    proc python;
    export data=sd1.hav1 python=hav1;
    export data=sd1.hav2 python=hav2;
    submit;
    from os import path;
    import pandas as pd;
    import numpy as np;
    import pandas as pd;
    from pandasql import sqldf;
    mysql = lambda q: sqldf(q, globals());
    from pandasql import PandaSQL;
    pdsql = PandaSQL(persist=True);
    sqlite3conn = next(pdsql.conn.gen).connection.connection;
    sqlite3conn.enable_load_extension(True);
    sqlite3conn.load_extension('c:/temp/libsqlitefunctions.dll');
    mysql = lambda q: sqldf(q, globals());
    want = pdsql('''
      select
         %do_over(_rn,phrase=l.? as ?_1,between=comma)
        ,%do_over(_rn,phrase=r.? as ?_2,between=comma)
      from
         hav1 as l inner join hav2 as r
      on
         l.gene = r.gene

    ''');
    print(want);
    endsubmit;
    import data=sd1.want python=want;
    run;quit;
    ");

    proc print data=sd1.want;
    run;quit;

    /*----                                                                   ----*/
    /*---- Remove macro array                                                ----*/
    /*----                                                                   ----*/

    %arraydelete(_rn);


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* The WPS PYTHON Procedure                                                                                               */
    /*                                                                                                                        */
    /*       GENE_1  C12_1  C24_1  C48_1  C72_1  ...  C72_2  T12_2  T24_2  T48_2  T72_2                                       */
    /* 0   Gnai3     514.0  319.0  974.0  198.0  ...  876.0  876.0   45.0  582.0   40.0                                       */
    /* 1   Cdc45      40.0   22.0   16.0   33.0  ...   41.0   22.0    0.0   38.0   78.0                                       */
    /* 2   H19         0.0    0.0    0.0    0.0  ...   36.0  177.0   34.0  402.0  458.0                                       */
    /* 3   Scml2      28.0   43.0   25.0   10.0  ...    3.0   12.0    0.0    0.0    9.0                                       */
    /* 4   Narf      238.0  190.0  122.0  181.0  ...   27.0   35.0    2.0   23.0  135.0                                       */
    /* 5   Cav2      199.0   53.0   36.0  130.0  ...   10.0   64.0    0.0   30.0   40.0                                       */
    /* 6   Klf6      478.0  471.0  337.0   59.0  ...   33.0  616.0  421.0  389.0  950.0                                       */
    /* 7   Scmh1     239.0  464.0  872.0  254.0  ...  273.0  457.0   29.0  303.0  534.0                                       */
    /* 8   Cox5a     144.0   68.0   97.0  112.0  ...   51.0  225.0   25.0  321.0   98.0                                       */
    /* 9   Tbx2        8.0    9.0    4.0    5.0  ...   10.0    3.0    0.0    7.0   11.0                                       */
    /* 10  Ngfr       51.0   60.0   50.0   32.0  ...   33.0    9.0   18.0   22.0   40.0                                       */
    /*                                                                                                                        */
    /*                                                                                                                        */
    .* The WPS                                                                                                                */
    /*                                                                                                                        */
    /*    GENE_1 C12_1 C24_1 C48_1 C72_1 T12_1 T24_1 T48_1 T72_1 GENE_2 C12_2 C24_2 C48_2 C72_2 T12_2 T24_2 T48_2 T72_2       */
    /* 1   Gnai3   514   319   974   198   936   829   807   882  Gnai3   171   446   278   876   876    45   582    40       */
    /* 2   Cdc45    40    22    16    33    44     0     6    32  Cdc45    47     9    19    41    22     0    38    78       */
    /* 3     H19     0     0     0     0     0     0     0    10    H19    77    52    33    36   177    34   402   458       */
    /* 4   Scml2    28    43    25    10    79     0    26    46  Scml2     2     0    10     3    12     0     0     9       */
    /* 5    Narf   238   190   122   181   122    60    54   118   Narf    43     5     4    27    35     2    23   135       */
    /* 6    Cav2   199    53    36   130    80     6    17    79   Cav2    54    23     5    10    64     0    30    40       */
    /* 7    Klf6   478   471   337    59   987   522   117   298   Klf6   498   730   454    33   616   421   389   950       */
    /* 8   Scmh1   239   464   872   254   307   799   869   959  Scmh1   591   129   260   273   457    29   303   534       */
    /* 9   Cox5a   144    68    97   112   251    23   163    71  Cox5a    70    21    39    51   225    25   321    98       */
    /* 10   Tbx2     8     9     4     5    13     0     8     9   Tbx2     6     0     0    10     3     0     7    11       */
    /* 11   Ngfr    51    60    50    32    46    57     0    10   Ngfr    14     8    21    33     9    18    22    40       */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
