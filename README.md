# utl-enhanced-ascii-graphics-side-by-side-hstograms-with-counts-using-sas-functions-in-formats
Enhanced ascii graphics side by side hstograms with counts using sas functions in formats
    %let pgm=utl-enhanced-ascii-graphics-side-by-side-hstograms-with-counts-using-sas-functions-in-formats;

    %stop_submission;

    Enhanced ascii graphics side by side hstograms with counts using sas functions in formats

    SAS base functions in formats without using FCMP by Data _NULL_

    giyhub
    https://tinyurl.com/4x6z3k6n
    https://github.com/rogerjdeangelis/utl-enhanced-ascii-graphics-side-by-side-hstograms-with-counts-using-sas-functions-in-formats

    /**************************************************************************************************************************/
    /* INPUT                      | PROCESS                               | OUTPUT                                            */
    /* =====                      | =======                               | ======                                            */
    /* AGE  FEMALES     MALES     | proc format ;                         |      COUNT  -------GENDERS-----  COUNT            */
    /*                            |  value $ryt                           | AGE  FEMALE FEMALES    MALES     MALE             */
    /*  10  FFFFFFFFF   MMMMM     |  other=[right()]                      |                                                   */
    /*  11  FFFFFFFFFF  MMMM      | ;                                     |  10  9       FFFFFFFFF.MMMMM     5                */
    /*  12  FFFF        MMMMMMMM  |  value $lms                           |  11  10     FFFFFFFFFF.MMMM      4                */
    /*  13  FFFFFF      MMMM      |  other=[length()]                     |  12  4            FFFF.MMMMMMMM  8                */
    /*  14  FFFFFF      MMMMM     | ;                                     |  13  6          FFFFFF.MMMM      4                */
    /*  15  FFFFFFFFFF  MMMM      | run;quit;                             |  14  6          FFFFFF.MMMMM     5                */
    /*                            |                                       |  15  10     FFFFFFFFFF.MMMM      4                */
    /* data have;                 | proc report data=have                 |                                                   */
    /*  retain age;               |  nowd split='_' headskip;;            |                                                   */
    /*  call streaminit(4321);    | cols                                  |                                                   */
    /*  length females males $10; |  age                                  |                                                   */
    /*  do age=10 to 15;          |  females=lfs                          |                                                   */
    /*   females=repeat("F",rand( |  ("-GENDERS-" females con males)      |                                                   */
    /*    "integer",1,10));       |  males=lms;                           |                                                   */
    /*   males=repeat("M",rand(   | define age/display width=4;           |                                                   */
    /*    "integer",1,10));       | define females /display f=$ryt10.     |                                                   */
    /*   output;                  |   spacing=0;                          |                                                   */
    /*  end;                      | define con/computed  "" f=1.          |                                                   */
    /* run;quit;                  |   spacing=0;                          |                                                   */
    /*                            | define males /display spacing=0 ;     |                                                   */
    /*                            | define lfs/display f=$lms.            |                                                   */
    /*                            |   "COUNT_FEMALE" width=7;             |                                                   */
    /*                            | define lms/display f=$lms.            |                                                   */
    /*                            | "COUNT_MALE";                         |                                                   */
    /*                            | compute con;                          |                                                   */
    /*                            |     con = .;                          |                                                   */
    /*                            | endcomp;                              |                                                   */
    /*                            | run;quit;                             |                                                   */
    /**************************************************************************************************************************/
    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    data have;
     retain age;
     call streaminit(4321);
     length females males $10;
     do age=10 to 15;
      females=repeat("F",rand(
       "integer",1,10));
      males=repeat("M",rand(
       "integer",1,10));
      output;
     end;
    run;quit;

    /**************************************************************************************************************************/
    /* AGE    FEMALES       MALES                                                                                             */
    /*  10    FFFFFFFFF     MMMMM                                                                                             */
    /*  11    FFFFFFFFFF    MMMM                                                                                              */
    /*  12    FFFF          MMMMMMMM                                                                                          */
    /*  13    FFFFFF        MMMM                                                                                              */
    /*  14    FFFFFF        MMMMM                                                                                             */
    /*  15    FFFFFFFFFF    MMMM                                                                                              */
    /**************************************************************************************************************************/

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    proc format ;
     value $ryt
     other=[right()]
    ;
     value $lms
     other=[length()]
    ;
    run;quit;

    proc report data=have
     nowd split='_' headskip;
    cols
     age
     females=lfs
     ("-GENDERS-" females con males)
     males=lms;
    define age/display width=4;
    define females /display f=$ryt10.
      spacing=0;
    define con/computed  "" f=1.
      spacing=0;
    define males /display spacing=0 ;
    define lfs/display f=$lms.
      "COUNT_FEMALE" width=7;
    define lms/display f=$lms.
    "COUNT_MALE";
    compute con;
        con = .;
    endcomp;
    run;quit;

    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

    /**************************************************************************************************************************/
    /*      COUNT  -------GENDERS-------  COUNT                                                                               */
    /* AGE  FEMALE FEMALES    MALES       MALE                                                                                */
    /*                                                                                                                        */
    /*  10  9       FFFFFFFFF.MMMMM       5                                                                                   */
    /*  11  10     FFFFFFFFFF.MMMM        4                                                                                   */
    /*  12  4            FFFF.MMMMMMMM    8                                                                                   */
    /*  13  6          FFFFFF.MMMM        4                                                                                   */
    /*  14  6          FFFFFF.MMMMM       5                                                                                   */
    /*  15  10     FFFFFFFFFF.MMMM        4                                                                                   */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */

